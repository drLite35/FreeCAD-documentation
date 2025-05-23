---
 GuiCommand:
   Name: Mesh VertexCurvature
   MenuLocation: Meshes , Curvature plot
   Workbenches: Mesh_Workbench
   SeeAlso: Mesh_CurvatureInfo
---

# Mesh VertexCurvature/de



## Beschreibung

Der Befehl **Mesh Knotenkrümmumg** erstellt Mesh-Krümmumgsobjekte (\*\_Curvature objects) für Mesh-Objekte (Netzobjekte). Ein Krümmumgsobjekt stellt die Krümmung eines Netzes dar und setzt unterschiedliche Farben für konvexe, ebene und konkave Bereiche ein.

![](images/Mesh_VertexCurvature_example.png ) 
*Beispiel eines Mesh-Krümmungsobjekts*



## Anwendung

1.  Select one or more mesh objects.
2.  There are several ways to invoke the command:
    -   Press the **<img src="images/Mesh_VertexCurvature.svg" width=16px> [Curvature plot](Mesh_VertexCurvature.md)** button.
    -   Select the **Meshes → <img src="images/Mesh_VertexCurvature.svg" width=16px> Curvature plot** option from the menu.
    -   Select the **<img src="images/Mesh_VertexCurvature.svg" width=16px> Curvature plot** option from the [Tree view](Tree_view.md) context menu or [3D view](3D_view.md) context menu.



## Eigenschaften

For a Mesh Curvature object the following properties are available in the [Property editor](Property_editor.md). Select the **Show all** option from the Property editor context menu to display the hidden properties.



### Daten


{{TitleProperty|Base}}

-    **Label|String**: a user editable name for the object, an arbitrary UTF8 string.

-    **Source|Link**: a link to the mesh object.

#### Data hidden 


{{TitleProperty|Base}}

-    **Curv Info|CurvatureList**: a list of curvature information.

-    **Expression Engine|ExpressionEngine**: a list of expressions.

-    **Label2|String**: a user editable description for the object, an arbitrary UTF8 string that may include newlines.

-    **Visibility|Bool**: if set to `True`, the object appears in the [3D view](3D_view.md).

### View


{{TitleProperty|Base}}

-    **Display Mode|Enumeration**: {{value|Absolute curvature}} (default), {{value|Mean curvature}}, {{value|Gaussian curvature}}, {{value|Maximum curvature}}, {{value|Minimum curvature}}.

-    **On Top When Selected|Enumeration**: {{value|Disabled}} (default), {{value|Enabled}}, {{value|Object}}, {{value|Element}}.

-    **Selection Style|Enumeration**: {{value|Shape}}, {{value|BoundBox}} (default).

-    **Show In Tree|Bool**: if set to `True`, the object appears in the [Tree view](Tree_view.md).

-    **Visibility|Bool**: if set to `True`, the object appears in the [3D view](3D_view.md).

#### View hidden 


{{TitleProperty|Base}}

-    **Texture Material|Material**: an [App Material](App_Material.md) associated with the object.





{{Mesh Tools navi

}}



---
⏵ [documentation index](../README.md) > [Mesh](Mesh_Workbench.md) > Mesh VertexCurvature/de
