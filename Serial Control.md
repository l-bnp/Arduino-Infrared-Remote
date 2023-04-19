# Arduino Infrared Remote Custom Controller

For now only used with HVAC or TV systems

### Communication Protocol

To control the arduino remote a JSON command is sent through serial USB communication to the Arduino. The command formats is explained below.

#### JSON with four properties plus terminator character "$"

- JSON string
  - Property: "subsystem" (String)
    - "HVAC"
    - "TV"
  - Property: "command" (String)
    - "Power", "Temperature"
    - "Power", "Channel"
  - Property: "value" (Integer)
    - 0-1, 18-26
    - 0-1, 1-2
  - Property: "port" (Integer)
    - 1-4
    - 1-4
- Terminator character "$"

#### Send command examples:

  ```json
  {
    "subsystem":"TV",
    "command":"Power",
    "value":0,
    "port":2
  }
  $
  ```
  ```json
  {
    "subsystem":"TV",
    "command":"Channel",
    "value":1,
    "port":4
  }
  $
  ```
  ```json
  {
    "subsystem":"HVAC",
    "command":"Power",
    "value":0,
    "port":1
  }
  $
  ```
  ```json
  {
    "subsystem":"HVAC",
    "command":"Temperature",
    "value":18,
    "port":3
  }
  $
  ```

#### Response command examples:

  ```json
  {
    "subsystem":"commandAccepted",
    "command":"HVAC Temperature",
    "value":18,
    "port":3
  }
  $
  ```
  ```json
  {
    "subsystem":"unknownCommand",
    "command":"TV Temperature",
    "value":0,
    "port":1
  }
  $
  ```