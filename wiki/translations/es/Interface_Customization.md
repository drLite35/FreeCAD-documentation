# Interface Customization/es
## Introducción

La interfaz de FreeCAD está basada en el moderno kit de herramientas [Qt](http://en.wikipedia.org/wiki/Qt_(toolkit)) y tiene una organización a nivel de la técnica . Algunos aspectos de la interfaz pueden ser personalizados. Puedes, por ejemplo, añadir barras de herramientas personalizadas, con herramientas de varios ambientes de trabajo o herramientas definidas en macros, y puedes crear tus propios atajos de teclado. Pero los menús y las barras de herramientas por defecto que vienen con FreeCAD y sus ambientes de trabajo no se pueden cambiar.

![](images/Std_DlgCustomize_tab_Toolbars.png ) 
*El cuadro diálogo Personalizar*



## Utilización


<div class="mw-translate-fuzzy">

1.  Los comandos disponibles en el cuadro de diálogo Personalizar dependen de los ambientes de trabajo que se hayan cargado en la sesión actual de FreeCAD. Así que deberías cargar primero todos las ambientes de trabajo a cuyos comandos quieras tener acceso.
2.  Hay varias formas de invocar el <img alt="" src=images/Std_DlgCustomize.svg  style="width:16px;"> [Std DiálogoPersonalizar](Std_DlgCustomize/es.md) comando:
    -   Seleccione la opción **Herramientas → <img src="images/Std_DlgCustomize.svg" width=16px> Personalizar...** en el menú.
    -   Haga clic con el botón derecho en un área de la barra de herramientas y elija **<img src="images/Std_DlgCustomize.svg" width=16px> Personalizar...** en el menú contextual.
3.  Se abre el cuadro de diálogo Personalizar. Para más información, consulte [Opciones](#Opciones.md).
4.  El botón **Ayuda** no funciona en este momento.
5.  Pulse el botón **Cerrar** para cerrar el cuadro de diálogo.


</div>



## Opciones

En el cuadro de diálogo Personalizar están disponibles las siguientes pestañas:



### Teclado

![](images/Std_DlgCustomize_tab_Keyboard.png ) 
*La pestaña del teclado*

En esta pestaña se pueden definir atajos de teclado personalizados. Los atajos de teclado para los comandos de macros se pueden definir en la pestaña [Macros](#Macros.md).

#### Search

You can search for commands by entering at least 3 characters of their menu text or name in the search field. The search is case-insensitive.

It is also possible to search for shortcuts:

-   In the search field special keys in shortcuts must be entered as strings. For example to search for commands that use **Ctrl** in their shortcut enter {{Value|ctrl}} (4 letters).
-   Add parenthesis to search for single character shortcuts, for example: {{Value|(c)}}.
-   Add a comma and space between the characters of multi-character shortcuts, for example: {{Value|g, b, b}}.




<div class="mw-translate-fuzzy">

#### Añadir un atajo personalizado 


</div>

1.  Select a command category from the **Category** dropdown list.
2.  Select a command from the **Commands** panel.
    -   Optionally click the {{Value|Command}}, {{Value|Shortcut}} or {{Value|Default}} column headings to reorder the list.
    -   Optionally drag the splitter to the right of the panel to resize it.
3.  The **Current shortcut** box displays the current short cut, if available.
4.  Enter a new shortcut in the **New shortcut** input box. Shortcuts can be up to 4 inputs long. Each input is either a single character, a combination of one or more special keys or a combination of one or more special keys and a character. Use **Backspace** to correct mistakes.
5.  Other active commands (see [Notes](#Notes.md)) that already use the shortcut will be listed in the **Shortcut priority list**.
6.  Press the **Assign** button to assign the new shortcut.
7.  If the **Shortcut priority list** contains more than one command: optionally change its order by selecting individual commands and pressing the **Up** button or the **Down** button. If active commands share the same shortcut, the shortcut will trigger the one that is highest in the list.

#### Remove a shortcut 

1.  Select a command category from the **Category** dropdown list.
2.  Select a command from the **Commands** panel.
3.  Press the **Clear** button.

#### Restore a default shortcut 

1.  Select a command category from the **Category** dropdown list.
2.  Select a command from the **Commands** panel.
3.  Press the **Reset** button.

#### Restore all default shortcuts 

1.  Pulse el botón **Reiniciar todo**.

#### Notes

-   Shortcuts only work for active commands. Active commands are commands that appear in the standard menu, or in the menu of the active workbench, or commands that appear in a *visible* toolbar.


{{Top}}



### Barras Herramientas 

![](images/Std_DlgCustomize_tab_Toolbars.png ) 
*La pestaña Barras Herramientas*

En esta pestaña se pueden crear y modificar barras de herramientas personalizadas.

#### Search 

See [Keyboard](#Search.md).



#### Seleccione el ambiente de trabajo 

1.  In the dropdown list on the right select the workbench whose custom toolbars you want to modify. The {{Value|Global}} option is there for custom toolbars that should be available in all workbenches.



#### Crear una barra herramientas 

1.  Press the **New...** button.
2.  Enter a name in the dialog box that opens.
3.  Press the **OK** button.
4.  The new toolbar will appear in the panel on the right.



#### Renombrar una barra herramientas 

1.  Select a toolbar in the panel on the right.
2.  Press the **Rename...** button.
3.  Enter a new name in the dialog box that opens.
4.  Press the **OK** button.



#### Eliminar una barra herramientas 

1.  Select a toolbar in the panel on the right.
2.  Press the **Delete** button.



#### Desactivar una barra herramientas 

1.  Uncheck the checkbox in front of the toolbar name in the panel on the right.
2.  A disabled toolbar will be invisible in the FreeCAD interface.



#### Añadir un comando 

1.  At least one custom toolbar is required. See [Create a toolbar](#Create_a_toolbar.md).
2.  Select the correct toolbar in the panel on the right. If no toolbar is selected, the command will be added to the first toolbar in the list.
3.  Select a command category from the **Category** dropdown list. Macro commands that have been set up on the [Macros](#Macros.md) tab appear in the {{Value|Macros}} category.
4.  Select a command from the **Commands** panel, or select {{Value|<Separator>}} to add a separator (a line between two toolbar buttons).
    -   Optionally drag the splitter to the right of the panel to resize it.
5.  Press **<img src="images/Button_right.svg" width=16px>** button.



#### Elimina un comando 

1.  If required, expand the toolbar in the panel on the right.
2.  Select a command.
3.  Press **<img src="images/Button_left.svg" width=16px>** button.



#### Cambiar la posición de un position comando 

1.  If required, expand the toolbar in the panel on the right.
2.  Select a command.
3.  Press the **<img src="images/Button_up.svg" width=16px>** button or the **<img src="images/Button_down.svg" width=16px>** button.
4.  Optionally repeat this until the command is in the correct position.

#### Notes 

-   Toolbars belonging to the current workbench are updated immediately, but after disabling/re-enabling a toolbar a workbench change is required (switch to a different workbench and then switch back).
-   To update global toolbars a workbench change (if commands have been added or removed) or a restart (if the order of a toolbar has changed or a toolbar was renamed) is required.


{{Top}}

### Macros

![](images/Std_DlgCustomize_tab_Macros.png ) 
*La pestaña Macros*

On this tab macro commands can be set up. Once set up, they can be added to custom toolbars. Macros installed with the <img alt="" src=images/Std_AddonMgr.svg  style="width:16px;"> [Addon Manager](Std_AddonMgr.md) are set up automatically, and added to a {{Value|Global}} toolbar (see [Toolbars](#Toolbars.md)), if you confirm the **Add button** popup during the installation process.

If you want to use a macro downloaded from a different source you will have to install it manually. See [How to install macros](How_to_install_macros.md) for more information. Note that FreeCAD uses a dedicated folder for macros and only macros in that folder can be set up. Use the <img alt="" src=images/Std_DlgMacroExecute.svg  style="width:16px;"> [Std DlgMacroExecute](Std_DlgMacroExecute.md) command to find this folder on your system.



#### Añadir un macrocomando 

1.  In the **Macro** dropdown list select a macro.
2.  Enter a **Menu text**. This will be the name used to identify the macro command and will also appear in the toolbar if there is no icon.
3.  Optionally enter a **Tool tip**. This text will appear near the location of the mouse when you hover the toolbar icon.
4.  Optionally enter a **Status text**. This text will appear in the [status bar](Status_bar.md) when you hover the toolbar icon.
5.  Optionally enter the wiki page for the macro, if available, in the **What\'s this** input box. Enter the page name, not the full URL.
6.  Optionally enter a shortcut in the **Accelerator** input box. See [Keyboard](#Keyboard.md) for more information.
7.  To add an icon:
    1.  Press the **Pixmap** **...** button.
    2.  The **Choose Icon** dialog box opens.
    3.  If required press the **Icon folders...** button to add an icon folder.
    4.  Select an icon from the panel. The **Choose Icon** dialog box closes automatically.
8.  Press the **Add** button.
9.  The macro command appears in the panel on the left.
10. The macro command can now be selected on the [Toolbars](#Toolbars.md) tab.



#### Elimina un macrocomando 

1.  Select the macro command in the panel on the left.
2.  Press the **Remove** button.



#### Cambiar un macrocomando 

1.  Double-click the macro command in the panel on the left.
2.  Make the required changes. Note that you cannot remove the icon, you can only replace it.
3.  Press the **Replace** button.


{{Top}}



### Movimiento Bola Espacial 

This tab is blank if no Spaceball is detected. See: [3Dconnexion input devices](3Dconnexion_input_devices.md). 

### Botones Bola Espacial 

This tab is blank if no Spaceball is detected. See: [3Dconnexion input devices](3Dconnexion_input_devices.md). 

## Temas

FreeCAD supports complete theming of the interface, via .qss stylesheets. The [qss format](https://doc.qt.io/qt-5/stylesheet-syntax.html) is very similar to the [css format](https://en.wikipedia.org/wiki/CSS) used in web pages, it basically adds methods to reference the different widgets and elements of the Qt interface. You can change the default theme (which simply takes the style defined by your desktop system) by selecting a **style sheet** in the [FreeCAD preferences](Preferences_Editor#General.md).

You can also create your own theme if you are not satisfied with the themes that are bundled with FreeCAD, for example by editing an [existing style sheet](https://github.com/FreeCAD/FreeCAD/tree/master/src/Gui/Stylesheets). Your new style must be placed in a specific folder for it to be found by FreeCAD:

-    **%APPDATA%/FreeCAD/Gui/Stylesheets**(on Windows). The **%APPDATA%** folder can be retrieved by entering {{Incode|App.getUserAppDataDir()}} in the [Python console](Python_console.md).

-    **$HOME/.FreeCAD/Gui/Stylesheets**(on Linux).

-    **$HOME/Library/Application Support/FreeCAD/Gui/Stylesheets**(on macOS).


{{Top}}



## Complementos


<div class="mw-translate-fuzzy">

Los complementos ofrecen otra forma de personalizar la interfaz de uso. A continuación se muestran algunos complementos creados por usuarios de la comunidad de FreeCAD. Pueden descargarse a través del <img alt="" src=images/Std_AddonMgr.svg  style="width:16px;"> [Gestor Complementos](Std_AddonMgr/es.md) (nota: están listados en la pestaña ambientes de trabajo).


</div>


{{Top}}





{{Std Base navi

}} {{Interface navi}}



---
⏵ [documentation index](../README.md) > Interface Customization/es
