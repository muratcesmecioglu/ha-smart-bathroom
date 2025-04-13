# 🚽💡 Smart Bathroom Occupancy Light Control

A Home Assistant blueprint for intelligent bathroom lighting automation by Murat Çeşmecioğlu.

## 🐝 The "Hornet in the Box" Principle

> If a hornet enters a closed box – it's trapped. If the box opens – it's gone. Now apply that logic to your bathroom.

This principle forms the core of this automation:
- When your bathroom door closes (the box seals), someone is definitely inside
- When the door opens again, the space becomes vacant
- Motion and timing parameters add extra intelligence to handle edge cases

## 🧠 How It Works

This blueprint combines door sensors, motion detection, and timing logic to create a bulletproof bathroom lighting system that:

1. **Turns lights on** when motion is detected or the door opens
2. **Keeps lights on** while the bathroom is occupied
3. **Turns lights off** when the person exits
4. **Prevents false triggers** by cross-validating door position + motion + time delays

### Main Scenarios

#### 🚶‍♂️ Entering the Bathroom
- **Door opens** → Lights turn on immediately
- **Motion detected** → Lights turn on immediately
- If door closes after motion → Room is marked as occupied
- If door stays open → Waits for motion to clear before turning off lights

#### 🚪 Inside the Bathroom
- The occupancy helper tracks that someone is in the bathroom
- Lights stay on regardless of motion detection
- Perfect for shower situations where motion sensors might not detect movement

#### 🚶‍♀️ Exiting the Bathroom
- **Door opens** → System waits for the exit timeout period
- Lights turn off after the timeout (giving you time to leave)
- Occupancy state is reset

## ⚙️ Configuration Options

| Parameter | Description | Default |
|-----------|-------------|---------|
| Door Sensor | Binary sensor tracking door state | Required |
| Motion Sensor | Binary sensor detecting motion | Required |
| Light | The light or switch to control | Required |
| Occupancy Helper | Input boolean to track occupancy | Required |
| Door Close Wait Time | Seconds to wait for door to close after motion | 6 |
| Light Off After Motion Time | Seconds before turning off lights when motion stops (door open) | 10 |
| Door Open Motion Clear | Timeout for lights when entering and exiting with door open | 10 |
| Room Exit Timeout | Seconds to leave room before lights turn off | 10 |

## 🛡️ Handling Edge Cases

This automation handles various edge cases:

### 🚿 Shower Scenarios

Since the system uses door closure as the primary occupancy indicator, it won't turn off lights during a shower when motion might not be detected.

### 🔄 Quick In-and-Out

If someone briefly enters and exits without closing the door, the system will:
1. Turn on lights when motion is detected
2. Wait for the configured timeout after motion clears
3. Turn off lights if no further motion is detected

## 🛠️ Installation

1. Import this blueprint to your Home Assistant instance
2. Create a new automation using this blueprint
3. Configure the required entities and timing parameters
4. Create an input_boolean helper to track occupancy state
5. Test the automation with different scenarios

## 🧪 Why It's Bulletproof

This automation eliminates common problems with bathroom lighting:
- No more lights turning off while you're in the shower
- No more manually turning lights off when leaving
- No more fumbling in the dark when entering
- Handles edge cases that single-sensor solutions miss

## 🔗 Links

- [Home Assistant Community Discussion](https://community.home-assistant.io/t/smart-bathroom-occupancy-light-control/874353)
- [GitHub Repository](https://github.com/muratcesmecioglu/ha-smart-bathroom/blob/main/smart-bathroom.yaml)

---

Created with ❤️ by [Murat Çeşmecioğlu](https://github.com/muratcesmecioglu)


























## 🚽💡 Smart Bathroom Occupancy Light Control (Hornet-in-the-Box Principle)

---

### 🐝 What is the “Hornet in the Box” Principle?

> *If a hornet enters a closed box – it’s trapped. If the box opens – it’s gone. Now apply that logic to your bathroom.*

This blueprint automates lights in bathrooms or toilets using **door** and **motion sensors** with pinpoint accuracy.

When the door **closes**, and motion is detected, someone is inside. When the door **opens**, and no motion follows, it’s safe to say it’s empty. It uses a **helper entity** to track occupancy reliably.

---

### 🔧 Why Use This Blueprint?

* Other occupancy blueprints do not check whether the door is opened but this does for reliability.
* Doesn't need fancy hardware – just simple binary sensors
* Light turns off **only when you're sure** the bathroom is empty

---

### ✅ How It Works – Scenarios

* **Entering**:
  * Door opens → Lights turn on
  * Motion detected → "Occupied" status activates (lights stay on until you leave)
  * *No rain dances needed* - lights won't turn off while you're inside!
  
* **Exiting**:
  1. Door opens → System waits for motion to clear
  2. No motion detected → Lights turn off
  
* *Smart edge cases*:
    * Open/close door without entering → Lights turn off immediately
    * Forget to close door → Lights turn off after motion clears

#### How It Works (A liltte bit detailed)
1. **Door opened, and no one was previously inside**
→ Light turns on, waiting to see if someone enters.
2. **Motion detected, but helper was off (first confirmation of entry)**
→ Someone entered. Mark bathroom as occupied.
3. **Motion detected while door is closed (fully confirmed entry)**
→ Occupied. Light is turned on and occupancy is set.
4. **Door opened, helper says “occupied” → wait for motion to stop**
→ After motion clears, turn off light and reset occupancy.
5. **Motion stopped while door is open, and someone was inside**
→ Turns off light and clears the occupancy state.
6. **Door closes, but no one was inside (false open/close)**
→ Light turns off instantly.

---

### 🧠 Motion Sensor Tips

* **Placement is key**: The motion sensor should *not* be triggered by someone just walking past the door or standing outside. Ideally, install it on the ceiling or corner inside the room, angled away from the door.
* **Cooldown (clear delay)**: Recommended `10–15 seconds` to ensure smoother transitions and avoid flickering.

---

### 🚀 Use Cases

* Automate bathroom lights/fans
* Smart occupancy-based nightlights
* Boost energy savings in shared homes
* Set up alerts if bathroom is “occupied too long” (via the helper)

---

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.|592x40](https://community-assets.home-assistant.io/original/4X/1/a/1/1a129e306bc6a339cf8a2b9222553254a1909b6f.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=)
