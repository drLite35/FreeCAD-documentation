# Artwork Guidelines
## Introduction


**Note:**

for all icons in the source tree, see [Artwork](Artwork.md).

A FreeCAD **icon** is composed of 6 elements which can be remembered by the acronym SALCHO: **S**troke, **A**lignment, **L**ighting, **C**olor, **H**ighlighting, **O**utline.

Here\'s a concrete, yet arbitrary example:

 ![](images/FreeCAD_icon_example_details.svg ) 

  --- 
  A   The highlight color is used for this entire surface to indicate light falling from above.
  B   The obligatory dark outline surrounds the icon shape to provide form contrast.
  C   Just inside the outline, the highlight stroke (Highlight color) provides contrast on dark backgrounds.
  D   This face is primarily the base color, but a light gradient from highlight (top left) to base (bottom right) gives the impression of light falling from above left.
  E   The highlight here is the base color (one tone down) to give the impression of this being the face furthest from the light.
  F   This face is like D but goes from Base (top left) to Dark (bottom right), to indicate that this is the face furthest from the light.
  --- 

The following sections explain these elements with more detail.

This icon is displayed as follows:

+++
| <img alt="" src=images/FreeCAD_icon_example.svg  style="width:64px;"> | 64 px, original size, large buttons.                                       |
+++
| <img alt="" src=images/FreeCAD_icon_example.svg  style="width:32px;"> | 32 px, medium size, regular buttons.                                       |
+++
| <img alt="" src=images/FreeCAD_icon_example.svg  style="width:16px;"> | 16 px, small size, as it appears in the [tree view](tree_view.md). |
+++

## Colors


**Obligatory**

