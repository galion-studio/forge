<!-- SPDX-License-Identifier: MIT -->
<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/logo/forge-banner-dark-1280x320.png">
    <img src="assets/logo/forge-banner-light-1280x320.png" alt="Forge" width="640">
  </picture>
</p>

# Forge

**Open-source AI car generation, physics first: every engineering number comes from a validated solver or a cited test, never from the AI.**

This repository is the project's front page. The work happens in the companion repository **[galion-studio/cargen](https://github.com/galion-studio/cargen)**. It holds the Rust crash orchestration, validation data, research notes and the work log.

## The idea
The goal is one prompt in, one car out. From a single prompt, Forge produces:
- a specification,
- geometry,
- solver runs (crash, stiffness, aerodynamics),
- an honest validation report,
- a drivable game model.

Physics comes first. The solver chain must reproduce real tests before Forge claims anything about a generated car.

There are two layers, and they are never mixed:
- **Truth layer:** external validated solvers and real test data. Every number cites its source and carries its error against a real test.
- **Play layer:** a drivable Bevy + Rapier game fed by truth-layer data. Its own physics is never presented as an engineering result.

## Physics stack (planned and in progress)
- **Crash:** OpenCourant (ex-OpenRadioss, AGPL-3.0), run unmodified as a separate program.
- **Stiffness:** MFEM and CalculiX.
- **Geometry and meshing:** Open CASCADE and Gmsh.
- **Vehicle dynamics:** Project Chrono.
- **Orchestration:** a Rust core. It runs on the CPU by default, with CUDA (local or RunPod A100) as an optional speed-up.
- **AI planning:** OpenRouter, under a hard spend cap. The AI plans and explains; it never produces physics numbers.

## Status
- **P1a** (in progress): square steel tube axial crush in OpenCourant vs a published experiment (Park et al. 2022, *Materials* 15:2107). No simulated result is published yet.
- **P1b** (next): NHTSA full-frontal test with the public CCSA Toyota Yaris model.
- **Later:** frame, panels, aero (DrivAerML/AhmedML), assembly, drivable game, one-prompt pipeline.

See [cargen](https://github.com/galion-studio/cargen) for the research, the 48-test crush dataset with its theory check, and progress.

## License
MIT, © 2026 galion-studio (see [LICENSE](LICENSE)). The logos are original artwork under the same licence. Third-party solvers keep their own licences and are not included.
