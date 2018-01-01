# The master server protocol

Heartbeat. This must be sent every 10 seconds by the master server client.
If the master server does not get a heartbeat after 30 seconds, the advertisement is removed.
```javascript
Heartbeat: {
  name: string
  maxPlayers: int
  currentPlayers: int
  server_software: string
  software_version: string
  country: string (ISO 3166-1 alpha-2)
  port: int
}
```
---
Chat. This allows all users to talk on the master server.
```javascript
MasterChat: {
  name: string
  message: string
}
```
---
Obtaining a server list, for game clients
```javascript
ServerListRequest: {
  client_version: string
}
```
Master Server response
```javascript
ServerListResponse: {
  servers: [
    {
      name: string
      port: int
      max_players: int
      current_players: int
      country: string
    },
    ...
  ]
}
```
