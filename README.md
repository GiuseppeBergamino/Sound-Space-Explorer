# Sound-Space-Explorer
SSE is an auditory augmented reality teaching system that lets students explore 360° soundscapes with head-tracked headphones.

## What you need
* **Laptop** (macOS/Windows)
* **Reaper** (you can download it [here](https://www.reaper.fm/))
* **IEM Plugin Suite** (you can download it [here](https://www.reaper.fm/](https://plugins.iem.at/)
* **Headphones** (stereo, over-ear preferred).
* *(Optional)* **Head-tracker** (ESP32/IMU or [similar](https://x-io.co.uk/x-imu3/)) sending **MIDI CC** or **OSC**

## Quick start (5 minutes — no head-tracker)

1. **Install** Reaper
2. **Install** IEM Plugin Suite (VST3/AU). Restart Reaper so it scans the plugins.
3. **Download** this repository and open `SSE_Reaper_Project.rpp` in Reaper.
4. **Set audio device:** *Preferences → Audio → Device* (CoreAudio/ASIO), **48 kHz**, buffer **128–256** samples.
5. **Choose one of the soundscapes**, pressing *solo* to the corrensponding one.
6. **Move sound sorces** by interacting with the *Stereo Encoder* associated to each track
7. **Simulate head turns** by interacting with the *SceneRotator* associated to each group


## Try the head-tracker (OSC or MIDI)

You can run SSE with a head tracker that sends **orientation values** (yaw/pitch/roll) many times per second.

### A) OSC (recommended)

1. Tracker sends to your laptop IP on **UDP port 9000** (example), addresses like `/yaw`,`/pitch` and `/roll` (floats −180…+180).
2. In Reaper: *Preferences → Control/OSC/web → Add → OSC (listen on port 9000)* and **Enable input for control messages**.
3. In **SceneRotator**, right-click **Yaw** → **Learn…** → move the tracker; repeat for **Pitch** and **Roll**.
4. Press **OK** and test by turning your head.

### B) MIDI CC

1. Connect the tracker as a MIDI device (if this feature is available). *Preferences → MIDI Devices → enable input (and input for control messages).*
2. In **SceneRotator**, right-click **Yaw** → **Learn…** → move the tracker (e.g., CC#1). Do the same for **Pitch** and **Roll**.
3. If motion is too coarse, enable **Soft takeover** or scale the range in the Learn dialog.

> Tip: keep **Yaw** full-range (±180°), **Pitch** and **Roll** small (±90°). Re-center by briefly setting Yaw/Pitch/Roll to **0**.

## Pick a Soundscape

The project includes groups of tracks for ready-to-use soudscapes:

* **River** — localization & figure–ground (cascades fixed, near droplets).
* **Forest** — selective attention & masking (wind + intermittent birds).
* **Lake** — width, reflections, depth.
* **Peak** — sparse, distant sources (sense of space).

**How to switch:** **Solo** the group you want to listent to or **Mute** the others. Each group has clearly named tracks(sound sources) you can raise/lower.

## Teacher controls (in Reaper)

* **Solo** a soundmark, **mute** layers, **adjust levels**.
* **Modify orientation:** set Yaw/Pitch = 0 to discuss what students hear.
* **Change soundscape** instantly by soloing another group.
* Keep **rotation → binaural** order in the FX chain.

## Safety & Inclusion

* Start **quiet**, set a class maximum level.
* Only **gross motor** movements (simple head turns) are required—no fine motor skills, screens, or special lighting.
* For students with limited mobility: use **smaller turns**, assisted positioning, or **role sharing** (navigator/reporter).
* Personal headphones are fine.

## Classroom recipe (10–15 min)

1. **Demo (2 min):** “Turn right; does the cascade move to the center?”
2. **Task 1 — Soundmark (4 min):** Find the reference sound, name its bearing, center it with a small head turn.
3. **Task 2 — Figure–ground (4 min):** Shift attention between wind (background) and bird (figure); which feels nearer and why?
4. **Whole-class recap (2–3 min).**

Tasks are **grounded in R. Murray Schafer’s ecological listening**.

## Troubleshooting

* **No sound:** check *Audio Device*, track **Monitoring** on, **BinauralDecoder** last in chain, scene not muted.
* **Feels wrong / inside head:** ensure **SceneRotator → BinauralDecoder** order; verify headphones are stereo (not speaker fold-down).
* **High latency / “sticky” motion:** lower buffer to **128–256**; use dedicate Wi-Fi link for OSC; close heavy apps.
* **Too dense / loud:** lower the **Soundscape** group fader; mute layers; use teacher **Solo** to spotlight.
* **OSC not learning:** check firewall and port; verify “Enable input for control messages”.

