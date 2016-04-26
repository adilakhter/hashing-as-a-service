Hashing-as-a-Service
=====================

This simple service is designed to hash strings. That's it: "Hashing-as-a-Service".
It accepts batch requests with a list of strings to hash. It returns a list of hashes of that strings (in the same order).


How To Run
----------

Please ensure that you have [SBT](http://www.scala-sbt.org/) installed, along with its dependencies. To run the service just issue the following command:

```
$ sbt service/run

```

Service will be started on port 9000 listening to all network interfaces. 

```
$ http localhost:9000/ping
```


Following is the expected outcome: 


```
HTTP/1.1 200 OK
Content-Length: 4
Content-Type: text/plain; charset=UTF-8
Date: Tue, 26 Apr 2016 14:42:32 GMT
Server: Simple Service (spray-can 1.3)

pong

```
Service API
-----------

Submit a job for processing:

```
POST /api/service
Accept: application/json
Body: <Job>
```

Returns an HTTP 202 (ACCEPTED).

Request Body example:

```scala 
      {
        "id": "job-1",
        "lines": [
           "This a line",
           "And that's another line."
        ]
      }
```

Response Body example:
```scala
     {
        "id": "job-1",
        "lines": [
            "62812ce276aa9819a2e272f94124d5a1",
            "13ea8b769685089ba2bed4a665a61fde"
        ]
     }
     
```     
Example of error response: 

HTTP 500 (Service Unavailable)
```
    {
        "error": "Something went wrong!"
    }
```     
