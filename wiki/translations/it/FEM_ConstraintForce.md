---
 GuiCommand:
   Name: FEM_ConstraintForce
   Name/it: Vincolo forza
   MenuLocation: Modello , Vincoli meccanici , Vincolo forza
   Workbenches: FEM_Workbench/it
   Shortcut: 
   SeeAlso: FEM_tutorial/it
---

# FEM ConstraintForce/it


</div>



## Descrizione


<div class="mw-translate-fuzzy">

Questo comando applica una forza del valore dato \[N\] alla geometria di destinazione selezionata.


</div>



## Utilizzo


<div class="mw-translate-fuzzy">

1\) Applicare di una forza in direzione normale a una faccia

-   -   In ambiente FEM, cliccare su <img alt="Vincolo forza" src=images/Fem-constraint-force.svg  style="width:24px;"> o selezionare **Modello** → **Vincoli meccanici** → **Forza** per aprire la finestra di dialogo delle Proprietà del Vincolo forza

![](images/FEMForceConstraintProperties.PNG )

-   -   Se c\'è l\'oggetto Mesh visualizzato, bisogna nasconderlo (selezionare l\'oggetto Mesh e premere **spazio** oppure fare clic con il tasto destro e selezionare **Nascondi**) e mostrare il modello originale.
    -   Cliccare sulla faccia *faccia* a cui deve essere applicata una forza. Essa appare nell\'elenco degli oggetti geometrici.
    -   Compilare il campo **Carico** con un valore di forza in \[N\] (attenzione: *Non* di pressione in \[N/m\])

![](images/ApplyingForceToFace.PNG )

-   -   
        **Direzione**
        
        : In un caso tipico, fare clic su questo campo vuoto per applicare una forza in direzione normale alla faccia. È possibile invertire la direzione della forza selezionando **Inverti direzione**. In altri casi, è necessario selezionare una faccia o un piano, che sia normale alla direzione della forza (può essere diversa dalla faccia a cui viene applicata la forza)

    -   Cliccare su **OK** per chiudere il dialogo e creare un oggetto **[<img src=images/FEM_ConstraintForce.png style="width:24px"> Vincolo forza**.


</div>

![](images/FEM_ConstraintForce_example.JPG )

## Notes

-   The defined force is applied uniformly to the selected objects. For example, if you define one force load with 200 N applied to two faces having the same area, each face will be uniformly loaded with 100 N.
-   This feature uses the [\*CLOAD card in CalculiX](https://web.mit.edu/calculix_v2.7/CalculiX/ccx_2.7/doc/ccx/node172.html).


<div class="mw-translate-fuzzy">





</div>


{{FEM Tools navi

}}



---
⏵ [documentation index](../README.md) > [FEM](Category_FEM.md) > FEM ConstraintForce/it
