# FEM ConstraintContact/ru
---
 GuiCommand:   Name: FEM ConstraintContact   Name/ru: FEM ConstraintContact   MenuLocation: FEM , Constraint contact   ---


</div>



## Описание

Creates a contact constraint between 2 surfaces. Unlike in the case of [tie constraint](FEM_ConstraintTie.md), the surfaces can separate and slide on each other (with or without friction) during the analysis.



## Применение

1.  There are several ways to invoke the command:
    -   Press the **<img src="images/FEM_ConstraintContact.svg" width=16px> [Contact constraint](FEM_ConstraintContact.md)** button.
    -   Select the **Model → Mechanical boundary conditions and loads → <img src="images/FEM_ConstraintContact.svg" width=16px> Contact constraint** option from the menu.

2.  Select the master face. Press the first **Add** button. To remove a face from the selection, click on it and press the first **Remove** button.

3.  Select the slave face. Press the second **Add** button. To remove a face from the selection, click on it and press the second **Remove** button.

4.  Optionally enter a contact stiffness.

5.  
    <small>(v1.0)</small> : Optionally enter a clearance adjustment. All nodes of the slave face whose distance from the master face is smaller or equal to this number will be moved to lie on the master face at the beginning of the analysis. This adjustment doesn\'t cause any strains.

6.  
    <small>(v1.0)</small> : Optionally check the *Enable Friction* box to specify the friction coefficient and stick slope value.

7.  Optionally enter a friction coefficient. Default value of 0 means frictionless contact.

8.  
    <small>(v1.0)</small> : Optionally enter a stick slope value. It\'s an equivalent of contact stiffness for frictional behavior. It defines the slope of the linear relationship between shear stress and relative tangential displacement in the stick range (before slipping occurs).



## Ограничения

-   The contact constraint can only be applied to two faces.
-   Development for multiple contact at once: <https://forum.freecadweb.org/viewtopic.php?f=18&t=15699&start=130#p303275>
-   Because multiple meshes are currently not supported, contact must be applied to faces that are separated by (at least) a small distance. If the faces were touching (no gap between them), the result of a boolean union or boolean fragments operation (necessary to avoid having multiple meshes which is not allowed at the moment) would be a continuous mesh and thus no need to use contact anymore. See [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=18&t=62307).



## Примечания

### Tips for modeling 

-   From: <https://forum.freecadweb.org/viewtopic.php?f=18&p=340874#p340494>
-   The use of linear elements is recommended. Otherwise, calculations can be very time-consuming.
-   Master/slave assignment:
    -   The larger of the two surfaces should act as the master surface.
    -   If the surfaces are of comparable size, the surface on the stiffer body should act as the master surface.
    -   If the surfaces are of comparable size and stiffness, the surface with the coarser mesh should act as the master surface.

### CalculiX

-   The contact stiffness can be estimated as 5 to 50 times the Young\'s modulus of the material. The higher the value for contact stiffness, the harder the contact between surfaces.
-   The slave face is the face that penetrates into the master face and therefore experiences more deformation.
-   The \*CONTACT PAIR card is used for modeling contact in CalculiX. The constraint uses Face-to-Face penalty contact and the contact formulation is explained in detail at <http://web.mit.edu/calculix_v2.7/CalculiX/ccx_2.7/doc/ccx/node112.html>
-   Overview of different contact types: <https://forum.freecadweb.org/viewtopic.php?f=18&t=15699&start=90#p188736>
-   Further interesting information:
    -   <https://forum.freecadweb.org/viewtopic.php?f=18&t=23102#p180709> and following posts !!!
    -   <https://forum.freecadweb.org/viewtopic.php?f=18&t=20276>
    -   <https://forum.freecadweb.org/viewtopic.php?f=18&t=21331>
    -   <https://forum.freecadweb.org/viewtopic.php?f=18&t=15699> (initial contact topic)

-   A very detailed CalculiX contact example. ([link](http://dip28p.web.fc2.com/calculix/netgen2calculix/index.html))

-   An interesting example found in the FreeCAD German subforum. ([link](https://forum.freecadweb.org/viewtopic.php?f=13&t=39663&start=10#p337254))





{{FEM Tools navi

}}



---
⏵ [documentation index](../README.md) > [FEM](Category_FEM.md) > FEM ConstraintContact/ru
