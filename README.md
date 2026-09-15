# TSPTW_results

Data and computational results associated with the paper **“Capturing the
logic of time windows: a dual-based path inequality approach”**, by Jorge
Riera-Ledesma and Inmaculada Rodríguez-Martín.

The repository contains Traveling Salesman Problem with Time Windows (TSPTW)
instances, solutions used as initial upper bounds, and execution results from
the branch-and-cut algorithm described in the paper. The material corresponds
to the experiments in Section **7. Computational study**.

## Contents

```text
input/
├── instances/    TSPTW instances
└── UB/            Solutions used to initialize the upper bound

output/
├── No_UB/         Runs without an initial upper bound
├── BH_UB/         Runs with the basic-heuristic upper bound
└── BK_UB/         Runs with the best-known upper bound
```

The `input/UB` and `output/` directories are organized by instance family.
The distributed families include `AFG`, `Dumas`, `GendreauDumasExtended`,
`Langevin`, `OhlmannThomas`, `SolomonPesant`, and
`SolomonPotvinBengio`. Some upper-bound files also include the
`da_Silva_Urrutia` family.

## Instances

Files in `input/instances/<family>/` are the original TSPTW benchmark
instances. Their original names and extensions are preserved, for example:

```text
input/instances/AFG/rbg016b.tw
input/instances/Dumas/n100w20.001.txt
```

Names usually encode the family, number of vertices, time-window width, or
other characteristics defined by the benchmark authors. The original source
documentation should be consulted for the exact format of each family.

## Initial Upper Bounds

Feasible solutions in `.sol` format are stored under `input/UB/`. An instance
may have a solution in one or both of the following configurations:

- `BH_UB`: solution obtained with the basic heuristic described in Section
  6.2 of the paper.
- `BK_UB`: best-known feasible solution used to initialize the solver.

The `No_UB` configuration does not require files in `input/UB`, since the run
starts without an initial incumbent.

## Results

Each directory under `output/` corresponds to an experimental configuration
and is organized by family. Results may include:

- `.log` files containing the CPLEX and branch-and-cut search logs;
- `.sol` files containing feasible solutions found during the run;
- other auxiliary files generated during the run, when available.

File names make it possible to associate each result with its corresponding
instance. For example, results for `n200w120.001.txt` under the `BH_UB`
configuration are located within `output/BH_UB/OhlmannThomas/`.

## Experimental Configurations

The three configurations reproduce the comparison in Table 2 of the paper:

| Configuration | Initial upper bound | Purpose |
| --- | --- | --- |
| `No_UB` | None | Measure performance without an initial incumbent |
| `BH_UB` | Basic heuristic | Evaluate the algorithm's recommended configuration |
| `BK_UB` | Best-known solution | Measure the effect of an idealized upper bound |

In the published study, `BH_UB` and `BK_UB` solved 248 out of 261 instances
(95.0%), while `No_UB` solved 243 (93.1%). These values are reported in the
paper and provide a reference for checking a new run.

## Experimental Environment

The paper reports the following execution conditions:

- Ubuntu 24.04 LTS;
- Intel Core i5-7500, single core;
- 20 GB of RAM;
- CPLEX 22.1 through the Callable Library;
- compiled with `gcc 13.3.0` and `-O2`;
- a time limit of 10,800 seconds per instance, unless otherwise stated.

This repository contains the data and experimental outputs, but does not
include the source code for the branch-and-cut algorithm or CPLEX. Re-running
the algorithm requires a compatible implementation and a CPLEX license.

## Reference

J. Riera-Ledesma and I. Rodríguez-Martín, *Capturing the logic of time
windows: a dual-based path inequality approach*, 2026.

The mathematical details of the temporal verifier, Farkas certificates, iPEC
inequalities, and tournament, fixed-endpoint, and hybrid strengthenings are
provided in the associated paper.

## License

The contents of this repository are released under [CC0 1.0
Universal](LICENSE), unless explicitly stated otherwise for a file originating
from an external source.
