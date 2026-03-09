🌋 Volcano Pyroclastic Eruptions — Forge v2.3

Cinematic environmental volcano event system for Beyond All Reason (BAR).

This gadget orchestrates a staged volcanic eruption including seismic buildup, warning systems, eruption column, projectile launch, shockwave, smoke turbulence, and impact effects.

📌 Usage: !bset forge_volcano 1 within the lobby, make sure the map Forge v2.3 is selected. Admin / host can issue the command /luarules volcano to pause / resume the event with cheats enabled.

📌 Scope

Map locked: Forge v2.3

Automatically unloads itself on all other maps

Purely environmental / cinematic (no direct gameplay logic)

⏱ Event Timeline

Each eruption cycle follows this sequence:

1️⃣ Dormant Interval

Randomized cooldown:

8–12 minutes

2️⃣ Seismic Buildup (~20 seconds)

Low-frequency rumble

Voice alert (LavaAlert.wav)

On-screen warning:

SEISMIC ACTIVITY DETECTED

3️⃣ Eruption Trigger

Shockwave CEG

Rising fireball column

Smoke turbulence

Volcanic projectile spawn

4️⃣ Projectile Phase

In-flight volcanic visuals

Impact effects on landing

Environmental smoke/debris

5️⃣ Reschedule

Next eruption randomized between 8–12 minutes.

🧱 Architecture
🔹 Synced

Frame-based eruption scheduler

State machine (Dormant → Buildup → Eruption)

Projectile spawning

CEG triggering

Sync→Unsynced messaging

🔹 Unsynced

Rumble audio

LavaAlert voice playback

Screen warning text rendering

Communication handled via:

SendToUnsynced()
📦 Dependencies
Effects
effects/volcano.lua

Defines:

volcano_rising_fireball_spawner

volcano_rising_fireball_sub

shockwaveceg

volcano_smoke_turbulence

Projectile impact CEG chains

Projectile Unit
volcano_projectile_unit.lua

Handles:

Spawned volcanic projectile entity

In-flight visuals

Impact behavior

Audio
sounds/voice-soundeffects/LavaAlert.wav
⚙ Timing Configuration

All timing values are frame-based (30 FPS baseline):

Constant	Purpose
FIRST_MIN / FIRST_MAX	Initial eruption delay
COOLDOWN_MIN / COOLDOWN_MAX	Repeat interval (8–12 min)
BUILDUP	Pre-eruption escalation duration
WARNING_FRAMES	On-screen text duration
🎯 Design Goals

Large-scale cinematic environmental event

Deterministic scheduling

Strict map isolation

🛠 Notes

Eruption intervals are randomized per cycle.

All CEGs in volcano.lua are actively referenced.

Designed specifically for Forge volcano terrain.
