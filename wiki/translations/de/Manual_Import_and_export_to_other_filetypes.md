# Manual:Import and export to other filetypes/de
{{Manual:TOC}}

FreeCAD kann viele Dateiarten importieren und exportieren. Hier ist eine Liste der wichtigsten, mit einer kurzen Beschreibung der verfügbaren Funktionen:

  Format   Import   Export   Anmerkungen
     
  STEP     Ja       Ja       Dies ist das zuverlässigste Import-/Exportformat, das es gibt, da es Festkörpergeometrie und NURBS unterstützt. Es sollte, wann immer es möglich ist, verwendet werden.
  IGES     Ja       Ja       Ein älteres Festkörper-Format, ebenfalls sehr gut unterstützt. Einige ältere Anwendungen unterstützen STEP nicht, haben aber IGES.
  BREP     Ja       Ja       Das systemeigene Format von [OpenCasCade](https://en.wikipedia.org/wiki/Open_Cascade_Technology), dem Geometriekernel von FreeCAD.
  DXF      Ja       Ja       Ein offenes Format, das von Autodesk gepflegt wird. Da die 3D-Daten in einer DXF-Datei in einem proprietären Format kodiert sind, kann FreeCAD nur 2D-Daten in dieses Format exportieren oder aus diesem Format importieren.
  DWG      Ja       Ja       Die urheberrechtlich geschützte Version von DXF. Erfordert die Installation des Dienstprogramms [Teigha File Converter](https://www.opendesign.com/guestfiles). Dieses Format unterliegt den gleichen Einschränkungen wie DXF.
  OBJ      Ja       Ja       Ein Netz-basiertes Format. Kann nur Dreiecksnetze enthalten. Alle Objekte von FreeCAD, die auf Festkörpern und NURBS basieren, werden beim Export in ein Netz umgewandelt. Eine alternative Exportfunktion wird vom Arbeitsbereich Arch zur Verfügung gestellt, der besser für den Export von Architekturmodellen geeignet ist..
  DAE      Ja       Ja       Das Haupt-Import-/Exportformat von Sketchup. Kann nur Dreiecksnetze enthalten. Alle auf Festkörpern und NURBS basierenden Objekte von FreeCAD werden beim Export in Netze umgewandelt..
  STL      Ja       Ja       Ein netz-basiertes Format, das häufig für den 3D-Druck verwendet wird. Kann nur Dreiecksnetze enthalten. Alle auf Festkörpern und NURBS basierenden Objekte von FreeCAD werden beim Export in Netze umgewandelt..
  PLY      Ja       Ja       Ein älteres netz-basiertes Format. Kann nur Dreiecksnetze enthalten. Alle auf Festkörpern und NURBS basierenden Objekte von FreeCAD werden beim Export in Netze umgewandelt..
  IFC      Ja       Ja       [Industry Foundation Classes](https://en.wikipedia.org/wiki/Industry_Foundation_Classes). Erfordert die Installation von [IfcOpenShell-python](http://ifcopenshell.org/python). Das IFC-Format und seine Kompatibilität mit anderen Anwendungen ist eine komplexe Angelegenheit, die mit Vorsicht zu verwenden ist.
  SVG      Ja       Ja       Ein ausgezeichnetes, weit verbreitetes 2D-Grafikformat
  VRML     Ja       Ja       Ein ziemlich altes Netz-basiertes Webformat.
  GCODE    Ja       Ja       FreeCAD kann bereits verschiedene GCode-Varianten importieren und exportieren, jedoch wird derzeit nur eine kleine Anzahl von Maschinen unterstützt..
  CSG      Ja       Nein     OpenSCADs [CSG](https://en.wikipedia.org/wiki/Constructive_solid_geometry) (Konstruktive-Festkörper-Geometrie)-Format.

Einige dieser Dateiformate haben Optionen. Diese können über das Menü **Bearbeiten → Einstellungen → Import/Export:** konfiguriert werden.

![](images/FreeCAD_022_ImportExport.png )

**Weiterlesen**

-   [Alle von FreeCAD unterstützten Dateiformate](Import_Export/de.md)
-   [Arbeiten mit DXF-Dateien in FreeCAD](Draft_DXF/de.md):
-   [Arbeiten mit SVG-Dateien in FreeCAD](Draft_SVG/de.md)
-   [Import und Export nach IFC](Arch_IFC/de.md)
-   [OpenCasCade](http://www.opencascade.com)
-   [Teigha File Converter](https://www.opendesign.com/guestfiles)
-   [IFC Spezifikationen Datenbank](https://technical.buildingsmart.org/standards/ifc/ifc-schema-specifications/)
-   [IfcOpenShell](http://ifcopenshell.org/)



---
⏵ [documentation index](../README.md) > [Poweruser Documentation](Category_Poweruser%20Documentation.md) > [Tutorials](Category_Tutorials.md) > Manual:Import and export to other filetypes/de
