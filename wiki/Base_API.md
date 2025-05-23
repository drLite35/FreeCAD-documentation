# Base API
**(October 2019) Do not edit this page. The information is incomplete and outdated. For the latest API, see the [https://www.freecadweb.org/api autogenerated API documentation], or generate the documentation yourself, see [Source documentation](Source_documentation.md).**

The Base module is contained inside the FreeCAD module and contains constructors for different types of objects heavily used in FreeCAD.


{{APIClass b|BoundBox|[Xmin,Ymin,Zmin,Xmax,Ymax,Zmax]}}


{{APIClass b|BoundBox|Tuple, Tuple}}


{{APIClass|BoundBox|Vector, Vector|
Creates a bounding box.
A bounding box is an orthographic cube which is a way to describe outer boundaries. You get a bounding box from a lot of 3D types. It is often used to check if a 3D entity lies in the range of another object. Checking for bounding interference first can save a lot of computing time!}}


{{APIClass|Matrix| |Creates a 4x4 [Matrix](Matrix_API.md), that can be used to apply transformations to objects.}}


{{APIClass b|Vector| }}


{{APIClass|Vector|x, y, z|Creates a FreeCAD 3D [Vector](Vector_API.md), representing a 3D point or a direction.}}


{{APIClass|Placement| |Creates a [Placement](Placement_API.md).}}



---
⏵ [documentation index](../README.md) > [API](Category_API.md) > [Poweruser Documentation](Category_Poweruser%20Documentation.md) > Base API
