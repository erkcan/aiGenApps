I want a billard ball simulation app as a single HTML/JS file. Below are the requirements.

---

## 🔬 Billiard Momentum Lab: Technical Specification

This program is a **2D Rigid Body Physics Simulator** built using HTML5 Canvas and the Web Audio API, specifically designed to demonstrate the **Conservation of Linear Momentum**.

### 1. Physics Engine Requirements

* **Collision Detection:** Discrete circle-circle and circle-boundary collision detection.
* **Collision Resolution:**
* **Elasticity:** Independent coefficients of restitution for Ball-to-Ball ($e_{ball}$) and Ball-to-Wall ($e_{wall}$).
* **Mass Ratio:** Support for variable mass on at least one object to demonstrate unequal momentum distribution.
* **Impulse-Based Resolution:** Velocity updates must follow the 1D elastic collision formula applied along the normal vector:

$$v'_1 = v_1 - \frac{2m_2}{m_1+m_2} \frac{\langle v_1-v_2, x_1-x_2 \rangle}{\|x_1-x_2\|^2} (x_1-x_2)$$

* **State Management:** Start the simulation with two balls on a horizontal centerline, equidistant from the center, with equal and opposite initial velocities (Head-on collision mode).

### 2. Visualization & UI

* **Real-time Value Display:** All control sliders (Velocity X/Y, Mass, Elasticity) must display their current numerical values in real-time above or beside the slider.
* **Vector Overlays:**
* **Momentum Arrows:** Solid arrows originating from each ball's center, where length is proportional to $p = mv$.
* **Center of Mass (CoM):** A toggleable marker (purple dot) showing the system's balance point.
* **Net Momentum Arrow:** A white vector originating from the CoM representing the system’s total momentum.
* **Interactive Tooltips**: Hovering over any slider label or button reveals its physical purpose.

* **Trace/Ghost Path:** A toggleable "long exposure" path that tracks the historical trajectory of each ball (limited to ~150 frames).
* **Interactive Placement:** The ability to "drag and drop" balls with the mouse while the simulation is paused.

### 3. Audio & Media Features

* **Dynamic Sound Synthesis:** Instead of audio files, use a `Sine/Triangle Oscillator` to generate "clinks" and "thuds."
* Frequency and Volume must be mapped to **Kinetic Energy Loss** during collision.


* **Synchronized Screen Recording:**
* **Recording Engine:** Use `MediaRecorder` API to capture the `<canvas>` stream at 60 FPS.
* **Audio-Visual Lock:** A crucial requirement is a **Silent Oscillator "Heartbeat."** This continuous stream of silent audio data must be piped into the `MediaStreamDestination` from the moment recording starts to prevent audio lag/bunching during the final `.webm` export.
* **Download Trigger:** Automatic download of a `.webm` file upon stopping the recording.



---

### 4. Component Summary Table

| Feature | Description |
| --- | --- |
| **Language** | Vanilla JavaScript, HTML5, CSS3 |
| **Rendering** | `requestAnimationFrame` for 60Hz smooth motion |
| **Audio** | Web Audio API (Oscillators + Gain Nodes) |
| **Momentum Lab** | Real-time readout of $P1$, $P2$, and  $P_{total}$|
| **Recording** | Canvas `captureStream` merged with `AudioDestinationNode` |

---

### 5. Essential Starting State Logic

To ensure the perfect demonstration every time, the "Reset" function must hard-code the following:

* **Ball 1:** Position $(W \times 0.35, H \times 0.5)$, Velocity $(+5, 0)$.
* **Ball 2:** Position $(W \times 0.65, H \times 0.5)$, Velocity $(-5, 0)$.
* **Elasticity:** Default to **1.00** for Ball-Ball (Perfectly Elastic).
