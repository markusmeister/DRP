# How to compute the "density recovery profile" of a set of locations
## Purpose
The goal is to test whether a population of neuronal cell bodies are spaced at regular distances from each other. The starting data are the $(x,y)$ points of cell bodies in a plane restricted to an observation window $W$. The null hypothesis is that all the points are statistically independent, like raindrops falling onto the surface $W$. 

A convenient test for this null hypothesis is the spatial autocorrelation function of the set of locations. This is the density of cells as a function of the displacement vector from any other cell. If one averages this over all directions of the displacement vector it becomes the density of cells as a function of distance from any other cell. This function is often called the "density recovery profile" (e.g. Rodieck 1991).

This notebook is about the practicalities of computing the density recovery profile. Most of the mental effort goes into dealing with edge effects that come from observing a finite window. Correcting for the shape of that window allows you to use the available data most efficiently.

The last part adds a parametric model for a regular set of locatons that can be useful for fitting a DRP.
## Table of contents

    1  How to compute the "density recovery profile" of a set of locations
        1.1  Purpose
        1.2  Examples
            1.2.1  On and Off Alpha cells in cat retina (Wässle 1981)
            1.2.2  Cones in chicken retina (Kram 2020)
            1.2.3  Ganglion cells of type W3 in mouse retina (Zhang 2012)
    2  The DRP in a finite observation window
        2.1  Theory for a rectangular window
        2.2  Analysis routines for a rectangular window
            2.2.1  Load the data from Wässle 1981 and histogram the pairwise distances between cells
            2.2.2  Compute the cell density by normalizing to the available area
            2.2.3  Add error bars
            2.2.4  Combining everything
        2.3  Non-rectangular windows
            2.3.1  Right triangle shape
            2.3.2  Arbitrary polygon shape
    3  A model of cells on a lattice
        3.1  Contribution from one cell
        3.2  All cells
        3.3  Simulation of cells on a jittered lattice
    4  References