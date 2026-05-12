# 🚗 Self-Driving Car — No Libraries

A self-driving car simulation built from scratch using vanilla JavaScript and the HTML5 Canvas API. The car learns to navigate traffic autonomously using a neural network trained through a neuroevolution process — no external ML libraries required.

---

## 📸 Preview

The simulation features two canvases side by side:
- **Left canvas** — the road, traffic, and AI cars driving in real time
- **Right canvas** — a live visualization of the best car's neural network

---

## 🧠 How It Works

### Neural Network
Each car is equipped with a small feedforward neural network with the architecture `[5, 6, 4]`:
- **5 inputs** — sensor ray readings detecting obstacles and road borders
- **6 hidden neurons**
- **4 outputs** — forward, left, right, reverse

The network uses a simple binary activation (threshold at bias value).

### Sensors
Each car casts **5 rays** in a 90° spread in front of it. Rays detect:
- Road borders
- Other cars (traffic)

The closer an obstacle, the higher the sensor reading passed to the network.

### Neuroevolution
On each run, **1000 AI cars** are spawned with the same base brain (loaded from `localStorage` if available), with slight random mutations applied to all but the first. The car that travels the furthest up the road is considered the best and can be saved.

---

## 🗂️ Project Structure

```
├── index.html       # Entry point — sets up canvases and loads scripts
├── style.css        # Layout and styling
├── main.js          # Simulation loop, car generation, save/discard logic
├── car.js           # Car class — movement, collision, drawing
├── road.js          # Road class — lane layout and border generation
├── sensor.js        # Sensor class — ray casting and obstacle detection
├── controls.js      # Controls class — keyboard input and dummy/AI control modes
├── network.js       # NeuralNetwork and Level classes — feedforward and mutation
├── visualizer.js    # Visualizer class — neural network canvas rendering
└── utils.js         # Utility functions — lerp, intersection, color helpers
```

---

## 🚀 Getting Started

No build step or dependencies needed.

1. **Clone or download** the repository.
2. Serve the files via a local HTTP server (required for ES module/image loading):
   ```bash
   # Using Python
   python -m http.server 8080

   # Or using Node.js (npx)
   npx serve .
   ```
3. Open `http://localhost:8080` in your browser.

> ⚠️ Opening `index.html` directly via `file://` may cause issues with image loading (`car.png`). Use a local server.

---

## 💾 Saving & Discarding Brains

Two buttons appear between the canvases:

| Button | Action |
|--------|--------|
| 💾 | Saves the best car's brain to `localStorage` |
| 🗑️ | Discards the saved brain and resets to random |

On the next page load, saved brains are automatically loaded and used as the base for mutation.

---

## ⚙️ Configuration

Key parameters you can tweak in `main.js` and the source files:

| Parameter | Location | Default | Description |
|-----------|----------|---------|-------------|
| `N` | `main.js` | `1000` | Number of AI cars per generation |
| `mutation amount` | `main.js` | `0.1` | How much each car's brain mutates |
| `maxSpeed` | `car.js` / `main.js` | `3` | Top speed of AI cars |
| `rayCount` | `sensor.js` | `5` | Number of sensor rays |
| `rayLength` | `sensor.js` | `150` | How far each ray reaches |
| `raySpread` | `sensor.js` | `π/2` | Angular spread of rays |
| Network shape | `car.js` | `[5, 6, 4]` | Neuron counts per layer |

---

## 🛠️ Car Control Types

The `Car` class supports three control modes:

- `"AI"` — driven by the neural network
- `"KEYS"` — driven by arrow keys (manual play)
- `"DUMMY"` — always drives forward (used for traffic)

---

## 📦 Dependencies

None. Pure HTML, CSS, and JavaScript — runs entirely in the browser.

---

## 📄 License

This project is open source and free to use for learning and experimentation.