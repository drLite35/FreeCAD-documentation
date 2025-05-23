---
 GuiCommand:Container|
{{GuiCommand
   Name: FEM ConstraintCurrentDensity
   MenuLocation: Model , Electromagnetic boundary conditions , Current density boundary condition
   Workbenches: FEM_Workbench
   Version: 0.21
   SeeAlso: FEM_EquationMagnetodynamic, FEM_EquationMagnetodynamic2D
}}
{{GuiCommandFemInfo
   Solvers: Elmer
}}
---

# FEM ConstraintCurrentDensity

## Description

Creates a FEM boundary condition for the current density. To be used together with the [Magnetodynamic](FEM_EquationMagnetodynamic.md) and [Magnetodynamic 2D](FEM_EquationMagnetodynamic2D.md) equations.

## Usage

1.  Press the **<img src="images/FEM_ConstraintCurrentDensity.svg" width=16px> [Current density boundary condition](FEM_ConstraintCurrentDensity.md)** button or use the menu **Model → Electromagnetic boundary conditions → <img src="images/FEM_ConstraintCurrentDensity.svg" width=16px> Current density boundary condition**.
2.  Press the **Add** button.
3.  In the [3D view](3D_view.md) select the object the boundary condition should be applied to.

## Options

-   **Current density\_\*\_1**: The real/imaginary part of the current density in x-direction in A/m². For other coordinate systems than Cartesian 3D, this will be the first coordinate of the system instead of x.
-   **Current density\_\*\_2**: The real/imaginary part of the current density in y-direction in A/m². For other coordinate systems than Cartesian 3D, this will be the second coordinate of the system instead of y.
-   **Current density\_\*\_3**: The real/imaginary part of the current density in z-direction in A/m². For other coordinate systems than Cartesian 3D, this will be the third coordinate of the system instead of z. If the coordinate system has no third coordinate, this setting will be ignored.
-   **Current density\_\*\_\*\_Disabled**: Whether the corresponding parameter is disabled (assumed as unknown by the solver).




 {{FEM Tools navi}}



---
⏵ [documentation index](../README.md) > [FEM](Category_FEM.md) > FEM ConstraintCurrentDensity
