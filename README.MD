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
