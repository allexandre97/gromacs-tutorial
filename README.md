# Biomolecular simulation with GROMACS

This is a short introduction to biomolecular simulation. Start with **[Exercises.ipynb](Exercises.ipynb)**: it contains the explanations, terminal commands, analysis code and questions for discussion.

- **Part 1:** prepare a small protein in water, minimise its energy, and equilibrate it in NVT and NPT.
- **Part 2:** compare how thermostat and barostat choices affect dynamics and volume fluctuations.

The tutorial is designed for a 90-minute session. All the simulations have been pre-run and their outputs are provided, so you can spend your time interpreting the results. We will probably **not** have time to run the simulations during class, but the notebook contains every command in case you want to repeat them yourself.

## Getting started

The [environment file](environment.yml) specifies GROMACS 2026.3, Python 3.12, JupyterLab and the packages used by the notebook. With Conda or Mamba installed, from the repository directory run:

```bash
conda env create -f environment.yml
conda activate gromacs-tutorial
jupyter lab
```

You can also run it in Binder (the link opens version `v1.0` of the tutorial):

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/allexandre97/gromacs-tutorial/v1.0?urlpath=%2Fdoc%2Ftree%2FExercises.ipynb)

Open `Exercises.ipynb` in JupyterLab. Run its Python cells in order. Commands shown in fenced `bash` blocks belong in a **terminal opened in this repository directory**, not in Python cells. If you work elsewhere, the relative paths in the notebook will not resolve. If you repeat the simulations, see the note on performance in the notebook for how to use several cores.

## Files and precomputed data

- [`structures/2RVD.pdb`](structures/2RVD.pdb) is the starting structure.
- [`mdp/`](mdp/) contains the simulation settings. The `ex2_*.mdp` files define the four Part 2 comparisons.
- [`exercise-1/`](exercise-1/) is the working directory for Part 1. It already contains the outputs of the quick preparation steps (box, solvation, topology, ions and energy minimisation), so the notebook's visualisation cells work even if a command fails. Running the commands yourself will replace these files with equivalent ones.
- [`exercise-1/reference/`](exercise-1/reference/) holds the reference data: a consistent copy of the ionised structure and topology, the minimisation results, and the pre-run NVT and NPT equilibrations with their extracted `.xvg` files. The Part 1 analysis cells read from here.
- [`exercise-2/reference/`](exercise-2/reference/) holds the pre-run Part 2 simulations: their `.tpr` inputs, `.edr` energy files, extracted temperature, MSD and NPT energy/volume data, and the two NVT `.xtc` trajectories needed to recalculate the water MSD. Other large run outputs are intentionally omitted. The Part 2 analysis cells read from here.

Commands you run yourself write to `exercise-1/` and `exercise-2/`, never to the `reference/` folders. If you run the simulations and want to plot your own results, change the paths in the analysis cells. Follow the notebook's order: in particular, the ionised topology must be used with the ionised structure, not the earlier un-ionised one. If your preparation files get out of sync, copy `2RVD_ions.pdb`, `2RVD_topol.top` and `2RVD_posre.itp` from `exercise-1/reference/` back into `exercise-1/`.
