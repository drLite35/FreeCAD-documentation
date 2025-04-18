---
 GuiCommand:
   Name: FEM SolverCalculixCxxtools
   Name/it: FEM SolverCalculixCxxtools
   MenuLocation: Solve , Solutore CalculiX Standard
   Workbenches: FEM_Workbench/it
   Shortcut: 
   SeeAlso: FEM_tutorial/it
---

# FEM SolverCalculixCxxtools/it


</div>



## Descrizione


<div class="mw-translate-fuzzy">

CalculiXccxTools abilita l\'uso del solutore [Calculix](https://en.wikipedia.org/wiki/Calculix). Può essere usato per

1.  impostare i parametri dell\'analisi
2.  selezionare la directory di lavoro
3.  eseguire il risolutore CalculiX.


</div>



## Utilizzo


<div class="mw-translate-fuzzy">

1.  L\'oggetto <img alt="" src=images/FEM_Solver.png  style="width:24px;"> CalculiXccxTools viene creato automaticamente con la creazione di un 
**<img src="images/FEM_Analysis.png" width=24px> [Contenitore di analisi](FEM_Analysis/it.md)**. Altrimenti usare **Solve** → **Solver CalculiX Standard** , o premere i tasti **S** e poi **X**
2.  Facoltativamente, impostare le proprietà dati degli oggetti **<img src="images/FEM_Solver.png" width=24px> CalculiXccxTools
**
3.  Fare doppio clic sull\'oggetto **<img src="images/FEM_Solver.png" width=24px> CalculiXccxTools
**
4.  Selezionare il tipo di analisi
5.  Cliccare **Write .inp file**
6.  Cliccare **Run CalculiX**


</div>



## Opzioni


<div class="mw-translate-fuzzy">

Usando **Edit .inp file** è possibile visualizzare e modificare manualmente il file di input CalculiX prima di eseguire l\'analisi. In questo caso può essere utile usare il parametro \"Split Input Writer = true\".


</div>



## Proprietà


<div class="mw-translate-fuzzy">

I valori predefiniti possono essere impostati nel menu **Modifica** → **Preferenze** → **FEM** → **CalculiX**


</div>


<div class="mw-translate-fuzzy">

-    **Analysis Type**:

    -   statico
    -   frequenza
    -   thermomech - per carichi meccanici e termici


</div>

