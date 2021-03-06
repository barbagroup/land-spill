# Available solver/code review

We searched open-source shallow-water equation solvers and tried to find
candidates. Note we only focused on solvers for full 2D shallow-water equations. 
The solvers for diffusive or kinematic wave approximations are not considered 
here. 

The focuses are:

1. Solver completeness: if a solver has more features that we require, we deem 
   it more complete because that means we need fewer code modifications.

2. The difficulty in modifying source code: we have to consider the programming
   language used and the code design of the candidate solvers. Easy-to-understand
   source code can facilitate the code modification tasks. The way to evaluate
   this is somehow subjective, however.

3. Software usability: we evaluate the software usability from end-users' aspect.
4. Open-source license.
5. Support from original development teams: whether the developments of the
   solvers are still active and whether the developers will likely to respond 
   to issues.

The essential solver features include:

1. Topography term
2. Friction models
3. Adaptive mesh refinement
4. Adaptive time steps
4. Well-balanced schemes
5. Dry/wet handling and positive preserving
6. Outflow/open boundary conditions
7. Parallelism (at least OpenMP)
8. Flow terminations when encountering water bodies
9. Evaporation models
9. Infiltration models
10. Point source terms

We evaluate software usability based on the following required software features:

1. Commonly-seen topography file format I/O: NetCDF (CF conventions) and Esri ASCII
2. Commonly-seen water body data or shapefiles I/O
3. Compressed output files, such as compressed HDF5 or compressed NetCDF
2. Methods to specify simulation parameters.
3. Ways to launch simulation.

Regarding the software usability, the performance should be a key factor from
users' aspect. However, we exclude this factor in at this stage because we do 
not have enough time to conduct a thorough performance study and comparison. 
We should do this in the future, if possible.

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
      there is a utility for converting ArcGIS file format to the customized 
      format.
    * No adaptive mesh refinement: an otem of news in 2015 from software repo 
      says now they support AMR, but no mention of AMR in the documentation, and 
      no examples using AMR.
    * Parallelization: an MPI version is under development and not yet released, 
      according to the 2017 paper. No mention of parallelization in the 
      documentation and no examples.

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
    * No AMR, but support unstructured mesh. However, unstructured meshes may 
      not be suitable for automatic and batched simulation processes. Unstructured
      meshes usually require users' manual pre-processing.
    * No support for commonly-used file formats. They use their own format for 
      I/O. So we will have to read the manual to understand the format and develop 
      some converters.
    * Lack of documentation for detailed numerical schemes or models used. 
      However, the documentation is useful for end-users who do not care about 
      what is behind the software.
    * Doesn't seem to have outflow/open BC.

## DassFlow

* Website: http://www.math.univ-toulouse.fr/DassFlow/

* Papers: https://www.math.univ-toulouse.fr/DassFlow/references.html

* Solver feature:
    * MPI parallelization
    * Manning's friction model
    * Wet/dry problem
    * Well-balanced schemes
    * Topology

* Source code:
    * Language: Fortran and Python

