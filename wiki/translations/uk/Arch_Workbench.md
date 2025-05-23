# Arch Workbench/uk
**In v1.0 the BIM, Native-IFC and Arch Workbenches have been merged into the integrated [BIM Workbench](BIM_Workbench.md).**

<img alt="Arch workbench icon" src=images/Workbench_Arch.svg  style="width:128px;">




 Робочий простір Архітектора (Arch workbench) забезпечує сучасний [BIM](http://uk.wikipedia.org/wiki/Building_Information_Modeling) робочий процес до FreeCAD, з підтримкою таких функцій як:

-   підтримка [IFC](http://uk.wikipedia.org/wiki/Industry_Foundation_Classes)
-   повністю параметричні архітектурні об\'єкти такі як стіни, елементи конструкцій або вікна

-   можливості для створення 2D документів.

Робочий простір Arch вміщює всі інструменти з [Робочого простору Draft](Draft_Workbench/uk.md).

The <img alt="" src=images/Workbench_Arch.svg  style="width:24px;"> [Arch Workbench](Arch_Workbench.md) provides a modern [**B**uilding **I**nformation **M**odelling](http://en.wikipedia.org/wiki/Building_Information_Modeling) (BIM) workflow to FreeCAD, with support for features like fully parametric architectural entities such as walls, beams, roofs, windows, stairs, pipes, and furniture. It supports [**I**ndustry **F**oundation **C**lasses](Arch_IFC.md) (IFC) files, and production of 2D floor plans in combination with the <img alt="" src=images/Workbench_TechDraw.svg  style="width:24px;"> [TechDraw Workbench](TechDraw_Workbench.md).

The Arch Workbench imports all tools from the <img alt="" src=images/Workbench_Draft.svg  style="width:24px;"> [Draft Workbench](Draft_Workbench.md), as it uses its 2D objects to build 3D parametric architectural objects. Nevertheless, Arch can also use solid shapes created with other workbenches like <img alt="" src=images/Workbench_Part.svg  style="width:24px;"> [Part](Part_Workbench.md) and <img alt="" src=images/Workbench_PartDesign.svg  style="width:24px;"> [PartDesign](PartDesign_Workbench.md).

The BIM functionality of FreeCAD is now progressively split into this Arch Workbench, which holds basic architectural tools, and the <img alt="" src=images/Workbench_BIM.svg  style="width:24px;"> [BIM Workbench](BIM_Workbench.md), which is available from the <img alt="" src=images/Std_AddonMgr.svg  style="width:24px;"> [Addon Manager](Std_AddonMgr.md). This BIM Workbench adds a new interface layer on top of the Arch tools, with the aim of making the BIM workflow more intuitive and user-friendly. See [FreeCAD BIM migration guide](https://yorik.uncreated.net/blog/2020-010-freecad-bim-guide).

The developers of Draft, Arch, and BIM also collaborate with the greater [OSArch community](https://osarch.org), with the ultimate goal of improving building design by using entirely free software.

<img alt="" src=images/Screenshot_arch_window.jpg  style="width:600px;">



## Інструменти

These are tools for creating architectural objects.

-   <img alt="" src=images/Arch_Wall.svg  style="width:32px;"> [Wall](Arch_Wall.md): Creates a wall from scratch or using a selected object as a base.

-   <img alt="" src=images/Arch_Structure.svg  style="width:32px;"> [Structure](Arch_Structure.md): Creates a structural element from scratch or using a selected object as a base.

-   <img alt="" src=images/Arch_CompRebarStraight.png  style="width:48px;"> [Rebar tools](Arch_CompRebarStraight.md): These tools, except the last, are only available if the [Reinforcement Workbench](Reinforcement_Workbench.md) has been installed.

  - <img alt="" src=images/Reinforcement_StraightRebar.svg  style="width:32px;"> [Straight Rebar](Reinforcement_StraightRebar.md): Creates a straight reinforcement bar in a selected structural element.

  - <img alt="" src=images/Reinforcement_UShapeRebar.svg  style="width:32px;"> [U-Shape Rebar](Reinforcement_UShapeRebar.md): Creates a U-shape reinforcement bar in a selected structural element.

  - <img alt="" src=images/Reinforcement_LShapeRebar.svg  style="width:32px;"> [L-Shape Rebar](Reinforcement_LShapeRebar.md): Creates an L-shape reinforcement bar in a selected structural element.

  - <img alt="" src=images/Reinforcement_StirrupRebar.svg  style="width:32px;"> [Stirrup](Reinforcement_StirrupRebar.md): Creates a stirrup reinforcement bar in a selected structural element.

  - <img alt="" src=images/Reinforcement_BentShapeRebar.svg  style="width:32px;"> [Bent-Shape Rebar](Reinforcement_BentShapeRebar.md): Creates a bent-shape reinforcement bar in a selected structural element.

  - <img alt="" src=images/Reinforcement_HelicalRebar.svg  style="width:32px;"> [Helical Rebar](Reinforcement_HelicalRebar.md): Creates a helical reinforcement bar in a selected structural element.

  - <img alt="" src=images/Reinforcement_ColumnRebars.svg  style="width:32px;"> [Column Reinforcement](Reinforcement_ColumnRebars.md): Creates reinforcement bars in a selected column.

  - <img alt="" src=images/Reinforcement_BeamRebars.svg  style="width:32px;"> [Beam Reinforcement](Reinforcement_BeamRebars.md): Creates reinforcement bars in a selected beam.

  - <img alt="" src=images/Reinforcement_SlabRebars.svg  style="width:32px;"> [Slab Reinforcement](Reinforcement_SlabRebars.md): Creates reinforcement bars in a selected slab.

  - <img alt="" src=images/Reinforcement_FootingRebars.svg  style="width:32px;"> [Footing Reinforcement](Reinforcement_FootingRebars.md): Creates reinforcement bars in a selected footing.

  - <img alt="" src=images/Arch_Rebar.svg  style="width:32px;"> [Custom Rebar](Arch_Rebar.md): Creates a custom reinforcement bar in a selected structural element using a sketch.

-   <img alt="" src=images/Arch_CurtainWall.svg  style="width:32px;"> [Curtain Wall](Arch_CurtainWall.md): Creates a curtain wall from scratch or using a selected object as a base.

-   <img alt="" src=images/Arch_BuildingPart.svg  style="width:32px;"> [Building Part](Arch_BuildingPart.md): Creates a building part including selected objects.

-   <img alt="" src=images/Arch_Project.svg  style="width:32px;"> [Project](Arch_Project.md): Creates a project including selected objects.

-   <img alt="" src=images/Arch_Site.svg  style="width:32px;"> [Site](Arch_Site.md): Creates a site including selected objects.

-   <img alt="" src=images/Arch_Building.svg  style="width:32px;"> [Building](Arch_Building.md): Creates a building including selected objects.

-   <img alt="" src=images/Arch_Floor.svg  style="width:32px;"> [Level](Arch_Floor.md): Creates a floor including selected objects.

-   <img alt="" src=images/Arch_Reference.svg  style="width:32px;"> [External reference](Arch_Reference.md): Links objects from another FreeCAD file into the current document.

-   <img alt="" src=images/Arch_Window.svg  style="width:32px;"> [Window](Arch_Window.md): Creates a window from scratch or using a selected object as a base.

-   <img alt="" src=images/Arch_Roof.svg  style="width:32px;"> [Roof](Arch_Roof.md): Creates a sloped roof from a selected wire.

-   <img alt="" src=images/Arch_CompAxis.png  style="width:48px;"> [Axis tools](Arch_CompAxis.md)

  - <img alt="" src=images/Arch_Axis.svg  style="width:32px;"> [Axis](Arch_Axis.md): Adds a 1-direction array of axes.

  - <img alt="" src=images/Arch_AxisSystem.svg  style="width:32px;"> [Axis System](Arch_AxisSystem.md): Adds an axis system composed of several axes.

  - <img alt="" src=images/Arch_Grid.svg  style="width:32px;"> [Grid](Arch_Grid.md): Adds a grid-like object.

-   <img alt="" src=images/Arch_SectionPlane.svg  style="width:32px;"> [Section Plane](Arch_SectionPlane.md): Adds a section plane object.

-   <img alt="" src=images/Arch_Space.svg  style="width:32px;"> [Space](Arch_Space.md): Creates a space object.

-   <img alt="" src=images/Arch_Stairs.svg  style="width:32px;"> [Stairs](Arch_Stairs.md): Creates a stairs object.

-   <img alt="" src=images/Arch_CompPanel.png  style="width:48px;"> [Panel tools](Arch_CompPanel.md)

  - <img alt="" src=images/Arch_Panel.svg  style="width:32px;"> [Panel](Arch_Panel.md): Creates a panel object from a selected 2D object.

  - <img alt="" src=images/Arch_Panel_Cut.svg  style="width:32px;"> [Panel Cut](Arch_Panel_Cut.md): Creates a 2D cut view from a panel.

  - <img alt="" src=images/Arch_Panel_Sheet.svg  style="width:32px;"> [Panel Sheet](Arch_Panel_Sheet.md): Creates a 2D cut sheet including panel cuts or other 2D objects.

  - <img alt="" src=images/Arch_Nest.svg  style="width:32px;"> [Nest](Arch_Nest.md): Allows to nest several flat objects inside a container shape.

-   <img alt="" src=images/Arch_Equipment.svg  style="width:32px;"> [Equipment](Arch_Equipment.md): Creates an equipment or furniture object.

-   <img alt="" src=images/Arch_Frame.svg  style="width:32px;"> [Frame](Arch_Frame.md): Creates a frame object from a selected layout.

-   <img alt="" src=images/Arch_Fence.svg  style="width:32px;"> [Fence](Arch_Fence.md): Creates a fence object from a selected post and path.

-   <img alt="" src=images/Arch_Truss.svg  style="width:32px;"> [Truss](Arch_Truss.md): Creates a truss from a selected line or from scratch.

-   <img alt="" src=images/Arch_Profile.svg  style="width:32px;"> [Profile](Arch_Profile.md): Creates a parametric 2D profile.

-   <img alt="" src=images/Arch_CompSetMaterial.png  style="width:48px;"> [Material tools](Arch_CompSetMaterial.md)

  - <img alt="" src=images/Arch_SetMaterial.svg  style="width:32px;"> [Material](Arch_SetMaterial.md): Creates a material and attributes it to selected objects, if any.

  - <img alt="" src=images/Arch_MultiMaterial.svg  style="width:32px;"> [Multi-Material](Arch_MultiMaterial.md): Creates a multi-material and attributes it to selected objects, if any.

-   <img alt="" src=images/Arch_Schedule.svg  style="width:32px;"> [Schedule](Arch_Schedule.md): Creates different types of schedules.

-   <img alt="" src=images/Arch_CompPipe.png  style="width:48px;"> [Pipe tools](Arch_CompPipe.md)

  - <img alt="" src=images/Arch_Pipe.svg  style="width:32px;"> [Pipe](Arch_Pipe.md): Creates a pipe.

  - <img alt="" src=images/Arch_PipeConnector.svg  style="width:32px;"> [Connector](Arch_PipeConnector.md): Creates a corner or T-connection between 2 or 3 selected pipes.

### Modification tools 

These are tools for modifying architectural objects.

-   <img alt="" src=images/Arch_CutPlane.svg  style="width:32px;"> [Cut with plane](Arch_CutPlane.md): Cuts an object according to a plane.

-   <img alt="" src=images/Arch_CutLine.svg  style="width:32px;"> [Cut with line](Arch_CutLine.md): Cuts an object according to a line.

-   <img alt="" src=images/Arch_Add.svg  style="width:32px;"> [Add component](Arch_Add.md): Adds objects to a component.

-   <img alt="" src=images/Arch_Remove.svg  style="width:32px;"> [Remove component](Arch_Remove.md): Subtracts or removes objects from a component.

-   <img alt="" src=images/Arch_Survey.svg  style="width:32px;"> [Survey](Arch_Survey.md): Enters or leaves surveying mode.

### Utilities

These are additional tools to help you in specific tasks.

-   <img alt="" src=images/Arch_Component.svg  style="width:32px;"> [Component](Arch_Component.md): Creates a non-parametric Arch component.

-   <img alt="" src=images/Arch_CloneComponent.svg  style="width:32px;"> [Clone component](Arch_CloneComponent.md): Produces Arch Components that are clones of selected Arch objects (not to be confused with [Draft Clone](Draft_Clone.md)).

-   <img alt="" src=images/Arch_SplitMesh.svg  style="width:32px;"> [Split Mesh](Arch_SplitMesh.md): Splits a selected mesh into separate components.

-   <img alt="" src=images/Arch_MeshToShape.svg  style="width:32px;"> [Mesh to Shape](Arch_MeshToShape.md): Converts a mesh into a shape, unifying coplanar faces.

-   <img alt="" src=images/Arch_SelectNonSolidMeshes.svg  style="width:32px;"> [Select non-manifold meshes](Arch_SelectNonSolidMeshes.md): Selects all non-manifold meshes from the current selection or from the document.

-   <img alt="" src=images/Arch_RemoveShape.svg  style="width:32px;"> [Remove Shape from Arch](Arch_RemoveShape.md): Turns cubic shape-based Arch object fully parametric.

-   <img alt="" src=images/Arch_CloseHoles.svg  style="width:32px;"> [Close holes](Arch_CloseHoles.md): Closes holes in a selected shape-based object.

-   <img alt="" src=images/Arch_MergeWalls.svg  style="width:32px;"> [Merge Walls](Arch_MergeWalls.md): Merge two or more walls.

-   <img alt="" src=images/Arch_Check.svg  style="width:32px;"> [Check](Arch_Check.md): Check if the selected objects are solids and don\'t contain defects.

-   <img alt="" src=images/Arch_ToggleIfcBrepFlag.svg  style="width:32px;"> [Toggle IFC Brep flag](Arch_ToggleIfcBrepFlag.md): Forces a selected object to be exported as an [IfcFacetedBrep](http://www.buildingsmart-tech.org/ifc/IFC4/final/html/schema/ifcgeometricmodelresource/lexical/ifcfacetedbrep.htm).

-   <img alt="" src=images/Arch_3Views.svg  style="width:32px;"> [3 Views from mesh](Arch_3Views.md): Creates top, front and side views from a [mesh](Mesh_Workbench.md).

-   <img alt="" src=images/Arch_IfcSpreadsheet.svg  style="width:32px;"> [Create IFC spreadsheet\...](Arch_IfcSpreadsheet.md): Creates a spreadsheet to store [IFC](Arch_IFC.md) properties of an object.

-   <img alt="" src=images/Arch_ToggleSubs.svg  style="width:32px;"> [Toggle subcomponents](Arch_ToggleSubs.md): Shows or hides the subcomponents of an Arch object.

### Preferences

-   <img alt="" src=images/Preferences-arch.svg  style="width:32px;"> [Preferences](Arch_Preferences.md): preferences for the default appearance of walls, structures, rebars, windows, stairs, panels, pipes, grids and axes.



### Формати файлів 


<div class="mw-translate-fuzzy">

-   [IFC](Arch_IFC.md) : Industry foundation Classes (тільки імпорт)
-   [DAE](Arch_DAE.md) : [ Меш](http://uk.wikipedia.org/wiki/Полігональна_сітка.md) в форматі Collada
-   [OBJ](Arch_OBJ.md) : [Меш](http://uk.wikipedia.org/wiki/Полігональна_сітка.md) в форматі Obj (тільки експорт)


</div>

## API


<div class="mw-translate-fuzzy">

Архітектурний модуль Arch може бути використаний в сценаріях на мові Python або [макросах](macros.md) за допомогою функцій [Arch Python API](http://www.freecadweb.org/api/Arch.html).


</div>



## Посібники


<div class="mw-translate-fuzzy">

-   [ Посібник Arch](Arch_tutorial/uk.md)
-   [Посібники Arch на блозі Yorik\'а](http://yorik.uncreated.net/guestblog.php?2012=180)


</div>



---
⏵ [documentation index](../README.md) > [Obsolete_Workbenches](Category_Obsolete_Workbenches.md) > [Arch](Category_Arch.md) > Arch Workbench/uk
