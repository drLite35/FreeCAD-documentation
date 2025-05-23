---
 GuiCommand:-br
   Name: Draft Clone
   Name/pt-br: Draft Clone
   MenuLocation: Draft , Clone
   Workbenches: Draft_Workbench/pt-br, Arch_Workbench/pt-br
   Shortcut: **C** **L**
   SeeAlso: Draft Scale/pt-br
---

# Draft Clone/pt-br


</div>



## Descrição

The <img alt="" src=images/Draft_Clone.svg  style="width:24px;"> **Draft Clone** command creates linked copies, clones, of selected objects. The shape of a clone is parametric, it will update if its source object changes. But a clone does have its own position, rotation, and scale, and its own [View properties](Property_editor.md). For [BIM](BIM_Workbench.md) objects the command creates a special type of clone: an Arch clone.

The command can be used on 2D objects created with the [Draft Workbench](Draft_Workbench.md) or [Sketcher Workbench](Sketcher_Workbench.md), but also on many 3D objects such as those created with the [Part Workbench](Part_Workbench.md), [PartDesign Workbench](PartDesign_Workbench.md) or [BIM Workbench](BIM_Workbench.md). Clones of 2D objects can be used in [PartDesign Bodies](PartDesign_Body.md).

<img alt="" src=images/Draft_Clone_example.jpg  style="width:400px;"> 
*Draft Clone next to its source object*



## Utilização

1.  Optionally select one or more objects.
2.  There are several ways to invoke the command:
    -   Press the **<img src="images/Draft_Clone.svg" width=16px> [Clone](Draft_Clone.md)** button.
    -   Select the **Modification → <img src="images/Draft_Clone.svg" width=16px> Clone** option from the menu.
    -   Use the keyboard shortcut: **C** then **L**.
3.  If you have not yet selected an object: select an object in the [3D view](3D_view.md).



## Propriedades

See also: [Property editor](Property_editor.md).

An object created with the Draft Clone command is derived from a [Part Part2DObject](Part_Part2DObject.md), a [Part Feature](Part_Feature.md) object or, if an Arch Clone is created, from the object type of the source object. It inherits all properties from that object. A clone derived from one of the first two objects also has the following additional properties:

### Data


{{TitleProperty|Draft}}

-    **Fuse|Bool**: specifies if overlapping shapes in the clone are fused or not.

-    **Objects|LinkListGlobal**: specifies the objects that are cloned.

-    **Scale|Vector**: specifies the X, Y and Z scale factors.

## Scripting

See also: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) and [FreeCAD Scripting Basics](FreeCAD_Scripting_Basics.md).

To create a clone use the `make_clone` method (<small>(v0.19)</small> ) of the Draft module. This method replaces the deprecated `clone` method.


```python
cloned_object = make_clone(obj, delta=None, forcedraft=False)
```

-    `obj`contains the objects to be cloned. It is either a single object or a list of objects.

-    `delta`is the displacement vector to be applied to the clone.

-   If `forcedraft` is `False` and `obj` contains a single [BIM object](BIM_Workbench.md), an Arch Clone is created. Set `forcedraft` to `True` to create a Draft Clone instead.

-    `cloned_object`is returned with the clone object.

Example:


```python
import FreeCAD as App
import Draft

doc = App.newDocument()

place = App.Placement(App.Vector(1000, 0, 0), App.Rotation())
polygon1 = Draft.make_polygon(3, 750)
polygon2 = Draft.make_polygon(5, 750, placement=place)

vector = App.Vector(2600, 500, 0)
cloned_object = Draft.clone([polygon1, polygon2], delta=vector)

cloned_object.Fuse = True

doc.recompute()
```


<div class="mw-translate-fuzzy">





</div>



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft Clone/pt-br
