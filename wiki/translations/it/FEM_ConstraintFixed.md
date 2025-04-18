---
 GuiCommand:
   Name: FEM_ConstraintFixed
   Name/it: Vincolo fissaggio
   MenuLocation: Modello , Vincoli meccanici , Vincolo fissaggio
   Workbenches: FEM_Workbench/it
   Shortcut: 
   SeeAlso: FEM_tutorial/it
---

# FEM ConstraintFixed/it


</div>



## Descrizione


<div class="mw-translate-fuzzy">

Crea un vincolo di fissaggio FEM per un elemento della geometria, bloccando tutti i 6 gradi di libertà dell\'oggetto selezionato.


</div>



## Utilizzo


<div class="mw-translate-fuzzy">

1.  Cliccare su <img alt="" src=images/FEM_ConstraintFixed.png  style="width:32px;"> o scegliere **Modello** → **Vincoli meccanici** → **<img src="images/FEM_ConstraintFixed.png" width=32px> Vincolo fissaggio** dal menu principale.
2.  Selezionare nella vista 3D l\'oggetto a cui deve essere applicato il vincolo, che può essere
    1.  vertice (angolo)
    2.  bordo
    3.  faccia


</div>



## Limitazioni


<div class="mw-translate-fuzzy">

Non è possibile ceare combinazioni di tipi di oggetti all\'interno dello stesso vincolo. Utilizzare un vincolo di fissaggio per ogni tipo di oggetto.


</div>

## Notes

-   This feature uses the [\*BOUNDARY card in CalculiX](https://web.mit.edu/calculix_v2.7/CalculiX/ccx_2.7/doc/ccx/node163.html).


<div class="mw-translate-fuzzy">





</div>


{{FEM Tools navi

}}



---
⏵ [documentation index](../README.md) > [FEM](Category_FEM.md) > FEM ConstraintFixed/it
