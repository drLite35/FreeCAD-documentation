# <img alt="Surface workbench icon" src=images/Workbench_Surface.svg  style="width:64px;"> Surface Workbench/ko






## 소개

<img alt="" src=images/Workbench_Surface.svg  style="width:24px;"> **표면 작업대**는 간단한 [NURBS 표면](https://en.wikipedia.org/wiki/Non-uniform_rational_B-spline)을 만들고 수정하는 도구를 제공합니다. **Face from edges** 옵션을 사용하는 경우 이 도구들은 **[<img src=images/Part_Builder.svg style="width:16px"> [Part Builder](Part_Builder.md)** 도구와 유사한 기능을 갖지만 해당 도구와 달리 표면 작업대의 도구는 매개 변수적이며 추가 옵션을 제공합니다. 그러나 해당 도구와 달리 표면 작업대의 도구는 파라메트릭하며 추가 옵션을 제공합니다. 이 점에서 이 작업대의 도구는 **[16px](file:PartDesign_AdditiveLoft.svg.md) [PartDesignAdditiveLoft](PartDesign_AdditiveLoft.md)** 및 **[16px](file:PartDesign_AdditivePipe.svg.md) [PartDesignAdditivePipe](PartDesign_AdditivePipe.md)**과 유사합니다.

Some of the features provided are:

-   Creation of surfaces from boundary edges.
-   Alignment of the curvature from neighboring faces.
-   Constraining of surfaces to additional curves and vertices.
-   Extension of faces.
-   A mesh can be used as a template to create spline curves on its surface.

<img alt="" src=images/Surface_example.png  style="width:350px;">

## Usage

The Surface Workbench intends to create faces with shapes, which is not possible to do with the standard tools in other workbenches.

<img alt="" src=images/Toy_Duck.png  style="width:350px;">



*Surface created with sketches placed in datum planes with the tools of the [PartDesign Workbench](PartDesign_Workbench.md)*

The Surface Workbench integrates with other workbenches of FreeCAD. The above example was created from **[<img src=images/Sketcher_NewSketch.svg style="width:16px"> [Sketches](Sketch.md)** placed on **[<img src=images/PartDesign_Plane.svg style="width:16px"> [PartDesign Datum planes](PartDesign_Plane.md)** in the <img alt="" src=images/Workbench_PartDesign.svg  style="width:24px;"> [PartDesign Workbench](PartDesign_Workbench.md). The design can be fully parametric if all datum planes and sketches are defined accordingly. In most cases it is sufficient to draw a closed sketch to define the boundary of a face, and then use different options to further modify its shape.

The generated surface cannot be placed inside a **[<img src=images/PartDesign_Body.svg style="width:16px"> [PartDesign Body](PartDesign_Body.md)**. However, the generated surface can be contained inside a **[<img src=images/Std_Part.svg style="width:16px"> [Std Part](Std_Part.md)** together with the associated **[<img src=images/PartDesign_Body.svg style="width:16px"> [PartDesign Body](PartDesign_Body.md)** that holds the datum planes and sketches. The non-parametric **[<img src=images/Part_Builder.svg style="width:16px"> [Part Builder](Part_Builder.md)** tool can then be used in order to create a [shell](Glossary#Shell.md) and finally a [solid](Glossary#Solid.md).

## Tools

-   <img alt="" src=images/Surface_Filling.svg  style="width:32px;"> [Filling](Surface_Filling.md): fills a series of boundary curves with a surface.

-   <img alt="" src=images/Surface_GeomFillSurface.svg  style="width:32px;"> [Fill boundary curves](Surface_GeomFillSurface.md): creates a surface from two, three or four boundary edges.

-   <img alt="" src=images/Surface_Sections.svg  style="width:32px;"> [Sections](Surface_Sections.md): creates a surface from edges that represent transversal sections of surface.

-   <img alt="" src=images/Surface_ExtendFace.svg  style="width:32px;"> [Extend face](Surface_ExtendFace.md): extrapolates the surface at the boundaries with its local U parameter and V parameter.

-   <img alt="" src=images/Surface_CurveOnMesh.svg  style="width:32px;"> [Curve on mesh](Surface_CurveOnMesh.md): creates approximated spline segments on top of a selected [mesh](Mesh_Workbench.md).

-   <img alt="" src=images/Surface_BlendCurve.svg  style="width:32px;"> [Blend Curve](Surface_BlendCurve.md): creates a Bezier curve between two edges, with desired continuity.





{{Surface Tools navi

}}



---
⏵ [documentation index](../README.md) > [Workbenches](Category_Workbenches.md) > [Surface](Category_Surface.md) > Surface Workbench/ko
