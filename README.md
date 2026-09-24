# Biomolecular simulation with GROMACS

This is a short introduction to biomolecular simulation. Start with **[Exercises.ipynb](Exercises.ipynb)**: it contains the explanations, terminal commands, analysis code and questions for discussion.

- **Part 1:** prepare a small protein in water, minimise its energy, and equilibrate it in NVT and NPT.
- **Part 2:** compare how thermostat and barostat choices affect dynamics and volume fluctuations.

The tutorial is designed for a one-hour session. You do **not** need to finish every simulation during class: precomputed data are provided so you can spend your time interpreting the results.

## Getting started

The [environment file](environment.yml) specifies GROMACS 2026.3, Python 3.12, JupyterLab and the packages used by the notebook. With Conda or Mamba installed, from the repository directory run:

```bash
conda env create -f environment.yml
conda activate gromacs-tutorial
jupyter lab
```

Open `Exercises.ipynb` in JupyterLab. Run its Python cells in order. Commands shown in fenced `bash` blocks belong in a **terminal opened in this repository directory**, not in Python cells. If you work elsewhere, the relative paths in the notebook will not resolve. The Part 2 commands request 4 MPI ranks × 8 OpenMP threads; if your machine has fewer cores, reduce `-ntmpi` and/or `-ntomp` rather than running four jobs in parallel.

## Files and precomputed data

- [`structures/2RVD.pdb`](structures/2RVD.pdb) is the starting structure.
- [`mdp/`](mdp/) contains the simulation settings. The `ex2_*.mdp` files define the four Part 2 comparisons.
- [`exercise-1/`](exercise-1/) already contains the intermediate structures, topology, minimised structure, equilibration trajectories and extracted `.xvg` data used by Part 1. [`exercise-1/results/`](exercise-1/results/) holds a small backup of the minimisation structure and energy file.
- [`exercise-2/results/`](exercise-2/results/) contains extracted temperature, MSD and NPT energy/volume data for the plots, as well as `.edr` files for re-extracting quantities. The two NVT `.xtc` trajectories are included so you can recalculate the water MSD; their matching `.tpr` inputs are in [`exercise-2/`](exercise-2/). Other large run outputs are intentionally omitted.

If your machine cannot run GROMACS, you can still run the notebook's analysis cells with the supplied `.xvg` files. If you do run the simulations, follow the notebook's order: in particular, the supplied Part 1 topology **already contains ions** and must be used with the ionised structure, not the earlier un-ionised one. Running the commands may replace or create output files under `exercise-1/` and `exercise-2/results/`.