* License: CeCILL (http://www.cecill.info/)

* Support and development: active

* Drawbacks:
    * No AMR. They use unstructured meshes, which require manual pre-processing.
    * To download the software, users require to fill out some forms and waiting
      for their approvals. Also, users are asked to create an account on SourceSup.
      It's not exactly "freely downloadable" software, from my personal viewpoint.

## GeoClaw

* Website:
    * Official website: http://depts.washington.edu/clawpack/geoclaw/
    * GitHub repo: https://github.com/clawpack/geoclaw

* Papers:
    * Berger, M. J., George, D. L., LeVeque, R. J., & Mandli, K. T. (2011). The 
      GeoClaw software for depth-averaged flows with adaptive refinement. 
      Advances in Water Resources, 34(9), 1195–1206.
    * González, F. I., Leveque, R. J., Chamberlain, P., Hirai, B., Varkovitzky, 
      J., & George, D. L. (2011). Validation of the GeoClaw Model. In NTHMP MMS 
      Tsunami Inundation Model Validation Workshop.
    * Arcos, M. E. M., & LeVeque, R. J. (2015). Validating Velocities in the 
      GeoClaw Tsunami Model Using Observations near Hawaii from the 2011 Tohoku
      Tsunami. Pure and Applied Geophysics, 172(3–4), 849–867.
    * LeVeque, R. J., George, D. L., & Berger, M. J. (2011). Tsunami modelling 
      with adaptively refined finite volume methods. Acta Numerica, 20(2011), 
      211–289.

* Solver features:
    * Topography handling
    * Manning's friction model
    * Adaptive mesh refinement
    * Adaptive time stepping
    * OpenMP parallelization
    * Well-balanced schemes
    * Dry/wet handling and positive preserving

* Source code:
    * Language: Fortran 77, Fortran 95, and Python
    * Users need to write some Fortran code/routines and re-compile the program
      to set up simulations.
    * The source code and software design is not difficult to understand.

* Software usability:
    * Several topography file formats are accepted: Esri ASCII and NetCDF
    * Output file formats include Esri ASCII format.
    * GeoClaw uses Python scripts to specify simulation settings and parameters.

* License: BSD 3-Clause

* Support and development: active

* Drawbacks:
    * No support to distributed-memory systems.
    * No NetCDF output support.
    * The core kernels are in Fortran 77 fixed format, which is annoying and
      not friendly from the aspect of code modification.

## Gerris

* Website: http://gfs.sourceforge.net/

* Gerris has stopped development for 5 years. And I'm not able to compile
  and build it with the compilers and third-party dependencies currently
  available on our workstations.

## Basilisk

* Websites: http://basilisk.fr/

* Papers: 
    * http://basilisk.fr/Bibliography
    * Popinet, S. (2011). Quadtree-adaptive tsunami modelling. Ocean Dynamics, 
      61(9), 1261-1285.

* Solver features (the pre-built SWE solver):
    * AMR
    * Well-balanced
    * Wet/dry problem and positivity-preserving
    * Topography term

* Source code:
    * Language: C and its own domain-specific language (DSL)
    * Basilisk is more like a toolbox or library for hyperbolic PDE solvers.
      Users create their own solvers through a DSL-like language. There are
      already some pre-built solvers provided in Bisilisk, and one of them is
      a full SWE solver.
    * The DSL-like language is largely based on C.

* License: GPL-v3 

* Support and development: active

* Drawbacks:
    * The pre-built SWE solver is very basic. The solver seems to be for the
      purpose of teaching in numerical PDE classes. To extend the solver to 
      real-world applications, it may require a lot of work and may not be more 
      efficient than developing a solver from scratch.
    * The DSL is largely based on C, and requires a compiler-like executable 
      binary file to parse the source code of the solver. The executable
      binary will translate the DSL source into C and call GCC to compile it.
      From my viewpoint, it's not convenient, though it may be a good thing from
      the viewpoint of teaching a PDE class.

## Reef3D

* Websites: https://reef3d.wordpress.com/

* Papers: https://reef3d.wordpress.com/publications-reef3d/

* Solver features:
    * MPI parallelization
    * Adaptive time stepping
    * Turbulence modeling
    * Multigrid solvers (through Hypre)
    * Many different numerical schemes available.

* Source code:
    * C++
    * The source files are not well-organized. Everything is inside a single
      folder. And due to Reef3D is a collection of three different flow solvers,
      it's not easy to identify what are files or code for the SWE solver. And
      the documentation is more end-user oriented, there's no mention of the
      software design and no useful code documentation. Many undocumented source
      files.

* License: The users' guide says it's GPL. But no license file or headers provided.

* Support and development: active

* Drawbacks:
    * The main functionality of Reef3D is to solve 3D Navier-Stokes equations with 
      free surfaces. Though Reef3D also has a 2D SWE solver, it's not 
      well-documented. There's not even a single example for the 2D SWE solver.
    * No AMR support. Reef3D uses unstructured meshes.
    * No support for common topography file formats.
    * Setting up the simulation parameters are not intutive. Reef3D uses characters
      and codes to represet different parameters. It does not use readable strings
      for that. For example, to set the time-step size with 0.01 sec, users have 
      to write "N 49 0.01" in their input files, instead of something more readable
      like "dt = 0.01".

## Other possibilities:
* ANUGA: 
    * https://anuga.anu.edu.au/
    * Still active
    * Unstructured meshes
* Firedrake-fluids
    * https://github.com/firedrakeproject/firedrake-fluids
    * Inactive for 3 years
    * Looks like a toy project for one single paper
    * Requires many third-party dependencies
* Floodrake
    * https://github.com/firedrakeproject/flooddrake
    * Inactive for 1.5 year
    * Looks like an one-man job or a student project
