# TechDraw API/pl
**''(Listopad 2018)'' Te informacje mogą być niekompletne i nieaktualne. Najnowsze API można znaleźć na stronie [https://www.freecadweb.org/api autogenerowana dokumentacja API].** Funkcje te są częścią środowiska pracy [Rysunek Techniczny](TechDraw_Workbench/pl.md) i mogą być używane w [makrodefinicjach](Macros/pl.md) oraz z konsoli środowiska [Python](Python/pl.md) po zaimportowaniu modułu `TechDraw`.

Dobre przykłady podstawowych skryptów Rysunku Technicznego można znaleźć na stronie [skrypty testów jednostkowych](https://github.com/FreeCAD/FreeCAD/tree/master/src/Mod/TechDraw/TDTest).

Zobacz stronę [Api dla GUI](TechDrawGui_API/pl.md) aby poznać więcej funkcji.

Przykład:


```python
import FreeCAD
import TechDraw

page = FreeCAD.ActiveDocument.addObject('TechDraw::DrawPage', 'Page')
FreeCAD.ActiveDocument.addObject('TechDraw::DrawSVGTemplate', 'Template')
FreeCAD.ActiveDocument.Template.Template = templateFileSpec
FreeCAD.ActiveDocument.Page.Template = FreeCAD.ActiveDocument.Template
page.ViewObject.show()
view = FreeCAD.ActiveDocument.addObject('TechDraw::DrawViewPart', 'View')
rc = page.addView(view)
```


{{APIFunction|EdgeWalker|listOfEdges, [bool]|Tworzy linie z krawędzi na wejściu przez planarne przechodzenie grafu.  Opcjonalnie wyklucza OuterWire ustawiając opcjonalny parametr na false.|Lista przewodów posortowana według rozmiaru (malejąco)}}


{{APIFunction|findOuterWire|listOfEdges|Wyszukuje OuterWire (największy) z listy krawędzi (które tworzą graf planarny).|Outer wire}}


{{APIFunction|findShapeOutline|TopoShape, scale, direction|Odwzorowuje kształt w kierunku i znajduje zewnętrzną linię wyniku.|Outline wire}}

.


{{APIFunction|viewPartAsDxf|DrawViewPart|Zwraca krawędzie DrawViewPart w formacie Dxf.|String}}

Przykład:


```python
fileSpecDxf = "fcOut.dxf"
v = App.ActiveDocument.View
s = TechDraw.viewPartAsDxf(v)
dxfEnd = "0\nEOF\n"
dxfFile = open(fileSpecDxf, "w")
dxfFile.write(s)
dxfFile.write(dxfEnd)
dxfFile.close()
```


{{APIFunction|viewPartAsSvg|DrawViewPart|Zwraca krawędzie DrawViewPart w formacie Svg.|String}}

Przykład:


```python
fileSpecSvg = "fcOut.svg"
v = App.ActiveDocument.View
s = TechDraw.viewPartAsSvg(v)
head = '<svg\n' + \
       '    xmlns="http://www.w3.org/2000/svg" version="1.1" \n' + \
       '    xmlns:freecad="http://www.freecadweb.org/wiki/index.php?title=Svg_Namespace">\n'
tail = '\n</svg>'
svgFile = open(fileSpecSvg, "w")
svgFile.write(head)
svgFile.write(s)
svgFile.write(tail)
svgFile.close()
```


{{APIFunction|writeDXFView|DrawViewPart, FileName|Zapisz DrawViewPart w formacie Dxf.|File}}

Przykład:


```python
import TechDraw
TechDraw.writeDXFView(myPart,myFileName)
```


{{APIFunction|writeDXFPage|DrawPage, FileName|Zapisz DrawPage w formacie Dxf.|File}}

Przykład:


```python
import TechDraw
TechDraw.writeDXFPage(myPage,myFileName)
```



### DrawViewPart geometrie pomocnicze 



#### Procedury CosmeticVertex (CV) dostępne z poziomu Pythona 

dvp = App.ActiveDocument.View #CV należą do widoków.
Dodaje wierzchołek CosmeticVertex w punkcie p1 *(współrzędne widoku)*. Zwraca unikalny znacznik.
tag = dvp.makeCosmeticVertex(vector p1)

Dodaje wierzchołek CosmeticVertex w punkcie p1 *(współrzędne modelu 3d)*. Zwraca unikalny znacznik.
tag = dvp.makeCosmeticVertex3d(vector p1)

Zwraca CosmeticVertex z unikalnym identyfikatorem.
cv = dvp.getCosmeticVertex(string id)

Zwraca CosmeticVertex z nazwą (Vertex6). Używany w selekcjach.
cv = dvp.getCosmeticVertexBySelection(string name)

Usuwa CosmeticVertex z widoku. Zwraca None.
dvp.removeCosmeticVertex(object cv)

Usuwa wszystkie CosmeticVertices z widoku. Zwraca None.
dvp.clearCosmeticVertices()

Atrybuty CosmeticView
Tag: niepowtarzalny identyfikator. String.
Point: lokalizacja w widoku. Vector.

-   -   


```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-


# Py CosmeticVertex demo
import FreeCAD
import TechDraw


v = App.ActiveDocument.View
p = App.Vector(-3.0, -3.0, 0.0)


#make CV
tag = v.makeCosmeticVertex(p)
print("t: {}".format(tag))


#retrieve CV
cv = v.getCosmeticVertex(tag)
print("cv: {}".format(cv))
print("Tag: {}".format(cv.Tag))



cv2 = v.getCosmeticVertexBySelection("Vertex4")
print("New Point: {}".format(cv2.Point))


#make CV from 3d
p3d = App.Vector(2.0, 2.0, 2.0)
print("3d point in: {}".format(p3d))
tag3d = v.makeCosmeticVertex3d(p3d)
cv3 = v.getCosmeticVertex(tag3d)
print("3d point out: {}".format(cv3.Point))
```



#### Procedury CosmeticEdge (CE) dostępne z poziomu Pythona 

dvp = App.ActiveDocument.View #CE\'s należą do widoków.
Utwórz krawędź CosmeticEdge od p1 do p2(współrzędne widoku). Zwraca unikalny znacznik.
tag = dvp.makeCosmeticLine(p1, p2)

tworzy krawędź CosmeticEdge w środku o promieniu radius(współrzędne widoku). Zwraca niepowtarzalny tag.
tag = dvp.makeCosmeticCircle(center, radius)

tworzy krawędź CosmeticEdge w środku o promieniu radius (współrzędne widoku) od kąta początkowego do kąta końcowego. Zwraca niepowtarzalny tag.
tag = dvp.makeCosmeticCircleArc(center, radius, start, end)

Zwraca CosmeticEdge z unikalnym identyfikatorem.
ce = dvp.getCosmeticEdge(id)

Zwraca CosmeticEdge według nazwy (Edge25). Używane w selekcjach.
ce = dvp.getCosmeticEdgeBySelection(name)

Usuwa CosmeticEdge ce z widoku. Zwraca None.
dvp.removeCosmeticEdge(ce)

Usuwa wszystkie linie CosmeticLines z widoku. Zwraca None.
dvp.clearCosmeticEdges()

atrybuty CosmeticEdge
Tag: niepowtarzalny identyfikator. String.
Format: appearance attributes (style, color, weight, visible). Tuple.

-   -   


```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-


# Py CosmeticEdge demo
import FreeCAD
import TechDraw


#points
org = App.Vector(0.0, 0.0, 0.0)
midTop = FreeCAD.Vector (1.0, 5.0, 0.0)   # middle, top
midBot = FreeCAD.Vector(2.0, -5.0, 0.0)      # middle, bottom
stdZ = FreeCAD.Vector(0.0, 0.0, 1.0)
center = FreeCAD.Vector(0.0, 0.0, 0.0)
arcCenter = FreeCAD.Vector(3.0, 3.0, 0.0)
vPt = FreeCAD.Vector(-3.0, 3.0, 0.0)
topRight = FreeCAD.Vector(5.0, 5.0, 0.0)
bottomLeft = FreeCAD.Vector(-5.0, -5.0, 0.0)


#angles
arcStart = -45
arcEnd = 45


#styles
solid = 1 
dashed = 2
dotted = 3
#weights
weight15 = 0.15
weight75 = 0.75
#colors
pyRed = (1.0, 0.0, 0.0, 0.0)
pyBlue = (0.0, 1.0, 0.0, 0.0)
pyGreen = (0.0, 0.0, 1.0, 0.0)
pyBlack = (0.0, 0.0, 0.0, 0.0)
shadow = (0.1, 0.1, 0.1, 0.0)


radius = 5.0
style = dashed
weight = weight75


dvp = App.ActiveDocument.View


print(dvp)


print("making line")
tag = dvp.makeCosmeticLine(midTop,midBot,style, weight, pyBlue)
ce = dvp.getCosmeticEdge(tag)
print("line tag: {}".format(tag))


print("making diagonal")
dvp.makeCosmeticLine(bottomLeft,topRight,solid, weight, pyGreen)


print("making circle")
tag2 = dvp.makeCosmeticCircle(center, radius, style, weight, pyRed)
ce2 = dvp.getCosmeticEdge(tag2)


print("making circleArc")
dvp.makeCosmeticCircleArc(arcCenter, radius, arcStart, arcEnd, style, weight, shadow)


#replace
print("making new format")
oldFormat = ce.Format
newFormat = (dotted,oldFormat[1], pyRed, True)
ce.Format = newFormat


print("removing CE with tag: {}".format(tag2))
dvp.removeCosmeticEdge(tag2)


print("finished")
```



#### Procedury CenterLine (CL) dostępne z poziomu Pythona 

Tworzy nową linię CenterLine
tag = dvp.makeCenterLine(subObjs, mode)
Pobiera CenterLine z niepowtarzalnym znacznikiem.
cl = dvp.getCenterLine(tag)

Pobiera CenterLine według nazwy podobiektu. Używane w selekcji.
cl = dvp.getCenterLine(\"Edge5\")

Usuwa CenterLine cl z widoku. Zwraca None.
dvp.removeCenterLine(cl)

Atrybuty CenterLine
Tag: niepowtarzalny identyfikator. String. ReadOnly.
Type: 0 - face, 1 - 2 line, 2 - 2 point. Integer. ReadOnly.
Mode: 0 - vert, 1 - horiz, 2 - aligned. Integer.
Format: atrybuty wyglądu (style, color, weight, visible). Tuple.
HorizShift: przesunięcie w lewo/prawo. Float.
VertShift: przesunięcie góra/dół. Float.
Rotation: obrót w stopniach. Float.
Extension: dodatkowa długość do dodania. Float.
Flip: Odwróć kolejność punktów, aby uzyskać 2 punkty CenterLine. Boolean.
Edges: nazwy krawędzi źródłowych. List of string.
Faces: nazwy ścian źródłowych. List of string.
Points: nazwy punktów źródłowych *(wierzchołków)*. List of string.

-   -   


```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-


# Py CenterLine demo
import FreeCAD
import Part
import TechDraw


start = FreeCAD.Vector (1.0, 5.0, 0.0)   # middle, top
end = FreeCAD.Vector(1.0, -5.0, 0.0)      # middle, bottom
faceNames = ["Face0"]
edgeNames = ["Edge2", "Edge3"]
vertNames = ["Vertex1", "Vertex2"]
vMode = 0   #vertical
hMode = 1   #horizontal
aMode = 2   #aligned
#styles
solid = 1 
dashed = 2
dotted = 3
#weights
weight15 = 0.15
weight75 = 0.75
#colors
pyRed = (1.0, 0.0, 0.0, 0.0)
pyBlue = (0.0, 1.0, 0.0, 0.0)
pyBlack = (0.0, 0.0, 0.0, 0.0)
#adjustments
hShift = 1.0
vShift = 1.0
extend = 4.0
rotate = 30.0
flip = False;


dvp = App.ActiveDocument.View


print("making face CenterLine")
tag = dvp.makeCenterLine(faceNames,vMode)
cline = dvp.getCenterLine(tag)
print("cline tag: {}".format(tag))


#replace
print("making new format")
oldFormat = cline.Format
newFormat = (dotted,oldFormat[1], pyRed, True)
cline.Format = newFormat
cline.Extension = 10.0


print("making edgeCenterLine")
cline2 = dvp.makeCenterLine(edgeNames,hMode)


print("making vertexCenterLine")
cline3 = dvp.makeCenterLine(vertNames,aMode)


print("finished")
```



### Geometrie DrawViewPart 

\[topoShapeEdge\] = dvp.getVisibleEdges()

\[topoShapeEdge\] = dvp.getHiddenEdges()

topoShapeEdge = dvp.getEdgeByIndex(i)
topoShapeEdge = dvp.getEdgeBySelection(\"Edge1\")

topoShapeVertex = dvp.getVertexByIndex(i)
topoShapeVertex = dvp.getVertexBySelection(\"Vertex1\")

Przerysuj grafikę dla tego widoku.
dvp.requestPaint()


{{TechDraw Tools navi

}}



---
⏵ [documentation index](../README.md) > [API](Category_API.md) > [Poweruser Documentation](Category_Poweruser%20Documentation.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw API/pl
