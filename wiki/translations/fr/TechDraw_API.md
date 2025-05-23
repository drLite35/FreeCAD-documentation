# TechDraw API/fr
**(Novembre 2018) Ces informations peuvent être incomplètes et obsolètes. Pour la dernière API, consultez [https://www.freecadweb.org/api autogenerated API documentation].** Ces fonctions font partie de l\'[atelier TechDraw](TechDraw_Workbench/fr.md) et peuvent être utilisées dans des [macros](Macros/fr.md) et à partir de la console [Python](Python/fr.md) une fois que le module `TechDraw` a été importé.

Vous trouverez de bons exemples de scripts TechDraw de base dans le site [unit test scripts](https://github.com/FreeCAD/FreeCAD/tree/master/src/Mod/TechDraw/TDTest).

Voir [TechDrawGui API](TechDrawGui_API/fr.md) pour plus de fonctions.

Exemple :


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


{{APIFunction|EdgeWalker|listOfEdges, [bool]|crée des polylignes à partir des arêtes en entrée en parcourant le graphe planaire.  Il est possible d'exclure la polyligne extérieure (OuterWire) en définissant le paramètre optionnel à false.|liste de polylignes triées par taille (décroissante) }}


{{APIFunction|findOuterWire|listOfEdges|trouve la polyligne extérieure (la plus grande) d'une liste d'arêtes (qui forment un graphe planaire).|polyligne extérieur}}


{{APIFunction|findShapeOutline|TopoShape, scale, direction|projette la forme dans la direction et trouve la polyligne extérieure du résultat.|polyligne de contour}}


{{APIFunction|viewPartAsDxf|DrawViewPart|renvoie les bords de DrawViewPart au format Dxf.|chaîne de caractères}}

Exemple :


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


{{APIFunction|viewPartAsSvg|DrawViewPart|renvoie les bords de DrawViewPart au format Svg.|chaîne de caractères}}

Exemple :


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


{{APIFunction|writeDXFView|DrawViewPart, FileName|enregistre DrawViewPart au format Dxf.|fichier}}

Exemple :


```python
import TechDraw
TechDraw.writeDXFView(myPart,myFileName)
```


{{APIFunction|writeDXFPage|DrawPage, FileName|enregistre DrawPage au format Dxf.|fichier}}

Exemple :


```python
import TechDraw
TechDraw.writeDXFPage(myPage,myFileName)
```



### Cosmétiques de DrawViewPart 



#### Routines de CosmeticVertex (CV) accessibles à partir de Python 

dvp = App.ActiveDocument.View #Les CV appartiennent à des vues.
Ajoute un CosmeticVertex à p1 (coordonnées de la vue). Renvoie une balise unique.
tag = dvp.makeCosmeticVertex(vector p1)

Ajoute un CosmeticVertex à p1 (coordonnées du modèle 3D). Renvoie une balise unique.
tag = dvp.makeCosmeticVertex3d(vector p1)

Renvoie un CosmeticVertex avec un identifiant unique.
cv = dvp.getCosmeticVertex(string id)

Renvoie le CosmeticVertex avec le nom (Vertex6). Utilisé dans les sélections.
cv = dvp.getCosmeticVertexBySelection(string name)

Supprime un CosmeticVertex d\'une vue. Ne renvoie rien.
dvp.removeCosmeticVertex(object cv)

Supprime tous les CosmeticVertices de la vue. Ne renvoie rien.
dvp.clearCosmeticVertices()

Attributs de CosmeticView
Tag : identifiant unique. Chaîne de caractères.
Point : emplacement dans la vue. Vecteur.

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



#### Routines de CosmeticEdge (CE) accessibles à partir de Python 

dvp = App.ActiveDocument.View #Les CE appartiennent à des vues.
Crée un CosmeticEdge de p1 à p2 (coordonnées de la vue). Renvoie une balise unique.
tag = dvp.makeCosmeticLine(p1, p2)

Crée un CosmeticEdge au centre avec un rayon (coordonnées de la vue). Retourne une balise unique.
balise = dvp.makeCosmeticCircle(center, radius)

Crée un CosmeticEdge au centre avec un rayon rayon(coordonnées de la vue). Retourne une balise unique.
tag = dvp.makeCosmeticCircleArc(center, radius, start, end)

Renvoie un CosmeticEdge avec un identifiant unique.
ce = dvp.getCosmeticEdge(id)

Renvoie un CosmeticEdge avec le nom (Edge25). Utilisé dans les sélections.
ce = dvp.getCosmeticEdgeBySelection(name)

Supprime un CosmeticEdge d\'une vue. Ne renvoie rien.
dvp.removeCosmeticEdge(ce)

Supprime tous les CosmeticLines de la vue. Ne renvoie rien.
dvp.clearCosmeticEdges()

Attributs de CosmeticEdge
Tag : identifiant unique. Chaîne de caractère.
Format : attributs d\'apparence (style, couleur, poids, visible). Tuple.

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



#### Routines de CenterLine (CL) accessibles à partir de Python 

Crée un nouveau CenterLine
tag = dvp.makeCenterLine(subObjs, mode)
Récupère un CenterLine avec une balise unique.
cl = dvp.getCenterLine(tag)

Récupère un CenterLine par nom de sous-objet. Utilisé dans la sélection.
cl = dvp.getCenterLine(\"Edge5\")

Supprime un CenterLine cl d\'une vue. Ne renvoie rien.
dvp.removeCenterLine(cl)

Attributs de CenterLine
Tag : identifiant unique. Chaîne de caractères. En lecture seule.
Type : 0 - face, 1 - 2 lignes, 2 - 2 points. Entier. En lecture seule.
Mode : 0 - vertical, 1 - horizontal, 2 - aligné. Entier.
Format : attributs d\'apparence (style, couleur, poids, visible). Tuple.
HorizShift : décalage gauche/droite. Flottant.
VertShift : décalage haut/bas. Flottant.
Rotation : rotation en degrés. Flottant.
Extension : longueur supplémentaire à ajouter. Flottant.
Flip : inverse l\'ordre des points pour une ligne centrale à 2 points. Booléen.
Edges : noms des bords de la source. Liste de chaînes de caractères.
Faces : noms des faces sources. Liste de chaînes de caractères.
Points : noms des points sources (sommets). Liste de chaînes de caractères.

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



### Géométrie de DrawViewPart 

\[topoShapeEdge\] = dvp.getVisibleEdges()

\[topoShapeEdge\] = dvp.getHiddenEdges()

topoShapeEdge = dvp.getEdgeByIndex(i)
topoShapeEdge = dvp.getEdgeBySelection(\"Edge1\")

topoShapeVertex = dvp.getVertexByIndex(i)
topoShapeVertex = dvp.getVertexBySelection(\"Vertex1\")

Redessine le graphique pour cette vue.
dvp.requestPaint()


{{TechDraw Tools navi

}}



---
⏵ [documentation index](../README.md) > [API](Category_API.md) > [Poweruser Documentation](Category_Poweruser%20Documentation.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw API/fr
