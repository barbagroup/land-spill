# Available solver/code review

We did a search for open-source shallow-water equation solvers and try to find
candidates. Note we only focus on solvers for full 2D shallow-water equations. 
The solvers for diffusive or kinematic wave approximations are not considered 
here. 

The focuses are:

1. Solver completeness: if a solver has more features that we require, it is 
deemed more complete because that means we need fewer code modifications.

2. Difficulty of code modifications: we have to consider the programming
language used and the code design of the candidate solvers. Easy-to-understand
source code can facilitate the code modification tasks. The way to evaluate
this is somehow subjective, though.

3. Software usability: we evaluate the software usability from users' aspect.
4. Open-source license.
5. Support from original development teams: whether the development of the
solvers are still active and whether the developers will likely to respond issues.

The required solver features includes:

1. Topography term
2. Friction term
3. Adaptive mesh refinement
4. Adaptive time steps
4. Well-balance schemes
5. Dry/wet handling and positive preserving
6. Outflow/open boundary conditions
7. Parallelism (at least OpenMP)
8. Flow terminations when encountering water bodies
9. Evaporation models
10. Point source terms

We evaluate software usability based on the following required software features:

1. Common-seen topography file format I/O: NetCDF (CF conventions) and Esri ASCII
2. Methods to specify simulation parameters.
3. Ways to launch simulation.

Regarding the software usability, the performance should be a key factor from
users' aspect. However, we exclude this factor in at this stage because we don't
have enough time to conduct a thourough performance study and comparison. But
we should do this in the future, if possible.

## FullSWOF
