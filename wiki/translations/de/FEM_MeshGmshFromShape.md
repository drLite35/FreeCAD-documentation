---
 GuiCommand:Container|
{{GuiCommand/de
   Name: FEM MeshGmshFromShape
   Name/de: FEM NetzGmshAusForm
   MenuLocation: Netz , FEM-Netz aus Form - Gmsh
   Workbenches: FEM_Workbench/de
   SeeAlso: FEM_tutorial/de
}}
{{GuiCommandFemInfo/de
   Solvers: Alle
}}
---

# FEM MeshGmshFromShape/de



## Beschreibung

Für eine Finite-Elemente-Analyse muss die Geometrie in ein [FEM-Netz](FEM_Mesh/de.md) diskretisiert werden. Dieser Befehl verwendet die Software [Gmsh](https://en.wikipedia.org/wiki/Gmsh) (die auf dem System installiert sein muss) zum Erstellen des Netzes.

Abhängig vom Betriebssystem und dem Installationspaket kann Gmsh in FreeCAD enthalten sein oder auch nicht. Für weitere Informationen siehe [FEM Installation](FEM_Install/de.md).



## Anwendung

1.  Die Form auswählen, die analysiert werden soll. Bei der Volumen-FEM muss es sich um einen Festkörper oder Compsolid (zusammengesetzten Festkörper) handeln. Ein Compsolid ist erforderlich, wenn dein Teil aus mehreren Materialien besteht. (Ein Compsolid kann mit dem Befehl [BoolescheFragmente](Part_BooleanFragments/de.md) erstellt werden).
2.  Das Werkzeug durch eine der folgenden Möglichkeiten aktivieren:
    -   Die Schaltfläche **<img src="images/FEM_MeshGmshFromShape.svg" width=16px> [FEM-Netz aus Form - Gmsh](FEM_MeshGmshFromShape/de.md)** drücken.
    -   Den Menüeintrag **Netz → <img src="images/FEM_MeshGmshFromShape.svg" width=16px> FEM-Netz aus Form - Gmsh** auswählen.
3.  Wahlweise minimale und maximale Elementgröße anpassen (Die vorgegebene Einstellung erstellt oft zu grobe Netze). Es kann auch die dimensionale Art (1D, 2D, 3D) eingestellt (wobei die Voreinstellung *From shape* meistens passt) sowie die Ordnung des Elements geändert werden.
4.  Die Schaltfläche **Anwenden** anklicken und warten, bis die Erstellung des Netzes abgeschlossen ist. {{Version/de|1.0}}: Wahlweise die Schaltfläche **Abbrechen** drücken, um das Vernetzen abzubrechen.
5.  Die Schaltfläche **OK** drücken, um die Aufgabe abschließen. Jetzt sollte sich ein neues FEMMeshGmsh-Objekt im aktiven Analysebehälter befinden. Oder die Schaltfläche **Abbrechen** drücken, um die Änderung oder die Erstellung des Netzobjekts abzubrechen.

Nachdem das Netz erstellt wurde, können seine Eigenschaften im [Eigenschafteneditor](Property_editor/de.md) angepasst werden. Nach dem Ändern einer Eigenschaft, muss der Gmsh-Dialog erneut geöffnet und die Schaltfläche **Anwenden** gedrückt werden (der Dialog kann geöffnet bleiben, während weitere Eigenschaften geändert werden).

The **Gmsh version** button allows you to check the details about the currently linked Gmsh binary.



## Eigenschaften

-    **Algorithm2D**: The algorithm to create 2D meshes. The different algorithms are [explained here](https://gmsh.info/doc/texinfo/gmsh.html#Choosing-the-right-unstructured-algorithm). For Delaunay, see [Delaunay triangulation](https://en.wikipedia.org/wiki/Delaunay_triangulation).

-    **Algorithm3D**: The algorithm to create 3D meshes. The different algorithms are [explained here](https://gmsh.info/doc/texinfo/gmsh.html#Choosing-the-right-unstructured-algorithm).

-    **Characteristic Length Max**: The maximal size of the mesh elements. If set to *0.0*, the size will be set automatically. This property can also be changed in the Gmsh dialog in the field **Max element size**.

-    **Characteristic Length Min**: The minimal size of the mesh elements. If set to *0.0*, the size will be set automatically. This property can also be changed in the Gmsh dialog in the field **Min element size**.

-    **Coherence Mesh**:

    -   true (default); duplicate mesh nodes will be removed
    -   false

-    **Element Dimension**: The dimension of the mesh elements. This property can also be changed in the Gmsh dialog in the field **Mesh element dimension**.

    -   From Shape (default); the dimension will be determined from the dimension of the object that is meshed
    -   1D
    -   2D
    -   3D

-    **Element Order**: The [mesh element order](https://www.comsol.de/support/knowledgebase/1270). This property can also be changed in the Gmsh dialog in the field **Mesh order**. <small>(v0.20)</small> 

    -   1st
    -   2nd (default)**Note:** If you use the solver [Elmer](FEM_SolverElmer.md) you may get this error: *ERROR:: GetEdgeBasis: Can\'t handle but linear elements, sorry.* This means the solver equation cannot handle 2nd order meshes. Use either 1st order meshes then, or check the FreeCAD Wiki page for the solver equation for possible options to handle 2nd order meshes.

-    **Geometrical Tolerance**: The geometrical tolerance for the mesh to match the object edges. The default *0.0* means that Gmsh\'s default of 1e-8 is used.

-    **Groups Of Nodes**: All nodes and not only the elements will be saved for each physical mesh group. Physical groups are collections of mesh entities (points, curves, surfaces and volumes). They and are identified by their dimension and by a tag. For example a mesh of the same object region is internally tagged the same. So all surfaces of this region will form one physical group.

-    **High Order Optimize**: If and how meshes with <small>(v0.20)</small>  Gmsh supports different optimization algorithms. **Elastic** is an algorithm in which the mesh elements are treated as a collection of deformable viscoelastic solids. 1st order meshes cannot be optimized because their element borders are linear an cannot be deformed.

-    **Mesh Size From Curvature**<small>(v0.20)</small> : The number of mesh elements per $2\pi$ times the radius of the curvature. To get a finer mesh at small corners or holes, this value can be increased for better results

<img alt="" src=images/FEM_Gmsh-MeshSizeFromCurvature.png  style="width:450px;"> 
*Effect of  ''Mesh Size From Curvature'''; left: set to 12, right: deactivated*

-    **Optimize Netgen**: Whether the mesh will be optimized using the 3D mesh generator [Netgen](https://github.com/NGSolve/netgen) to improve the quality of tetrahedral elements. **Note:** since Netgen can only create tetrahedral elements, this option is ignored for meshes whose **Element Dimension** is not *3D*.

-    **Recombination Algorithm**<small>(v0.20)</small> : The algorithm used for **Recombine 3D All** and also for **Recombine All**. For more info, see section [Element Recombination](#Element_Recombination.md) and for technical details see the [Gmsh documentation](https://www.gmsh.info/doc/texinfo/gmsh.html#t11).

-    **Recombine 3D All**<small>(v0.20)</small> : Applies a recombination 3D-algorithm to all volumes. Tetrahedra will be recombined into prisms, hexahedra or pyramids if possible.

-    **Recombine All**: Applies a recombination algorithm to all surfaces. Triangles will be recombined into quadrangles when possible.

-    **Optimize Std**Optimizes the mesh to improve the quality of tetrahedral elements.

-    **Second Order Linear**: Option if second order nodes (if **Element Order** set to *2nd*) and/or mesh refinement points are created by linear interpolation.

    -   true; linear interpolation is used
    -   false (default); curvilinear interpolation is used

-    **Subdivision Algorithm**<small>(v1.0)</small> : allows the creation of quadrilateral and hexahedral elements by subdivision

    -   None; doesn\'t use any subdivision algorithm
    -   All Quadrangles; creates quadrilateral elements by subdivision
    -   All Hexahedra; creates hexahedral elements by subdivision
    -   Barycentric; creates triangular elements by barycentric subdivision



## Hinweise

### Nonpositive Jacobians 

When you get a meshing error about nonpositive Jacobians, you can try out the following strategies:

-   Set **Second Order Linear** to *true* but keep **Element Order** at *2nd*.
-   Set **Element Order** to *1st*.
-   Use a smaller element size by reducing the **Characteristic Length Max**.
-   If solver ccxtools is used and the run button is used (not the task panel) the nodes of nonpositive jacobian elements will be green.

### Mesh Growth 

At edges and small geometric entities, the mesh has to be smaller than in areas without edges. So the mesh element size grows away from the edges. The growing strategy of Gmsh is to grow between edges of different sizes. So the growing fails when an area has the same sized edges like for example this tube:

<img alt="" src=images/FEM_Gmsh-MeshGrowth-failing.png  style="width:400px;"> 
*Failing mesh growing because the cylindrical area is surrounded by the same edges*

To enable a sensible mesh growing, you must in this case add an edge to the area. In the example, this would be a circle in the middle of the cylinder. The circle is added as part of a [BooleanFragments](Part_BooleanFragments.md) compound (to form a CompSolid), see [the project file](https://forum.freecadweb.org/download/file.php?id=146255) of the example.

<img alt="" src=images/FEM_Gmsh-MeshGrowth-success.png  style="width:400px;"> 
*Sensible mesh growing due to the additional edge in the middle of the cylindrical area*

### Element Recombination 

Elements can be recombined in two ways, on the surface of objects so that triangles will be recombined into quadrangles if possible and in the volume of objects so that tetrahedra will be recombined into prisms, hexahedra or pyramids if possible. Thinking about the geometry, it becomes clear that the recombination result depends strongly on the geometry of the body and that recombining a 3D body only at the surface will mostly lead to strange results.

To illustrate this, look at the image below. A cuboid body is meshed using the standard settings (tetrahedra, 2nd order mesh). This is the subimage at the upper left. The image at the upper right shows the result, when additionally the elements are recombined only at the surface of the body. The result is bad because the changed surface elements don\'t fit to the unchanged volume elements. So When we use now also **Recombine 3D All**, the result is better, see the lower left subimage. However, the result doesn\'t show a great difference compared to the mesh without recombinations. Since our body is a cuboid, it is therefore sensible to use a recombination algorithm that tries to create cuboids as well. And this result is shown in the subimage at the lower right.

The *Simple* recombination algorithm will leave some triangles in the mesh in case the recombining leads to badly shaped quads. In such cases use a *full-quad* recombination algorithm, which will automatically perform a coarser mesh followed by the recombination, smoothing and subdividing. See [forum topic](https://forum.freecadweb.org/viewtopic.php?f=18&t=20351#p520392)

<img alt="" src=images/FEM_Gmsh-Recombination.png  style="width:600px;"> 
*Effect of mesh element recombination.<br>
Upper left: standard mesh.<br>
Upper right: recombination only at the surface using the '''Simple''' algorithm.<br>
Lower left: recombination at the surface and in the volume using the '''Simple''' algorithm.<br>
Lower right: recombination at the surface and in the volume using the '''Simple full-quad''' algorithm*





{{FEM Tools navi

}}



---
⏵ [documentation index](../README.md) > [FEM](Category_FEM.md) > FEM MeshGmshFromShape/de
