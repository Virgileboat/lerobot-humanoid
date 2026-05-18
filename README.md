# LeRobot Humanoid Workspace

This workspace groups the full LeRobot humanoid project in one place, from design to deployment:

- mechanical/control co-design
- hardware build assets
- robot model assets
- runtime and deployment stack
- simulation-based identification

Each folder below is an independent Git repository with its own history/remotes.

## Repository Names

Local folder names are aligned with canonical `origin` repository names:

- `lerobot-humanoid-design`
- `lerobot-humanoid-hardware`
- `lerobot-humanoid-identification`
- `lerobot-humanoid-model`
- `lerobot-humanoid-runtime`

## Repository Map

| Folder | Remote | Role | Main Outputs |
|---|---|---|---|
| `lerobot-humanoid-design` | `Virgileboat/lerobot-humanoid-design` | Mechanical/control co-design (URDF + optimization experiments) | Design vectors, URDF assumptions, feasibility studies |
| `lerobot-humanoid-hardware` | `Virgileboat/lerobot-humanoid-hardware` | Build documentation, BOM, STL exports, wiring, commissioning tooling | Printable parts, buy-list, assembly/electronics procedures |
| `lerobot-humanoid-model` | `Virgileboat/lerobot-humanoid-model` | Versioned model assets + Python helpers (`lerobot_humanoid_models`) | MJCF/URDF assets and constants consumed by runtime/identification |
| `lerobot-humanoid-runtime` | `Virgileboat/lerobot-humanoid-runtime` | Real robot + simulation runtime, calibration, policy execution, LeRobot integration | Deploy scripts, controllers, calibration flow, data acquisition |
| `lerobot-humanoid-identification` | `Virgileboat/lerobot-humanoid-identification` | MJWarp replay + CMA-ES parameter identification | Identified simulator parameters and run artifacts |

## How The Repos Connect

1. `design` explores geometry/control tradeoffs and defines feasible robot assumptions.
2. `hardware` is the build source of truth (what is physically assembled).
3. `model` packages robot descriptions (`MJCF`/`URDF`) and constants for software stacks.
4. `runtime` runs simulation and the real robot using calibrated models and policies.
5. `identification` replays real logs to tune simulator parameters, feeding back into runtime/model/design.

## Typical End-to-End Loop

1. Update CAD/design assumptions (`design`, `hardware`).
2. Export/update robot model assets (`model`).
3. Validate calibration + policies in simulation/robot runtime (`runtime`).
4. Collect logs and run joint-wise identification (`identification`).
5. Push identified parameters back into runtime/model and iterate.

## Quick Ops

Check state of every repo:

```bash
for repo in lerobot-humanoid-*; do
  echo "=== $repo ==="
  git -C "$repo" status -sb
  echo
 done
```

Show remotes for every repo:

```bash
for repo in lerobot-humanoid-*; do
  echo "=== $repo ==="
  git -C "$repo" remote -v | head -n 2
  echo
 done
```
