# Arch OBJ/en
## Description

Additionally to the standard FreeCAD [OBJ](https://en.wikipedia.org/wiki/Wavefront_.obj_file) exporter, the [BIM Workbench](BIM_Workbench.md) features an alternative exporter that exports coplanar faces as whole OBJ faces, instead of triangulating [Shape](Shape.md)-based objects, like the standard exporter does.

## Exporting without GUI 

Exporting without the graphical interface is possible from the command line, using the [Mesh Workbench](Mesh_Workbench.md) exporter only.

In this example, a STEP file is imported, the colors of the [Shape](Shape.md) are saved, then a mesh is created from it, the colors of the original object are re-applied to the faces of the new mesh, which is then exported to OBJ format. Since this is done with the Mesh Workbench, the result is a triangulated mesh.


```python
import Mesh
import MeshPart
import Import

data = Import.open("example.stp")
shape = data[0][0].Shape
shape_colors = data[0][1]

mesh = MeshPart.meshFromShape(Shape=shape, LinearDeflection=0.1, Segments=True)

face_colors = [(0, 0, 0)] * mesh.CountFacets

for i in range(mesh.countSegments()):
    color = shape_colors[i]
    segm = mesh.getSegment(i)
    for j in segm:
        face_colors[j] = color

mesh.write(Filename="new_example.obj", Material=face_colors, Format="obj")
```

## More information 

-   [Convert STEP to Wavefront OBJ with colors of faces](https://forum.freecadweb.org/viewtopic.php?f=8&t=37452)

## Tutorials

-   [Import from STL or OBJ](Import_from_STL_or_OBJ.md)
-   [Export to STL or OBJ](Export_to_STL_or_OBJ.md)



---
⏵ [documentation index](../README.md) > [File_Formats](Category_File_Formats.md) > [BIM](Category_BIM.md) > Arch OBJ/en
