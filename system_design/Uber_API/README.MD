# Design The Uber API

## Gathering Requirements

As with any API design interview question, the first thing that we want to do is to gather API requirements; we need to figure out what API we're building exactly.

We're designing the core ride-hailing service that Uber offers. Passengers can book a ride from their phone, at which point they're matched with a driver; they can track their driver's location throughout the ride, up until the ride is finished or canceled; and they can also see the price of the ride as well as the estimated time to destination throughout the trip, amongst other things.

The core taxiing service that Uber offers has a passenger-facing side and a driver-facing side; we're going to be designing the API for both sides.

## Coming Up With A Plan

It's important to organize ourselves and to lay out a clear plan regarding how we're going to tackle our design. What are the major, potentially contentious parts of our API? Why are we making certain design decisions?

We're going to center our API around a Ride entity; every Uber ride will have an associated Ride containing information about the ride, including information about its passenger and driver.

Since a normal Uber ride can only have one passenger (one passenger account--the one that hails the ride) and one driver, we're going to cleverly handle all permissioning related to ride operations through passenger and driver IDs. In other words, operations like `GetRide` and `EditRide` will purely rely on a passed userId, the userId of the passenger or driver calling them, to return the appropriate ride tied to that passenger or driver.

We'll start by defining the Ride entity before designing the passenger-facing API and then the driver-facing API.

## Entities

### Ride

The Ride entity will have a unique id, info about its passenger and its driver, a status, and other details about the ride.

- rideId: string

- passengerInfo: PassengerInfo

- driverInfo?: DriverInfo

- rideStatus: RideStatus - enum CREATED/MATCHED/STARTED/FINISHED/CANCELED

- start: GeoLocation

- destination: GeoLocation

- createdAt: timestamp

- startTime: timestamp

- estimatedPrice: int

- timeToDestination: int

We'll explain why the driverInfo is optional when we get to the API endpoints.

### PassengerInfo

- id: string

- name: string

- rating: int

### DriverInfo

- id: string

- name: string

- rating: int

- ridesCount: int

- vehicleInfo: VehicleInfo

### VehicleInfo

- licensePlate: string

- description: string

## Passenger API

The passenger-facing API will be fairly straightforward. It'll consist of simple CRUD operations around the Ride entity, as well as an endpoint to stream a driver's location throughout a ride.

```
CreateRide(userId: string, pickup: Geolocation, destination: Geolocation)
=> Ride
```

Usage: called when a passenger books a ride; a Ride is created with no DriverInfo and with a CREATED RideStatus; the Uber backend calls an internal FindDriver API that uses an algorithm to find the most appropriate driver; once a driver is found and accepts the ride, the backend calls EditRide with the driver's info and with a MATCHED RideStatus.

```
GetRide(userId: string)
=> Ride
```

Usage: polled every couple of seconds after a ride has been created and until the ride has a status of MATCHED; afterwards, polled every 20-90 seconds throughout the trip to update the ride's estimated price, its time to destination, its RideStatus if it's been canceled by the driver, etc..

```
EditRide(userId: string, [...params?: all properties on the Ride object that need to be edited])
=> Ride
```

```
CancelRide(userId: string)
=> void
```

Wrapper around EditRide -- effectively calls EditRide(userId: string, rideStatus: CANCELLED).

```
StreamDriverLocation(userId: string)
=> Geolocation
```

Usage: continuously streams the location of a driver over a long-lived websocket connection; the driver whose location is streamed is the one associated with the Ride tied to the passed userId.

## Driver API

The driver-facing API will rely on some of the same CRUD operations around the Ride entity, and it'll also have a SetDriverStatus endpoint as well as an endpoint to push the driver's location to passengers who are streaming it.

```
SetDriverStatus(userId: string, driverStatus: DriverStatus)
  => void

DriverStatus: enum UNAVAILABLE/IN RIDE/STANDBY
```

Usage: called when a driver wants to look for a ride, is starting a ride, or is done for the day; when called with STANDBY, the Uber backend calls an internal FindRide API that uses an algorithm to enqueue the driver in a queue of drivers waiting for rides and to find the most appropriate ride; once a ride is found, the ride is internally locked to the driver for 30 seconds, during which the driver can accept or reject the ride; once the driver accepts the ride, the internal backend calls EditRide with the driver's info and with a MATCHED RideStatus.

```
GetRide(userId: string)
=> Ride
```

Usage: polled every 20-90 seconds throughout the trip to update the ride's estimated price, its time to destination, whether it's been canceled, etc..

```
EditRide(userId: string, [...params?: all properties on the Ride object that need to be edited])
=> Ride
```

```
AcceptRide(userId: string)
=> void
```

Calls EditRide(userId, MATCHED) and SetDriverStatus(userId, IN_RIDE).

```
CancelRide(userId: string)
=> void
```

Wrapper around EditRide -- effectively calls EditRide(userId, CANCELLED).

```
PushLocation(userId: string, location: Geolocation)
=> void
```

Usage: continuously called by a driver's phone throughout a ride; pushes the driver's location to the relevant passenger who's streaming the location; the passenger is the one associated with the Ride tied to the passed userId.

## UberPool

As a stretch goal, your interviewer might ask you to think about how you'd expand your design to handle UberPool rides.

UberPool rides allow multiple passengers (different Uber accounts) to share an Uber ride for a cheaper price.

One way to handle UberPool rides would be to allow Ride objects to have multiple passengerInfos. In this case, Rides would also have to maintain a list of all destinations that the ride will stop at, as well as the relevant final destinations for individual passengers.

Perhaps a cleaner way to handle UberPool rides would be to introduce an entirely new entity, a PoolRide entity, which would have a list of Rides attached to it. Passengers would still call the CreateRide endpoint when booking an UberPool ride, and so they would still have their own, normal Ride entity, but this entity would be attached to a PoolRide entity with the rest of the UberPool ride information.

Drivers would likely have an extra DriverStatus value to indicate if they were in a ride but still accepting new UberPool passengers.

Most of the other functionality would remain the same; passengers and drivers would still continuously poll the GetRide endpoint for updated information about the ride, passengers would still stream their driver's location, passengers would still be able to cancel their individual rides, etc..
