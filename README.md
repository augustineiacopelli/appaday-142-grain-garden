# Grain Garden

**AppADay 142** | Interactive | [Live app](https://augustineiacopelli.github.io/appaday-142-grain-garden/) | [AppADay portfolio](https://augustineiacopelli.github.io/appaday/)

A falling sand garden. Pour sand, water, acid, lava, stone, wood, plant, and fire, and watch them fall, flow, and react. Water quenches lava into stone, fire races through wood, acid eats what it touches, and plants drink up water. Flip gravity or tilt your phone, then save a crisp PNG.

## How to play

Pick an element from the chip strip and draw on the canvas. Holding your finger or mouse still keeps pouring. The brush slider sets the size from 1 to 8. Powders and liquids pour at about half density so they tumble naturally, while Stone, Wood, and Plant paint solid. New material fills only empty space, except Stone and the Eraser, which paint over anything.

Pause freezes the simulation so you can build, Clear empties the garden, and Flip reverses gravity. Tilt turns your phone into the gravity source, snapping to whichever edge is lowest (iOS asks for motion permission the first time). Snap saves the garden as a PNG at four times the grid resolution with no smoothing, so every grain stays sharp, and uses the share sheet where the browser supports it. The Preset menu loads an Hourglass (made for Flip), a Lava Lake with a waterfall, or a Tinder Forest with a fire already started.

## The elements

| Element | Behavior |
| --- | --- |
| Sand | Falls and piles, sinks through water and acid |
| Water | Flows and levels, turns lava to stone, douses fire |
| Acid | Flows, dissolves sand, stone, wood, and plant, and is used up as it works |
| Lava | Slow heavy liquid, ignites wood and plant, hardens to stone on contact with water |
| Stone | Solid, holds liquids, can be eaten by acid |
| Wood | Solid fuel that burns |
| Plant | Solid, grows by converting neighboring water, burns fast |
| Fire | Rises, spreads through wood and plant, burns out to smoke |
| Steam and Smoke | Byproducts that rise and fade; some steam condenses back to water |

## How it works

The garden is a cellular automaton on a grid 160 cells wide, with a height set once at load from the screen shape (capped at 260). State lives in flat `Uint8Array` buffers for element, shade, lifetime, and a per tick move stamp that keeps any cell from moving twice in one step. Every movement rule is written against a gravity vector, so down, the diagonals, and the sideways spread all rotate when gravity flips or the phone tilts, and the scan order always starts from the floor side. Each reactive cell checks one random neighbor per tick for reactions. Rendering writes a precomputed 32 bit palette straight into one `ImageData` buffer, with fire and lava flickering at draw time.

## Tech

Single `index.html` with inline CSS and vanilla JavaScript. No libraries, no build step. Google Fonts (Silkscreen, Space Grotesk) for the interface. Your selected element and brush size are remembered in localStorage. Nothing leaves your device.

## Part of AppADay

One complete app shipped every day. See the whole archive at the [AppADay portfolio](https://augustineiacopelli.github.io/appaday/).
