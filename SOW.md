# Statement of Work

G2 Integrated Solutions ([G2-IS](https://g2-is.com)) would like to upgrade their capacity to simulate spreading of hydrocarbon products (crude oil and refined products) from pipeline breakage events.
Such simulations may be part of the analysis aimed at understanding the potential damage from release of liquid hydrocarbons, 
which federal regulators require of interstate pipeline operators. 
A current simplified model uses transport mechanisms on a topography, obtained using the 
[ArcGIS](https://www.esri.com/en-us/arcgis/about-arcgis/overview) mapping platform with the 
[Spatial Analyst](http://www.esri.com/software/arcgis/extensions/spatialanalyst) extension.
The model is based on flow trajectory, lateral spread and hydrographic transport, 
coupled with 1D open channel flow, and considers effects like evaporation, and infiltration.

The aim of this work is to demonstrate a model with more detailed physics, using 2D shallow-water equations.
This modeling framework simplifies the 3D Navier-Stokes equation for fluid flow, 
assuming that depth of the fluid is very small in scale, compared with the horizontal dimensions.
Several open-source research software packages are available for modeling via the shallow-water equations.
As a starting point, we consider [GeoClaw](http://depts.washington.edu/clawpack/geoclaw/), developed at University of Washington, 
and based in the [Clawpack](http://www.clawpack.org) library for hyperbolic partial differential equations.
These software are under the [3-clause BSD](https://opensource.org/licenses/BSD-3-Clause) open-source license,
a permissive license allowing commercial uses.

We will assess the appropriateness of the shallow-water-equations framework for the target scenario of overland flow
from pipeline rupture points. We will also refine a workflow that G2-IS can adopt for regular use, according to requirements.
All software deliverables will open source, under the permissive 3-clause BSD license.

## Anticipated tasks

1. Modifications to the GeoClaw software will be required to extend its use from tsunami simulation (its original application), to overland hydrocarbon flows. The following modifications are likely to be needed:

	* Moving the friction term from Manning's equation to Darcy-Weisbach equation.
	* Implementing automatic simulation termination based on contact of the hydrocarbon plume with any hydrologic feature (rivers, ponds, lakes, pools, etc.).
	* Allowing a configurable input for the locations and time histories (flow hydrographs) of point sources, representing pipe rupture points.
	* Allowing configurable input for the physical properties of the working fluid (density and viscosity).
	* Outflow boundary conditions from the domain.
	* Adding evaporation and infiltration models, with configurable input parameters.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Other modifications may also be required, based on the input from G2-IS during the course of this project.

2. Performance improvement to achieve runtimes in the order of minutes per rupture point. Possible approaches include:

	* Taking advantage of Clawpack's multi-core parallelism (OpenMP), including Graphical Processing Unit (GPU) processing.
	* Experimenting with different settings for Adaptive Mesh Refinement (AMR).
	* Modifying the code to ignore dry regions.
	* Investigating the use of adaptive time steps.

3. Refining of a workflow for repeated simulation of rupture points, as part of a larger analysis. We will consider the following potential improvements, given that GeoClaw is not user-friendly:

	* Create a simple way to launch simulations, without needing to re-compile for different initial conditions.
	* Simplify the way to configure the various simulation parameters.
	* Integrate with Jupyter Notebooks for seamless workflows and reports.
	* Design for implementation via REST web service.
	* Integrate with Esri GIS software, as needed.
	* For topgraphy data input, incorporate common Esri-supported raster formats, and/or direct read from the Esri [World Terrain](https://www.arcgis.com/home/item.html?id=58a541efc59545e6b7137f961d7de883) web service.
	* For hydrography data input, incorporate common Esri-supported vector formats, and/or direct read from the Esri [USA National Hydrography](https://www.arcgis.com/home/item.html?id=c3cbe1eaf6f4492db74e62f7f4ba2418) web service.
	* Study the use of GPU-enabled Amazon AWS, Microsoft Azure or other cloud services.
	* Output to commonly used GIS file formats: e.g., NetCDF.
	* Resampling of AMR output (in both the X/Y and time domains) to single-resolution, square X/Y mesh and uniform time step to conform to Esri raster format limitations.
	* Consider the workflow using Windows systems, including compiling underlying Fortran libraries for use in Windows operating systems.
	
4. Possible model improvements (research questions):

	* Study the effect of Darcy friction factor.
	* Consider the effect of surface tension.
	* Consider the effect of weather conditions: winds, rains, etc.
