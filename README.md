# Double Pendulum LQR

An interactive, browser-based simulation of a double inverted pendulum on a
cart. It compares a numerically computed discrete-time LQR controller with a
manually tunable PD controller.

## Live demo

After GitHub Pages is enabled, the application is published at:

<https://mahditranjbar-coder.github.io/double-pendulum-LQR/>

## Features

- nonlinear double-pendulum-on-cart dynamics
- fourth-order Runge–Kutta integration
- numerical linearization around the upright equilibrium
- discrete algebraic Riccati iteration and live LQR gain calculation
- adjustable physical parameters, PD gains, time step, and force limit
- real-time pendulum animation, state readout, force plot, and controller
  contribution debugger
- keyboard controls: `Space` starts or pauses, `R` resets, and `M` switches
  between LQR and PD

The application is self-contained. It requires no build step, package manager,
server-side component, or third-party JavaScript dependency.

## Run locally

Open `index.html` directly in a modern browser, or serve the directory:

```bash
python -m http.server 8000
```

Then open <http://localhost:8000>.

## Controller model

The state vector is:

```text
[cart position, angle 1, angle 2, cart velocity, angular velocity 1, angular velocity 2]
```

The LQR controller linearizes the nonlinear model around the upright state,
discretizes it at the selected simulation time step, solves for `K`, and
applies `u = -Kx` subject to the selected force limit.

This is an educational simulation, not a validated plant or safety-critical
controller. The LQR law is local: large initial angles or restrictive force
limits can put the system outside its stabilizable region.

## Deployment

Every push to `main` validates the HTML and deploys the repository through
GitHub Pages using `.github/workflows/pages.yml`.

## License

GPL-3.0. See `LICENSE`.
