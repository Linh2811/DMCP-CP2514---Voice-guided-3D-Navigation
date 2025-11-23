# DMCP: CP2514 – Voice-guided 3D Solar System Navigation

## Project Overview
This project is a **voice-controlled 3D Solar System simulator** built in **Unity**, with a **Python backend using Vosk** for speech recognition. Users can navigate the solar system by voice commands, zoom in/out, change rotation speed, and get planet information. Supports **English and Vietnamese** commands.

**Features:**
- **Voice Navigation:** Move the camera to planets by saying their names.
- **Zoom Control:** `"zoom in/out"` or `"phóng to/thu nhỏ"`.
- **Rotation Speed Control:** `"speed up/slow down"` or `"tăng tốc/giảm tốc"`.
- **Planet Info Display:** Each planet has a `PlanetInfo` component with name, description, diameter, moons.
- **TCP/JSON Communication:** Python backend sends parsed commands to Unity in real-time.
- **Expandable:** Tour mode, quizzes, TTS narration, particle effects, camera fly-through.

---

## Project Structure

```

DMCP-VoiceSolarSystem/
│
├─ Unity/
│   ├─ Assets/
│   │   ├─ Models/          # FBX/GLTF Solar System model
│   │   ├─ Scripts/
│   │   │   ├─ CameraController.cs
│   │   │   ├─ RotationController.cs
│   │   │   ├─ TcpListenerUnity.cs
│   │   │   └─ PlanetInfo.cs
│   │   └─ Scenes/
│   │       └─ SolarSystemScene.unity
│
├─ PythonBackend/
│   ├─ voice_server.py       # Vosk + Python TCP server
│   └─ models/               # Vosk models (EN & VN)
│
└─ README.md

````

---

## Getting Started

### 1. Unity Setup
1. Import Solar System 3D model (FBX/GLTF) into Unity.
2. Create `PlanetsRoot` empty GameObject and add all planets under it.
3. Assign `PlanetInfo` script to each planet and fill in `displayName`, `description`, `diameterKm`, `moons`.
4. Add `CameraController`, `RotationController`, and `TcpListenerUnity` to a GameObject (`CameraRig`).
5. Ensure camera's clear color is black and `MainCamera` is assigned.

---

### 2. Python Backend
1. Install dependencies:

```bash
pip install vosk sounddevice pyttsx3
````

2. Download Vosk model for English or Vietnamese:

```text
models/vosk-model-small-en-us-0.15
models/vosk-model-small-vn-0.22
```

3. Run the voice server:

```bash
python voice_server.py
```

It will listen to your microphone, parse commands, and send JSON to Unity.

---

### 3. Integration

* Unity `TcpListenerUnity.cs` connects to Python TCP server.
* Commands received in JSON format, e.g.:

```json
{"command":"goto_planet","planet":"sao hoa"}
{"command":"zoom_in"}
{"command":"speed_up"}
```

* CameraController handles zooming and moving to planet.
* RotationController handles planetary rotation speed.
* PlanetInfo can optionally trigger TTS or UI display.

---

## Example Voice Commands

| Command                   | Action                               |
| ------------------------- | ------------------------------------ |
| phóng to / zoom in        | Zoom in camera                       |
| thu nhỏ / zoom out        | Zoom out camera                      |
| tới Sao Hỏa / go to Mars  | Move camera to Mars                  |
| tăng tốc / speed up       | Increase rotation speed              |
| giảm tốc / slow down      | Decrease rotation speed              |
| bắt đầu tour / start tour | Automatic tour mode (future feature) |

---

## Team Roles

* **Trần Trang Linh:** Unity setup, CameraController, PlanetInfo, scene configuration.
* **Phạm Tùng Lâm:** Python backend, Vosk command parser, TCP server.
* **Nguyễn Minh Huyền:** Unity TCP listener, RotationController, PlanetInfo integration.

**Deliverable:** Demo running with basic voice commands (goto planet, zoom, speed control).

---



