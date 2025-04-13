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
