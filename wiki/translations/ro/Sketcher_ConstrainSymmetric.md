---
 GuiCommand:
   Name: Sketcher ConstrainSymmetric
   Workbenches: Sketcher Workbench
   MenuLocation: Sketch , Sketcher constraints , Constrain symmetrical
   Shortcut: S
   SeeAlso: Sketcher ConstrainParallel
---

# Sketcher ConstrainSymmetric/ro


</div>

## Description


<div class="mw-translate-fuzzy">

## Descriere

Constrângerea de simetrie obligă două puncte selectate pentru a deveni simetrice cu o anumită linie de simetrie, adică două puncte selectate sunt constrânse să stea pe o linie normală care trece prin cele două puncte și sunt constrânse să fie echidistan0te față de linia de simetrie. Alternativ, poate forța două puncte să fie simetrice față de al treilea.


</div>




<div class="mw-translate-fuzzy">

## Utilizare

<img alt="" src=images/SymmetricConstraint1.png  style="width:256px;">
Selectați două puncte (vârfuri) din schiță și o linie din schiță. Punctele selectate și linia vor fi verde închis.
<img alt="" src=images/SymmetricConstraint2.png  style="width:256px;">
Click pe iconița SymmetricalConstraint <img alt="" src=images/Constraint_Symmetric.png  style="width:16px;"> în bara de instrumente Sketcher sau selectați elementul de meniu Constrain Symmetrical din submeniul Sketcher Costraint din elementul de meniu Sketcher (sau Part Design). Aceasta va aplica constrângerea elementelor selectate.
<img alt="" src=images/SymmetricConstraint3.png  style="width:256px;">
Aceasta este o constrângere geometrică și nu are parametri editabili.


</div>

See also: [Drawing aids](Sketcher_Workbench#Drawing_aids.md).

### [Continue mode](Sketcher_Workbench#Continue_modes.md) 

1.  Make sure there is no selection.
2.  There are several ways to invoke the tool:
    -   Press the **<img src="images/Sketcher_ConstrainSymmetric.svg" width=16px> [Constrain symmetric](Sketcher_ConstrainSymmetric.md)** button.

    -   Select the **Sketch → Sketcher constraints → <img src="images/Sketcher_ConstrainSymmetric.svg" width=16px> Constrain symmetric** option from the menu.

    -   
        <small>(v1.0)</small> 
        
        : Right-click in the [3D view](3D_view.md) and select the **Constrain → <img src="images/Sketcher_ConstrainSymmetric.svg" width=16px> Constrain symmetric** option from the context menu.

    -   Use the keyboard shortcut: **S**.
3.  The cursor changes to a cross with the tool icon.
4.  Do one of the following:
    -   Select two points and a symmetry point (in that order).
    -   Select two points and a symmetry line (idem).
    -   Select a point, a symmetry line and another point (idem).
    -   Select a line and a symmetry point (idem).
5.  A constraint is added.
6.  Optionally keep creating constraints.
7.  To finish, right-click or press **Esc**, or start another geometry or constraint creation tool.

### Run-once mode 

1.  Do one of the following:
    -   Select two points and a symmetry point (in that order).
    -   Select two points and a symmetry line (in any order).
    -   Select a line and a symmetry point (idem).
2.  Invoke the tool as explained above, or with the following additional option:
    -   
        <small>(v1.0)</small> 
        
        : Right-click in the [3D view](3D_view.md) and select the **<img src="images/Sketcher_ConstrainSymmetric.svg" width=16px> Constrain symmetric** option from the context menu.
3.  A constraint is added.

## Notes

-   The arrows of this constraint show the color of the dimensional constraints.

## Scripting

Two points and a symmetry line:


```pythonSketch.addConstraint(Sketcher.Constraint('Symmetric', Line1, PointOfLine1, Line2, PointOfLine2, SymmetryLine))```

Two points and a symmetry point:


```pythonSketch.addConstraint(Sketcher.Constraint('Symmetric', Line1, PointOfLine1, Line2, PointOfLine2, LineS, PointOfLineS))```

A line and a symmetry point (In the GUI one can select a line and a point, but it uses internally the same form as above, with the two extremities of the same line):


```pythonSketch.addConstraint(Sketcher.Constraint('Symmetric', Line, 1, Line, 2, LineS, PointOfLineS))```

The [Sketcher scripting](Sketcher_scripting.md) page explains the values which can be used for `Line1`, `Line2`, `LineS`, `Line`, `PointOfLine1`, `PointOfLine2` and `PointOfLineS`, and contains further examples on how to create constraints from Python scripts.



---
⏵ [documentation index](../README.md) > [Sketcher](Sketcher_Workbench.md) > Sketcher ConstrainSymmetric/ro
