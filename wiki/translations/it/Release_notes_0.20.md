# Release notes 0.20/it
**FreeCAD 0.20** è stato rilasciato il **14 giugno 2022**, scaricalo dalla pagina di [Download](Download/it.md). Questa pagina elenca tutte le nuove funzionalità e modifiche.

Le note di rilascio precedenti di FreeCAD possono essere trovate nella [lista delle funzionalità](Feature_list#Note_di_rilascio.md).

+++
| ![](images/FreeCAD_highlight_relnotes_0.20.gif ) | *Model of a 775 DC motor by user \"jimmihenry\", see [Users Showcase](https://forum.freecadweb.org/viewtopic.php?p=551765#p551765).The model was made completely with the weekly [development snapshots](https://github.com/FreeCAD/FreeCAD-Bundle/releases/tag/weekly-builds) of FreeCAD 0.20. The pictures for the animated graphic were made with the FreeCAD macro [ Screen Wiki](Macro_Screen_Wiki.md). The animated GIF itself was made using [GIMP](https://en.wikipedia.org/wiki/GIMP). For the release notes it was cropped and resized using [ezgif](https://ezgif.com/crop).* |
+++



## Generale

### freecad.org

Siamo felici che il [progetto KiCAD](https://www.kicad.org/), attraverso [KiCAD services corp.](https://www.kipro-pcb.com/), ci abbia sponsorizzato il dominio freecad.org. Ora tutti i siti Web di FreeCAD sono disponibili in [freecadweb.org](https://freecadweb.org) e [freecad.org](https://freecad.org).

### Bug/Issue tracker 

Il bug tracker di FreeCAD è stato spostato su GitHub: <https://github.com/FreeCAD/FreeCAD/issues>

**Nota:** Verranno prese in considerazione solo le segnalazioni di bug con una precedente discussione nel forum. I report senza questa condizione verranno chiusi.



### Nuovo sistema di help 

Il sistema di aiuto è stato riscritto e aggiornato per visualizzare le informazioni direttamente dal nostro [Wiki](User_hub/it.md). Il sistema ora si basa sul [Help Addon](https://github.com/FreeCAD/FreeCAD-Help). Quando utilizzi per la prima volta lo strumento [Aiuto](Std_Help/it.md) o lo strumento [Cos\'è questo?](Std_WhatsThis/it.md) ti verrà chiesto di installarlo.



## Interfaccia utente 

+++
| ![](images/Navi_Cube_relnotes_0.20.gif ) | The navigation cube was reworked:                                                                                                                                                                                                                                                                                                                                                                                                                        |
|                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                                                                | -   There are now edge faces to rotate the 3D view 45°.                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                                                | -   A new preference [Rotate to nearest](Preferences_Editor#Navigation.md) has been introduced. If selected, the 3D view is rotated to the nearest most logical position, based on the current orientation of the cube, when a cube face is clicked. Else clicking a face will always result in the same rotation. To experience the difference try the same click sequence as in the animation with and without the option *Rotate to nearest*. |
|                                                                | -   By clicking the new round button in the top right corner you can quickly switch to the backview of the current scene.                                                                                                                                                                                                                                                                                                                                |
|                                                                | -   The size of the cube can now be adjusted with the [Cube size](Preferences_Editor#Navigation.md) preference.                                                                                                                                                                                                                                                                                                                                  |
|                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                                                                | [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=3&t=52118), [Pull request #4502](https://github.com/FreeCAD/FreeCAD/pull/4502).                                                                                                                                                                                                                                                                                                          |
+++

+++
| ![](images/Improved_tooltips_relnotes_0.20.gif ) | Tooltips now display the command name in the title, making it easier for new users to look for help. At the end of the tooltip the \"internal\" command name is added in parentheses: *(Std_WhatsThis)*. This is also the name of the page that documents the command in the Wiki. [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=34&t=58747), [Pull request #4978](https://github.com/FreeCAD/FreeCAD/pull/4978). |
+++

+++
| <img alt="" src=images/Std_UserEditMode_relnotes_0.20.gif  style="width:384px;"> | The new [Std UserEditMode](Std_UserEditMode.md) command allows the user to choose an edit mode that will be used when an object is double-clicked in the [Tree view](Tree_view.md). Click the image on the left so see an animation of the selection. If a selected edit mode is not applicable, the object\'s default edit mode is used instead. [Pull request #5110](https://github.com/FreeCAD/FreeCAD/pull/5110). |
+++

+++
| ![](images/Dependencies-selection_relnotes_0.20.png ) | The [Tree view](Tree_view.md) context menu has the new entry **Add dependent objects to selection**.          |
|                                                                                          | [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=8&t=13566), [Pull request #4133](https://github.com/FreeCAD/FreeCAD/pull/4133). |
|                                                                                          |                                                                                                                                                 |
|                                                                                          | In the image the *Hole001* object was selected and then its                                                                                     |
|                                                                                          | dependencies were added to the selection via the context menu.                                                                                  |
+++

+++
| <img alt="" src=images/Part_SectionCut_example_relnotes_0.20.png  style="width:200px;"> | The new tool [Section Cut](Part_SectionCut.md) allows to get non-hollow and also persistent cuts of parts and assemblies.                |
|                                                                                                         | [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=27&t=52441), [Pull request #4118](https://github.com/FreeCAD/FreeCAD/pull/4118). |
+++



### Ulteriori miglioramenti dell\'interfaccia utente 

-   It is now possible to use the decimal separator belonging to the language specified for the FreeCAD interface. For example on a German Windows, when you set the interface language to **English** and select the new option **Use selected language number format**, the dot will be used as the decimal separator. See [Preferences](Preferences_Editor#General.md). [Pull request #6364](https://github.com/FreeCAD/FreeCAD/pull/6364)**Note**: For [FEM](FEM_Workbench.md) simulations using the dot as decimal separator is highly recommended to get correct results.
-   Two new mouse navigation styles have been added. One based on [OpenSCAD](Mouse_navigation#OpenSCAD_navigation.md), the other on [TinkerCAD](Mouse_navigation#TinkerCAD_navigation.md). [Forum discussion OpenSCAD](https://forum.freecadweb.org/viewtopic.php?f=8&t=60975), [Forum discussion TinkerCAD](https://forum.freecadweb.org/viewtopic.php?p=544639#p544376), [commit 1](https://github.com/FreeCAD/FreeCAD/commit/a1c9ab658c), [commit 2](https://github.com/FreeCAD/FreeCAD/commit/ef100d55e9d50), [commit 3](https://github.com/FreeCAD/FreeCAD/commit/549e5b5650).
-   It is now possible to pan the view of the [dependency graph](Std_DependencyGraph.md) with the mouse. [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=3&t=34791), [Pull request #4638](https://github.com/FreeCAD/FreeCAD/pull/4638).
-   Fixed an issue where using tablet pen devices (e.g. Wacom tablet) was slow to the point of being completely unusable. [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=8&t=45046), [Pull request #4687](https://github.com/FreeCAD/FreeCAD/pull/4687).
-   The coordinate system in the 3D view can be resized in the preferences in the section [Display → 3D View](Preferences_Editor#3D_View.md). [Pull request #5182](https://github.com/FreeCAD/FreeCAD/pull/5182)
-   A new setting in [Preferences → General](Preferences_Editor#General.md) allows to substitute the numerical keypad decimal separator with the appropriate locale separator if they are different. [Pull request #3256](https://github.com/FreeCAD/FreeCAD/pull/3256) [Pull request #5150](https://github.com/FreeCAD/FreeCAD/pull/5150) [Pull request 5203](https://github.com/FreeCAD/FreeCAD/pull/5203)
-   It is now possible to set the **Backspace** key as a standalone shortcut key without the need to specify an additional modifier key. [Pull request #5428](https://github.com/FreeCAD/FreeCAD/pull/5428)



## Sistema principale e API 



### Sistema principale 

+++
| <img alt="" src=images/Object_selection_relnotes_0.20.png  style="width:384px;"> | When using **Edit → Copy** or **Edit → Duplicate selection** for an object with dependencies there is a new **Use Original Selections** button in the object selection dialog. Click this button to copy/duplicate only the objects you originally selected prior to opening the dialog, ignoring dependencies and ignoring any actions you might have taken while the dialog was open, such as checking or unchecking some of the checkboxes. The effect is the same as if you had unchecked all the checkboxes next to the objects you did not originally select and pressed OK. Note: special care should be taken when copying/duplicating TechDraw Pages. It is recommended to also copy/duplicate all children of the Page (Templates, Views, Dimensions, etc.). Otherwise changes to one Page will also impact the other page. For example, deleting a View on one Page also removes it from the other Page, or deleting a page will also remove all its content from the other Page. |
+++

+++
| <img alt="" src=images/PrefPacks_relnotes_0.20.png  style="width:384px;"> | A new type of add-on called a [Preference Pack](Preference_Packs.md) was added, allowing a subset of a user preferences file (user.cfg) to be saved, distributed, and easily applied by other users. Preference Packs can be use to distribute \"Themes,\" for example, by allowing a developer to include both a Qt stylesheet for widgets as well as a set of other colors and styles for items in the user interface that cannot be set using a stylesheet (e.g. text colors in the Python editor or report view, etc.). Anything that can be configured via a user.cfg file can be set using a Preference Pack. [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=17&t=62477) |
+++

+++
| <img alt="" src=images/Autoload_relnotes_0.20.png  style="width:384px;"> | The \"Workbenches\" preference panel was modified to support the ability to \"autoload\" workbenches on FreeCAD startup. |
+++

On Linux, the default location of FreeCAD\'s configuration, data and cache files was changed to follow the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html). [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=9&t=63648). Here is a comparison of the old and new locations:

  Description           Old location      New location                Defaults to
     
  Configuration files   \$HOME/.FreeCAD   \$XDG_CONFIG_HOME/FreeCAD   \$HOME/.config/FreeCAD
  Data files            \$HOME/.FreeCAD   \$XDG_DATA_HOME/FreeCAD     \$HOME/.local/share/FreeCAD
  Cache files           /tmp              \$XDG_CACHE_HOME/FreeCAD    \$HOME/.cache/FreeCAD

If you wish to keep using the old locations you may start FreeCAD with the `--keep-deprecated-paths` option.

### API

FreeCAD ha adottato molte nuove funzioni API Python:


<div class="mw-collapsible mw-collapsed toccolours">



#### Nuove API Python 


<div class="mw-collapsible-content">

-   *ChFi2d_AnaFilletAlgoPy*: An analytical algorithm for the calculation of fillets. [commit f94ab3ec](https://github.com/FreeCAD/FreeCAD/commit/f94ab3ec)
-   *ChFi2d_ChamferAPIPy*: Algorithm that creates a chamfer between two linear edges. [commit 30f8015e7](https://github.com/FreeCAD/FreeCAD/commit/30f8015e7)

-   *Circle2dPy::getCircleCenter*: Gets the circle center defined by three points. [commit 3dc91fa2](https://github.com/FreeCAD/FreeCAD/commit/3dc91fa2)

-   *ComplexGeoDataPy::applyRotation*: Applies an additional rotation to the placement. [commit 32592de8](https://github.com/FreeCAD/FreeCAD/commit/32592de8)
-   *ComplexGeoDataPy::applyTranslation*: Applies an additional translation to the placement. [commit 32592de8](https://github.com/FreeCAD/FreeCAD/commit/32592de8)
-   *ComplexGeoDataPy::countSubElements*: Returns the number of elements of a type. [commit 32592de8](https://github.com/FreeCAD/FreeCAD/commit/32592de8)
-   *ComplexGeoDataPy::getElementTypes*: Returns a list of element types. [commit 32592de8](https://github.com/FreeCAD/FreeCAD/commit/32592de8)
-   *ComplexGeoDataPy::getFaces*: Returns a tuple of points and triangles with a given accuracy. [commit 32592de8](https://github.com/FreeCAD/FreeCAD/commit/32592de8)
-   *ComplexGeoDataPy::getLines*: Returns a tuple of points and lines with a given accuracy. [commit 32592de8](https://github.com/FreeCAD/FreeCAD/commit/32592de8)
-   *ComplexGeoDataPy::getLinesFromSubelement*: Returns vertexes and lines from a sub-element. [commit 32592de8](https://github.com/FreeCAD/FreeCAD/commit/32592de8)
-   *ComplexGeoDataPy::getPoints*: Returns a tuple of points and normals with a given accuracy. [commit 32592de8](https://github.com/FreeCAD/FreeCAD/commit/32592de8)
-   *ComplexGeoDataPy::transformGeometry*: Applies a transformation to the underlying geometry. [commit 32592de8](https://github.com/FreeCAD/FreeCAD/commit/32592de8)

-   *ControlPy::showModelView*: Shows the model view. [commit 033bf619](https://github.com/FreeCAD/FreeCAD/commit/033bf619)

-   *DocumentPy::clearDocument*: Clears the whole document. [commit 526dc1a0](https://github.com/FreeCAD/FreeCAD/commit/526dc1a0)
-   *DocumentPy::getFileName*: For a regular document it returns its file name property. For a temporary document it returns its transient directory. [commit 526dc1a0](https://github.com/FreeCAD/FreeCAD/commit/526dc1a0)
-   *DocumentPy::getProgramVersion*: Gets the program version that a project file was created with. [commit 526dc1a0](https://github.com/FreeCAD/FreeCAD/commit/526dc1a0)
-   *DocumentPy::isClosable*: Checks if the document can be closed. [commit 526dc1a0](https://github.com/FreeCAD/FreeCAD/commit/526dc1a0)
-   *DocumentPy::isSaved*: Checks if the document is saved. [commit 526dc1a0](https://github.com/FreeCAD/FreeCAD/commit/526dc1a0)
-   *DocumentPy::isTouched*: Checks if any object is in touched state. [commit 526dc1a0](https://github.com/FreeCAD/FreeCAD/commit/526dc1a0)
-   *DocumentPy::mustExecute*: Checks if any object must be recomputed. [commit 526dc1a0](https://github.com/FreeCAD/FreeCAD/commit/526dc1a0)
-   *DocumentPy::purgeTouched*: Purges the touched state of all objects. [commit 526dc1a0](https://github.com/FreeCAD/FreeCAD/commit/526dc1a0)
-   *DocumentPy::setClosable*: Sets a flag that allows or forbids to close a document. [commit 526dc1a0](https://github.com/FreeCAD/FreeCAD/commit/526dc1a0)

-   *DrawPagePy::requestPaint*: Paints a TechDraw page. [commit 79f9fb68](https://github.com/FreeCAD/FreeCAD/commit/79f9fb68)

-   *HLRBRep_AlgoPy*: To access Part\'s hidden line removal (HLR). [commit 73a98671](https://github.com/FreeCAD/FreeCAD/commit/73a98671)
-   *HLRBRep_PolyAlgoPy*: To access Part\'s poly hidden line removal (HLR). [commit ea85cf5e](https://github.com/FreeCAD/FreeCAD/commit/ea85cf5e)
-   *HLRToShapePy*: To access Part\'s hidden line removal (HLR). [commit 73a98671](https://github.com/FreeCAD/FreeCAD/commit/73a98671)
-   *PolyHLRToShapePy*: To access Part\'s poly hidden line removal (HLR). [commit ea85cf5e](https://github.com/FreeCAD/FreeCAD/commit/ea85cf5e)

-   *MDIViewPy::printPdf*: Prints a PDF. [commit c93031da](https://github.com/FreeCAD/FreeCAD/commit/c93031da)
-   *MDIViewPy::printPreview*: Prints a preview. [commit c93031da](https://github.com/FreeCAD/FreeCAD/commit/c93031da)
-   *MDIViewPy::printView*: Prints a view. [commit c93031da](https://github.com/FreeCAD/FreeCAD/commit/c93031da)
-   *MDIViewPy::redoActions*: Redoes actions. [commit c93031da](https://github.com/FreeCAD/FreeCAD/commit/c93031da)
-   *MDIViewPy::undoActions*: Undoes actions. [commit c93031da](https://github.com/FreeCAD/FreeCAD/commit/c93031da)

-   *PrecisionPy*: To access the precision defined by the OpenCascade kernel. [commit 20b86e55](https://github.com/FreeCAD/FreeCAD/commit/20b86e55)

-   *PropertyContainerPy::setDocumentationOfProperty*: Sets the documentation string of a dynamic property of this class. [commit 8cf3cf33](https://github.com/FreeCAD/FreeCAD/commit/8cf3cf33)
-   *PropertyContainerPy::setGroupOfProperty*: Set the name of the group of a dynamic property. [commit 8cf3cf33](https://github.com/FreeCAD/FreeCAD/commit/8cf3cf33)

-   *PythonWorkbenchPy::reloadActive*: Reload the active workbench after changing menus or toolbars. [commit 0bbc253d](https://github.com/FreeCAD/FreeCAD/commit/0bbc253d)

-   *RotationPy::fromEuler*: Sets the Euler angles of a rotation or gets the Euler angles in a given sequence for a rotation. [commit 951a0be9](https://github.com/FreeCAD/FreeCAD/commit/951a0be9)
-   *RotationPy::toEulerAngles*: Gets the Euler angles in a given sequence for this rotation.. [commit c1454dfb](https://github.com/FreeCAD/FreeCAD/commit/c1454dfb)

-   *SpreadsheetViewPy*: To access spreadsheets. [commit 6e713628](https://github.com/FreeCAD/FreeCAD/commit/6e713628)

-   *UnitsApi::sToNumber*: Converts a quantity or float to a string. [commit befbd95d](https://github.com/FreeCAD/FreeCAD/commit/befbd95d)

-   *View3DInventorPy::getCornerCrossSize*: Returns current corner axis cross size. [commit 9d15df29](https://github.com/FreeCAD/FreeCAD/commit/9d15df29)
-   *View3DInventorPy::setPopupMenuEnabled*: Enables popup menu. [commit 9def811a](https://github.com/FreeCAD/FreeCAD/commit/9def811a)
-   *View3DInventorPy::isCornerCrossVisible*: Returns current corner axis cross visibility. [commit 9d15df29](https://github.com/FreeCAD/FreeCAD/commit/9d15df29)
-   *View3DInventorPy::isPopupMenuEnabled*: Returns if popup menu is enabled. [commit 9def811a](https://github.com/FreeCAD/FreeCAD/commit/9def811a)
-   *View3DInventorPy::projectPointToLine*: Projects the given 2d point to a line. [commit b6527a70](https://github.com/FreeCAD/FreeCAD/commit/b6527a70)
-   *View3DInventorPy::setCornerCrossSize*: Defines corner axis cross size. [commit 9d15df29](https://github.com/FreeCAD/FreeCAD/commit/9d15df29)
-   *View3DInventorPy::setCornerCrossVisible*: Defines corner axis cross visibility. [commit 9d15df29](https://github.com/FreeCAD/FreeCAD/commit/9d15df29)

-   *ViewProviderSpreadsheetPy*: To handle spreadsheet cells.[commit 16bbe123](https://github.com/FreeCAD/FreeCAD/commit/16bbe123) and [commit 093f15dc](https://github.com/FreeCAD/FreeCAD/commit/093f15dc)


</div>

#### Changed Python API 

-   *MeshObject::trim(base, normal)* was changed to *MeshPy::trimByPlane(base, normal)*: Trims the mesh with a given plane. [commit 837de28e](https://github.com/FreeCAD/FreeCAD/commit/837de28e)


</div>

## Addon Manager 

+++
| <img alt="" src=images/AddonManagerExpanded_relnotes_0.20.png  style="width:400px;"> | The [Addon Manager](Std_AddonMgr.md) was modified to support the distribution of Preference Packs, and to display information found in an addon\'s metadata. The Addon Manager also includes improved support for Addons whose source code is located at several different git hosting locations. Networking support was improved to provide more robust handling of SSL connections and support for proxies requiring authentication. Support was added for automatically adding macro buttons to the toolbar after installing, for disabling Addons without removing them, and for switching which git branch of an Addon is checked out. Finally, the user interface was modified to improve searching and display of different list filters. |
+++

## Arch Workbench 

+++
| <img alt="" src=images/ArchWindow_Placement_1r_relnotes_0.20.png  style="width:250px;"> <img alt="" src=images/ArchWindow_Placement_2r_relnotes_0.20.png  style="width:250px;"> | **SketchArch workbench**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                                                                                                                                                                                                 | With the <img alt="" src=images/Attach_in_SketchArch.svg  style="width:20px;"> [Attach Feature](https://github.com/paullee0/FreeCAD_SketchArch) it is now possible to place <img alt="" src=images/Arch_Window.svg  style="width:20px;"> [Windows](Arch_Window.md) and <img alt="" src=images/Arch_Equipment.svg  style="width:20px;"> [Equipment](Arch_Equipment.md) parametrically and intuitively in relation to <img alt="" src=images/Arch_Wall.svg  style="width:20px;"> [Walls](Arch_Wall.md). To use this feature the experimental external <img alt="" src=images/SketchArch_Workbench.svg  style="width:20px;"> [SketchArch Workbench](https://github.com/paullee0/FreeCAD_SketchArch) must be installed. [Add-on and ReadMe on Github](https://github.com/paullee0/FreeCAD_SketchArch) (Not yet available in the [Add-on Manager](Std_AddonMgr.md)). |
|                                                                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                                                                                                                                                                                                 | [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=23&t=50802)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
+++

+++
| <img alt="" src=images/NewArchStructureProperties_relnotes_0.20.jpg  style="width:250px;"> | **New properties for Arch Structure objects**:                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                                                               | -   **BasePerpendicularToTool**: it creates a copy of the Base (extrusion profile) at the beginning of the Tool (extrusion path) and places it perpendicular to the first edge of the tool. It is the same as attaching the Base with MapMode=NormalToEdge, but it is automatic and allows to reuse the same Base object for multiple Structures. When BasePerpendicularToTool = True, more properties control the placement of the Base relative to the Tool axis. They are shown in the attached image. |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|                                                                                                               | -   **ToolOffsetFirst** and **ToolOffsetLast**: extend/trim the Structure at the start and end respectively (the real length of the Structure is available in the ComputedLength read-only property).                                                                                                                                                                                                                                                                                                     |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|                                                                                                               | -   **BaseRotation**: rotate the Base (the rotation is around the Base\'s \"(0,0)\" point which is the center for [Arch Profiles](Arch_Profile.md), the origin for Sketches and usually the first point for [Draft Wires](Draft_Wire.md)).                                                                                                                                                                                                                                                |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|                                                                                                               | -   **BaseOffsetX** and **BaseOffsetY**: move the Base (extrusion profile).                                                                                                                                                                                                                                                                                                                                                                                                                               |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|                                                                                                               | -   **BaseMirror**: mirror the Base (extrusion profile).                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                                                               | A new command **Create multiple Arch Structure** was also added. It uses the first selected object as a Base, and creates Arch Structures objects for every Edge of the other selected objects. Then, the properties of individual Structure objects can be adjusted in the Property editor. This command was added for workflow with a master Sketch (there is risk of topological naming problem unless you create non-parametric copy of the master Sketch or use Realthunder\'s version).             |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                                                               | Support for **2D data** such as linework, hatches, texts and dimensions is now enabled in IFC import and export, which contributes to making the IFC format more and more suitable for traditional 2D CAD work. A similar effort is being made in [BlenderBIM](https://blenderbim.org). More 2D workflow improvements are documented [in this forum thread](https://forum.freecadweb.org/viewtopic.php?p=563067#p563067).                                                                                 |
|                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                                                               | [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=23&t=43228&start=60), [Pull request #3229](https://github.com/FreeCAD/FreeCAD/pull/3229)                                                                                                                                                                                                                                                                                                                                                  |
+++

## Draft Workbench 

-   A **Global** checkbox was added to the task panel of many drafting commands. Checking it allows input of coordinates in the global coordinate system even if the [working plane](Draft_SelectPlane.md) is not aligned with the global XY plane.

-   The <img alt="" src=images/Draft_Hatch.svg  style="width:24px;"> [Draft Hatch](Draft_Hatch.md) command was introduced. It creates hatches on the faces of a selected object using patterns from AutoCAD PAT files.

-   The <img alt="" src=images/Draft_AddNamedGroup.svg  style="width:24px;"> [Draft AddNamedGroup](Draft_AddNamedGroup.md) command was introduced. The <img alt="" src=images/Draft_AddToGroup.svg  style="width:24px;"> [Draft AddToGroup](Draft_AddToGroup.md) command was extended with the same functionality.

-   Work on the <img alt="" src=images/Draft_SetStyle.svg  style="width:24px;"> [Draft SetStyle](Draft_SetStyle.md) command, still in progress in FreeCAD version 0.19, was completed.

-   A double-click edit option was added for <img alt="" src=images/Draft_Text.svg  style="width:24px;"> [Draft Texts](Draft_Text.md). It opens the same edit task panel used when creating a text.

-   For <img alt="" src=images/Draft_Dimension.svg  style="width:24px;"> [Draft Dimensions](Draft_Dimension.md) the {{Value|arch}} **Unit Override** for imperial architectural dimensions was introduced.

-   <img alt="" src=images/Draft_Shape2DView.svg  style="width:24px;"> [Draft Shape2DView](Draft_Shape2DView.md) objects now have an **Auto Update** property. Setting it to {{False}} can be useful if there are many Draft Shape2DViews in a document or if they are complex.

-   It is now possible to reverse a [Draft Wire](Draft_Wire.md) via the <img alt="" src=images/Draft_Edit.svg  style="width:24px;"> [Draft Edit](Draft_Edit.md) context menu. [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=23&t=58643&start=20), [Pull request #4811](https://github.com/FreeCAD/FreeCAD/pull/4811).

### Further Draft improvements 

-   Fixed [Draft Snap Grid](Draft_Snap_Grid.md) when the cursor is over a face. [Forum discussion](https://forum.freecad.org/viewtopic.php?f=23&t=62274). [Git commit](https://github.com/FreeCAD/FreeCAD/commit/1761eb8ce).

-   New [Draft Texts](Draft_Text.md) are now aligned with the [working plane](Draft_SelectPlane.md), [Pull request #5092](https://github.com/FreeCAD/FreeCAD/pull/5092).

-   Support for two DWG converters was added: [LibreDWG](https://www.gnu.org/software/libredwg) and [QCAD pro](https://qcad.org/en/qcad-command-line-tools#dwg2dwg). See [Import Export Preferences](Import_Export_Preferences#DWG.md) and [FreeCAD and DWG Import](FreeCAD_and_DWG_Import.md) for more information.

## FEM Workbench 

   
  <img alt="" src=images/FEM_Z88-settings_relnotes_0.20.png  style="width:384px;">The new Z88 settings and their default values                                                                                The [Z88 solver](FEM_SolverZ88.md) is now fully usable. You can specify the solver method and change the memory settings. The new default values allow you to perform also complex simulations directly. [commit d035bbc1ca and following](https://github.com/FreeCAD/FreeCAD/commit/d035bbc1ca)
  <img alt="" src=images/FEM_buckling-analysis_relnotes_0.20.gif  style="width:384px;">Result of a linear buckling analysis.Click on the image to see the animation.                        It is now possible to perform buckling analyses using the [Calculix](FEM_SolverCalculixCxxtools.md) solver. [Pull request #4379](https://github.com/FreeCAD/FreeCAD/pull/4379)
  <img alt="" src=images/FEM_Gmsh-MeshSizeFromCurvature_relnotes_0.20.png  style="width:384px;">Effect of *Mesh Size From Curvature*; left: set to 12, right: deactivated                        There is a new property for the [Gmsh](FEM_MeshGmshFromShape.md) mesher. The number of mesh elements per $2\pi$ times the radius of the curvature can be specified. The default is 12 and to get a finer mesh at small corners or holes, this value can be increased for better results. This feature requires Gmsh 4.8 or newer. [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=18&t=56401), [Pull request #4596](https://github.com/FreeCAD/FreeCAD/pull/4596)
  <img alt="" src=images/FEM_Gmsh-RecombinationAlgorithm_relnotes_0.20.png  style="width:384px;">Effect of the recombination algorithm; left: using *Simple*, right: using *Simple full-quad*   FreeCAD now allows to select an algorithm as well as 3D mesh recombination for the [Gmsh](FEM_MeshGmshFromShape.md) mesher. For more details about mesh element recombination see [FEM MeshGmshFromShape](FEM_MeshGmshFromShape#Element_Recombination.md). [Pull request #4706](https://github.com/FreeCAD/FreeCAD/pull/4706)
   

### Further FEM improvements 

-   **Important:** Starting from this release, FreeCAD will use [SI units](https://en.wikipedia.org/wiki/International_System_of_Units) (m, kg, s, K, A, mol, cd) to write the [Elmer solver](FEM_SolverElmer.md) input files (*case.sif* and *mesh.nodes*). This is independent of the used FreeCAD [unit system](Preferences_Editor#Units.md).
-   **Important:** Starting from this release, the scale of [result pipelines](FEM_PostPipelineFromResult.md) and their [filters](FEM_Workbench#Menu__Results.md) will use SI units (m, kg, s, K, A, mol, cd). So the displacement is given in meter, the stress in Pascal. This applies to all SI-derived FreeCAD [unit systems](Preferences_Editor#Units.md).
-   Solving with the [Calculix](FEM_SolverCalculixCxxtools.md) solver now uses all CPU cores. [Pull request #6374](https://github.com/FreeCAD/FreeCAD/pull/6374)
-   Meshing with [Gmsh](FEM_MeshGmshFromShape.md) now uses all CPU cores. [Pull request #6370](https://github.com/FreeCAD/FreeCAD/pull/6370)
-   The element order of [Gmsh](FEM_MeshGmshFromShape.md) meshes can be changed via the mesh dialog. [Pull request #4660](https://github.com/FreeCAD/FreeCAD/pull/4660)
-   The [Data at point clip](FEM_PostFilterDataAtPoint.md) result filter is now actually working: One gets info from result meshes by clicking into them or by specifying a mesh coordinate.
-   A new constraint was added: **Model → Mechanical Constraints → [<img src=images/FEM_ConstraintCentrif.svg style="width:16px"> [Constraint Centrif](FEM_ConstraintCentrif.md)**. [Pull request #4738](https://github.com/FreeCAD/FreeCAD/pull/4738)
-   A new solver was added: **Solve → [<img src=images/FEM_SolverMystran.svg style="width:16px"> [Solver Mystran](FEM_SolverMystran.md)**. Multiple commits.
-   A new constraint was added: **Model → Mechanical Constraints → [<img src=images/FEM_ConstraintSpring.svg style="width:16px"> [Constraint Spring](FEM_ConstraintSpring.md)**. [Pull request #4982](https://github.com/FreeCAD/FreeCAD/pull/4982)
-   It is now possible to have [result pipelines](FEM_PostPipelineFromResult.md) with several filters, where some take other filters as input, and some take the results directly from the pipeline. [commit 708a300b](https://github.com/FreeCAD/FreeCAD/commit/708a300b)
-   Material cards can now contain values for the electrical conductivity. [Pull request #4647](https://github.com/FreeCAD/FreeCAD/pull/4647)
-   Material cards added for Nitrogen and Argon. [Pull request #4649](https://github.com/FreeCAD/FreeCAD/pull/4649)
-   Support for the [Gmsh](FEM_MeshGmshFromShape.md) mesh algorithms *\"HXT\"* (3D) and *\"Packing Parallelograms\"* (2D) added. [Pull request #4654](https://github.com/FreeCAD/FreeCAD/pull/4654)
-   Allow to specify an algorithm for the [Gmsh](FEM_MeshGmshFromShape#Properties.md) property *\"High Order Optimize\"*. [Pull request #4705](https://github.com/FreeCAD/FreeCAD/pull/4705)
-   Nonlinear solid materials with simple hardening can now have an arbitrary number of yield points. [Pull request #5024](https://github.com/FreeCAD/FreeCAD/pull/5024)
-   Allow modal adding/removal of geometric entities to constraints acting on boundaries. [Pull request #5117](https://github.com/FreeCAD/FreeCAD/pull/5117)
-   Most FEM constraint dialogs now behave uniformly and provide the same 3D object selection features. [Pull request #5391](https://github.com/FreeCAD/FreeCAD/pull/5391)

## Export

-   DXF: The missing unit block was added to the header14.rub file. [Pull request #5793](https://github.com/FreeCAD/FreeCAD/issues/5793)

## Mesh

### Improved support for NASTRAN GRID elements 

The Mesh import tool now supports the high-precision \"GRID\*\" element. The standard-precision \"GRID\" element was also improved, now supporting both space-delimited numeric input as well as fixed-field-width input, per the NASTRAN95 format documentation.

### Further Mesh improvements 

Fixed false negatives during self-intersection tests when facets are coplanar: [Pull request #5002](https://github.com/FreeCAD/FreeCAD/pull/5002).

## OpenSCAD Workbench 

Interoperability with OpenSCAD has been improved, adding support for several operations missing from earlier versions (linear extrude with rotations, rotational extrusions). Several operations are modified to provide improved FreeCAD object equivalents, particularly for twisted extrusions. Surface generation from discrete data was modified to give more OpenSCAD-like results, rather than splined surfaces.

New options were added to support running either FreeCAD, OpenSCAD, or both, in sandboxed environments such as AppImages and Snap packages: data can now be transferred to and from OpenSCAD via the standard temporary directory mechanism, via a user-specified temp directory that both executables have access to, or new to OpenSCAD 2021.1, via a \"stdout pipe\" mechanism, bypassing temporary files entirely.

+++
| <img alt="" src=images/OpenSCAD_AddElement_relnotes_0.20.png  style="width:384px;"> | The following options were added to the task panel of the [Add OpenSCAD element](OpenSCAD_AddOpenSCADElement.md) feature: |
|                                                                                                 |                                                                                                                                   |
|                                                                                                 | Load    - load a scad file                                                                                                      |
|                                                                                                 | Save    - save a scad file                                                                                                      |
|                                                                                                 | Refresh - Update FreeCAD view                                                                                                   |
|                                                                                                 | Clear   - Clear text input                                                                                                      |
|                                                                                                 |                                                                                                                                   |
|                                                                                                 | A new text box gives feedback about OpenSCAD errors.                                                                              |
+++

## Part Workbench 

   
  <img alt="" src=images/Part_Extrusion-inner-structures_relnotes_0.20.png  style="width:384px;">Tapered extrusion of a sketch with an inner structure.   A tapered [extrusion](Part_Extrude.md) of inner structures now creates usable results. Previously, inner structures were extruded as if they were stand-alone and not part of a structure. [Pull request #5367](https://github.com/FreeCAD/FreeCAD/pull/5367)
   

### Further Part improvements 

-   The dialog to edit [Cylinders](Part_Cylinder.md) now allows to specify an angle relative to the normal of the chosen attachment plane. This way one can create skew cylinders. [Pull request #4708](https://github.com/FreeCAD/FreeCAD/pull/4708)
-   The [Face Colors](Part_ColorPerFace.md) tool now also allows to set the transparency (*Alpha channel*) of faces. This transparency can be [exported](Import_Export.md), making e.g. STEP files with transparent parts possible.
-   The following commands now support App::Links: [Loft](Part_Loft.md), [Sweep](Part_Sweep.md), [Extrude](Part_Extrude.md), [Revolve](Part_Revolve.md), [Reverse shapes](Part_ReverseShape.md), [Mirror](Part_Mirror.md), [Offset2D](Part_Offset2D.md), [Offset3D](Part_Offset.md), [Check Geometry](Part_CheckGeometry.md), [Ruled Surface](Part_RuledSurface.md), [Cross-sections](Part_CrossSections.md), and [Thickness](Part_Thickness.md). [Pull request #6478](https://github.com/FreeCAD/FreeCAD/pull/6478)

## PartDesign Workbench 

+++
| <img alt="" src=images/PD_Pad-Length-along-reference_relnotes_0.20.gif  style="width:384px;">Padding along an edge from the model.Click on the image to see the animation.                                                                      | There is a new option to [Pad](PartDesign_Pad.md) along the direction of an edge in the 3D model. [Pull request #4685](https://github.com/FreeCAD/FreeCAD/pull/4685)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
+++
| <img alt="" src=images/PartDesign_Chamfer_Face_Selection_relnotes_0.20.png  style="width:384px;">                                                                                                                                                                       | When Distance and Angle is specified in the [Chamfer](PartDesign_Chamfer.md) tool and faces are selected, the distance will be applied along the selected faces. Likewise if two distances are specified then Size 1 will be applied along the selected face. This behaviour can be swapped to the other face using the flip direction button. [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=19&t=62084), [Pull request #5039](https://github.com/FreeCAD/FreeCAD/pull/5039)                                                                                                                                                                                                                                                                    |
+++
| <img alt="" src=images/PartDesign_Loft_Vertex_relnotes_0.20.png  style="width:384px;">A loft with multiple sections, the final one is a vertex.                                                                                                                      | It is now possible to create an [Additive](PartDesign_AdditiveLoft.md) or [Subtractive Loft](PartDesign_SubtractiveLoft.md), or an [Additive](PartDesign_AdditivePipe.md) or [Subtractive Pipe](PartDesign_SubtractivePipe.md) towards, or from, a [Vertex](Glossary#V.md) of either a sketch or a body. This allows to create pyramids for example.**Note**: Vertices in sketches are created as construction geometry. To use them as endpoints of lofts, you must first [change them to normal geometry](Sketcher_ToggleConstruction.md). [Pull request #5170](https://github.com/FreeCAD/FreeCAD/pull/5170) (for lofts), [Pull request #5193](https://github.com/FreeCAD/FreeCAD/pull/5193) (for pipes) |
+++
| <img alt="" src=images/PD_Pad-Taper-angle_relnotes_0.20.png  style="width:384px;">A tapered pocket within a non-tapered pad.                                                                                                                                             | The dialog for [Pad](PartDesign_Pad.md) and [Pocket](PartDesign_Pocket.md) offers to set a taper angle for the extrusion. [Pull request #5357](https://github.com/FreeCAD/FreeCAD/pull/5357)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
+++
| <img alt="" src=images/PD_Pocket-direction_relnotes_0.20.gif  style="width:384px;">Pocketing along different directions.Click on the image to see the animation.                                                                                          | It is now possible to specify the direction for the [Pocket](PartDesign_Pocket.md) extrusion. [Pull request #5164](https://github.com/FreeCAD/FreeCAD/pull/5164)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
+++
| <img alt="" src=images/PartDesign_Cylinder_direction_relnotes_0.20.png  style="width:384px;">                                                                                                                                                                               | The dialog to edit [Cylinders](PartDesign_AdditiveCylinder.md) (additive and subtractive) now allows to specify an angle relative to the normal of the chosen attachment plane. This way one can create skew cylinders. [Pull request #4708](https://github.com/FreeCAD/FreeCAD/pull/4708)                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
+++
| <img alt="" src=images/PartDesign_Helix_Growth_relnotes_0.20.png  style="width:384px;">                                                                                                                                                                                           | The [Helix](PartDesign_AdditiveHelix.md) feature has the new mode **Height-Turns-Growth** to create flat spirals. [Forum thread](https://forum.freecadweb.org/viewtopic.php?f=19&t=56378) [Pull request #4590](https://github.com/FreeCAD/FreeCAD/pull/4590)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
+++
| <img alt="" src=images/PartDesign_Islands-Extrude_relnotes_0.20.png  style="width:384px;">A single Pad and a single [Revolution](PartDesign_Revolution.md) with nested profiles. The base block is only there to ensure that the part is a single solid. | All PartDesign features that can extrude sketches can now handle sketches with nested profiles that form islands. For example it is possible to [Revolve](PartDesign_Revolution.md) a sketch consisting of 3 nested circles with the same center point.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                                                                                                                                                                                                                                                   | **Note**: Extruding nested profiles only works if the result is still a single body. [Pull request #6381](https://github.com/FreeCAD/FreeCAD/pull/6381)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
+++
| <img alt="" src=images/PD_Pad-Length-alog-direction_relnotes_0.20.gif  style="width:384px;">Effect of the new option *Length along sketch normal*.Click on the image to see the animation.                                                       | There is a new option to [Pad](PartDesign_Pad.md) a certain length along the direction. The length is either measured along the sketch normal or along the custom direction. [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=17&t=50466), [Pull request #3893](https://github.com/FreeCAD/FreeCAD/pull/3893)                                                                                                                                                                                                                                                                                                                                                                                                                                      |
+++
| <img alt="" src=images/PartDesign_Hole_thread_relnotes_0.20.PNG  style="width:384px;">                                                                                                                                                                                             | The [Hole](PartDesign_Hole.md) feature can now model true threads. [Forum thread](https://forum.freecadweb.org/viewtopic.php?f=34&t=54240) [Pull request #4274](https://github.com/FreeCAD/FreeCAD/pull/4274)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
+++
|                                                                                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
+++

### Further PartDesign improvements 

-   In the [Helix](PartDesign_AdditiveHelix.md) feature one can now also use the sketch normal as axis. [Pull request #5199](https://github.com/FreeCAD/FreeCAD/pull/5199)
-   The [Sprocket](PartDesign_Sprocket.md) feature can now also create ISO-normed sprockets. [Forum thread](https://forum.freecadweb.org/viewtopic.php?f=22&t=44525#p478369) [Pull request #4478](https://github.com/FreeCAD/FreeCAD/pull/4478)
-   The [Loft](PartDesign_AdditiveLoft.md) and [Pipe](PartDesign_AdditivePipe.md) features now allow using the body\'s faces for sections. [Pull request #5155](https://github.com/FreeCAD/FreeCAD/pull/5155)
-   It is now possible to select several faces before calling the [Pad](PartDesign_Pad.md) or [Pocket](PartDesign_Pocket.md) dialog. In this case the first selected face will be used to determine the default padding/pocketing direction. [commit d34a5616](https://github.com/FreeCAD/FreeCAD/commit/d34a5616a2b38c96ad05f9a0763ba7504dfb814d)
-   It is possible to offset [SubShapeBinders](PartDesign_SubShapeBinder.md) if they are based on edges, wires or faces. [Pull request #6338](https://github.com/FreeCAD/FreeCAD/pull/6338)
-   [SubShapeBinders](PartDesign_SubShapeBinder.md) now have the *Refine* property like all other PartDesign objects. [Pull request #6550](https://github.com/FreeCAD/FreeCAD/pull/6550)
-   In the [Chamfer](PartDesign_Chamfer.md) and [Fillet](PartDesign_Fillet.md) dialogs all edges of a body can be selected via the context menu while in Add mode. [Pull request #5269](https://github.com/FreeCAD/FreeCAD/pull/5269)
    When you selected a 3D object before clicking the icon to create a fillet or chamfer, all object edges will automatically be selected. [Pull request #5328](https://github.com/FreeCAD/FreeCAD/pull/5328)
-   [Chamfer](PartDesign_Chamfer.md) and [Fillet](PartDesign_Fillet.md) dialogs now each have a new Use all edges checkbox, which is connected to the Use All Edges property for these objects. When the box is checked the property is set to True, when unchecked the property is set to False. When Use All Edges is True there is protection against the [topological naming problem](Topological_naming_problem.md) because then all of the edges of the base object are used regardless of how many edges there are. [Pull request #5340](https://github.com/FreeCAD/FreeCAD/pull/5340)
-   Plane selection when [adding a new sketch](PartDesign_NewSketch.md) can now be achieved with a single-click in the 3D View. [Pull request](https://github.com/FreeCAD/FreeCAD/pull/5408) [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=19&t=65020)
-   When a PartDesign tool is run without an active body, FreeCAD now offers to activate a body or create a new one. [Pull request #4949](https://github.com/FreeCAD/FreeCAD/pull/4949)
-   The [Face Colors](Part_ColorPerFace.md) tool is now also available from the PartDesign workbench.

## Path Workbench 

-   The Extensions feature was added to the [Adaptive](Path_Adaptive.md) operation. [Pull request #4388](https://github.com/FreeCAD/FreeCAD/pull/4388)
-   The [Helix](Path_Helix.md) operation was refactored and Extra offset property was added to it. [Pull request #5405](https://github.com/FreeCAD/FreeCAD/pull/5405)
-   The check if the current schema is using minutes for velocity expression and appropriate warning were added. [Pull request #6357](https://github.com/FreeCAD/FreeCAD/pull/6357)
-   External threads were added to the thread milling operation. [Pull request #6485](https://github.com/FreeCAD/FreeCAD/pull/6485)
-   The stability of engraving on sketches was improved. [Pull request #6394](https://github.com/FreeCAD/FreeCAD/pull/6394)
-   The visibility of path objects was made more natural. [Pull request #4911](https://github.com/FreeCAD/FreeCAD/pull/4911)

## Plot module 

-   FreeCAD now provides the Plot module by default, so any other module/workbench may create plots without requiring external tools [Pull request #4971](https://github.com/FreeCAD/FreeCAD/pull/4971).

## Sketcher Workbench 

+++
| <img alt="" src=images/SketcherSplitExample2_relnotes_0.20.png )                                                | New ![](images/Sketcher_Split.svg  style="width:24px;"> [Split](Sketcher_Split.md) function to split existing lines or arcs. [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=9&t=55412) [Pull request #4420](https://github.com/FreeCAD/FreeCAD/pull/4420)                                                                                                                                                                       |
+++
| <img alt="" src=images/SketcherCreateRoundedRectangleExample_relnotes_0.20.png )                | New ![](images/Sketcher_CreateOblong.svg  style="width:24px;"> [Rounded rectangle](Sketcher_CreateOblong.md) tool to create rectangles with rounded corners. [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=17&t=59210) [Main Pull request #4835](https://github.com/FreeCAD/FreeCAD/pull/4835)                                                                                                                          |
+++
| <img alt="" src=images/SketcherCreateCenteredRectangleExample_relnotes_0.20.png  style="width:384px;"> | New <img alt="" src=images/Sketcher_CreateRectangle_Center.svg  style="width:24px;"> [Centered rectangle](Sketcher_CreateRectangle_Center.md) tool to define rectangles via a center point. [Main commit](https://github.com/FreeCAD/FreeCAD/commit/8b4acf11c2caf53cc1cb8dccd8bb6de8516f4492)                                                                                                                                               |
+++
| <img alt="" src=images/Radiam_anim_relnotes_0.20.gif )                                                                    | New ![](images/Sketcher_ConstrainRadiam.svg  style="width:24px;"> [Radiam](Sketcher_ConstrainRadiam.md) function to automatically assign weight on B-spline pole, diameter on complete circle, or radius on arc. Support multi-selection as diameter/radius tools. [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=3&t=57584&start=20#p509485) [Main Pull request #4855](https://github.com/FreeCAD/FreeCAD/pull/4855) |
+++
| <img alt="" src=images/SketcherRemoveAxesAlignmentResult_relnotes_0.20.png )                        | New ![](images/Sketcher_RemoveAxesAlignment.svg  style="width:24px;"> [Remove Axes Alignment](Sketcher_RemoveAxesAlignment.md) constraint tool to remove axes alignment while trying to preserve the constraint relationship of the selection. [Main commit](https://github.com/FreeCAD/FreeCAD/commit/3c593a33cedc3e6a42928d9087f8a160852cc685)                                                                                   |
+++
| ![](images/SketcherSnapSlot_relnotes_0.20.gif )                                                          | [Slots](Sketcher_CreateSlot.md) can be constrained horizontally or vertically either by snapping it manually with the **Ctrl** key, or by using the **Auto constraints** option of Sketcher. [Pull request #5200](https://github.com/FreeCAD/FreeCAD/pull/5200)                                                                                                                                                                     |
+++
| <img alt="" src=images/SketcherBSplineInsertKnot_relnotes_0.20.gif )                                        | New ![](images/Sketcher_BSplineInsertKnot.svg  style="width:24px;"> [Insert Knot](Sketcher_BSplineInsertKnot.md) tool to insert a knot in an existing B-spline. [Pull request #5311](https://github.com/FreeCAD/FreeCAD/pull/5311) and [Pull request #6356](https://github.com/FreeCAD/FreeCAD/pull/6356)                                                                                                                            |
+++

### Further Sketcher improvements 

-   Refactored Trim support. [Pull request #4330](https://github.com/FreeCAD/FreeCAD/pull/4330) [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=10&t=54441)
-   The behavior of the <img alt="" src=images/Sketcher_CreateSlot.svg  style="width:24px;"> [Slot](Sketcher_CreateSlot.md) tool has changed. Slots can now be created by defining the center of both semicircles. [Pull request](https://github.com/FreeCAD/FreeCAD/pull/4843) [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=17&t=59243&p=508658#p508658)
-   Visibility automation allows to open Sketcher in [Section mode](Sketcher_ViewSection.md) when entering edit mode. [Pull request #4742](https://github.com/FreeCAD/FreeCAD/pull/4742) [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=3&t=57056)
-   Visibility automation allows to force camera in [Orthographic mode](Std_OrthographicCamera.md) when entering edit mode. [Pull request #4778](https://github.com/FreeCAD/FreeCAD/pull/4778) [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=22&t=44747)
-   Option to display the dimensional constraint name and use a custom format for it. [Pull request #4966](https://github.com/FreeCAD/FreeCAD/pull/4966) [Forum discussion](https://forum.freecadweb.org/viewtopic.php?t=61153)
-   When sketching a [3-point arc](Sketcher_Create3PointArc.md) with Autoconstraint enabled, [tangent constraint](Sketcher_ConstrainTangent.md) is proposed for all 3 points when hovering a line/curve. [Pull request #4945](https://github.com/FreeCAD/FreeCAD/pull/4945) [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=3&t=60596&p=520217#p520209)
-   Radius/diameter constraints are displayed using an angular rotation to ease visualization. Angle and optional randomness are user settable through parameters documented in [Fine-tuning](Fine-tuning.md). [Pull request #4934](https://github.com/FreeCAD/FreeCAD/pull/4934) [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=22&t=60370)
-   It is now possible to fix the angle of the direction when using the [Rectangular array](Sketcher_RectangularArray.md) tool. [commitc9eaa239](https://github.com/FreeCAD/FreeCAD/commit/c9eaa239) [Forum discussion](https://forum.freecadweb.org/viewtopic.php?p=535691#p535691)
-   It is now possible to fix the angle of the direction when using the tools [Clone](Sketcher_Clone.md), [Copy](Sketcher_Copy.md) and [Move](Sketcher_Move.md). [commit](https://github.com/FreeCAD/FreeCAD/commit/6e4a09f569cf) [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=8&t=62799)
-   By right-clicking a sketch in the Tree view you will now get a context menu entry \"Attachment editor\" that opens the [Attachment dialog](Part_EditAttachment.md) to modify the attachment. [commit c3511ba2f0](https://github.com/FreeCAD/FreeCAD/commit/c3511ba2f0)
-   Constraint selection is disabled when using a geometry or constraint tool. It can also be disabled manually at any time by pressing **Shift** key. [Pull request #5398](https://github.com/FreeCAD/FreeCAD/pull/5398) [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=10&t=65465)
-   A versatile view filter has been added in the Sketcher task panel to ease constraints visibility management [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=17&t=60569)
-   It is now possible to set the degree of a B-Spline ([Pull request #6463](https://github.com/FreeCAD/FreeCAD/pull/6463)) and undo the last defined control point ([Pull request #6476](https://github.com/FreeCAD/FreeCAD/pull/6476)) at creation time.
-   Revised the default shortcuts to remove conflicting shortcuts and make shortcuts easier to remember. [Forum discussion](https://forum.freecadweb.org/viewtopic.php?f=3&t=41272); Screenshots of the shortcuts for [constraints](https://wiki.freecadweb.org/images/0/0c/Sketcher_Shortcuts_v0.20_Screenshot_Constraints.png), [geometry](https://wiki.freecadweb.org/images/4/48/Sketcher_Shortcuts_v0.20_Screenshot_Geometry.png) and [various tools](https://wiki.freecadweb.org/images/9/90/Sketcher_Shortcuts_v0.20_Screenshot_variousTools.png)

## Spreadsheet Workbench 

+++
| <img alt="" src=images/Spreadsheet-Preferences-Spreadsheet_relnotes_0.20.png )      | The workbench now has ![](images/Std_DlgPreferences.svg  style="width:24px;"> [Preferences](Spreadsheet_Preferences.md). They are used by the <img alt="" src=images/Spreadsheet_Import.svg  style="width:16px;"> [Spreadsheet Import](Spreadsheet_Import.md) and <img alt="" src=images/Spreadsheet_Export.svg  style="width:16px;"> [Spreadsheet Export](Spreadsheet_Export.md) commands. [Pull request #5073](https://github.com/FreeCAD/FreeCAD/pull/5073) |
+++
| <img alt="" src=images/Spreadsheet_configuration_table_relnotes_0.20.png  style="width:384px;"> | It is now possible to setup [configuration tables](Spreadsheet_Workbench#Configuration_tables.md). This way one can define different parameter sets for the same part. Part of [Pull request #2862](https://github.com/FreeCAD/FreeCAD/pull/2862).                                                                                                                                                                                                                                |
+++
| ![](images/Spreadsheet_binding-dialog_relnotes_0.20.png )                        | Cells can now be [bound to other cells](Spreadsheet_Workbench#Cell_binding.md) of the same or a different spreadsheet. Part of [Pull request #2862](https://github.com/FreeCAD/FreeCAD/pull/2862).                                                                                                                                                                                                                                                                                |
+++

### Further Spreadsheet improvements 

-   In the row/column context-menu it is now possible to specify the position when inserting rows/columns. [Pull request #4704](https://github.com/FreeCAD/FreeCAD/pull/4704).
-   Import XLSX (used by [Std Import](Std_Import.md)): Added support for floor and ceil functions. [Pull request #5015](https://github.com/FreeCAD/FreeCAD/pull/5015).
-   Improved navigation using the **Tab** and **Enter** keys.
-   Improved interface for cutting and pasting blocks of cells.

## TechDraw Workbench 

+++
| <img alt="" src=images/TechDraw_ExtensionExample_relnotes_0.20.png  style="width:384px;"> | More than 30 new tools, so-called [Extensions](TechDraw_Workbench#Extensions.md), are now available. They offer new cosmetic features to enhance drawings. |
+++

### Further TechDraw improvements 

-   It is now possible to [Share](TechDraw_ShareView.md) and [Move](TechDraw_MoveView.md) [Views](TechDraw_Workbench#Views.md) between pages.
-   When there are several [Pages](TechDraw_PageDefault.md) and a [View](TechDraw_View.md), [ProjectionGroup](TechDraw_ProjectionGroup.md) etc. is added, there is now a dialog to ask to what page the view should be added. [Pull request #5309](https://github.com/FreeCAD/FreeCAD/pull/5309).
-   A new format specifier *%w* was added to print the given number of digits after dot and remove any trailing zeros. [Pull request #5401](https://github.com/FreeCAD/FreeCAD/pull/5401).
-   The new *%w* format specifier is now the default. And the format specifier preference was moved from the Advanced tab to the Dimension tab. [Pull request #6504](https://github.com/FreeCAD/FreeCAD/pull/6504).
-   Flipped diagonal hatch was added for the [Geometric Hatch](TechDraw_GeometricHatch.md) tool. [Pull request #6429](https://github.com/FreeCAD/FreeCAD/pull/6429).
-   There is a new option to show a grid in a [page](TechDraw_PageDefault.md). Several related [preferences](TechDraw_Preferences#Grid.md) have been introduced. [Pull request #6465](https://github.com/FreeCAD/FreeCAD/pull/6465).
-   The unit display in dimensions was fixed according to standards. The degree symbol is always present for the dimension value and tolerances, other units only appear if ShowUnits is set. The unit appears immediately after the dimension value unless there is a tolerance, then it appears after the tolerance. [Pull request #6581](https://github.com/FreeCAD/FreeCAD/pull/6581)

## Web

Qt WebEngine is now considered the default option instead of Qt WebKit.

## External workbenches 


**Note:**

these are the new workbenches created in this development cycle, or older workbenches that received updates. See [external workbenches](External_workbenches.md) for more workbenches that can be installed, and which cover a wide variety of topics. If you want to see your workbench added, join the [forum](https://forum.freecadweb.org/index.php) and present your code.

### A2plus

Several features to view, inspect and edit existing constraints were added. One can now e.g. highlight constraints with a label, suppress a constraint temporarily or run the solver only for a particular constraint.

For more information see [the constraint handling description](A2plus_Workbench#Constraint_Handling.md).

### Assembly3

+++
| <img alt="" src=images/Asm3_relnotes_0.20.jpg  style="width:384px;">     | The Assembly3 Workbench is available (as of March 2022) through the [AddonManager](Std_AddonMgr.md). This makes for easy installation and management of the external dependencies of the workbench.                                                                                                  |
|                                                                       |                                                                                                                                                                                                                                                                                                              |
|                                                                       | Assembly3 is used to create assemblies of different bodies contained in a single file or in multiple documents leveraging the full power of FreeCAD's Link system. Learn more about [Links](App_Link.md) in this [video presentation](https://www.youtube.com/watch?v=yTDkJ7JZAWs) from Realthunder. |
|                                                                       |                                                                                                                                                                                                                                                                                                              |
|                                                                       | Assembly3 Workbench uses [SolveSpace](https://solvespace.com) as it's solver.                                                                                                                                                                                                                                |
|                                                                       |                                                                                                                                                                                                                                                                                                              |
|                                                                       | Extensive documentation can be found at the main FreeCAD [Assembly3 wiki](Assembly3.md) page or Realthunder\'s GitHub [Assembly3 wiki](https://github.com/realthunder/FreeCAD_assembly3/wiki)                                                                                                        |
+++
| <img alt="" src=images/Asm3_1_relnotes_0.20.jpg  style="width:384px;"> | **Main features:**                                                                                                                                                                                                                                                                                           |
|                                                                       |                                                                                                                                                                                                                                                                                                              |
|                                                                       | -   Dynamic/interactive solver: move parts with the mouse while the solver constrains the motion.                                                                                                                                                                                                            |
|                                                                       | -   Links: use one single part multiple times in an assembly.                                                                                                                                                                                                                                                |
|                                                                       | -   External links: allows usage of parts from external documents.                                                                                                                                                                                                                                           |
|                                                                       | -   Hierarchical assemblies: permits the creation of sub assemblies.                                                                                                                                                                                                                                         |
|                                                                       | -   Assembly freeze: assemblies that are not required to remain dynamic can be excluded from calculations and are considered fixed geometry by the asm3 solver.                                                                                                                                              |
|                                                                       | -   And much more.                                                                                                                                                                                                                                                                                           |
+++

### Assembly4

   
  <img alt="" src=images/A4_veriant-beam_relnotes_0.20.png  style="width:384px;">Different length of a beam as variant.                                                  New feature to add variants. These are [links](App_Link.md) to a part with varying parameters, meaning that you can insert the same part several times, and adjust the parameters of each instance. For more info see [this forum thread](https://forum.freecadweb.org/viewtopic.php?p=538666#p538666).
  <img alt="" src=images/A4_veriant-animation_relnotes_0.20.gif  style="width:384px;">An animated assembly.Click on the image to see the animation.   Animations can be exported to the MP4 and GIF format.
   

### FCGear

The [FCGear Workbench](FCGear_Workbench.md) received a couple of improvements:

-   For involute gears, the outside (aka tip) and root diameter are exposed as properties ([details](https://github.com/looooo/freecad.gears/pull/69)).
-   Gear objects are now [attachable](Part_EditAttachment.md) ([details](https://github.com/looooo/freecad.gears/pull/72)).
-   Gear objects can now be used as additive features in PartDesign Bodies ([details](https://github.com/looooo/freecad.gears/pull/74)).
-   The creation of gear objects now appears in the undo stack ([details](https://github.com/looooo/freecad.gears/pull/83)).

### Plot

-   The Plot module has been stripped from the [Plot Workbench](Plot_Workbench.md) since it is now provided by FreeCAD.

### Ship

The [Ship Workbench](Ship_Workbench.md) is back to life!

-   A new tool to compute the [static sink and trim](https://github.com/FreeCAD/freecad.ship#static-sink-and-trim) has been added.
-   A new tool to compute the [response amplitude operators](https://github.com/FreeCAD/freecad.ship#raos) has been added on top of [capytaine](https://github.com/mancellin/capytaine).

## Compilation

Since this release FreeCAD can only be compiled using Qt 5.x and Python 3.x. The lowest supported Python version is 3.6.9 according to [this forum thread](https://forum.freecadweb.org/viewtopic.php?f=10&t=62701).

To compile FreeCAD see the instructions for [Windows](Compile_on_Windows.md), [Linux](Compile_on_Linux.md) and [MacOS](Compile_on_MacOS.md).

The supported operating systems are:

-   Windows 7, 8, 10 and 11
-   Linux Ubuntu Bionic Beaver (18.04) and Focal Fossa (20.04)
-   MacOS: 10.12 Sierra or newer

## Known Limitations 

### 32-bit Windows 

Since FreeCAD 0.19 we no longer officially support 32-bit Windows. FreeCAD might work on these systems, but no support is given.

### Remote Desktop under Windows 

Depending on the OpenGL graphics capabilities of a computer, it might be that one encounters a crash when running FreeCAD via remote desktop. To fix this upgrade your OpenGL driver. Only if this doesn\'t help:

-   Download [this](https://downloads.fdossena.com/geth.php?r=mesa64-latest) OpenGL library for 64bit Windows and extract it.
-   Rename the DLL file to *opengl32sw.dll* and copy it to the *bin* subfolder of FreeCAD\'s installation folder (overwrite the existing DLL there).

### MacOS: Start Workbench shows blank page 

If the [Start Workbench](Start_Workbench.md) shows only a blank page, you must enable the option **Use software OpenGL** in the menu **Edit → Preferences → Display**.



---
⏵ [documentation index](../README.md) > [News](Category_News.md) > [Documentation](Category_Documentation.md) > [Releases](Category_Releases.md) > Release notes 0.20/it
