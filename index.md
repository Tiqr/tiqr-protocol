# Tiqr Protocoll

Here we will describe the communication between the Tiqr app and the Tiqr library, used in a webserver. 

## Enroll

During enrollment a user registers his Tiqr-app with the server

[![Flow diagram enrollment](/enroll.png)](https://sequencediagram.org/index.html?presentationMode=readOnly#initialData=C4S2BsFMAIBUQI4CdqQHZIPbnAW3cAFCEAOAhkqAMYjlrADmWAridAMTggMAWwARuGYxIAE2YBJACKEAkKLLAy-MgGcYzdSlXBMSMg0hzylEDTrA4iJAFotAN0i2u-Dl16MkkdMYrVaZPTQAOqQ-A5O0ACqEhxeooTootDEJv4WVsgA9GKSUtBkJGyc3HxM3mjEoeFOjigxNgB88Mh2tU42LgBcAMpKlKgY2HgE0AAUmk4gogA00JNIoiCqJOBkAJ5oZPgAlIRomMAwmHWZthHOIPxdAOLoToqQXQA6aDaDWDj49AD6ANaQdbEFrndqXfhNBbQHR6AxPPp6DRaApoZIA9bQEBoaGQVSqECYSqEEFtJB1TpXJrVC7RCRdACiQy+owA0oDoAANYgHI7QE6Ralg2m3e76XnoT4jILMJDgV58YAkVRdLI5cTTAB0aHAWVAyAlwyy+CUCiUAH4DczfuiALwc153NAPXkARQASjYqJhREZCGQqKB7I8QmEaTE-QGQEHeSSLhT+IRBWTIg0mrGwfGugAFYbQpTATRVUNChrNaxqvIFIpdaA9KiBJ3JKJugAywPLuWkVZIaespPJ3Ru9Ng0GNZFNZHlwEVytVuU12t11ktOrHE4tTKlwH+gLt7dacZcAB5IciYfpDF1wJhMH9WNAANRYoNcU0iTffbfo16GSxrxRkEWNTJvUEg2L2B4Zt0OY4HmiiFtyhzHKc6YgZmjrOu+kqfj86hUF4RDEn2h6Uo0SanDEXQALKQCaAGvBMWg-NMcyYPhZC4cwYCQDMlo4XhBF7ImxYgbS4FlpBaHQbmOjwaoQFhmBElIBWXaFCQ1G0eOAHjOoMD8JA14AO5CTyyGRCCqn5OpNYYWKMAAPIAMJugAgji+G0fuKmdtZRRUiJFF0gqSoqhWC46nqXibjkMUAGZYssPA2Cun4bthBC4ZAnnADaACa0DQFmDk9COcV6LgKVoF6PqiC8aBjHp0AGcZQnkSmSmoQOVwMpu0ATgxaxoAwMw8iACX1qAhLAOsJA8XU+KEjMCwsQJtG8R+mVrcAQldR0x6npE55wl0ABqZCvsGD6YmgL7TMGqVbdlBHef2+2kVCx2XgiXgeS9wnAUF4l7eC2YyfmCHEMQQA)

### Metadata format
```json
{
   "service":{
      "displayName":"TestServerController http:\/\/localhost:8001",
      "identifier":"localhost",
      "logoUrl":"http:\/\/localhost:8001\/logoUrl",
      "infoUrl":"http:\/\/localhost:8001\/infoUrl",
      "authenticationUrl":"http:\/\/localhost:8001\/authentication",
      "ocraSuite":"OCRA-1:HOTP-SHA1-6:QH10-S064",
      "enrollmentUrl":"http:\/\/localhost:8001\/finish-enrollment?enrollment_secret=Y"
   },
   "identity":{
      "identifier":"test-user",
      "displayName":"test user name"
   }
}

```

### POST /finish_enrollment FORM DATA
```
secret=Z
language=nl
notificationAddress=1234567890
notificationType=GCM
operation=register
```

## Authentication

[![Flow diagram enrollment](/auth.png)](https://sequencediagram.org/index.html?presentationMode=readOnly#initialData=C4S2BsFMAIBUQI4CdoEMCuwAWkB2oBjVUAe1wChyAHVJQkG-AcyRPSugGJwQmtgARuHQxIAE3QBJACLkAkGOKoBqAM4x06lKuAkkqJpGq16jYHERIAtDwFcefYC0h55NOiAINU+aAHVIAS0AN0gUAFVJLiRxcjwxaEp3Ux9zeGQAenEpaTQqDm5efmdXcnTrWwAeKwCgsNCIyQAuAGVgE2gAQUwcfE9iEDJoAApNMJAxAEpyXBJgGBIGi2QbEAEmgHE8MOJIJoAdXCtodVVVQdwAfQBrSABPQ+OCLFRwKFxDSnIx7V19Q2q5VW6zaehgp3OZBu92gAGpoM9Xu9PkDbFYAHy1EJhaCRJoQi7Qu6UWbzaCLHFY+o4vFbXA7MkYbB4QgDIboJDgQ78YBUVRNDIZH4TAAC2QmADpcOAMqBkEysBlKgSobc7uilYi3nhDBrldSkJcJngwAAzEBhPUNSG4dEkuYLJZUpBLWnbfRkgCKACUrAQSGJIIc9IcWvFoFRNFhoKSQOaiKQKORna7JBjUWsmgAFKPQAByczj-UT9rJFJQGZB4cjqmjsfjbKTqAIoGCu38gWxjXIzdb7cryc7BtxafTlmB2ZIbxO7WAmhGKquaumg7qLppafR5SyEhkeSoTWgLSIuHpCXC3oAMhkSFQ8BHc-XixdS46cdvsnvUPlNu72wB5ABhb1OmgGJVCoMh1GgU09GgSotWRSA7TKSwdxyfcMRTDcmh5PkBXQyVpVlSwFQyBUWWLSAMkOLN-xaWAYL0ABbKw8H9QMxAOXBhnUGABEgcASAAdxXbDGjHFZbCabpmT6BMYEUdpDl4yAzguABpe4ABofkkMRtPAyDcHUbTwB8Jh0AMSBtNvBkLm0w4nwTC5gDuO8ADIrFQMRwNUFdK2qdEfhnPRrN-cx1AIGJzFglAflfcklkrJpANeAh0HMskgJAsC1OM9RDkAkhmPcGBdC6HpKIU6AlNQL5KwxEKdDCwwmnCKglMUpRKHEkcrEkipMyzKdwBnYhNHIQNexANsyQHaaW1m9s+siVCpLWLCh3XRomkvEgmBAXA8tUTLgC+L4gA)

### POST /authenticate FORM DATA
```
sessionKey=<sessionkey>
userId=test-user
response=012345
language=nl
operation=login
notificationType: APNS | GCM
notificationAddress: 123455667890
```
