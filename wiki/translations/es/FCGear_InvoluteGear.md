---
 GuiCommand:
   Name: FCGear InvoluteGear
   Name/es: FCGear EngranajeEvolvente
   MenuLocation: Gear , Involute Gear
   Workbenches: FCGear_Workbench
   Shortcut: None
   Version: v0.16
   SeeAlso: FCGear_CycloideGear
---

# FCGear InvoluteGear/es



## Descripción

Debido a la favorable relación de engrane y su fabricación relativamente sencilla, el dentado de espiral es la forma de diente más común en la construcción de máquinas. Las ruedas dentadas se encuentran allí donde se desea transferir movimiento y fuerza de una pieza a otra. Se pueden encontrar, por ejemplo, en máquinas, coches, relojes o electrodomésticos. A menudo, el movimiento se transmite directamente de una rueda dentada a otra, pero a veces también a través de una cadena. Además, se puede cambiar el sentido de giro. También es posible cambiar un movimiento radial a uno lineal mediante un [cremallera involuta](FCGear_InvoluteRack/es.md).

![](images/Involute-Gear_example.png ) 
*De izquierda a derecha: engranaje recto, engranaje helicoidal, engranaje helicoidal doble*



## Uso

1.  Cambie a <img alt="" src=images/FCGear_workbench_icon.svg  style="width:16px;"> [entorno de trabajo FCGear](FCGear_Workbench/es.md).
2.  Hay varias formas de invocar el comando:
    -   Presione el botón **[<img src=images/FCGear_InvoluteGear.svg style="width:16px"> [engranaje evolvente](FCGear_InvoluteGear/es.md)** en la barra de herramientas.
    -   Seleccione la opción **Gear → [<img src=images/FCGear_InvoluteGear.svg style="width:16px"> Engranaje evolvente** del menú.
3.  Cambie el parámetro de engranaje a las condiciones requeridas (ver [Propiedades](#Properties.md)).



## Propiedades

Un objeto FCGear InvoluteGear se deriva de un objeto [Part Feature](Part_Feature/es.md) y hereda todas sus propiedades. También tiene las siguientes propiedades adicionales:



### Datos


{{Properties_Title|accuracy}}

-    **numpoints|Integer**: Default is {{Value|20}}. Change of the involute profile. Changing the value can lead to unexpected results.

-    **simple|Bool**: Default is {{False}}, {{True}} generates a simplified display (without teeth and only a cylinder in pitch diameter).


{{Properties_Title|base}}

-    **height|Length**: Default is {{Value|5 mm}}. Value of the gear width.

-    **module|Length**: Default is {{Value|1 mm}}. Module is the ratio of the reference diameter of the gear divided by the number of teeth (see [Notes](#Notes.md)).

-    **num_teeth|Integer**: Default is {{Value|15}}. Number of teeth (see [Notes](#Notes.md)).


{{Properties_Title|computed}}

-    **addendum_diameter|Length**: Default is {{Value|17 mm}}. Outside diameter, measured at the addendum (the tip of the teeth).

-    **angular_backlash|Angle**: (read-only) The angle by which this gear can turn without moving the mating gear.

-    **pitch_diameter|Length**: Default is {{Value|15 mm}}. The pitch diameter.

-    **root_diameter|Length**: (read-only) The root diameter, measured at the foot of the teeth.

-    **transverse_pitch|Length**: Default is {{Value|3.14 mm}}. The transverse pitch.

-    **traverse_module|Length**: Default is {{Value|1 mm}}. The traverse module of the generated gear.


{{Properties_Title|fillets}}

-    **head_fillet|Float**: Default is {{Value|0 mm}}. A fillet for the tooth-head.

-    **root_fillet|Float**: Default is {{Value|0 mm}}. A fillet for the tooth-root.

-    **undercut|Bool**: Default is {{False}}, {{True}} changes the profile of the tooth root (see [Notes](#Notes.md)).


{{Properties_Title|helical}}

-    **double_helix|Bool**: Default is {{False}}, {{True}} creates a double helix gear (see [Notes](#Notes.md)).

-    **helix_angle|Angle**: Default is {{Value|0 °}}. With the helix angle β a helical gear is created -- positive value → rotation direction right, negative value → rotation direction left (see [Notes](#Notes.md)).

-    **properties_from_tool|Bool**: Default is {{False}}. If {{True}} and **helix_angle** is not zero, gear parameters are recomputed internally for the rotated gear.


{{Properties_Title|hole}}

-    **Axle_hole|Bool**: Default is {{False}}. {{True}} enables a central hole for an axle.

-    **Axle_holesize|Length**: Default is {{Value|10 mm}}. Diameter of the hole for an axle.

-    **offset_hole|Bool**: Default is {{False}}, {{True}} enables an offset hole.

-    **offset_holeoffset|Length**: Default is {{Value|10 mm}}. The offset of the offset hole.

-    **offset_holesize|Length**: Default is {{Value|10 mm}}. The diameter of the offset hole.


{{Properties_Title|involute}}

-    **pressure_angle|Angle**: Default is {{Value|20 °}} (see [Notes](#Notes.md)).

-    **shift|Float**: Default is {{Value|0}}. Generates a positive and negative profile shift (see [Notes](#Notes.md)).


{{Properties_Title|tolerance}}

-    **backlash|Length**: Default is {{Value|0}}. Backlash, also called lash or play, is the distance between the teeth at a gear pair.

-    **clearance|Float**: Default is {{Value|0.25}} (see [Notes](#Notes.md)).

-    **head|Float**: Default is {{Value|0}}. This value is used to change the tooth height.

-    **reversed_backlash|Bool**: {{True}} backlash decrease or {{False}} (default) backlash increase see [Notes](#Notes.md)).


{{Properties_Title|version}}

-    **version|String**:



## Notas

-    **beta**: When **beta** is changed, **pitch diameter** also changes. The following formula illustrates how the parameters interact: d = m \* Z / cos beta (Z = number of teeth, d = pitch diameter, m = module). This means for the spur gear: cos beta = 0 and for the helical gear: cos beta \> 0. However, a helix angle of less than 10° has hardly any advantages over straight teeth.

-    **clearance**: At a gear pair, clearance is the distance between the tooth tip of the first gear and the tooth root of the second gear.

-    **double_gear**: To use the double helical gearing the helix angle β (**beta**) for the helical gearing must first be entered.

-    **module**: Using ISO (International Organization for Standardization) guidelines, Module size is designated as the unit representing gear tooth-sizes. Module (m): m = 1 (p = 3.1416), m = 2 (p = 6.2832), m = 4 (p = 12.566). If you multiply Module by Pi, you can obtain Pitch (p). Pitch is the distance between corresponding points on adjacent teeth.

-    **shift**: Profile shift is not merely used to prevent undercut. It can be used to adjust center distance between two gears. If a positive correction is applied, such as to prevent undercut in a pinion, the tooth thickness at top is thinner.

-    **teeth**: If the number of teeth is changed, the pitch diameter also changes (**dw**).

-    **undercut**: Undercut is used when the number of teeth of a gear is too small. Otherwise the mating gear will cut into the tooth root. The undercut not only weakens the tooth with a wasp-like waist, but also removes some of the useful involute adjacent to the base circle.

-    **pressure_angle**: 20° is a standard value here. The pressure angle is defined as the angle between the line-of-action (common tangent to the base circles) and a perpendicular to the line-of-centers. Thus, for standard gears, 14.5° pressure angle gears have base circles much nearer to the roots of teeth than 20° gears. It is for this reason that 14.5° gears encounter greater undercutting problems than 20° gears. Important. the pressure angle changes with a profile shift. Only change the parameter, if sufficient knowledge of the gear geometry is available.

-    **reversed_backlash**: If there are several gears, pay attention to which gear the parameter is set for.



## Limitaciones

A 2D tooth profile, obtained by setting the **height** to zero, cannot be used with features requiring a 2D shape. For example [PartDesign Pad](PartDesign_Pad.md) and [PartDesign AdditiveHelix](PartDesign_AdditiveHelix.md) features do not accept such a profile as base. For technical details, please refer to the related [issue on GitHub](https://github.com/looooo/freecad.gears/issues/97).



## Fórmulas útiles 

### Standard Spur Gears 

Aquí \"standard\" se refiere a aquellos engranajes rectos sin coeficiente de cambio de perfil ($x$).

+++++
| Symbol   | Term                                     | Formula                        | FCGear Parameter                        |
+==========+==========================================+================================+=========================================+
| $m$      | *Module*                                 | \-                             | $\texttt{module}$                       |
+++++
| $z$      | *Number of Teeth*                        | \-                             | $\texttt{teeth}$                        |
+++++
| $\alpha$ | *Pressure Angle*                         | Typically, $\alpha = 20^\circ$ | $\texttt{pressure} {\_} \texttt{angle}$ |
+++++
| $d$      | *Reference Diameter* or *Pitch Diameter* | $z \cdot m$                    | $\texttt{dw}$                           |
+++++
| $h^*_a$  | *Addendum Coefficient*                   | Typically, $h^*_a = 1$         | $h^*_a = 1 + \texttt{ head}$            |
+++++
| $h^*_f$  | *Dedendum Coefficient*                   | Typically, $h^*_f = 1.25$      | $h^*_f = 1 + \texttt{ clearance}$       |
+++++
| $h_a$    | *Addendum*                               | $h_a = h^*_a \cdot m$          | \-                                      |
+++++
| $h_f$    | *Dedendum*                               | $h_f = h^*_f \cdot m$          | \-                                      |
+++++
| $h$      | *Tooth Height* or *Tooth Depth*          | $h = h_a + h_f$                | \-                                      |
|          |                                          | Typically, $h = 2.25 \cdot m$  |                                         |
+++++
| $x$      | *Profile Shift Coefficient*              | For standard gears, $x = 0$    | $\texttt{shift}$                        |
+++++

: style=\"text-align: left;\" \| Basic formulas common to internal and external standard spur gears

++++
| Symbol | Term            | Formula                              |
+========+=================+======================================+
| $d_a$  | *Tip Diameter*  | $d_a = d + 2 \cdot h_a$              |
|        |                 | Typically, $d_a = (z + 2) \cdot m$   |
++++
| $d_f$  | *Root Diameter* | $d_f = d - 2 \cdot h_f$              |
|        |                 | Typically, $d_f = (z - 2.5) \cdot m$ |
++++

: style=\"text-align: left;\" \| Basic formulas specific to external standard spur gears

++++
| Symbol | Term            | Formula                              |
+========+=================+======================================+
| $d_a$  | *Tip Diameter*  | $d_a = d - 2 \cdot h_a$              |
|        |                 | Typically, $d_a = (z - 2) \cdot m$   |
++++
| $d_f$  | *Root Diameter* | $d_f = d + 2 \cdot h_f$              |
|        |                 | Typically, $d_f = (z + 2.5) \cdot m$ |
++++

: style=\"text-align: left;\" \| Basic formulas specific to internal standard spur gears

++++
| Symbol | Term                     | Formula                       |
+========+==========================+===============================+
| $a$    | *Center Distance*        | $a = \frac{d_1 + d_2}{2}$     |
++++
| $c$    | *Tip and Root Clearance* | $c_1 = h_{f2} - h_{a1}$       |
|        |                          | $c_2 = h_{f1} - h_{a2}$       |
|        |                          | Typically, $c = 0.25 \cdot m$ |
++++

: style=\"text-align: left;\" \| Basic formulas specific for a pair of external standard spur gears

-   **Helical and double helical gearing**
    -   
        **pitch diameter (dw)**
        
        = **module** \* **teeth** : **cos beta**

    -   
        **axle base**
        
        = **(pitch diameter (dw) 1 + pitch diameter (dw) 2)** : 2

    -   
        **addendum diameter**
        
        = **pitch diameter (dw)** + 2 \* **module**

    -   
        **module**
        
        = **pitch diameter (dw)** \* **cos beta** : **teeth**



## Programación

Utilice el poder de Python para automatizar el modelado de sus engranajes: 
```python
import FreeCAD as App
import freecad.gears.commands
gear = freecad.gears.commands.CreateInvoluteGear.create()
gear.teeth = 20
gear.beta = 20
gear.height = 10
gear.double_helix = True
App.ActiveDocument.recompute()
Gui.SendMsgToActiveView("ViewFit")
```



---
⏵ [documentation index](../README.md) > [Addons](Category_Addons.md) > [FCGear](Category_FCGear.md) > [External Command Reference](Category_External%20Command%20Reference.md) > FCGear InvoluteGear/es