FreeCAD uses a palette adapted from the [Tango palette](https://web.archive.org/web/20190921043652/http://tango.freedesktop.org/tango_icon_theme_guidelines). Each main color comes in 4 tones: Highlight, Base, Dark and Outline. Notice that the Outline is not completely black but a very dark variation of the Base.



+++++
| #fce94f         | #edd400         | #c4a000         | #302b00         |
| (252, 233, 79)  | (237, 212, 0)   | (196, 160, 0)   | (48, 43, 0)     |
| Butter 1        | Butter 2        | Butter 3        | Butter 4        |
+=================+=================+=================+=================+
| #8ae234         | #73d216         | #4e9a06         | #172a04         |
| (138, 226, 52)  | (115, 210, 22)  | (78, 154, 6)    | (23, 42, 4)     |
| Chameleon 1     | Chameleon 2     | Chameleon 3     | Chameleon 4     |
+++++
| #fcaf3e         | #f57900         | #ce5c00         | #321900         |
| (252, 175, 62)  | (245, 121, 0)   | (206, 92, 0)    | (50, 25, 0)     |
| Orange 1        | Orange 2        | Orange 3        | Orange 4        |
+++++
| #729fcf         | #3465a4         | #204a87         | #0b1521         |
| (114, 159, 207) | (52, 101, 164)  | (32, 74, 135)   | (11, 21, 33)    |
| Sky Blue 1      | Sky Blue 2      | Sky Blue 3      | Sky Blue 4      |
+++++
| #ad7fa8         | #75507b         | #5c3566         | #171018         |
| (173, 127, 168) | (117, 80, 123)  | (92, 53, 102)   | (23, 16, 24)    |
| Plum 1          | Plum 2          | Plum 3          | Plum 4          |
+++++
| #e9b96e         | #c17d11         | #8f5902         | #271903         |
| (233, 185, 110) | (193, 125, 17)  | (143, 89, 2)    | (39, 25, 3)     |
| Chocolate 1     | Chocolate 2     | Chocolate 3     | Chocolate 4     |
+++++
| #ef2929         | #cc0000         | #a40000         | #280000         |
| (239, 41, 41)   | (204, 0, 0)     | (164, 0, 0)     | (40, 0, 0)      |
| Scarlet Red 1   | Scarlet Red 2   | Scarlet Red 3   | Scarlet Red 4   |
+++++
| #34e0e2         | #16d0d2         | #06989a         | #042a2a         |
| (52, 224, 226)  | (22, 208, 210)  | (6, 152, 154)   | (4, 42, 42)     |
| FreeTeal 1      | FreeTeal 2      | FreeTeal 3      | FreeTeal 4      |
+++++
| #ffffff         | #eeeeec         | #d3d7cf         | #babdb6         |
| (255, 255, 255) | (238, 238, 236) | (211, 215, 207) | (186, 189, 182) |
| Snowy White     | Aluminium 1     | Aluminium 2     | Aluminium 3     |
+++++
| #888a85         | #555753         | #2e3436         | #000000         |
| (136, 138, 133) | (85, 87, 83)    | (46, 52, 54)    | (0, 0, 0)       |
| Aluminium 4     | Aluminium 5     | Aluminium 6     | Jet Black       |
+++++

 
*Complete palette*

A selection of some key colors.

      
                                                                                                                                                          Use the Yellow tones for tools that create objects; for an example, see [Part](Part_Workbench.md) and [Draft Workbenches](Draft_Workbench.md).
  style=\"background-color:#729fcf;\|   style=\"background-color:#3465a4;\|   style=\"background-color:#204a87;\|   style=\"background-color:#0b1521;\|   Use the Blue tones for tools that modify objects; for an example, see [Part](Part_Workbench.md) and [Draft Workbenches](Draft_Workbench.md).
  style=\"background-color:#34e0e2\|    style=\"background-color:#16d0d2\|    style=\"background-color:#06989a\|    style=\"background-color:#042a2a\|    Use the Teal tones for view-related tools; for an example, see the [View Menu](Std_View_Menu.md).
  style=\"background-color:#ef2929\|    style=\"background-color:#cc0000\|    style=\"background-color:#a40000\|    style=\"background-color:#280000\|    Use the Red tones for Constraint related tools; for an example, see [Sketcher Workbench](Sketcher_Workbench.md).
      

   
  style=\"width: 25%;\|Why limit myself to these colors?   Restricting the colors to a defined palette helps avoid heterogeneous iconography and improves readability when there are many icons.
  How do I use the FreeCAD palette?                        Installing [the palette](https://gist.github.com/GAZ082/724d2092b2986e3b17b9663f34093cf5) is as easy as [copying it into your Inkscape palette folder](https://inkscape.org/en/learn/faq/#how-install-new-extensions-palettes-document-templates-symbol-sets-icon-sets-etc).
   

## Grid and stroke width 


**Obligatory**

FreeCAD icons have a nominal size of 64 pixels both in width and height. When creating or editing an icon, make sure the document size is 64 x 64 with the units being pixels (px). Leaving an inner 2px margin of empty space all around the document area is useful as it prevents effects like anti-aliasing (blurring of edges). That is, the usable space for the icon should be considered 60 x 60, and the edges should be left empty.

 <img alt="" src=images/FreeCAD_icon_size.svg  style="width:128px;">  
*Draw the icon inside the blue area and everything will work out fine.*

It\'s also strongly recommended to use a visual grid that has a minor grid line every pixel, and a major grid line every 2 pixels. The strokes of the icon should be aligned along the minor grid intersections.

Strokes should be no *thinner* than 2px, with rounded caps and corners in most cases. Strokes can be *thicker*, but they should preferably be a multiple of 2px in order to minimize scaling fuzziness.

 <img alt="" src=images/FreeCAD_icon_stroke_2px.svg  style="width:320px;">  
*Grid with strokes that are multiples of 2px.*

   
  Why use this grid and stroke size?   For historical reasons, FreeCAD uses a 64x64 icon that then gets scaled down. Not ideal, but it adds character. As a result, keeping things aligned to a power of two grid with thicknesses that are powers of two helps to avoid or at least mitigate anti-aliasing issues upon re-scaling.
  How do I comply with this?           If you are using Inkscape, go to **File → Document Properties** and confirm the width, height and units of your page are correct. Then go to the **Grids** tab, click **New**, set the units to `px`, `Spacing X` and `Spacing Y` to 1 and `Major grid line every` to 2.
   

## Outline


**Obligatory**

Basing yourself on the main color of the icon, ensure that there is a dark outline of 2px, as mentioned earlier. This works in unison with the highlight to ensure good form contrast on multiple background tones.

 <img alt="" src=images/Draft_Point.svg  style="width:" height="128px;"> <img alt="" src=images/Draft_Point_backgrounds.svg  style="width:" height="128px;">  
*The dark edge of the icon is the outline.*

   
  Why is the outline needed?   The outline is the skeleton on which everything else hangs by adding form contrast. Using the Outline color or the Dark color depends on the situation, but without this line, the range of backgrounds on which the icon is visible gets drastically limited
  How do I comply with this?   Simply add a stroke of 2px around every part of the icon that will be adjacent to the background color, that is, the outline is for external strokes. In case of shapes that have a hole in the middle, for example, a donut, the outline should also be added to the interior hole. Snap your path\'s nodes to the grid whenever possible, aiming for the minor grid intersections.
   

## Highlight


**Strongly advised**

Using the Highlight color, add an internal stroke of 2px to help make that outline pop. On dark backgrounds, it\'s this highlight what will be providing the form to the icon.

 <img alt="" src=images/Draft_Move.svg  style="width:" height="128px;"> <img alt="" src=images/Draft_Move_backgrounds.svg  style="width:" height="128px;">  
*The light highlight helps in dark backgrounds.*

   
  Why use the highlight?       The highlight works in unison with the outline to improve form contrast, especially on dark backgrounds. It is never a bad idea, but if you don\'t have the space, for example, you have a very thin line, you can opt out of it provided you have ensured enough contrast between the main color and the outline.
  How do I comply with this?   Just like the outline, simply trace a stroke of 2px around the internal side of the outline, snapping nodes to the grid when possible, aiming for the minor grid intersections.
   

## Lighting


**Optional**

As per Tango guidelines, if you\'re adding a gradient lighting effect, try to make it look like the light is coming from the top left. This is done by adding the highlight color up top left and the Base or Dark color bottom right. Notice that only palette colors are used.

 <img alt="" src=images/Draft_Clone.svg  style="width:" height="128px;"> <img alt="" src=images/Draft_Clone_backgrounds.svg  style="width:" height="128px;">  
*Subtle lighting effect coming from top left.*

   
  style=\"width:25%;\|Why use lighting?   Lighting is just another way to tie icons together and ensure that there are varying levels of [\"value\"](https://en.wikipedia.org/wiki/Lightness) to improve their readability. Provided the outline and highlight are present though, it can be considered optional
  How do I comply with this?              Set the fill to be a linear or a radial gradient. In Inkscape this is available in the stroke and fill settings; with \"F2\" it is possible to move the nodes of the gradient around to make sure they are at the right angle.
   

## Recommended recording format 

All icons should be created in [SVG](SVG.md) format with a vector image application, such as [Inkscape](http://inkscape.org). This makes it easier to apply changes and derive additional icons in the same application space.

When committing icons to be used directly by FreeCAD (in a \*.qrc file), save them as \"Plain SVG\". This will reduce the icon size and save the disk and memory space.

## Closing remarks 

Remember: **SALCHO**, Stroke, Alignment, Lighting, Color, Highlight, Outline

Here are some tips to check your work.

### Checking size 

Inkscape has a handy tool to check your icon at various sizes. Go to **View → Icon Preview...** and it\'ll show you previews of your icon resized to 16, 24, 32 and 64 pixels.

### Checking your outline 

1.  Put your icon on a big rectangle that is the same color as the darkest color in your icon.
2.  Still looks OK? Great. Go to the next step. If not, adjust the highlight.
3.  Do the same but this time using the lightest color.
4.  Still looks OK? Great. Outlines and highlights have been used appropriately. Otherwise, adjust the outline.

 <img alt="" src=images/Draft_Move_backgrounds_outline.svg  style="width:" height="128px;">  
*Testing the icon against the darkest and lightest colors as background*

   
  My icon is barely visible.   You have poor form contrast. Double check the outline and highlight, one of these is probably missing or improperly applied.
   

### Checking your contrast 

1.  Export your icon from SVG to a bitmap format, like `.png` or `.jpg`.
2.  Load your bitmap in an image program, and change it to grayscale. For example, in GIMP you would go to **Image → Mode → Grayscale**.
3.  Inkscape allows you to convert the SVG directly to grayscale using **Extensions → Color → Grayscale**.
4.  Can you still clearly make out any internal details? Great. The contrast is good.

A grayscale image allows you to more easily identify problems in contrast, as only a mix of black and white is present. Testing grayscale images is also good for colorblind users. If they can see the details in a grayscale image, then the contrast of the fully colored image is probably good as well.

 <img alt="" src=images/Draft_Move_contrast_grayscale.svg  style="width:" height="128px;">  
*Testing the icon's contrast in grayscale*

   
  I can\'t make out all the details.   The colors you\'ve chosen have poor value contrast. Try using colors that are further apart in your 4 tone palette, that is, a highlight green beside a highlight yellow will be difficult to see, knock one of those colors down to Base or Dark.



---
⏵ [documentation index](../README.md) > [Artwork](Category_Artwork.md) > [Developer Documentation](Category_Developer%20Documentation.md) > Artwork Guidelines