-    **Beam Reduced Integration**\- <small>(v1.0)</small> :

    -   true - uses beam elements with reduced integration (B31R or B32R), required when pipe beam section is used, can also make it possible to obtain [accurate results with plasticity](https://forum.freecad.org/viewtopic.php?t=61233)
    -   false - uses regular (fully-integrated) beam elements


<div class="mw-translate-fuzzy">

-    **Beam Shell Result Output 3D**: si noti che CalculiX espande internamente elementi 1D e 2D in elementi 3D per eseguire l\'analisi FE

    -   falso - i risultati degli elementi 1D e 2D verranno calcolati in base alla media dei nodi della mesh 1D o 2D originale (ad esempio, il raggio puramente piegato mostrerà 0 sforzi nodali dovuti alla media)
    -   true - la mesh risultante conterrà elementi 1D e 2D espansi in elementi 3D


</div>

-    **Buckling Accuracy**\- <small>(v1.1)</small> : defines the accuracy of buckling eigenvalue evaluation. In most cases it can be left with the default value (0.01) but sometimes it might be necessary to lower it (e.g. to 0.0001) to capture the first eigenvalue.

-    **Eigenmode High Limit**: Gli autovalori superiori a questo limite non verranno calcolati. **Nota**: se gli autovalori del modello sono sopra al limite superiore, CalculiX terminerà senza output.

-    **Eigenmode Low Limit**: Gli autovalori al di sotto di questo limite non verranno calcolati

-    **Eigenmodes Count**: numero di eigenmodes più bassi da calcolare


<div class="mw-translate-fuzzy">

-    **Geometric Nonlinearity**:

    -   lineare - l\'analisi lineare verrà eseguita se il modello non contiene materiale non lineare
    -   non lineare - verrà eseguita l\'analisi non lineare


</div>


<div class="mw-translate-fuzzy">

-    **Iterations Control parameter Cutb**:definisce la seconda riga dei parametri di iterazione avanzati in \* scheda CONTROLS, utilizzata quando \"Iterations Control Parameter Time Use\" è true


</div>


<div class="mw-translate-fuzzy">

-    **Iterations Control Parameter Iter**: definisce la prima riga dei parametri di iterazione avanzati sotto \* scheda CONTROLS, utilizzata quando \"Iterations Control Parameter Time Use\" è true


</div>


<div class="mw-translate-fuzzy">

-    **Iterations Control Parameter Time Use**-   true - attiva \"Iterations Control Parameter Cutb\" e \"Iterations Control Parameter Iter\"


</div>


<div class="mw-translate-fuzzy">

-    **Iterations Thermo Mech Maximum**:numero massimo di incrementi nell\'analisi termomeccanica dopo la quale il lavoro sarà interrotto.


</div>

-    **Iterations User Defined Incrementations**:

    -   true - il controllo di incremento automatico verrà disattivato tramite il parametro DIRECT
    -   falso - il controllo di incremento sarà automatico


<div class="mw-translate-fuzzy">

-    **Iterations User Defined Time Step Length**:

    -   true - attiva i parametri \"Time End\" e \"Time Initial Step\"


</div>


<div class="mw-translate-fuzzy">

-    **Material Nonlinearity**:

    -   lineare: solo le proprietà del materiale lineare saranno incluse nell\'analisi
    -   non lineare - le proprietà del materiale non lineare verranno utilizzate dall\'oggetto **<img src="images/FEM_MaterialMechanicalNonlinear.png" width=24px> '''[Nonlinear mechanical material](FEM_MaterialMechanicalNonlinear.md)'''
**


</div>


<div class="mw-translate-fuzzy">

-    **Matrix Solver Type**: tipo del risolutore per risolvere il sistema di equazioni all\'interno dell\'analisi FE. Può influenzare in modo significativo la velocità di calcolo e le richieste di memoria. L\'idoneità dipende dal modello FE e dall\'hardware disponibile

    -   predefinito: seleziona automaticamente il risolutore di matrici in base ai risolutori disponibili (probabilmente sarà Spool)
    -   spooles - risolutore diretto con supporto di più CPU. È necessario impostare il numero di CPU **Edit** → **Preferences** → **FEM** → **CalculiX** → Solver defaults → Number of CPU\'s to use)
    -   iterativescaling - risolutore iterativo con meno richieste di memoria, adatto se il modello contiene principalmente elementi 3D
    -   iterativecholesky - risolutore iterativo con precondizionamento con e con esigenze di memoria ridotta, adatto se il modello contiene principalmente elementi 3D


</div>

-    **Model Space**\- <small>(v1.0)</small> : switches between 3D and 2D analyses, the latter require surface geometry on the XY plane (on the right of the Y axis in the axisymmetric case) with [thickness definition](FEM_ElementGeometry2D.md) (value ignored in the axisymmetric case) and proper boundary conditions ([displacement boundary condition](FEM_ConstraintDisplacement.md) with degrees of freedom X and Y has to be used instead of [fixed boundary condition](FEM_ConstraintFixed.md)) and in-plane loads applied to edges

    -   3D - three-dimensional solid/shell/beam elements are used
    -   plane stress - plane stress 2D solid elements are used
    -   plane strain - plane strain 2D solid elements are used
    -   axisymmetric - axisymmetric 2D solid elements are used

-    **Output Frequency**\- <small>(v1.0)</small> : defines the frequency of results writing in increments (the default setting of 1 means that the results are written every increment, setting 2 would save the results every 2 increments and so on), particularly useful for nonlinear and transient simulations, helps reduce the clutter in the tree since currently a pair of results objects (CCX_Results and Pipeline_CCX_Results) is created for each results frame

-    **Split Input Writer**:

    -   false - scrive l\'intero input in un file \* .inp da utilizzare con il risolutore CalculiX
    -   true - split solver input in più \* file .inp, che possono chiarire la modifica della mano


<div class="mw-translate-fuzzy">

-    **Thermo Mechanical Steady State**:

    -   vero - analisi termo meccanica allo steady state
    -   falso - analisi termo meccanica temporanea


</div>

-    **Thermo Mech Type**\- <small>(v1.0)</small> :

    -   coupled - coupled thermo-mechanical analysis
    -   uncoupled - uncoupled thermo-mechanical analysis
    -   pure heat transfer - purely thermal analysis (*\*HEAT TRANSFER*)


<div class="mw-translate-fuzzy">

-    **Time End**: periodo di tempo del passo, utilizzato quando il parametro \"Iterazioni User Defined Incrementations\" o \"Iterations User Defined Time Step Length\" è vero


</div>


<div class="mw-translate-fuzzy">

-    **Time Initial Step**: incremento del tempo iniziale del passo, utilizzato quando il parametro \"Iterazioni User Defined Incrementations\" o \"Iterations User Defined Time Step Length\" è vero


</div>

-    **Time Maximum Step**\- <small>(v1.0)</small> : maximum time increment of the step, used when parameter **Iterations User Defined Incrementations** or **Iterations User Defined Time Step Length** is *true*

-    **Time Minimum Step**\- <small>(v1.0)</small> : minimum time increment of the step, used when parameter **Iterations User Defined Incrementations** or **Iterations User Defined Time Step Length** is *true*

-    **Working Dir**:percorso alla directory di lavoro che verrà utilizzata per i file di analisi CalculiX.



## Limitazioni

When running a CalculiX, you might end up with **error 4294977295**. This means you don\'t have enough RAM space. You have then 2 options:

1.  reduce the number of mesh nodes, preferably by omitting geometry that is not absolutely necessary for your analysis
2.  buy more RAM for your PC



## Note

La documentazione originale di CalculiX è disponibile all\'indirizzo <http://dhondt.de/> in the \"ccx\" paragraph.



## Script


<div class="mw-translate-fuzzy">





</div>


{{FEM Tools navi

}}



---
⏵ [documentation index](../README.md) > [FEM](Category_FEM.md) > FEM SolverCalculixCxxtools/it
