---
 GuiCommand:
   Name: CAM Engrave
   Name/de: CAM Gravieren
   MenuLocation: CAM , Gravieren
   Workbenches: CAM_Workbench/de
---

# CAM Engrave/de



## Beschreibung

The <img alt="" src=images/CAM_Engrave.svg  style="width:24px;"> [Engrave](CAM_Engrave.md) tool is primarily for engraving a <img alt="" src=images/Draft_ShapeString.svg  style="width:24px;"> [Draft ShapeString](Draft_ShapeString.md) onto a part. However, it may be useful for other kinds of 2D.



## Anwendung

Empty



## Optionen

Empty



## Eigenschaften



### Daten


{{TitleProperty|Base}}

-    **Placement**:

-    **Label**: User name of the object (UTF-8)


{{TitleProperty|Depth}}

-    **Clearance Height**: The height needed to clear clamps and obstructions

-    **Final Depth**: Final Depth of Tool- lowest value in Z

-    **Safe Height**: The above which Rapid motions are allowed.

-    **Start Depth**: Starting Depth of Tool- first cut depth in Z

-    **Step Down**: Incremental Step Down of Tool


{{TitleProperty|Path}}

-    **Active**: Make False, to prevent operation from generating code

-    **Base**: The base geometry for this operation

-    **Comment**: An optional comment for this operation

-    **Coolant Mode**: Coolant mode for this operation

-    **Cycle Time**: Estimated cycle time for this operation

-    **Start Vertex**: The vertex index to start the path from

-    **Tool Controller**: The tool controller that will be used to calculate the path

-    **User Label**: User assigned label


{{TitleProperty|Hidden}}

-    **Base Object**:

-    **Base Shapes**:

-    **Expression Engine**:

-    **Label2**:

-    **Path**:

-    **Proxy**:

-    **Visibility**:

### View

Empty

## Scripting


**Siehe auch:**

[FreeCAD Grundlagen Skripten](FreeCAD_Scripting_Basics/de.md).

Beispiel:


```python
#Place code example here.
```





{{CAM_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [CAM](CAM_Workbench.md) > CAM Engrave/de
