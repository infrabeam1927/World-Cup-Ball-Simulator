# World-Cup-Ball-Simulator

> **Disclaimer:** This is an unofficial, non-commercial educational project created for learning purposes only. It is not affiliated with, endorsed by, or produced in association with FIFA, Adidas, Kinexon, or any other organization. All product and organization names are the property of their respective owners and are referenced here solely for educational commentary.

This simulator is a browser-based study tool for the Adidas Trionda contact-detection concept used in the 2026 World Cup ball.

## Table of contents

- [What this sim models](#what-this-sim-models)
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

## How to use it

Open [index.html](index.html) in a browser and use the controls to trigger contact events.

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

## Deep dive

<details>
<summary>Why the sensor is mounted in the sidewall</summary>

A sidewall-mounted IMU can pick up sharp changes in acceleration and vibration more effectively than a perfectly centered sensor in a static position. The ball is still balanced by distributed counterweights so that the geometry remains realistic.
</details>

<details>
<summary>Why hair-touch detection matters</summary>

The Croatia vs. Portugal example shows that a barely-there contact can register above the detection threshold. In the simulator, that appears as a very small spike that is distinct from ordinary noise but still easy to miss at a glance.
</details>
