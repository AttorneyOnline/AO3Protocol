# The master server protocol

Heartbeat. This must be sent every 10 seconds by the master server client.
If the master server does not get a heartbeat after 30 seconds, the advertisement is removed.
```javascript
heartbeat: {
  name: string
  motd: string
  maxPlayers: int
  currentPlayers: int
  serverSoftware: string
  softwareVersion: string
  language: string
  advertise: bool
  port: int
}
```
---
Chat. This allows all users to talk on the master server.
```javascript
masterChat: {
  name: string
  message: string
}
```
---
Obtaining a server list, for game clients
```javascript
serverRequest: {
  clientVersion: string
}
```
Master Server response
```javascript
serverResponse: {
  servers: [
    {
      motd: string
      name: string
      port: int
      maxPlayers: int
      currentPlayers: nt
      language: string
    },
    ...
  ]
}
```
