---
 GuiCommand:
   Name: FEM EquationFluxsolver
   Name/ru: FEM EquationFluxsolver
   Icon: Fem-equation-fluxsolver.svg
   MenuLocation:  Solve , Equation fluxsolver
   Workbenches: FEM_Workbench/ru
   Shortcut: 
   SeeAlso: FEM_tutorial/ru
---

# FEM EquationFlux/ru


</div>

## Description


<div class="mw-translate-fuzzy">

В разработке\...


</div>

For info about the math of the equation, see the [Elmer models manual](http://www.elmerfem.org/blog/documentation/), section *Flux Computation*.

## Usage

1.  After adding an Elmer solver as described [here](FEM_SolverElmer#Equations.md), select it in the [tree view](Tree_view.md).
2.  Either use the toolbar button <img alt="" src=images/FEM_EquationFlux.svg  style="width:24px;"> or the menu **Solve → Flux equation**.
3.  Now either add a heat equation (toolbar button <img alt="" src=images/FEM_EquationHeat.svg  style="width:24px;"> or menu **Solve → [Heat equation](FEM_EquationHeat.md)**) or an electrostatic equation (toolbar button <img alt="" src=images/FEM_EquationElectrostatic.svg  style="width:24px;"> or menu **Solve → [Electrostatic equation](FEM_EquationElectrostatic.md)**). This is important because the flux equation needs the boundary conditions set for these equations.
4.  When using the electrostatic equation, change the property **Flux Coefficient** to *None*. and the property **Flux Variable** to *Potential*.
5.  Change the [equation\'s solver settings](#Solver_Settings.md) or the [general solver settings](FEM_SolverElmer_SolverSettings.md) if necessary.

## Solver Settings 

For the general solver settings, see the [Elmer solver settings](FEM_SolverElmer_SolverSettings.md).

The flux equation provides these special settings:

-    **Average Within Materials**: If `True`, continuity is enforced within the same material in the discontinuous Galerkin discretization using the penalty terms of the discontinuous Galerkin formulation.

-    **Calculate Flux**: Calculates the flux vector.

-    **Calculate Flux Abs**: Calculates the absolute of the flux vector. Requires that **Calculate Flux** is `True`.

-    **Calculate Flux Magnitude**: Computes the magnitude of the vector field. Requires that Basically it is the same as **Calculate Flux Abs** but this requires less memory because it solves the matrix equation only once. The downside is that negative values may be introduced.

-    **Calculate Grad**: Calculates the gradient of the flux.

-    **Calculate Grad Abs**: Calculates the absolute flux gradient. Requires that **Calculate Grad** is `True`.

-    **Calculate Grad Magnitude**: Computes the magnitude of the vector field. Requires that Basically it is the same as **Calculate Grad Abs** but this requires less memory because it solves the matrix equation only once. The downside is that negative values may be introduced.

-    **Discontinuous Galerkin**: For discontinuous fields the standard Galerkin approximation enforces continuity which may be unphysical. As a remedy for this, set this property to `True`. Then the result may be discontinuous and may even be visualized as such.

-    **Enforce Positive Magnitude**: If `True`, the negative values of the computed magnitude fields are set to zero.

-    **Flux Coefficient**: Name of the proportionality coefficient to compute the flux.

-    **Flux Variable**: Name of the potential variable used to compute the gradient.

## Analysis Feature Information 

The flux equation does not have its own boundary conditions. It takes the boundary conditions from the <img alt="" src=images/FEM_EquationHeat.svg  style="width:24px;"> [Heat equation](FEM_EquationHeat.md) or the <img alt="" src=images/FEM_EquationElectrostatic.svg  style="width:24px;"> [Electrostatic equation](FEM_EquationElectrostatic.md).

## Results

The available results depend on the [solver settings](#Solver_Settings.md). If none of the **Calculate *** settings was set to `True`, nothing is calculated. Otherwise the corresponding results will also be available.

The resulting flux is either the heat flux in $\rm W/m^2$ (misleadingly named \"temperature flux\") or the potential flux in $\rm W/m^2$ ($\rm A\cdot V/m^2$).





{{FEM Tools navi

}}



---
⏵ [documentation index](../README.md) > [FEM](Category_FEM.md) > FEM EquationFlux/ru
