# World-Cup-Ball-Simulator

**Live demo:** https://infrabeam1927.github.io/World-Cup-Ball-Simulator/

> **Disclaimer:** This is an unofficial, non-commercial educational project created for learning purposes only. It is not affiliated with, endorsed by, or produced in association with FIFA, Adidas, Kinexon, or any other organization. All product and organization names are the property of their respective owners and are referenced here solely for educational commentary.

This simulator is a browser-based study tool for the Adidas Trionda contact-detection concept used in the 2026 World Cup ball.

## Table of contents

- [What this sim models](#what-this-sim-models)
- [Other factors that affect detection](#other-factors-that-affect-detection)
- [How to use it](#how-to-use-it)
- [Reproducing the Croatia vs. Portugal incident](#reproducing-the-croatia-vs-portugal-incident)
- [Try this](#try-this)
- [Deep dive](#deep-dive)

## What this sim models

This project focuses on the real mechanism behind the Trionda system:

- a sidewall-mounted IMU in the ball shell
- inertial sensing rather than a simple touch switch
- contact events that can be strong, sharp, faint, or just noise
- the distinction between a real touch and a barely-there hair contact that may still cross the threshold

## Other factors that affect detection

Contact type isn't the only thing that shapes what the sensor reports. The simulator also models:

- **Environmental conditions** — temperature, humidity, altitude, and wind change the ambient noise floor and how fast the battery drains (cold weather drains it faster).
- **Ball & contact surface** — inflation pressure, spin rate, and what the ball actually hits (grass, turf, a boot, or a body/head) all reshape the impact spike's amplitude and duration. An underinflated ball hit on the body, for example, can push a normally-detectable hair-touch below the detection threshold entirely.
- **RF / electronic interference** — stadium electronics and broadcast equipment can inject noise spikes that cross the detection threshold with no real touch at all — a false trigger. The simulator flags these separately from genuine detections, including in the offside scenario.
- **Multi-touch ambiguity** — a "simultaneous challenge" button fires two touches a few frames apart to show how the trace can show a single merged peak instead of two distinct contacts.

## How to use it

Open the [live demo](https://infrabeam1927.github.io/World-Cup-Ball-Simulator/), or open [index.html](index.html) directly in a browser, and use the controls to trigger contact events.

## Reproducing the Croatia vs. Portugal incident

The incident is modeled as a very faint contact event:

1. Set the simulation to a faint contact type such as hair or shoulder.
2. Keep rolling noise on to mimic a live match.
3. Watch the pulse trace for the small spike.
4. Compare that against ambient noise to see why the system can be sensitive to tiny events.

## Try this

- Trigger a hair-touch with rolling noise on and see whether you can still spot the spike.
- Compare a clean pass with a shot and notice how much larger the trace becomes.
- Toggle the offside line to see how a faint contact can flip a decision when timing is close.
- Set the surface to "Body / head" and drop ball pressure to the minimum, then trigger a hair-touch — watch it disappear below the threshold.
- Crank RF/electronic interference to a high value and watch the trace throw false triggers with no button pressed at all.
- Press "Simulate simultaneous challenge" and see whether the trace reads as one touch or two.

## Deep dive

<details>
<summary>Why the sensor is mounted in the sidewall</summary>

A sidewall-mounted IMU can pick up sharp changes in acceleration and vibration more effectively than a perfectly centered sensor in a static position. The ball is still balanced by distributed counterweights so that the geometry remains realistic.
</details>

<details>
<summary>Why hair-touch detection matters</summary>

The Croatia vs. Portugal example shows that a barely-there contact can register above the detection threshold. In the simulator, that appears as a very small spike that is distinct from ordinary noise but still easy to miss at a glance.
</details>
