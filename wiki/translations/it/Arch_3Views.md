---
 GuiCommand:
   Name: Arch 3Views
   Name/it: 3 Viste da mesh
   MenuLocation: Arch , Utilità , 3 Viste da mesh
   Workbenches: Arch_Workbench/it
   SeeAlso: Arch_SplitMesh/it, Arch_MeshToShape/it
---

# Arch 3Views/it



## Descrizione


**Questo comando non è attualmente in uso.**

Esso servirà a generare delle viste piatte, di un oggetto [Mesh](Mesh_Workbench/it.md), da usare con lo strumento **<img src="images/Arch_Equipment.svg" width=24px> [Arredo](Arch_Equipment/it.md)**.



## Utilizzo

1.  Selezionare un oggetto Mesh
2.  Selezionare il pulsante **<img src="images/Arch_3Views.svg" width=16px>**, o **Arch** → **Utilità** → **<img src="images/Arch_3Views.svg" width=16px> [3 viste](Arch_3Views/it.md)** dal menu principale.



## Script


**Vedere anche:**

[API di Arch](Arch_API/it.md) e [Nozioni di base sugli script di FreeCAD](FreeCAD_Scripting_Basics/it.md).

Questo strumento può essere utilizzato nelle [macro](Macros/it.md) e dalla console [Python](FreeCAD_Scripting_Basics/it.md) tramite la seguente funzione: 
```python
shape = createMeshView(obj, direction=FreeCAD.Vector(0, 0, -1), outeronly=False, largestonly=False)
```

-   Crea una `shape` piatta che è la proiezione nella data `direction` dell\'oggetto mesh (`obj`) specificato.
-   Se `outeronly` è `True` viene preso in considerazione solo il contorno esterno, scartando i fori interni.
-   Se `largestonly` è `True` viene utilizzato solo il segmento più grande della mesh specificata.

Usare `Part.show()` per visualizzare la forma piatta risultante.

Esempio: 
```python
import FreeCAD, Draft, Arch, Mesh, MeshPart

Line = Draft.makeWire([FreeCAD.Vector(0, 0, 0), FreeCAD.Vector(2000, 2000, 0)])
Wall = Arch.makeWall(Line, width=150, height=3000)
FreeCAD.ActiveDocument.recompute()

Shape = Wall.Shape.copy(False)
Shape.Placement = Wall.getGlobalPlacement()

mesh_obj = FreeCAD.ActiveDocument.addObject("Mesh::Feature", "Mesh")
mesh_obj.Mesh = MeshPart.meshFromShape(Shape=Shape, MaxLength=520)
mesh_obj.ViewObject.DisplayMode = "Flat Lines"
FreeCAD.ActiveDocument.recompute()

XAxis = FreeCAD.Vector(1, 0, 0)
YAxis = FreeCAD.Vector(0, 1, 0)
ZAxis = FreeCAD.Vector(0, 0, -1)

s1 = Arch.createMeshView(mesh_obj, ZAxis)
s2 = Arch.createMeshView(mesh_obj, XAxis)
s3 = Arch.createMeshView(mesh_obj, YAxis)

Part.show(s1)
Part.show(s2)
Part.show(s3)

Wall.ViewObject.Visibility = False
mesh_obj.ViewObject.Visibility = False
```



---
⏵ [documentation index](../README.md) > [BIM](Category_BIM.md) > Arch 3Views/it
