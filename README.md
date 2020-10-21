# ebsd2abaqusEuler
Nicolò Grilli

University of Oxford

2020

nicolo.grilli@eng.ox.ac.uk

Abaqus Mesh and Grain Orientation from EBSD using MTEX

The MTEX Matlab package is used to convert EBSD data to Abaqus input file

Please see the following link for the original code:
http://latmarat.net/blog/ebsd2abaqus/

I have added the following feature:
adding rotation matrix for each grain of a polycrystal as
constants for the corresponding user materials

Usage:
Open MTEX and launch:
import EBSD data
import a .ctf file with the EBSD data
set x and y axis according to the convention of your sample and instrument
import the variable "ebsd" in the workspace

EBSD data can be filtered,
non-indexed regions can be removed

clean4fem function identifies the grains

reduce function reduces the size of EBSD map and leads to a coarser mesh in Abaqus

ebsd2abaqusEuler.m
generates an Abaqus input file with one material for each grain in a polycrystal
the user materials contain 10 constants, the last 9 constants are the components
of the rotation matrix for each grain, transforming a vector from the crystal reference frame
to the sample reference frame (Abaqus xyz coordinates)

The three Euler angles of each grain are found by using the following
commands from MTEX:
grainsReconstructed(ii).meanOrientation.phi1;
grainsReconstructed(ii).meanOrientation.Phi;
grainsReconstructed(ii).meanOrientation.phi2;

The Matlab script:
AbaqusTitanium.m
contains an example of EBSD data processing leading to Abaqus input file
with reduced number of elements, non-indexed regions removed and clean grain boundaries

Open Abaqus CAE:
import > Model
and select the input file ebsd.inp generated by the function ebsd2abaqusEuler.m
Assembly must be defined
Boundary conditions must be defined
Generate input file and run Abaqus simulation

See the following paper for an application example:
Nicolò Grilli, Philip Earp, Alan C.F. Cocks, James Marrow, Edmund Tarleton
Characterisation of slip and twin activity using digital image correlation and 
crystal plasticity finite element simulation: Application to orthorhombic α-uranium
Journal of the Mechanics and Physics of Solids 135 (2020) 103800
