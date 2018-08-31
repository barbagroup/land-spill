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
2. Friction models
3. Adaptive mesh refinement
4. Adaptive time steps
4. Well-balance schemes
5. Dry/wet handling and positive preserving
6. Outflow/open boundary conditions
7. Parallelism (at least OpenMP)
8. Flow terminations when encountering water bodies
9. Evaporation models
9. Infiltration models
10. Point source terms

We evaluate software usability based on the following required software features:

1. Commonly-seen topography file format I/O: NetCDF (CF conventions) and Esri ASCII
2. Commonly-seen hydrophysic data I/O
3. Compressed output files, such as compressed HDF5 or compressed NetCDF
2. Methods to specify simulation parameters.
3. Ways to launch simulation.

Regarding the software usability, the performance should be a key factor from
users' aspect. However, we exclude this factor in at this stage because we don't
have enough time to conduct a thourough performance study and comparison. But
we should do this in the future, if possible.

## FullSWOF: Full Shallow Water equations for Overland Flow

* Websites:
    * Official website: https://www.idpoisson.fr/en/fullswof/
    * Code repo: https://sourcesup.renater.fr/

* Papers:
    * Delestre, O., Darboux, F., James, F., Lucas, C., Laguerre, C., & Cordier, S. 
      (2017). FullSWOF: Full Shallow-Water equations for Overland Flow. The Journal of 
      Open Source Software, 2(20), 448. https://doi.org/10.21105/joss.00448

* Solver features:
    * Well-balanced schemes
    * Dry/wet handling and positivity preserving
    * Various friction models: Manning's, Darcy-Weisbach, Chezy
    * Rainfall modeling
    * Infiltration model: Green-Ampt model
    * Topography term
    * Adaptive time steps
    * Neumann BC (similar to outflow/open BC, but not exactly the same)

* Source code:
    * Language: C++
    * Programming model: objected-oriented, modularized
    * Easy to modify the code or implement new features

* Software usability:
    * GUI (another standalone program written in Java)
    * ASCII file input for parameters

* License: CeCILL-V2 (GPL-compatible)

* Support and development: active

* Drawbacks:
    * The solver itself only accepts customized topography file format, though 
      there is an utility for converting ArcGIS file format to the customized 
      format.
    * No adaptive mesh refinement: a news in 2015 from software repo says now 
      they support AMR, but no mention of AMR in the documentation, and no 
      examples using AMR.
    * Parallelization: a MPI version is under development and not yet released, 
      according to the 2017 paper. No mention of parallelization in the 
      documention and no examples.

## TELEMAC-MASCARET

* Website: http://www.opentelemac.org/

* Papers: http://www.opentelemac.org/index.php/publications

* Solver features
    * MPI parallelization
    * Friction models
    * Coriolis force
    * Rain and wind effects
    * Evaporation models
    * Turbulence models
    * Dry/wet problem
    * Porosity phenomena (probabily inflitration)
    * Oil spill modelling (oil on water surfaces)
    * Support both finite element and finite volume methods

* Source code:
    * Language: Fortran 95 and Python
    * Sometimes it requres user-provided Fortran code/routines to set up the 
      simulations.

* License: not clear. Some of the source files have the GPL license in their 
  header sections. But many of them don't. And there's no LICENSE file in the 
  project.

* Drawbacks:
    * Parallel version requires some third-party domain partitioning library.
      This may be annoying when packaging the software and shipping it as an end 
      product.
    * No AMR, but support unstructured mesh. However, I think unstructured mesh
      is not suitable for automatical and batch simulation processes. Unstructured
      mesh usually requires users' manual pre-processing.
    * No support for commonly-used file formats. They use their own format. And
      we'll have to read the manual to understand the format and develop some 
      converters.
    * Lack of documentation for detailed numerical schemes or models used. 
      However, the documentation is good for end-users who don't care about what 
      are behind the software.
    * Doesn't seem to have outflow/open BC.

## DassFlow
## GeoClaw
## Gerris/Basilisk
