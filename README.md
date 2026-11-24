# Double Pendulum Simulation

A NetLogo simulation of a double pendulum, using the nonlinear equations of motion and a fourth-order Runge–Kutta (RK4) numerical integrator.

> **Project status:** Initial working version. The source has been organized for GitHub; runtime verification in NetLogo is still required before treating the release as fully tested.

## Overview

A double pendulum consists of two masses connected in series by two massless rods, with the first rod attached to a fixed pivot. Its motion is nonlinear and can become highly sensitive to initial conditions.

This project calculates the angular positions and angular velocities of both pendulums, integrates their equations of motion numerically, and updates their positions in NetLogo.

## Features

- Two connected pendulum bobs and a fixed pivot.
- Nonlinear equations of motion for a double pendulum.
- Fourth-order Runge–Kutta (RK4) integration.
- Configurable masses, rod lengths, gravity, time step, and initial conditions in `setup`.
- Real-time visualization using NetLogo agents and links.

## Initial Parameters

| Parameter | Initial value | Meaning |
|---|---:|---|
| `l1` | 55 | First rod length (model length units) |
| `l2` | 55 | Second rod length (model length units) |
| `m1` | 1 | First bob mass (consistent mass units) |
| `m2` | 1 | Second bob mass (consistent mass units) |
| `g` | 9.81 | Gravitational acceleration |
| `dt` | 0.002 | Integration time step (seconds, if SI units are used) |
| `theta1` | 120° | Initial first-rod angle |
| `theta2` | −10° | Initial second-rod angle |
| `omega1` | 0 | Initial first-rod angular velocity |
| `omega2` | 0 | Initial second-rod angular velocity |

The angles are stored in radians and measured from the downward vertical. Importantly, `theta2` is an **absolute angle**, not an angle relative to the first rod.

The current rod lengths are primarily used for the model's geometry. For a physically dimensioned SI model, rod lengths, gravitational acceleration, and the time step must all use a consistent unit system.

## Numerical Method

The state vector is:

\[
\mathbf{x} = [\theta_1,\; \theta_2,\; \omega_1,\; \omega_2]^T
\]

The derivative function returns:

\[
\dot{\mathbf{x}} = [\omega_1,\; \omega_2,\; \alpha_1,\; \alpha_2]^T
\]

where \(\alpha_1\) and \(\alpha_2\) are calculated from the coupled equations of motion. The state is advanced with the classical fourth-order Runge–Kutta method. See [`docs/equations.md`](docs/equations.md) for the equations and angle convention.

## How to Run

1. Install and open the NetLogo desktop application.
2. Create a new model.
3. Open `src/double_pendulum.nls` in a text editor and copy its contents into the model's **Code** tab.
4. In the Interface tab, add a button with the command `setup`.
5. Add another button with the command `go` and enable its **Forever** option.
6. Click `setup`, then click `go` to start the simulation.

You can also run `setup` and `go` from NetLogo's Command Center. The source file is provided as NetLogo code (`.nls`); it is not a complete saved Interface model (`.nlogo`).

## Repository Structure

```text
Double-Pendulum-Simulation/
├── README.md
├── LICENSE
├── .gitignore
├── src/
│   └── double_pendulum.nls
├── docs/
│   └── equations.md
└── media/
    └── README.md
```

## Demo

The following preview is extracted from the project's screen recording:

![Double pendulum simulation preview](media/simulation.gif)

[Watch the full simulation video](media/double_pendulum_demo.mp4)

A representative application screenshot is available at [`media/thumbnail.png`](media/thumbnail.png).

## Limitations and Next Steps

- The model has not yet been independently executed and validated in NetLogo as part of this packaging step.
- A saved `.nlogo` model with a ready-made interface can be added in a later revision.
- Energy monitoring, trajectory trails, parameter controls, and a comparison with other numerical integrators would be useful extensions.

## License

This project is distributed under the MIT License. See [`LICENSE`](LICENSE).
