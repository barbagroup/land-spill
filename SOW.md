# Statement of Work

G2 Integrated Solutions ([G2-IS](https://g2-is.com)) would like to upgrade their capacity to simulate spreading of oil products from pipeline breakage events.
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
