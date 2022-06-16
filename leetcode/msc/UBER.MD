# Question 1

Given two GPS traces from riders' and drivers' phone, infer pickup and dropoff timestamps

rider: [(lat, lng, ts), (lat, lng, ts), ...]

driver: [(lat, lng, ts), (lat, lng, ts), ...]

Return pickup_ts, dropoff_ts

```
                                   pickup_ts                     dropoff_ts
                                          v                             v
R: [(0, 0, 0),  (0, 0, 2000), (0, 0, 4000),  (1, 1, 6000), (2, 2, 8000), (2, 2, 10000)]
D: [(2, 0, 10), (1, 0, 1990), (0, 0.1, 4010), (1, 1, 6010), (2, 2, 8010), (3, 3, 10000)]

    Tolerances:
        distance: 0.5
        time: 100
```

    len(arr) is different

    looking for rider: dif lat lng
    riding:  same lat lng
    dropping of: dif lat lng

    for loop: ts from driver: 0, 2000, 4000, 6000
    riderTS = curRider => while(curRider <= driverTS - timeTorelances): curRider += 1
    => if same time period: check lat lng
    => if same lat lng: pickup = tsDriver
    => if (pickup) => check until different

    Time O(N) N = length (driver + user)
    return (pickup, dropoff) if pickup else (-1, -1)

driver: 0, 1000, 2000, 3000, 4000

dTS: 2000
userTS: 0, 1000, 3000, 4000
uTS: 3000

if valid pickup: save 3000 as pickupTime

```py
  def distance(lat1, lng1, lat2, lng2):
    return math.sqrt(math.pow(lat1 - lat2, 2) + math.pow(lng1 - lng2, 2))

  def pickupDropoff(driver, user):
    userTS = 0
    driverTS = 0
    pickUp = -1
    dropOff = -1

    for dLat, dLng, dTS in driver:
        uLat, uLng, uTS = user[userTS]
        while(uTS < dTS - 100):
            userTS += 1
            if userTS == len(user):
                break
            uLat, uLng, uTS = user[userTS]

        if uTS > dTS + 100:
            driverTS += 1
            continue

        # collapse the same TS

        if pickUp == -1 and distance(dLat, dLng, uLat, uLng) <= 0.5 and abs(dTS - uTS) < 100:
            pickUp = dTS

        if pickUp != -1 and distance(dLat, dLng, uLat, uLng) > 0.5 and abs(dTS - uTS) < 100:
            dropOff = driver[driverTS - 1][2]
            break

        driverTS += 1

    return (pickUp, dropOff)
```

Test

```py
user = [(0, 0, 0), (0, 0, 2000), (0, 0, 4000), (1, 1, 6000), (2, 2, 8000), (2, 2, 10000)]
driver = [(2, 0, 10), (1, 0, 1990), (0, 0.1, 4010), (1, 1, 6010), (2, 2, 8010), (3, 3, 10000)]
res = pickupDropoff(driver, user)
print(res)

user = [(0, 0, 0), (0, 0, 2000), (1, 1, 6000), (2, 2, 8000), (2, 2, 10000)]
driver = [(2, 0, 10), (1, 0, 1990), (0, 0.1, 4010), (1, 1, 6010), (2, 2, 8010), (3, 3, 10000)]
res = pickupDropoff(driver, user)
print(res)

user = [(0, 0, 0), (0, 0, 2000), (2, 2, 10000)]
driver = [(2, 0, 10), (1, 0, 1990), (0, 0.1, 4010), (1, 1, 6010), (2, 2, 8010), (3, 3, 10000)]
res = pickupDropoff(driver, user)
print(res)

user = [(0, 0, 0), (0, 0, 2000), (0, 0, 4000), (1, 1, 6000), (2, 2, 8000)]
driver = [(2, 0, 10), (1, 0, 1990), (0, 0.1, 4010), (1, 1, 6010), (2, 2, 8010), (3, 3, 10000)]
res = pickupDropoff(driver, user)
print(res)
```

# Question 2

Given an input array of integers, return the indices of all local minima in the array.

An element is a local minima if it is <= its immediate neighbors.

```
Ex. 1
In: 4,8,2,10
Out: 0,2

Ex. 2
In: 7,3,5,7,9,0,2
Out: 1,5
```

```py
def continueCount(arr, res, i):
  n = len(arr)
  continuesIndices = i
    while continuesIndices < n-1 and arr[continuesIndices] == arr[continuesIndices + 1]:
      continuesIndices += 1
    if continuesIndices == n - 1:
      for j in range(i-1, continuesIndices):
        res.append(i + j)
    elif continuesIndices < n-1 and arr[continuesIndices] < arr[continuesIndices + 1]:
      for j in range(i-1, continuesIndices):
        res.append(i + j)
  return continuesIndices

# Time: O(N)

# Space: O(N)

def findMinimas(arr):
  n = len(arr)
  res = list()
  i = 0
  while i < n:
    if i == 0:
      if arr[i] < arr[i + 1]:
        res.append(i)
        # continue
    elif i == n-1:
      if arr[i] < arr[i - 1]:
        res.append(i)
        # continue
    elif arr[i] < arr[i-1]:
      #do some while
      if arr[i] < arr[i + 1]:
        res.append(i)
      if arr[i] == arr[i + 1]:
        i = continueCount(arr, res, i)
    i += 1
  return res
```

Test

```py
arr = [4,8,2,10]
res = findMinimas(arr)
print(res)

arr = [7,3,5,7,9,0,2]
res = findMinimas(arr)
print(res)

arr = []
res = findMinimas(arr)
print(res)

arr = [5, 4, 3, 2, 1]
res = findMinimas(arr)
print(res)

# Black line

arr = [5, 3, 3, 3, 1]
res = findMinimas(arr)
print(res)

# Red line

arr = [5, 3, 3, 3, 5]
res = findMinimas(arr)
print(res)

# Red line never up

arr = [5, 3, 3, 3, 3]
res = findMinimas(arr)
print(res)

# Red line never up

arr = [3, 3, 3, 3, 3]
res = findMinimas(arr)
print(res)
```
