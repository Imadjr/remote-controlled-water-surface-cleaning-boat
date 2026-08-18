# Project Audit

This audit records what is verified by the supplied firmware, photographs, demonstration video, and poster. It intentionally separates implemented behavior from poster concepts and future possibilities.

## Verified Implementation

| Area | Finding | Evidence |
| --- | --- | --- |
| Control mode | Remote control; not autonomous | Directional browser controls and command-driven firmware; no autonomy loop |
| Controller | ESP32-CAM | Firmware includes `esp_camera`; module is visible and labelled in project material |
| Firmware | One Arduino/C++ sketch with embedded HTML/CSS/JavaScript | `firmware/boat_controller/boat_controller.ino` |
| Communication | ESP32-CAM Wi-Fi access point, HTTP, and two WebSockets | `WiFi.softAP`, server on port 80, `/Camera`, and `/CarInput` |
| Video | VGA JPEG capture streamed as binary WebSocket messages | Camera configuration and `sendCameraPicture()` |
| Propulsion | Two DC motors through an L298N driver | Firmware direction pins, wiring diagram, photographs, and water test |
| Steering | Differential motor direction, including pivot turns | `moveCar()` |
| Speed | One shared PWM speed command | Both motor-enable entries use the same PWM channel and GPIO mapping |
| Camera motion | Pan and tilt servos | GPIO 14/15 servo code and wiring diagram |
| Lighting | PWM illumination output | GPIO 4 and the web light slider |
| Cleaning | Passive flared guides and open collection area | Prototype photographs; no cleaning-actuator code |
| Power | Diagram documents a rechargeable 7–12 V source and UBEC/buck converter | Recovered wiring diagram; exact installed models are not documented |
| Test status | Water movement and live browser monitoring/control shown | 58-second demonstration video |

## Not Verified or Not Implemented

- autonomous navigation or path planning;
- obstacle avoidance;
- GPS, IMU, ultrasonic, LiDAR, or other navigation sensors;
- computer vision, AI inference, waste classification, or automatic target detection;
- cloud connectivity or a separate mobile application;
- an active conveyor, rake, pump, or powered cleaning assembly;
- a completed debris pickup cycle, collection rate, or payload capacity;
- motor model, battery chemistry/capacity, exact ESP32-CAM board variant, or measured performance figures.

The poster describes autonomous operation and AI-based waste detection as a concept. Those claims are not supported by the supplied firmware or test media and are therefore excluded from the public feature list.

## File Classification

### Keep in the public repository

- cleaned ESP32-CAM firmware;
- safe credential-configuration example;
- selected prototype photographs;
- representative water-test and browser-interface frames;
- recovered wiring diagram;
- README and audit documentation.

### Local archive only

- raw 58-second MP4 demonstration;
- original PowerPoint poster.

Both local archive directories are ignored by Git. The poster contains names of other project participants and broad concept claims that are not implemented in the supplied code; the raw video is retained locally to avoid adding a 24 MB source-media file to ordinary Git history.

### Excluded or ignored

- `.DS_Store` and operating-system metadata;
- editor settings;
- Arduino/PlatformIO build output and compiled binaries;
- logs and local environment files;
- the real `secrets.h` configuration file.

## Security Review

The original sketch contained Wi-Fi access-point credentials. Their values were not retained in the public source. The firmware now includes a local `secrets.h`, which is ignored by Git, and the repository provides only `secrets.example.h` placeholders.

No API keys, cloud credentials, tokens, web credentials, or private service URLs are required by the supplied implementation. The browser interface itself provides no user-level login, TLS, or application-layer authorization; access is controlled only by the local Wi-Fi access-point password.

## Media Review

- Two supplied photographs show the assembled prototype and passive front collection structure.
- The video is 58.13 seconds long and shows an in-water movement test followed by the mobile browser's live video and controls.
- The video does not visibly demonstrate collection of floating debris.
- The poster contains a useful wiring diagram, which was recovered as a standalone public image.

## Validation Boundaries

The source file is complete after credential externalization. No build manifest, pinned library versions, board profile, or Arduino CLI configuration was supplied, so reproducible compilation requires the original board and toolchain details to be documented.
