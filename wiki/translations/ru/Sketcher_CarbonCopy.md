---
 GuiCommand:
   Name: Sketcher CarbonCopy
   Name/ru: Структурная Копия
   MenuLocation: Эскиз , Геометрия эскиза , Структурная Копия
   Workbenches: Sketcher_Workbench/ru
   Version: 0.17
---

# Sketcher CarbonCopy/ru


</div>



## Описание


<div class="mw-translate-fuzzy">

Инструмент **[<img src=images/Sketcher_CarbonCopy.svg style="width:16px"> [Структурная Копия](Sketcher_CarbonCopy/ru.md)** копирует всю геометрию и ограничения из другого эскиза в активный эскиз.


</div>


<div class="mw-translate-fuzzy">

Размерные ограничения, которые существовали до применении функции копирования останутся связанными с размерными ограничениями исходного эскиза через [выражения](expressions/ru.md).


</div>



## Применение


<div class="mw-translate-fuzzy">

1.  Убедитесь, что Вы в режиме редактирования текущего **[<img src=images/Sketcher_NewSketch.svg style="width:16px"> [Эскиза](Sketcher_NewSketch/ru.md)**. Этот эскиз будет целью операции.
2.  Нажмите кнопку **[<img src=images/Sketcher_CarbonCopy.svg style="width:16px"> [Структурная Копия](Sketcher_CarbonCopy/ru.md)**.
3.  Нажмите на ребро другого эскиза. Этот эскиз будет источником операции.
4.  Элементы геометрии, а также ограничения cкопируются в активный эскиз.
5.  Нажатие **ESC** или правой кнопки мыши заканчивает операцию.


</div>



## Примечания


<div class="mw-translate-fuzzy">

Примечания:

-   Когда эскизы используются в <img alt="" src=images/Workbench_PartDesign.svg  style="width:24px;"> [верстаке PartDesign](PartDesign_Workbench/ru.md), обычно эскиз для точной копии должен находиться в той же **[<img src=images/PartDesign_Body.svg style="width:16px"> [теле PartDesign](PartDesign_Body/ru.md)** в качестве текущего активного эскиза. Если копируемый эскиз отсутствует в активном [теле](PartDesign_Body/ru.md), указатель мыши не даст выбирать. В этом случае удерживайте **Ctrl**, чтобы разрешить выбор эскизов из других тел.
-   Обычно выбираемый эскиз должен находиться в плоскости, параллельной текущему активному эскизу. Если эскиз, который нужно скопировать, не параллелен текущему активному эскизу, удерживайте **Ctrl** + **Alt**, чтобы разрешить выбор непараллельных эскизов. Затем объект будет настроен на плоскость активного эскиза. Обратите внимание: на момент написания этой статьи необходимо сохранить и перезагрузить документ, чтобы сделать его видимым. Это также работает для эскизов, находящихся за пределами текущего активного [Body](PartDesign_Body/ru.md).


</div>


<div class="mw-translate-fuzzy">





</div>



---
⏵ [documentation index](../README.md) > [Sketcher](Sketcher_Workbench.md) > Sketcher CarbonCopy/ru
