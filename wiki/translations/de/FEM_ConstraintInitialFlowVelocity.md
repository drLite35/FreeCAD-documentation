---
 GuiCommand:Container|
{{GuiCommand/de
   Name: FEM ConstraintInitialFlowVelocity
   Name/de: FEM StartbedingungStrömungsgeschwindigkeit
   MenuLocation: Model , Fluid-Randbedingungen , Startbedingung Strömungsgeschwindigkeit
   Workbenches: FEM_Workbench/de
   SeeAlso: FEM_ConstraintFlowVelocity/de, FEM_ConstraintInitialPressure/de
}}
{{GuiCommandFemInfo/de
   Solvers: Elmer
}}
---

# FEM ConstraintInitialFlowVelocity/de



## Beschreibung

Erstellt eine Startbedingung einer Strömungsgeschwindigkeit für die Strömungsanalyse eines Fluids.



## Anwendung

1.  Die Schaltfläche **<img src="images/FEM_ConstraintInitialFlowVelocity.svg" width=16px> [Startbedingung Strömungsgeschwindigkeit](FEM_ConstraintInitialFlowVelocity/de.md)** drücken oder den Menüeintrag **Modell → Fluid-Randbedingungen → <img src="images/FEM_ConstraintInitialFlowVelocity.svg" width=16px> Startbedingung Strömungsgeschwindigkeit** auswählen.
2.  Einen Startwert der Strömungsgeschwindigkeit für die Analyse eingeben. Der Wert wird als Kombination der 3 kartesischen Hauptvektorkomponenten (X,Y,Z) angegeben.
3.  Für eine 3D-Analyse wird ein Festkörper (Body) des Modells ausgewählt, für eine 2D-Analyse eine Fläche. Es ist aber auch möglich eine Fläche (z.B. den Einlass einer Leitung) in 3D oder eine Kante in 2D auszuwählen.



## Formeln

Eine Beschreibung, wie man Formeln einsetzt, befindet sich im Abschnitt *Formeln* auf der Seite [RandbedingungStrömungsgeschwindigkeit](FEM_ConstraintFlowVelocity/de#Formeln.md).



## Hinweise

In einfachen Analysen ist es nicht erforderlich, einen Startwert für die Strömungsgeschwindigkeit anzugeben, wird aber als bewährte Vorgehensweise empfohlen.





{{FEM Tools navi

}}



---
⏵ [documentation index](../README.md) > [FEM](Category_FEM.md) > FEM ConstraintInitialFlowVelocity/de
