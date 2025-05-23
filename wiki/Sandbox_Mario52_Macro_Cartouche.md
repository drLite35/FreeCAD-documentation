# Sandbox:Mario52 Macro Cartouche
Sandbox page to store the obsolete \'Cartouche\' macros created by Mario52.


<div class="mw-collapsible mw-collapsed toccolours">

# Macro CartoucheFC 


<div class="mw-collapsible-content">


{{Macro
|Name=Macro CartoucheFC
|Icon=Macro_CartoucheFC.png
|Description=This macro is a complete application, it allows to fill the cartridge of the drawing sheet delivered with FreeCAD (Only For [Drawing Workbench](Drawing_Workbench.md)).
|Author=Mario52
|Version=0.3
|Date=2014-07-02
|FCVersion=All version using Drawing Workbench
|Download=[https://www.freecadweb.org/wiki/images/0/0a/Macro_CartoucheFC.png ToolBar Icon]
}}

## Description

This macro is a complete application, it allows to fill simply all the fields of the cartridge of the drawing sheet delivered with FreeCAD.

The date and time fields are separated by a \"space negative space\" \" - \" and constitute a single line textedit.

<img alt="CartoucheFC" src=images/CartoucheFC.png  style="width:480px;">

Fields in red are the **\"freecad:editable\"** fields, fields in green are annotations inserted in the template.
Here the version for the new sheet with all the editable text fields.

## Usage

**Changing the map in Inkscape can at the moment cause operation problems in the program (where you remove the symbol on the worksheet, same problem with FreeCAD), work on a copy of A3_Landscape.svg.**
**PS: Some characters such as & \$ are not accepted (and possibly other special characters).**

If you have any questions or want to add a function, you can address you on the french forum [Remplir cartouche](http://forum.freecadweb.org/viewtopic.php?f=12&t=2049)
\*The window remains above other Windows, thereby controlling the cartridge without leaving the program.

-   Copy the code into a file named **Macro_CartoucheFC.FCMacro** and place it in your usual macros directory.
-   After you have created your drawing sheet using the Drawing of FreeCAD module, run the macro **Macro_CartoucheFC**.
-   At the opening, the program will register in memory all data already present in the cartridge of the sheet (if they are filled), all these data will be automatically returned to using the button ** Memo** and kept in memory until the closure of the programme.
-   Date button ** D.** and time ** H.** displayed the date and time of the system.

  -The date format depends on the selected symbol **EU** or **US** which determines the regional format. Change does not happen automatically (for the case or you have entered a date manually) you must again click buttons dates if you change the symbol (check before printing).

-   The field **A3** is not functional (this program is based on the the A3 of FreeCAD sheet cartridge).
-   Button **Symbole EU** or US change the meaning of the symbol of projection \"Select your Symbol\" is displayed by default, and then the active symbol appears. Click on the button and check the leaf symbol, click a second time to modify the symbol.

  -The choice of this symbol, affects the date format **EU = dd/MM/yyyy** and **US = MM/dd/yyyy**.

  -**Attention**: this command does not pass through the button **Apply** and immediately changes the symbol to each presses on the key, always check if you have the appropriate symbol on your worksheet.

-   Button **Clean** Clears all fields in the cartridge. You can revert to the original data using the button **Memo**.
-   Button **Apply** saves all fields of the cartridge in the sheet. You can revert to the original data using the button **Memo** (except for the regional symbol that works in independent and is effective immediately).

## Code

ToolBar Icon ![](images/Macro_CartoucheFC.png )

**Macro_CartoucheFC.FCMacro**


{{MacroCode|code=

# -*- coding: utf-8 -*-
# Macro_CartoucheFC.py
# Remplir les zones du cartouche de la feuille originale de FreeCAD
# http://www.freecadweb.org/wiki/index.php?title=Macro_CartoucheFC/fr
# il faut que la page (drawing viewer) s'appelle " Page " qui est le nom par défaut du module Drawing
# Fill the area of the cartridge
# http://www.freecadweb.org/wiki/index.php?title=Macro_CartoucheFC
# It is necessary that the page (drawing viewer) is called "Page", which is the default name of the Drawing module
# ver 0.3
# Created: 02/07/2014
# Created:  by mario52
# PyQt and PySide 

#OS: Windows Vista
#Word size: 32-bit
#Version: 0.14.3700 (Git)
#Branch: releases/FreeCAD-0-14
#Hash: 32f5aae0a64333ec8d5d160dbc46e690510c8fe1
#Python version: 2.6.2
#Qt version: 4.5.2
#Coin version: 3.1.0
#SoQt version: 1.4.1

try:
    import PyQt4
    from PyQt4 import QtCore, QtGui
except Exception:
    import PySide
    from PySide import QtCore, QtGui

import Draft, Part, FreeCAD, math, PartGui, FreeCADGui
from math import sqrt, pi, sin, cos, asin
from FreeCAD import Base

global  path

path = FreeCAD.ConfigGet("AppHomePath")

def heure():
    return QtCore.QTime().currentTime().toString('hh:mm:ss')
def dateEu():
    return QtCore.QDate().currentDate().toString('dd/MM/yyyy') # forme euro
def dateUs():
    return QtCore.QDate().currentDate().toString('MM/dd/yyyy') # forme us
def dateComp():
    return QtCore.QDate().currentDate().toString('dddd d MMMM yyyy') # Retourne "dimanche 20 Juillet 69"

try:
    _fromUtf8 = QtCore.QString.fromUtf8
except AttributeError:
    def _fromUtf8(s):
        return s
try:
    _encoding = QtGui.QApplication.UnicodeUTF8
    def _translate(context, text, disambig):
        return QtGui.QApplication.translate(context, text, disambig, _encoding)
except AttributeError:
    def _translate(context, text, disambig):
        return QtGui.QApplication.translate(context, text, disambig)

def errorDialog(msg):
    # Create a simple dialog QMessageBox
    # The first argument indicates the icon used: one of QtGui.QMessageBox.{NoIcon, Information, Warning, Critical, Question} 
    diag = QtGui.QMessageBox(QtGui.QMessageBox.Critical,u"Error Message",msg)
    try:
        diag.setWindowFlags(PyQt4.QtCore.Qt.WindowStaysOnTopHint)  #PyQt4 cette fonction met la fenêtre en avant
    except Exception:
        diag.setWindowFlags(PySide.QtCore.Qt.WindowStaysOnTopHint) #PySide cette fonction met la fenêtre en avant
    #diag.setWindowModality(QtCore.Qt.ApplicationModal) # la fonction a été désactivée pour favoriser "WindowStaysOnTopHint"
    diag.exec_()

def symbol_EU(depx,depy):    #symbol_EU
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_US")
    except:
        None
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_EU")
    except:
        None
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("SymbolUS")
    except:
        None
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("SymbolEU")
    except:
        None
    App.activeDocument().addObject('Sketcher::SketchObject','Symbol_EU')
    App.activeDocument().Symbol_EU.Placement = App.Placement(App.Vector(0.0,0.0,0.0),App.Rotation(0.000000,0.000000,0.000000,1.000000))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Line(App.Vector(-7.5,0.0,0.0),App.Vector(20.0,0.0,0.0)))

    App.ActiveDocument.Symbol_EU.Placement = App.Placement(App.Vector(0.0,0.0),App.Rotation(0.000000,0.000000,0.000000,1.000000))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Line(App.Vector(12.50,-7.5,0),App.Vector(12.50,7.5,0.0)))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Circle(App.Vector(12.50,0.0,0),App.Vector(0,0,1),2.5))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Circle(App.Vector(12.50,0.0,0),App.Vector(0,0,1),5.0))

    App.ActiveDocument.Symbol_EU.addGeometry(Part.Line(App.Vector(5.0,5.0,0.0),App.Vector(-5.0,2.5,0.0)))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Line(App.Vector(-5.0,-2.5,0.0),App.Vector(-5.0,2.5,0.0)))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Line(App.Vector(5.0,-5.0,0.0),App.Vector(-5.0,-2.5,0.0)))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Line(App.Vector(5.0,-5.0,0.0),App.Vector(5.0,5.0,0.0)))
    Gui.getDocument(App.ActiveDocument.Name).resetEdit()
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_EU").LineColor = (0.00,0.00,0.00)
    App.ActiveDocument.recompute()

    App.activeDocument().addObject('Drawing::FeatureViewPart','SymbolEU')
    App.activeDocument().SymbolEU.Source = App.activeDocument().Symbol_EU
    App.activeDocument().SymbolEU.Direction = (0.0,0.0,1.0)
    App.activeDocument().SymbolEU.X = depx
    App.activeDocument().SymbolEU.Y = depy
    App.activeDocument().SymbolEU.Scale = 0.8
    App.activeDocument().Page.addObject(App.activeDocument().SymbolEU)
    App.ActiveDocument.recompute()
#    App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_EU")
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_EU").Visibility = False

def symbol_US(depx,depy):    #symbol_US
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_US")
    except:
        None
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_EU")
    except:
        None
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("SymbolUS")
    except:
        None
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("SymbolEU")
    except:
        None
    App.activeDocument().addObject('Sketcher::SketchObject','Symbol_US')
    App.activeDocument().Symbol_US.Placement = App.Placement(App.Vector(0.0,0.0,0.0),App.Rotation(0.000000,0.000000,0.000000,1.000000))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Line(App.Vector(-7.5,0.0,0.0),App.Vector(20.0,0.0,0.0)))

    App.ActiveDocument.Symbol_US.Placement = App.Placement(App.Vector(0.0,0.0),App.Rotation(0.000000,0.000000,0.000000,1.000000))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Line(App.Vector(0.0,-7.5,0.0),App.Vector(0.0,7.5,0.0)))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Circle(App.Vector(0.0,0.0,0.0),App.Vector(0,0,1),2.5))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Circle(App.Vector(0.0,0.0,0.0),App.Vector(0,0,1),5.0))

    App.ActiveDocument.Symbol_US.addGeometry(Part.Line(App.Vector(17.5,5.0,0.0),App.Vector(7.5,2.5,0.0)))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Line(App.Vector(7.5,-2.5,0.0),App.Vector(7.5,2.5,0.0)))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Line(App.Vector(17.5,-5.0,0.0),App.Vector(7.5,-2.5,0.0)))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Line(App.Vector(17.5,-5.0,0.0),App.Vector(17.5,5.0,0.0)))
    Gui.getDocument(App.ActiveDocument.Name).resetEdit()
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_US").LineColor = (0.00,0.00,0.00)
    App.ActiveDocument.recompute()

    App.activeDocument().addObject('Drawing::FeatureViewPart','SymbolUS')
    App.activeDocument().SymbolUS.Source = App.activeDocument().Symbol_US
    App.activeDocument().SymbolUS.Direction = (0.0,0.0,1.0)
    App.activeDocument().SymbolUS.X = depx
    App.activeDocument().SymbolUS.Y = depy
    App.activeDocument().SymbolUS.Scale = 0.8
    App.activeDocument().Page.addObject(App.activeDocument().SymbolUS)
    App.ActiveDocument.recompute()
#    App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_US")
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_US").Visibility = False

try:
    DESIGNED_BY = App.activeDocument().getObject("Page").EditableTexts[0] #lineEdit01 DESIGNED_BY
    CREATION_DATE = App.activeDocument().getObject("Page").EditableTexts[1] #lineEdit02 CREATION_DATE date
    CREA_DATE = CREATION_DATE[0:10] # lineEdit02h date
    CREA_TIME = CREATION_DATE[13:21] # lineEdit02h heure
    CHECKED_BY = App.activeDocument().getObject("Page").EditableTexts[2] # lineEdit03
    CHECK_DATE = App.activeDocument().getObject("Page").EditableTexts[3] # lineEdit04 date
    CHEC_DATE = CHECK_DATE[0:10] # lineEdit04 date
    CHEC_TIME = CHECK_DATE[13:21] # lineEdit04h heure
    SIZE = "A3"  # lineEdit05
    SCALE = App.activeDocument().getObject("Page").EditableTexts[4] # lineEdit06
    WEIGHT = App.activeDocument().getObject("Page").EditableTexts[5] # lineEdit07
    DRAWING_NUMBER = App.activeDocument().getObject("Page").EditableTexts[6] # lineEdit08
    SHEET = App.activeDocument().getObject("Page").EditableTexts[7] # lineEdit09
    TITLE = App.activeDocument().getObject("Page").EditableTexts[8] # textEdit_01
    DESCRIPTION = App.activeDocument().getObject("Page").EditableTexts[9] # textEdit_02

except:
    errorDialog("erreur cartouche")
try:
    try:
        lineEdit18 = App.activeDocument().getObject("Note_I").Text[0] 
    except:
        lineEdit18 = ""
    try:
        lineEdit17 = App.activeDocument().getObject("Note_H").Text[0] 
    except:
        lineEdit17 = ""
    try:
        lineEdit16 = App.activeDocument().getObject("Note_G").Text[0] 
    except:
        lineEdit16 = ""
    try:
        lineEdit15 = App.activeDocument().getObject("Note_F").Text[0] 
    except:
        lineEdit15 = ""
    try:
        lineEdit14 = App.activeDocument().getObject("Note_E").Text[0] 
    except:
        lineEdit14 = ""
    try:
        lineEdit13 = App.activeDocument().getObject("Note_D").Text[0] 
    except:
        lineEdit13 = ""
    try:
        lineEdit12 = App.activeDocument().getObject("Note_C").Text[0] 
    except:
        lineEdit12 = ""
    try:
        lineEdit11 = App.activeDocument().getObject("Note_B").Text[0] 
    except:
        lineEdit11 = ""
    try:
        lineEdit10 = App.activeDocument().getObject("Note_A").Text[0] 
    except:
        lineEdit10 = ""
    try:
        lineEdit20 = App.activeDocument().getObject("CopyRight").Text[0] 
    except:
        lineEdit20 = ""
except:
    errorDialog("erreur note")

class Ui_MainWindow(object):

    def __init__(self, MainWindow):
        self.window = MainWindow
#___________________________________________________________________________________

        MainWindow.setObjectName(_fromUtf8("MainWindow"))
        MainWindow.resize(810, 440)
        MainWindow.setMaximumSize(QtCore.QSize(810, 480))
        self.centralWidget = QtGui.QWidget(MainWindow)
        self.centralWidget.setObjectName(_fromUtf8("centralWidget"))

#        self.pushButton01 = QtGui.QPushButton(self.centralWidget)
#        self.pushButton01.setGeometry(QtCore.QRect(115, 360, 93, 28))
#        self.pushButton01.setObjectName(_fromUtf8("pushButton01"))
#        self.pushButton01.clicked.connect(self.on_pushButton01_clicked) #connection pushButton01

        self.pushButton02 = QtGui.QPushButton(self.centralWidget)
        self.pushButton02.setGeometry(QtCore.QRect(225, 360, 93, 28))
        self.pushButton02.setObjectName(_fromUtf8("pushButton02"))
        self.pushButton02.clicked.connect(self.on_pushButton02_clicked) #connection pushButton02

        self.pushButton03 = QtGui.QPushButton(self.centralWidget)
        self.pushButton03.setGeometry(QtCore.QRect(335, 360, 93, 28))
        self.pushButton03.setObjectName(_fromUtf8("pushButton03"))
        self.pushButton03.clicked.connect(self.on_pushButton03_clicked) #connection pushButton03

        self.pushButton04 = QtGui.QPushButton(self.centralWidget)
        self.pushButton04.setGeometry(QtCore.QRect(445, 360, 93, 28))
        self.pushButton04.setObjectName(_fromUtf8("pushButton04"))
        self.pushButton04.clicked.connect(self.on_pushButton04_clicked) #connection pushButton04

        self.pushButton05 = QtGui.QPushButton(self.centralWidget)
        self.pushButton05.setGeometry(QtCore.QRect(555, 360, 93, 28))
        self.pushButton05.setObjectName(_fromUtf8("pushButton05"))
        self.pushButton05.clicked.connect(self.on_pushButton05_clicked) #connection pushButton05

        self.pushButton06 = QtGui.QPushButton(self.centralWidget)
        self.pushButton06.setGeometry(QtCore.QRect(170, 56, 20, 20))
        self.pushButton06.setObjectName(_fromUtf8("pushButton06"))
        self.pushButton06.clicked.connect(self.on_pushButton06_clicked) #connection pushButton06

        self.pushButton07 = QtGui.QPushButton(self.centralWidget)
        self.pushButton07.setGeometry(QtCore.QRect(190, 56, 20, 20))
        self.pushButton07.setObjectName(_fromUtf8("pushButton07"))
        self.pushButton07.clicked.connect(self.on_pushButton07_clicked) #connection pushButton07

        self.pushButton08 = QtGui.QPushButton(self.centralWidget)
        self.pushButton08.setGeometry(QtCore.QRect(170, 136, 20, 20))
        self.pushButton08.setObjectName(_fromUtf8("pushButton08"))
        self.pushButton08.clicked.connect(self.on_pushButton08_clicked) #connection pushButton08

        self.pushButton09 = QtGui.QPushButton(self.centralWidget)
        self.pushButton09.setGeometry(QtCore.QRect(190, 136, 20, 20))
        self.pushButton09.setObjectName(_fromUtf8("pushButton09"))
        self.pushButton09.clicked.connect(self.on_pushButton09_clicked) #connection pushButton09

        self.pushButton10 = QtGui.QPushButton(self.centralWidget)
        self.pushButton10.setGeometry(QtCore.QRect(100, 220, 101, 20))
        self.pushButton10.setObjectName(_fromUtf8("pushButton10"))
        self.pushButton10.clicked.connect(self.on_pushButton10_clicked) #connection pushButton10

        self.lineEdit_01 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_01.setGeometry(QtCore.QRect(20, 20, 181, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_01.setFont(font)
        self.lineEdit_01.setObjectName(_fromUtf8("lineEdit_01"))
        self.lineEdit_01.setText(DESIGNED_BY)

        self.lineEdit_02 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_02.setGeometry(QtCore.QRect(20, 60, 82, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_02.setFont(font)
        self.lineEdit_02.setObjectName(_fromUtf8("lineEdit_02"))
        self.lineEdit_02.setText(CREA_DATE)

        self.lineEdit_02h = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_02h.setGeometry(QtCore.QRect(98, 60, 72, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_02h.setFont(font)
        self.lineEdit_02h.setObjectName(_fromUtf8("lineEdit_02h"))
        self.lineEdit_02h.setText(CREA_TIME)

        self.lineEdit_03 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_03.setGeometry(QtCore.QRect(20, 100, 181, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_03.setFont(font)
        self.lineEdit_03.setObjectName(_fromUtf8("lineEdit_03"))
        self.lineEdit_03.setText(CHECKED_BY)

        self.lineEdit_04 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_04.setGeometry(QtCore.QRect(20, 140, 82, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_04.setFont(font)
        self.lineEdit_04.setObjectName(_fromUtf8("lineEdit_04"))
        self.lineEdit_04.setText(CHEC_DATE)

        self.lineEdit_04h = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_04h.setGeometry(QtCore.QRect(98, 140, 72, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_04h.setFont(font)
        self.lineEdit_04h.setObjectName(_fromUtf8("lineEdit_04h"))
        self.lineEdit_04h.setText(CHEC_TIME)

        self.lineEdit_05 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_05.setGeometry(QtCore.QRect(20, 180, 61, 61))
        font = QtGui.QFont()
        font.setPointSize(17)
        font.setBold(False)
        font.setWeight(50)
        self.lineEdit_05.setFont(font)
        self.lineEdit_05.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_05.setObjectName(_fromUtf8("lineEdit_05"))
        self.lineEdit_05.setText(SIZE)

        self.lineEdit_06 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_06.setGeometry(QtCore.QRect(20, 280, 61, 41))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_06.setFont(font)
        self.lineEdit_06.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_06.setObjectName(_fromUtf8("lineEdit_06"))
        self.lineEdit_06.setText(SCALE)

        self.lineEdit_07 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_07.setGeometry(QtCore.QRect(100, 280, 101, 41))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_07.setFont(font)
        self.lineEdit_07.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_07.setObjectName(_fromUtf8("lineEdit_07"))
        self.lineEdit_07.setText(WEIGHT)

        self.lineEdit_08 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_08.setGeometry(QtCore.QRect(220, 280, 341, 41))
        self.lineEdit_08.setObjectName(_fromUtf8("lineEdit_08"))
        self.lineEdit_08.setText(DRAWING_NUMBER)

        self.lineEdit_09 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_09.setGeometry(QtCore.QRect(570, 280, 81, 41))
        self.lineEdit_09.setObjectName(_fromUtf8("lineEdit_09"))
        self.lineEdit_09.setText(SHEET)

        self.lineEdit_10 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_10.setGeometry(QtCore.QRect(690, 290, 101, 30))
        self.lineEdit_10.setObjectName(_fromUtf8("lineEdit_10"))
        self.lineEdit_10.setText(lineEdit10)

        self.lineEdit_11 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_11.setGeometry(QtCore.QRect(690, 260, 101, 30))
        self.lineEdit_11.setObjectName(_fromUtf8("lineEdit_11"))
        self.lineEdit_11.setText(lineEdit11)

        self.lineEdit_12 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_12.setGeometry(QtCore.QRect(690, 230, 101, 30))
        self.lineEdit_12.setObjectName(_fromUtf8("lineEdit_12"))
        self.lineEdit_12.setText(lineEdit12)

        self.lineEdit_13 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_13.setGeometry(QtCore.QRect(690, 200, 101, 30))
        self.lineEdit_13.setObjectName(_fromUtf8("lineEdit_13"))
        self.lineEdit_13.setText(lineEdit13)

        self.lineEdit_14 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_14.setGeometry(QtCore.QRect(690, 170, 101, 30))
        self.lineEdit_14.setObjectName(_fromUtf8("lineEdit_14"))
        self.lineEdit_14.setText(lineEdit14)

        self.lineEdit_15 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_15.setGeometry(QtCore.QRect(690, 140, 101, 30))
        self.lineEdit_15.setObjectName(_fromUtf8("lineEdit_15"))
        self.lineEdit_15.setText(lineEdit15)

        self.lineEdit_16 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_16.setGeometry(QtCore.QRect(690, 110, 101, 30))
        self.lineEdit_16.setObjectName(_fromUtf8("lineEdit_16"))
        self.lineEdit_16.setText(lineEdit16)

        self.lineEdit_17 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_17.setGeometry(QtCore.QRect(690, 80, 101, 30))
        self.lineEdit_17.setObjectName(_fromUtf8("lineEdit_17"))
        self.lineEdit_17.setText(lineEdit17)

        self.lineEdit_18 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_18.setGeometry(QtCore.QRect(690, 50, 101, 30))
        self.lineEdit_18.setObjectName(_fromUtf8("lineEdit_18"))
        self.lineEdit_18.setText(lineEdit18)

        self.lineEdit_20 = QtGui.QLineEdit(self.centralWidget) # Copyright
        self.lineEdit_20.setGeometry(QtCore.QRect(20, 330, 771, 22))
        self.lineEdit_20.setObjectName(_fromUtf8("lineEdit_20"))
        self.lineEdit_20.setText(lineEdit20)

        self.textEdit_01 = QtGui.QTextEdit(self.centralWidget)
        self.textEdit_01.setGeometry(QtCore.QRect(220, 20, 431,60 ))
        font = QtGui.QFont()
        font.setPointSize(15)
        font.setBold(True)
        font.setWeight(75)
        self.textEdit_01.setFont(font)
        self.textEdit_01.setObjectName(_fromUtf8("textEdit_01"))
        self.textEdit_01.setText(TITLE)

        self.textEdit_02 = QtGui.QTextEdit(self.centralWidget)
        self.textEdit_02.setGeometry(QtCore.QRect(220, 90, 431, 60))
        self.textEdit_02.setObjectName(_fromUtf8("textEdit_02"))
        self.textEdit_02.setText(DESCRIPTION)

#        self.graphicsView_01 = QtGui.QGraphicsView(self.centralWidget)
#        self.graphicsView_01.setGeometry(QtCore.QRect(100, 160, 101, 81))
#        brush = QtGui.QBrush(QtGui.QColor(0, 170, 255))
#        brush.setStyle(QtCore.Qt.NoBrush)
#        self.graphicsView_01.setBackgroundBrush(brush)
#        self.graphicsView_01.setObjectName(_fromUtf8("graphicsView_01"))

        self.textEdit_03 = QtGui.QTextEdit(self.centralWidget)
        self.textEdit_03.setGeometry(QtCore.QRect(100, 160, 101, 55))
        self.textEdit_03.setAlignment(QtCore.Qt.AlignCenter)
        self.textEdit_03.setObjectName(_fromUtf8("textEdit_03"))
        self.textEdit_03.setText("Select your Symbol")

        self.graphicsView_02 = QtGui.QGraphicsView(self.centralWidget)
        self.graphicsView_02.setGeometry(QtCore.QRect(220, 160, 431, 81))#570, 160, 81, 81
        self.graphicsView_02.setObjectName(_fromUtf8("graphicsView_02"))

        self.label_01 = QtGui.QLabel(self.centralWidget)
        self.label_01.setGeometry(QtCore.QRect(20, 0, 91, 16))
        self.label_01.setObjectName(_fromUtf8("label_01"))

        self.label_02 = QtGui.QLabel(self.centralWidget)
        self.label_02.setGeometry(QtCore.QRect(20, 40, 53, 16))
        self.label_02.setObjectName(_fromUtf8("label_02"))

        self.label_03 = QtGui.QLabel(self.centralWidget)
        self.label_03.setGeometry(QtCore.QRect(20, 80, 101, 16))
        self.label_03.setObjectName(_fromUtf8("label_03"))

        self.label_04 = QtGui.QLabel(self.centralWidget)
        self.label_04.setGeometry(QtCore.QRect(20, 120, 91, 16))
        self.label_04.setObjectName(_fromUtf8("label_04"))

        self.label_05 = QtGui.QLabel(self.centralWidget)
        self.label_05.setGeometry(QtCore.QRect(20, 160, 53, 16))
        self.label_05.setObjectName(_fromUtf8("label_05"))

        self.label_06 = QtGui.QLabel(self.centralWidget)
        self.label_06.setGeometry(QtCore.QRect(20, 260, 53, 16))
        self.label_06.setObjectName(_fromUtf8("label_06"))

        self.label_07 = QtGui.QLabel(self.centralWidget)
        self.label_07.setGeometry(QtCore.QRect(100, 260, 101, 16))
        self.label_07.setObjectName(_fromUtf8("label_07"))

        self.label_08 = QtGui.QLabel(self.centralWidget)
        self.label_08.setGeometry(QtCore.QRect(220, 260, 121, 16))
        self.label_08.setObjectName(_fromUtf8("label_08"))

        self.label_09 = QtGui.QLabel(self.centralWidget)
        self.label_09.setGeometry(QtCore.QRect(570, 260, 53, 16))
        self.label_09.setObjectName(_fromUtf8("label_09"))

        self.label_10 = QtGui.QLabel(self.centralWidget)
        self.label_10.setGeometry(QtCore.QRect(670, 290, 16, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_10.setFont(font)
        self.label_10.setObjectName(_fromUtf8("label_10"))

        self.label_11 = QtGui.QLabel(self.centralWidget)
        self.label_11.setGeometry(QtCore.QRect(670, 260, 16, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_11.setFont(font)
        self.label_11.setObjectName(_fromUtf8("label_11"))

        self.label_12 = QtGui.QLabel(self.centralWidget)
        self.label_12.setGeometry(QtCore.QRect(670, 230, 16, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_12.setFont(font)
        self.label_12.setObjectName(_fromUtf8("label_12"))

        self.label_13 = QtGui.QLabel(self.centralWidget)
        self.label_13.setGeometry(QtCore.QRect(670, 200, 18, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_13.setFont(font)
        self.label_13.setObjectName(_fromUtf8("label_13"))

        self.label_14 = QtGui.QLabel(self.centralWidget)
        self.label_14.setGeometry(QtCore.QRect(670, 170, 15, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_14.setFont(font)
        self.label_14.setObjectName(_fromUtf8("label_14"))

        self.label_15 = QtGui.QLabel(self.centralWidget)
        self.label_15.setGeometry(QtCore.QRect(670, 140, 14, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_15.setFont(font)
        self.label_15.setObjectName(_fromUtf8("label_15"))

        self.label_16 = QtGui.QLabel(self.centralWidget)
        self.label_16.setGeometry(QtCore.QRect(670, 110, 18, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_16.setFont(font)
        self.label_16.setObjectName(_fromUtf8("label_16"))

        self.label_17 = QtGui.QLabel(self.centralWidget)
        self.label_17.setGeometry(QtCore.QRect(670, 80, 18, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_17.setFont(font)
        self.label_17.setObjectName(_fromUtf8("label_17"))

        self.label_18 = QtGui.QLabel(self.centralWidget)
        self.label_18.setGeometry(QtCore.QRect(670, 50, 10, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_18.setFont(font)
        self.label_18.setObjectName(_fromUtf8("label_18"))

        self.label_19 = QtGui.QLabel(self.centralWidget)
        self.label_19.setGeometry(QtCore.QRect(720, 15, 100, 33))
        self.label_19.setObjectName(_fromUtf8("label_19"))

        MainWindow.setCentralWidget(self.centralWidget)
        self.menuBar = QtGui.QMenuBar(MainWindow)
        self.menuBar.setGeometry(QtCore.QRect(0, 0, 810, 26))
        self.menuBar.setObjectName(_fromUtf8("menuBar"))
        MainWindow.setMenuBar(self.menuBar)
        self.statusBar = QtGui.QStatusBar(MainWindow)
        self.statusBar.setObjectName(_fromUtf8("statusBar"))
        MainWindow.setStatusBar(self.statusBar)

        self.retranslateUi(MainWindow)
        QtCore.QMetaObject.connectSlotsByName(MainWindow)

    def retranslateUi(self, MainWindow):
        try:
            MainWindow.setWindowFlags(PyQt4.QtCore.Qt.WindowStaysOnTopHint)  # PyQt4 cette fonction met la fenêtre en avant
        except Exception:
            MainWindow.setWindowFlags(PySide.QtCore.Qt.WindowStaysOnTopHint) # PySide cette fonction met la fenêtre en avant

        MainWindow.setWindowTitle(_translate("MainWindow", "Cartouche", None))
#        self.pushButton01.setText(_translate("MainWindow", "Position", None))
        self.pushButton02.setText(_translate("MainWindow", "Quitter", None))
        self.pushButton03.setText(_translate("MainWindow", "Memo", None))
        self.pushButton04.setText(_translate("MainWindow", "Nettoyer", None))
        self.pushButton05.setText(_translate("MainWindow", "Appliquer", None))
        self.pushButton06.setText(_translate("MainWindow", "D.", None))
        self.pushButton07.setText(_translate("MainWindow", "H.", None))
        self.pushButton08.setText(_translate("MainWindow", "D.", None))
        self.pushButton09.setText(_translate("MainWindow", "H.", None))
        self.pushButton10.setText(_translate("MainWindow", "Symbole EU", None))


        self.label_01.setText(_translate("MainWindow", "Designed by :", None))
        self.label_02.setText(_translate("MainWindow", "Date :", None))
        self.label_03.setText(_translate("MainWindow", "Checked by :", None))
        self.label_04.setText(_translate("MainWindow", "Date :", None))
        self.label_05.setText(_translate("MainWindow", "Size :", None))
        self.label_06.setText(_translate("MainWindow", "Scale :", None))
        self.label_07.setText(_translate("MainWindow", "Weight (Kg) :", None))
        self.label_08.setText(_translate("MainWindow", "Drawing number :", None))
        self.label_09.setText(_translate("MainWindow", "Sheet :", None))
        self.label_10.setText(_translate("MainWindow", "A", None))
        self.label_11.setText(_translate("MainWindow", "B", None))
        self.label_12.setText(_translate("MainWindow", "C", None))
        self.label_13.setText(_translate("MainWindow", "D", None))
        self.label_14.setText(_translate("MainWindow", "E", None))
        self.label_15.setText(_translate("MainWindow", "F", None))
        self.label_16.setText(_translate("MainWindow", "G", None))
        self.label_17.setText(_translate("MainWindow", "H", None))
        self.label_18.setText(_translate("MainWindow", "I", None))
        self.label_19.setText(_translate("MainWindow", "Notes", None))
#______________________________________________________________________________________
    # Boutons
    def on_pushButton10_clicked(self):    # Bouton /Symbole
        if self.textEdit_03.toPlainText()=="Symbole US":
            self.pushButton10.setText(_translate("MainWindow", "Symbole US", None))
            self.textEdit_03.setText("Symbole EU")
            symbol_EU(247.5,263.5) #(247.5,263.5)
        else:
            self.pushButton10.setText(_translate("MainWindow", "Symbole EU", None))
            self.textEdit_03.setText("Symbole US")
            symbol_US(247.5,263.5) #(247.5,263.5)
    def on_pushButton09_clicked(self):    # Bouton /heure document
        self.lineEdit_04h.setText(str(heure()))
    def on_pushButton08_clicked(self):    # Bouton date/ document
        if self.textEdit_03.toPlainText()=="Symbole US":
            self.lineEdit_04.setText(str(dateUs()))
        else:
            self.lineEdit_04.setText(str(dateEu()))
    def on_pushButton07_clicked(self):    # Bouton /heure checked
        self.lineEdit_02h.setText(str(heure()))
    def on_pushButton06_clicked(self):    # Bouton date/ checked
        if self.textEdit_03.toPlainText()=="Symbole US":
            self.lineEdit_02.setText(str(dateUs()))
        else:
            self.lineEdit_02.setText(str(dateEu()))
    def on_pushButton05_clicked(self):    # Bouton Appliquer
        DESIGNED_BY = self.lineEdit_01.text()     
        CREATION_DATE = self.lineEdit_02.text()+" - "+self.lineEdit_02h.text()
        CHECKED_BY = self.lineEdit_03.text()
        CHECK_DATE = self.lineEdit_04.text()+" - "+self.lineEdit_04h.text()
        SIZE  = "A3" # self.lineEdit_05.text()
        SCALE = self.lineEdit_06.text()
        WEIGHT = self.lineEdit_07.text()
        DRAWING_NUMBER = self.lineEdit_08.text()
        SHEET = self.lineEdit_09.text()
        TITLE = self.textEdit_01.toPlainText()
        DESCRIPTION = self.textEdit_02.toPlainText()
        SYMBOL = self.textEdit_03.toPlainText()
        try:
            FreeCAD.getDocument (App.ActiveDocument.Name).getObject("Page").EditableTexts = [unicode(DESIGNED_BY, 'utf-8'), unicode(CREATION_DATE, 'utf-8'), unicode(CHECKED_BY, 'utf-8'), unicode(CHECK_DATE, 'utf-8'), unicode(SCALE, 'utf-8'), unicode(WEIGHT, 'utf-8'), unicode(DRAWING_NUMBER, 'utf-8'), unicode(SHEET, 'utf-8'), unicode(TITLE, 'utf-8'), unicode(DESCRIPTION, 'utf-8'),]
        except Exception:
            FreeCAD.getDocument (App.ActiveDocument.Name).getObject("Page").EditableTexts = [DESIGNED_BY.encode('utf-8'), CREATION_DATE.encode('utf-8'), CHECKED_BY.encode('utf-8'), CHECK_DATE.encode('utf-8'), SCALE.encode('utf-8'), WEIGHT.encode('utf-8'), DRAWING_NUMBER.encode('utf-8'), SHEET.encode('utf-8'), TITLE.encode('utf-8'), DESCRIPTION.encode('utf-8'),]

        #print App.ActiveDocument.Name
        try:
            App.activeDocument().removeObject('Note_I')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_H')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_G')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_F')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_E')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_D')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_C')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_B')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_A')
        except:
            None
        try:
            App.activeDocument().removeObject('CopyRight')
        except:
            None
        if self.lineEdit_18.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_I')
            App.activeDocument().Note_I.X = 391.0
            App.activeDocument().Note_I.Y = 232
            App.activeDocument().Note_I.Scale = 3.0
            App.activeDocument().Note_I.Text = str(self.lineEdit_18.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_I)
        if self.lineEdit_17.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_H')
            App.activeDocument().Note_H.X = 391.0
            App.activeDocument().Note_H.Y = 238.8
            App.activeDocument().Note_H.Scale = 3.0
            App.activeDocument().Note_H.Text = str(self.lineEdit_17.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_H)
        if self.lineEdit_16.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_G')
            App.activeDocument().Note_G.X = 391.0
            App.activeDocument().Note_G.Y = 245.4
            App.activeDocument().Note_G.Scale = 3.0
            App.activeDocument().Note_G.Text = str(self.lineEdit_16.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_G)
        if self.lineEdit_15.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_F')
            App.activeDocument().Note_F.X = 391.0
            App.activeDocument().Note_F.Y = 252
            App.activeDocument().Note_F.Scale = 3.0
            App.activeDocument().Note_F.Text = str(self.lineEdit_15.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_F)
        if self.lineEdit_14.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_E')
            App.activeDocument().Note_E.X = 391.0
            App.activeDocument().Note_E.Y = 258.6
            App.activeDocument().Note_E.Scale = 3.0
            App.activeDocument().Note_E.Text = str(self.lineEdit_14.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_E)
        if self.lineEdit_13.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_D')
            App.activeDocument().Note_D.X = 391.0
            App.activeDocument().Note_D.Y = 265.2
            App.activeDocument().Note_D.Scale = 3.0
            App.activeDocument().Note_D.Text = str(self.lineEdit_13.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_D)
        if self.lineEdit_12.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_C')
            App.activeDocument().Note_C.X = 391.0
            App.activeDocument().Note_C.Y = 271.8
            App.activeDocument().Note_C.Scale = 3.0
            App.activeDocument().Note_C.Text =  str(self.lineEdit_12.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_C)
        if self.lineEdit_11.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_B')
            App.activeDocument().Note_B.X = 391.0
            App.activeDocument().Note_B.Y = 278.4
            App.activeDocument().Note_B.Scale = 3.0
            App.activeDocument().Note_B.Text = str(self.lineEdit_11.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_B)
        if self.lineEdit_10.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_A')
            App.activeDocument().Note_A.X = 391.0
            App.activeDocument().Note_A.Y = 285.0
            App.activeDocument().Note_A.Scale = 3.0
            App.activeDocument().Note_A.Text = str(self.lineEdit_10.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_A)
        if self.lineEdit_20.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','CopyRight')
            App.activeDocument().CopyRight.X = 221
            App.activeDocument().CopyRight.Y = 286
            App.activeDocument().CopyRight.Scale = 3.0
            App.activeDocument().CopyRight.Text = str(self.lineEdit_20.text())
            App.activeDocument().Page.addObject(App.activeDocument().CopyRight)

        App.ActiveDocument.recompute()

    def on_pushButton04_clicked(self):    # Bouton nettoyer
        try:
            App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_US")
        except:
            None
        try:
            App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_EU")
        except:
            None
        try:
            App.getDocument(App.ActiveDocument.Name).removeObject("SymbolUS")
        except:
            None
        try:
            App.getDocument(App.ActiveDocument.Name).removeObject("SymbolEU")
        except:
            None
        DESIGNED_BY = ""    ;self.lineEdit_01.setText("")
        CREATION_DATE = ""  ;self.lineEdit_02.setText("")
        self.lineEdit_02h.setText("")
        CHECKED_BY = ""     ;self.lineEdit_03.setText("")
        CHECK_DATE = ""     ;self.lineEdit_04.setText("")
        self.lineEdit_04h.setText("")
        SIZE  = "A3"        ;self.lineEdit_05.setText("A3")
        SCALE = ""          ;self.lineEdit_06.setText("")
        WEIGHT = ""         ;self.lineEdit_07.setText("")
        DRAWING_NUMBER = "" ;self.lineEdit_08.setText("")
        SHEET = ""          ;self.lineEdit_09.setText("")
        TITLE = ""          ;self.textEdit_01.setText("")
        DESCRIPTION = ""    ;self.textEdit_02.setText("")
        
        self.lineEdit_10.setText("")
        self.lineEdit_11.setText("")
        self.lineEdit_12.setText("")
        self.lineEdit_13.setText("")
        self.lineEdit_14.setText("")
        self.lineEdit_15.setText("")
        self.lineEdit_16.setText("")
        self.lineEdit_17.setText("")
        self.lineEdit_18.setText("")
        self.lineEdit_20.setText("")

    def on_pushButton03_clicked(self):    # Bouton Memo
        self.lineEdit_01.setText(DESIGNED_BY)
        self.lineEdit_02.setText(CREA_DATE)
        self.lineEdit_02h.setText(CREA_TIME)
        self.lineEdit_03.setText(CHECKED_BY)
        self.lineEdit_04.setText(CHEC_DATE)
        self.lineEdit_04h.setText(CHEC_TIME)
        self.lineEdit_05.setText(SIZE)
        self.lineEdit_06.setText(SCALE)
        self.lineEdit_07.setText(WEIGHT)
        self.lineEdit_08.setText(DRAWING_NUMBER)
        self.lineEdit_09.setText(SHEET)
        self.textEdit_01.setText(TITLE)
        self.textEdit_02.setText(DESCRIPTION)

        self.lineEdit_18.setText(lineEdit18)
        self.lineEdit_17.setText(lineEdit17)
        self.lineEdit_16.setText(lineEdit16)
        self.lineEdit_15.setText(lineEdit15)
        self.lineEdit_14.setText(lineEdit14)
        self.lineEdit_13.setText(lineEdit13)
        self.lineEdit_12.setText(lineEdit12)
        self.lineEdit_11.setText(lineEdit11)
        self.lineEdit_10.setText(lineEdit10)
        self.lineEdit_20.setText(lineEdit20)

    def on_pushButton02_clicked(self):    # Bouton Quitter
        App.Console.PrintMessage("Terminé\r\n")
        self.window.hide()
#    def on_pushButton01_clicked(self):    # Bouton appel de Position
#        MainWindow.resize(210, 480)
#        executer()
#        MainWindow.resize(810, 480)
#______________________________________________________________________________________

MainWindow = QtGui.QMainWindow()
ui = Ui_MainWindow(MainWindow)
MainWindow.show()

}}

## Other

The fields have no length limit, check your cartouche.
This program creates a drawing representing the regional projection symbol on your project, do not touch it is registered therefore hidden form invisible.
If you want it to be cleared uncomment the commented lines and vice versa


```python

#    App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_EU")
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_EU").Visibility = False
et
#    App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_US")
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_US").Visibility = False
```

(I had some times an error in execution when the symbol was erased)
This module works with the drawing sheet included in FreeCAD this sheet is called **Page**, do not change the name of this sheet!

## Revision

ver 0.3 02/07/2014 converted to PyQt4 and PySide


</div>


</div>





<div class="mw-collapsible mw-collapsed toccolours">

# Macro CartoucheFC/fr 


<div class="mw-collapsible-content">


{{Macro/fr
|Name=Macro CartoucheFC
|Icon=Macro_CartoucheFC.png
|Description=Cette macro est une application complète, elle permet de remplir le cartouche de la feuille de dessin livrée avec FreeCAD (Seulement pour l'[atelier Drawing](Drawing_Workbench/fr.md)).
|Author=Mario52
|Version=0.3
|Date=2014-07-02
|FCVersion=Toutes versions utilisant l'atelier Drawing
|Download=[https://www.freecadweb.org/wiki/images/0/0a/Macro_CartoucheFC.png ToolBar Icon]
}}

## Description 

Cette macro est une application complète, elle permet de remplir simplement tous les champs du cartouche de la feuille de dessin livrée avec FreeCAD.

La date et l\'heure sont séparés par un \"espace tiret espace\" et constitue une seule ligne dans le textéditable de FreeCAD.

<img alt="CartoucheFC" src=images/CartoucheFC.png  style="width:480px;">

Les champs en rouge sont les champs **\"FreeCAD: modifiable\"**., les champs en vert sont des annotations insérées dans le modèle
Ici une version de Macro_CartoucheFC_Full pour les nouvelles feuilles avec textéditable à tous les champs.

## Utilisation

**La modification de la feuille dans Inkscape peut pour le moment poser des problèmes de fonctionnement au programme (dans le cas ou vous enlevez le symbole sur la feuille, même problème avec FreeCAD), travaillez sur une copie de A3_Landscape.svg.**
**PS: certains caractères comme & \$ ne sont pas acceptés (et peut être d\'autres caractères spéciaux)!**

Si vous avez des questions ou désirez ajouter une fonction, vous pouvez vous adresse sur le forum [Remplir cartouche](http://forum.freecadweb.org/viewtopic.php?f=12&t=2049)

-   La fenêtre reste au dessus des autres fenêtres et permet ainsi de contrôler le cartouche sans quitter le programme.

-   Copiez le code dans un fichier nommé **Macro_CartoucheFC.py** et placez le dans votre répertoire de macros habituelle.

-   Après avoir créé votre feuille de dessin à l\'aide du module Drawing de FreeCAD, lancez la macro **Macro_CartoucheFC**.

-   A l\'ouverture, le programme enregistrera en mémoire toutes les données déjà présente dans le cartouche de la feuille (s\'ils sont remplis), toutes ces données seront automatiquement restituées à l\'aide du bouton **Memo** et tenus en mémoire jusqu'à la fermeture du programme.

-   Les boutons de date ** D.** et heure ** H.** affichent la date et heure du système.

  -Le format de la date est tributaire du symbole sélectionné **EU** ou **US** qui détermine le format régional. Le changement ne se fait pas automatiquement (pour le cas ou vous avez entré une date manuellement) il faut cliquer à nouveau sur les boutons dates si vous changez le symbole (vérifiez avant d\'imprimer).

-   Le champ **A3** n\'est pas fonctionnel (ce programme est basé sur le cartouche de la feuille A3 de FreeCAD).

-   Le bouton **Symbole EU** ou US change le sens du symbole de projection \"Select your Symbol\" est affiché par défaut, puis le symbole actif s\'affiche. Cliquez sur le bouton et vérifiez sur la feuille le symbole, cliquez une seconde fois pour modifier le symbole.

  -Le choix de ce symbole, influe le format de la date **EU = dd/MM/yyyy** et **US = MM/dd/yyyy**.

  -**Attention** : Cette commande ne passe pas par le bouton **Appliquer** et modifie immédiatement le symbole à chaque appuis sur la touche, vérifiez toujours si vous avez sur votre feuille le symbole approprié.

-   Le bouton **Nettoyer** efface tous les champs du cartouche. Vous pouvez revenir aux données d\'origine à l\'aide du bouton **Memo**.

-   Le bouton **Appliquer** enregistre tous les champs du cartouche dans la feuille. Vous pouvez revenir aux données d\'origine à l\'aide du bouton **Memo** (sauf pour le symbole régional qui travaille en indépendant et est effectif immédiatement).

## Code 

ToolBar Icon ![](images/Macro_CartoucheFC.png )

**Macro_CartoucheFC.FCMacro**


{{MacroCode|code=

# -*- coding: utf-8 -*-
# Macro_CartoucheFC.py
# Remplir les zones du cartouche de la feuille originale de FreeCAD
# http://www.freecadweb.org/wiki/index.php?title=Macro_CartoucheFC/fr
# il faut que la page (drawing viewer) s'appelle " Page " qui est le nom par défaut du module Drawing
# Fill the area of the cartridge
# http://www.freecadweb.org/wiki/index.php?title=Macro_CartoucheFC
# It is necessary that the page (drawing viewer) is called "Page", which is the default name of the Drawing module
# ver 0.3
# Created: 02/07/2014
# Created:  by mario52
# PyQt and PySide 

#OS: Windows Vista
#Word size: 32-bit
#Version: 0.14.3700 (Git)
#Branch: releases/FreeCAD-0-14
#Hash: 32f5aae0a64333ec8d5d160dbc46e690510c8fe1
#Python version: 2.6.2
#Qt version: 4.5.2
#Coin version: 3.1.0
#SoQt version: 1.4.1

try:
    import PyQt4
    from PyQt4 import QtCore, QtGui
except Exception:
    import PySide
    from PySide import QtCore, QtGui

import Draft, Part, FreeCAD, math, PartGui, FreeCADGui
from math import sqrt, pi, sin, cos, asin
from FreeCAD import Base

global  path

path = FreeCAD.ConfigGet("AppHomePath")

def heure():
    return QtCore.QTime().currentTime().toString('hh:mm:ss')
def dateEu():
    return QtCore.QDate().currentDate().toString('dd/MM/yyyy') # forme euro
def dateUs():
    return QtCore.QDate().currentDate().toString('MM/dd/yyyy') # forme us
def dateComp():
    return QtCore.QDate().currentDate().toString('dddd d MMMM yyyy') # Retourne "dimanche 20 Juillet 69"

try:
    _fromUtf8 = QtCore.QString.fromUtf8
except AttributeError:
    def _fromUtf8(s):
        return s
try:
    _encoding = QtGui.QApplication.UnicodeUTF8
    def _translate(context, text, disambig):
        return QtGui.QApplication.translate(context, text, disambig, _encoding)
except AttributeError:
    def _translate(context, text, disambig):
        return QtGui.QApplication.translate(context, text, disambig)

def errorDialog(msg):
    # Create a simple dialog QMessageBox
    # The first argument indicates the icon used: one of QtGui.QMessageBox.{NoIcon, Information, Warning, Critical, Question} 
    diag = QtGui.QMessageBox(QtGui.QMessageBox.Critical,u"Error Message",msg)
    try:
        diag.setWindowFlags(PyQt4.QtCore.Qt.WindowStaysOnTopHint)  #PyQt4 cette fonction met la fenêtre en avant
    except Exception:
        diag.setWindowFlags(PySide.QtCore.Qt.WindowStaysOnTopHint) #PySide cette fonction met la fenêtre en avant
    #diag.setWindowModality(QtCore.Qt.ApplicationModal) # la fonction a été désactivée pour favoriser "WindowStaysOnTopHint"
    diag.exec_()

def symbol_EU(depx,depy):    #symbol_EU
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_US")
    except:
        None
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_EU")
    except:
        None
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("SymbolUS")
    except:
        None
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("SymbolEU")
    except:
        None
    App.activeDocument().addObject('Sketcher::SketchObject','Symbol_EU')
    App.activeDocument().Symbol_EU.Placement = App.Placement(App.Vector(0.0,0.0,0.0),App.Rotation(0.000000,0.000000,0.000000,1.000000))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Line(App.Vector(-7.5,0.0,0.0),App.Vector(20.0,0.0,0.0)))

    App.ActiveDocument.Symbol_EU.Placement = App.Placement(App.Vector(0.0,0.0),App.Rotation(0.000000,0.000000,0.000000,1.000000))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Line(App.Vector(12.50,-7.5,0),App.Vector(12.50,7.5,0.0)))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Circle(App.Vector(12.50,0.0,0),App.Vector(0,0,1),2.5))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Circle(App.Vector(12.50,0.0,0),App.Vector(0,0,1),5.0))

    App.ActiveDocument.Symbol_EU.addGeometry(Part.Line(App.Vector(5.0,5.0,0.0),App.Vector(-5.0,2.5,0.0)))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Line(App.Vector(-5.0,-2.5,0.0),App.Vector(-5.0,2.5,0.0)))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Line(App.Vector(5.0,-5.0,0.0),App.Vector(-5.0,-2.5,0.0)))
    App.ActiveDocument.Symbol_EU.addGeometry(Part.Line(App.Vector(5.0,-5.0,0.0),App.Vector(5.0,5.0,0.0)))
    Gui.getDocument(App.ActiveDocument.Name).resetEdit()
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_EU").LineColor = (0.00,0.00,0.00)
    App.ActiveDocument.recompute()

    App.activeDocument().addObject('Drawing::FeatureViewPart','SymbolEU')
    App.activeDocument().SymbolEU.Source = App.activeDocument().Symbol_EU
    App.activeDocument().SymbolEU.Direction = (0.0,0.0,1.0)
    App.activeDocument().SymbolEU.X = depx
    App.activeDocument().SymbolEU.Y = depy
    App.activeDocument().SymbolEU.Scale = 0.8
    App.activeDocument().Page.addObject(App.activeDocument().SymbolEU)
    App.ActiveDocument.recompute()
#    App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_EU")
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_EU").Visibility = False

def symbol_US(depx,depy):    #symbol_US
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_US")
    except:
        None
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_EU")
    except:
        None
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("SymbolUS")
    except:
        None
    try:
        App.getDocument(App.ActiveDocument.Name).removeObject("SymbolEU")
    except:
        None
    App.activeDocument().addObject('Sketcher::SketchObject','Symbol_US')
    App.activeDocument().Symbol_US.Placement = App.Placement(App.Vector(0.0,0.0,0.0),App.Rotation(0.000000,0.000000,0.000000,1.000000))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Line(App.Vector(-7.5,0.0,0.0),App.Vector(20.0,0.0,0.0)))

    App.ActiveDocument.Symbol_US.Placement = App.Placement(App.Vector(0.0,0.0),App.Rotation(0.000000,0.000000,0.000000,1.000000))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Line(App.Vector(0.0,-7.5,0.0),App.Vector(0.0,7.5,0.0)))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Circle(App.Vector(0.0,0.0,0.0),App.Vector(0,0,1),2.5))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Circle(App.Vector(0.0,0.0,0.0),App.Vector(0,0,1),5.0))

    App.ActiveDocument.Symbol_US.addGeometry(Part.Line(App.Vector(17.5,5.0,0.0),App.Vector(7.5,2.5,0.0)))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Line(App.Vector(7.5,-2.5,0.0),App.Vector(7.5,2.5,0.0)))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Line(App.Vector(17.5,-5.0,0.0),App.Vector(7.5,-2.5,0.0)))
    App.ActiveDocument.Symbol_US.addGeometry(Part.Line(App.Vector(17.5,-5.0,0.0),App.Vector(17.5,5.0,0.0)))
    Gui.getDocument(App.ActiveDocument.Name).resetEdit()
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_US").LineColor = (0.00,0.00,0.00)
    App.ActiveDocument.recompute()

    App.activeDocument().addObject('Drawing::FeatureViewPart','SymbolUS')
    App.activeDocument().SymbolUS.Source = App.activeDocument().Symbol_US
    App.activeDocument().SymbolUS.Direction = (0.0,0.0,1.0)
    App.activeDocument().SymbolUS.X = depx
    App.activeDocument().SymbolUS.Y = depy
    App.activeDocument().SymbolUS.Scale = 0.8
    App.activeDocument().Page.addObject(App.activeDocument().SymbolUS)
    App.ActiveDocument.recompute()
#    App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_US")
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_US").Visibility = False

try:
    DESIGNED_BY = App.activeDocument().getObject("Page").EditableTexts[0] #lineEdit01 DESIGNED_BY
    CREATION_DATE = App.activeDocument().getObject("Page").EditableTexts[1] #lineEdit02 CREATION_DATE date
    CREA_DATE = CREATION_DATE[0:10] # lineEdit02h date
    CREA_TIME = CREATION_DATE[13:21] # lineEdit02h heure
    CHECKED_BY = App.activeDocument().getObject("Page").EditableTexts[2] # lineEdit03
    CHECK_DATE = App.activeDocument().getObject("Page").EditableTexts[3] # lineEdit04 date
    CHEC_DATE = CHECK_DATE[0:10] # lineEdit04 date
    CHEC_TIME = CHECK_DATE[13:21] # lineEdit04h heure
    SIZE = "A3"  # lineEdit05
    SCALE = App.activeDocument().getObject("Page").EditableTexts[4] # lineEdit06
    WEIGHT = App.activeDocument().getObject("Page").EditableTexts[5] # lineEdit07
    DRAWING_NUMBER = App.activeDocument().getObject("Page").EditableTexts[6] # lineEdit08
    SHEET = App.activeDocument().getObject("Page").EditableTexts[7] # lineEdit09
    TITLE = App.activeDocument().getObject("Page").EditableTexts[8] # textEdit_01
    DESCRIPTION = App.activeDocument().getObject("Page").EditableTexts[9] # textEdit_02

except:
    errorDialog("erreur cartouche")
try:
    try:
        lineEdit18 = App.activeDocument().getObject("Note_I").Text[0] 
    except:
        lineEdit18 = ""
    try:
        lineEdit17 = App.activeDocument().getObject("Note_H").Text[0] 
    except:
        lineEdit17 = ""
    try:
        lineEdit16 = App.activeDocument().getObject("Note_G").Text[0] 
    except:
        lineEdit16 = ""
    try:
        lineEdit15 = App.activeDocument().getObject("Note_F").Text[0] 
    except:
        lineEdit15 = ""
    try:
        lineEdit14 = App.activeDocument().getObject("Note_E").Text[0] 
    except:
        lineEdit14 = ""
    try:
        lineEdit13 = App.activeDocument().getObject("Note_D").Text[0] 
    except:
        lineEdit13 = ""
    try:
        lineEdit12 = App.activeDocument().getObject("Note_C").Text[0] 
    except:
        lineEdit12 = ""
    try:
        lineEdit11 = App.activeDocument().getObject("Note_B").Text[0] 
    except:
        lineEdit11 = ""
    try:
        lineEdit10 = App.activeDocument().getObject("Note_A").Text[0] 
    except:
        lineEdit10 = ""
    try:
        lineEdit20 = App.activeDocument().getObject("CopyRight").Text[0] 
    except:
        lineEdit20 = ""
except:
    errorDialog("erreur note")

class Ui_MainWindow(object):

    def __init__(self, MainWindow):
        self.window = MainWindow
#___________________________________________________________________________________

        MainWindow.setObjectName(_fromUtf8("MainWindow"))
        MainWindow.resize(810, 440)
        MainWindow.setMaximumSize(QtCore.QSize(810, 480))
        self.centralWidget = QtGui.QWidget(MainWindow)
        self.centralWidget.setObjectName(_fromUtf8("centralWidget"))

#        self.pushButton01 = QtGui.QPushButton(self.centralWidget)
#        self.pushButton01.setGeometry(QtCore.QRect(115, 360, 93, 28))
#        self.pushButton01.setObjectName(_fromUtf8("pushButton01"))
#        self.pushButton01.clicked.connect(self.on_pushButton01_clicked) #connection pushButton01

        self.pushButton02 = QtGui.QPushButton(self.centralWidget)
        self.pushButton02.setGeometry(QtCore.QRect(225, 360, 93, 28))
        self.pushButton02.setObjectName(_fromUtf8("pushButton02"))
        self.pushButton02.clicked.connect(self.on_pushButton02_clicked) #connection pushButton02

        self.pushButton03 = QtGui.QPushButton(self.centralWidget)
        self.pushButton03.setGeometry(QtCore.QRect(335, 360, 93, 28))
        self.pushButton03.setObjectName(_fromUtf8("pushButton03"))
        self.pushButton03.clicked.connect(self.on_pushButton03_clicked) #connection pushButton03

        self.pushButton04 = QtGui.QPushButton(self.centralWidget)
        self.pushButton04.setGeometry(QtCore.QRect(445, 360, 93, 28))
        self.pushButton04.setObjectName(_fromUtf8("pushButton04"))
        self.pushButton04.clicked.connect(self.on_pushButton04_clicked) #connection pushButton04

        self.pushButton05 = QtGui.QPushButton(self.centralWidget)
        self.pushButton05.setGeometry(QtCore.QRect(555, 360, 93, 28))
        self.pushButton05.setObjectName(_fromUtf8("pushButton05"))
        self.pushButton05.clicked.connect(self.on_pushButton05_clicked) #connection pushButton05

        self.pushButton06 = QtGui.QPushButton(self.centralWidget)
        self.pushButton06.setGeometry(QtCore.QRect(170, 56, 20, 20))
        self.pushButton06.setObjectName(_fromUtf8("pushButton06"))
        self.pushButton06.clicked.connect(self.on_pushButton06_clicked) #connection pushButton06

        self.pushButton07 = QtGui.QPushButton(self.centralWidget)
        self.pushButton07.setGeometry(QtCore.QRect(190, 56, 20, 20))
        self.pushButton07.setObjectName(_fromUtf8("pushButton07"))
        self.pushButton07.clicked.connect(self.on_pushButton07_clicked) #connection pushButton07

        self.pushButton08 = QtGui.QPushButton(self.centralWidget)
        self.pushButton08.setGeometry(QtCore.QRect(170, 136, 20, 20))
        self.pushButton08.setObjectName(_fromUtf8("pushButton08"))
        self.pushButton08.clicked.connect(self.on_pushButton08_clicked) #connection pushButton08

        self.pushButton09 = QtGui.QPushButton(self.centralWidget)
        self.pushButton09.setGeometry(QtCore.QRect(190, 136, 20, 20))
        self.pushButton09.setObjectName(_fromUtf8("pushButton09"))
        self.pushButton09.clicked.connect(self.on_pushButton09_clicked) #connection pushButton09

        self.pushButton10 = QtGui.QPushButton(self.centralWidget)
        self.pushButton10.setGeometry(QtCore.QRect(100, 220, 101, 20))
        self.pushButton10.setObjectName(_fromUtf8("pushButton10"))
        self.pushButton10.clicked.connect(self.on_pushButton10_clicked) #connection pushButton10

        self.lineEdit_01 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_01.setGeometry(QtCore.QRect(20, 20, 181, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_01.setFont(font)
        self.lineEdit_01.setObjectName(_fromUtf8("lineEdit_01"))
        self.lineEdit_01.setText(DESIGNED_BY)

        self.lineEdit_02 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_02.setGeometry(QtCore.QRect(20, 60, 82, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_02.setFont(font)
        self.lineEdit_02.setObjectName(_fromUtf8("lineEdit_02"))
        self.lineEdit_02.setText(CREA_DATE)

        self.lineEdit_02h = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_02h.setGeometry(QtCore.QRect(98, 60, 72, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_02h.setFont(font)
        self.lineEdit_02h.setObjectName(_fromUtf8("lineEdit_02h"))
        self.lineEdit_02h.setText(CREA_TIME)

        self.lineEdit_03 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_03.setGeometry(QtCore.QRect(20, 100, 181, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_03.setFont(font)
        self.lineEdit_03.setObjectName(_fromUtf8("lineEdit_03"))
        self.lineEdit_03.setText(CHECKED_BY)

        self.lineEdit_04 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_04.setGeometry(QtCore.QRect(20, 140, 82, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_04.setFont(font)
        self.lineEdit_04.setObjectName(_fromUtf8("lineEdit_04"))
        self.lineEdit_04.setText(CHEC_DATE)

        self.lineEdit_04h = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_04h.setGeometry(QtCore.QRect(98, 140, 72, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_04h.setFont(font)
        self.lineEdit_04h.setObjectName(_fromUtf8("lineEdit_04h"))
        self.lineEdit_04h.setText(CHEC_TIME)

        self.lineEdit_05 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_05.setGeometry(QtCore.QRect(20, 180, 61, 61))
        font = QtGui.QFont()
        font.setPointSize(17)
        font.setBold(False)
        font.setWeight(50)
        self.lineEdit_05.setFont(font)
        self.lineEdit_05.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_05.setObjectName(_fromUtf8("lineEdit_05"))
        self.lineEdit_05.setText(SIZE)

        self.lineEdit_06 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_06.setGeometry(QtCore.QRect(20, 280, 61, 41))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_06.setFont(font)
        self.lineEdit_06.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_06.setObjectName(_fromUtf8("lineEdit_06"))
        self.lineEdit_06.setText(SCALE)

        self.lineEdit_07 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_07.setGeometry(QtCore.QRect(100, 280, 101, 41))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_07.setFont(font)
        self.lineEdit_07.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_07.setObjectName(_fromUtf8("lineEdit_07"))
        self.lineEdit_07.setText(WEIGHT)

        self.lineEdit_08 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_08.setGeometry(QtCore.QRect(220, 280, 341, 41))
        self.lineEdit_08.setObjectName(_fromUtf8("lineEdit_08"))
        self.lineEdit_08.setText(DRAWING_NUMBER)

        self.lineEdit_09 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_09.setGeometry(QtCore.QRect(570, 280, 81, 41))
        self.lineEdit_09.setObjectName(_fromUtf8("lineEdit_09"))
        self.lineEdit_09.setText(SHEET)

        self.lineEdit_10 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_10.setGeometry(QtCore.QRect(690, 290, 101, 30))
        self.lineEdit_10.setObjectName(_fromUtf8("lineEdit_10"))
        self.lineEdit_10.setText(lineEdit10)

        self.lineEdit_11 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_11.setGeometry(QtCore.QRect(690, 260, 101, 30))
        self.lineEdit_11.setObjectName(_fromUtf8("lineEdit_11"))
        self.lineEdit_11.setText(lineEdit11)

        self.lineEdit_12 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_12.setGeometry(QtCore.QRect(690, 230, 101, 30))
        self.lineEdit_12.setObjectName(_fromUtf8("lineEdit_12"))
        self.lineEdit_12.setText(lineEdit12)

        self.lineEdit_13 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_13.setGeometry(QtCore.QRect(690, 200, 101, 30))
        self.lineEdit_13.setObjectName(_fromUtf8("lineEdit_13"))
        self.lineEdit_13.setText(lineEdit13)

        self.lineEdit_14 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_14.setGeometry(QtCore.QRect(690, 170, 101, 30))
        self.lineEdit_14.setObjectName(_fromUtf8("lineEdit_14"))
        self.lineEdit_14.setText(lineEdit14)

        self.lineEdit_15 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_15.setGeometry(QtCore.QRect(690, 140, 101, 30))
        self.lineEdit_15.setObjectName(_fromUtf8("lineEdit_15"))
        self.lineEdit_15.setText(lineEdit15)

        self.lineEdit_16 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_16.setGeometry(QtCore.QRect(690, 110, 101, 30))
        self.lineEdit_16.setObjectName(_fromUtf8("lineEdit_16"))
        self.lineEdit_16.setText(lineEdit16)

        self.lineEdit_17 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_17.setGeometry(QtCore.QRect(690, 80, 101, 30))
        self.lineEdit_17.setObjectName(_fromUtf8("lineEdit_17"))
        self.lineEdit_17.setText(lineEdit17)

        self.lineEdit_18 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_18.setGeometry(QtCore.QRect(690, 50, 101, 30))
        self.lineEdit_18.setObjectName(_fromUtf8("lineEdit_18"))
        self.lineEdit_18.setText(lineEdit18)

        self.lineEdit_20 = QtGui.QLineEdit(self.centralWidget) # Copyright
        self.lineEdit_20.setGeometry(QtCore.QRect(20, 330, 771, 22))
        self.lineEdit_20.setObjectName(_fromUtf8("lineEdit_20"))
        self.lineEdit_20.setText(lineEdit20)

        self.textEdit_01 = QtGui.QTextEdit(self.centralWidget)
        self.textEdit_01.setGeometry(QtCore.QRect(220, 20, 431,60 ))
        font = QtGui.QFont()
        font.setPointSize(15)
        font.setBold(True)
        font.setWeight(75)
        self.textEdit_01.setFont(font)
        self.textEdit_01.setObjectName(_fromUtf8("textEdit_01"))
        self.textEdit_01.setText(TITLE)

        self.textEdit_02 = QtGui.QTextEdit(self.centralWidget)
        self.textEdit_02.setGeometry(QtCore.QRect(220, 90, 431, 60))
        self.textEdit_02.setObjectName(_fromUtf8("textEdit_02"))
        self.textEdit_02.setText(DESCRIPTION)

#        self.graphicsView_01 = QtGui.QGraphicsView(self.centralWidget)
#        self.graphicsView_01.setGeometry(QtCore.QRect(100, 160, 101, 81))
#        brush = QtGui.QBrush(QtGui.QColor(0, 170, 255))
#        brush.setStyle(QtCore.Qt.NoBrush)
#        self.graphicsView_01.setBackgroundBrush(brush)
#        self.graphicsView_01.setObjectName(_fromUtf8("graphicsView_01"))

        self.textEdit_03 = QtGui.QTextEdit(self.centralWidget)
        self.textEdit_03.setGeometry(QtCore.QRect(100, 160, 101, 55))
        self.textEdit_03.setAlignment(QtCore.Qt.AlignCenter)
        self.textEdit_03.setObjectName(_fromUtf8("textEdit_03"))
        self.textEdit_03.setText("Select your Symbol")

        self.graphicsView_02 = QtGui.QGraphicsView(self.centralWidget)
        self.graphicsView_02.setGeometry(QtCore.QRect(220, 160, 431, 81))#570, 160, 81, 81
        self.graphicsView_02.setObjectName(_fromUtf8("graphicsView_02"))

        self.label_01 = QtGui.QLabel(self.centralWidget)
        self.label_01.setGeometry(QtCore.QRect(20, 0, 91, 16))
        self.label_01.setObjectName(_fromUtf8("label_01"))

        self.label_02 = QtGui.QLabel(self.centralWidget)
        self.label_02.setGeometry(QtCore.QRect(20, 40, 53, 16))
        self.label_02.setObjectName(_fromUtf8("label_02"))

        self.label_03 = QtGui.QLabel(self.centralWidget)
        self.label_03.setGeometry(QtCore.QRect(20, 80, 101, 16))
        self.label_03.setObjectName(_fromUtf8("label_03"))

        self.label_04 = QtGui.QLabel(self.centralWidget)
        self.label_04.setGeometry(QtCore.QRect(20, 120, 91, 16))
        self.label_04.setObjectName(_fromUtf8("label_04"))

        self.label_05 = QtGui.QLabel(self.centralWidget)
        self.label_05.setGeometry(QtCore.QRect(20, 160, 53, 16))
        self.label_05.setObjectName(_fromUtf8("label_05"))

        self.label_06 = QtGui.QLabel(self.centralWidget)
        self.label_06.setGeometry(QtCore.QRect(20, 260, 53, 16))
        self.label_06.setObjectName(_fromUtf8("label_06"))

        self.label_07 = QtGui.QLabel(self.centralWidget)
        self.label_07.setGeometry(QtCore.QRect(100, 260, 101, 16))
        self.label_07.setObjectName(_fromUtf8("label_07"))

        self.label_08 = QtGui.QLabel(self.centralWidget)
        self.label_08.setGeometry(QtCore.QRect(220, 260, 121, 16))
        self.label_08.setObjectName(_fromUtf8("label_08"))

        self.label_09 = QtGui.QLabel(self.centralWidget)
        self.label_09.setGeometry(QtCore.QRect(570, 260, 53, 16))
        self.label_09.setObjectName(_fromUtf8("label_09"))

        self.label_10 = QtGui.QLabel(self.centralWidget)
        self.label_10.setGeometry(QtCore.QRect(670, 290, 16, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_10.setFont(font)
        self.label_10.setObjectName(_fromUtf8("label_10"))

        self.label_11 = QtGui.QLabel(self.centralWidget)
        self.label_11.setGeometry(QtCore.QRect(670, 260, 16, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_11.setFont(font)
        self.label_11.setObjectName(_fromUtf8("label_11"))

        self.label_12 = QtGui.QLabel(self.centralWidget)
        self.label_12.setGeometry(QtCore.QRect(670, 230, 16, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_12.setFont(font)
        self.label_12.setObjectName(_fromUtf8("label_12"))

        self.label_13 = QtGui.QLabel(self.centralWidget)
        self.label_13.setGeometry(QtCore.QRect(670, 200, 18, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_13.setFont(font)
        self.label_13.setObjectName(_fromUtf8("label_13"))

        self.label_14 = QtGui.QLabel(self.centralWidget)
        self.label_14.setGeometry(QtCore.QRect(670, 170, 15, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_14.setFont(font)
        self.label_14.setObjectName(_fromUtf8("label_14"))

        self.label_15 = QtGui.QLabel(self.centralWidget)
        self.label_15.setGeometry(QtCore.QRect(670, 140, 14, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_15.setFont(font)
        self.label_15.setObjectName(_fromUtf8("label_15"))

        self.label_16 = QtGui.QLabel(self.centralWidget)
        self.label_16.setGeometry(QtCore.QRect(670, 110, 18, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_16.setFont(font)
        self.label_16.setObjectName(_fromUtf8("label_16"))

        self.label_17 = QtGui.QLabel(self.centralWidget)
        self.label_17.setGeometry(QtCore.QRect(670, 80, 18, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_17.setFont(font)
        self.label_17.setObjectName(_fromUtf8("label_17"))

        self.label_18 = QtGui.QLabel(self.centralWidget)
        self.label_18.setGeometry(QtCore.QRect(670, 50, 10, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_18.setFont(font)
        self.label_18.setObjectName(_fromUtf8("label_18"))

        self.label_19 = QtGui.QLabel(self.centralWidget)
        self.label_19.setGeometry(QtCore.QRect(720, 15, 100, 33))
        self.label_19.setObjectName(_fromUtf8("label_19"))

        MainWindow.setCentralWidget(self.centralWidget)
        self.menuBar = QtGui.QMenuBar(MainWindow)
        self.menuBar.setGeometry(QtCore.QRect(0, 0, 810, 26))
        self.menuBar.setObjectName(_fromUtf8("menuBar"))
        MainWindow.setMenuBar(self.menuBar)
        self.statusBar = QtGui.QStatusBar(MainWindow)
        self.statusBar.setObjectName(_fromUtf8("statusBar"))
        MainWindow.setStatusBar(self.statusBar)

        self.retranslateUi(MainWindow)
        QtCore.QMetaObject.connectSlotsByName(MainWindow)

    def retranslateUi(self, MainWindow):
        try:
            MainWindow.setWindowFlags(PyQt4.QtCore.Qt.WindowStaysOnTopHint)  # PyQt4 cette fonction met la fenêtre en avant
        except Exception:
            MainWindow.setWindowFlags(PySide.QtCore.Qt.WindowStaysOnTopHint) # PySide cette fonction met la fenêtre en avant

        MainWindow.setWindowTitle(_translate("MainWindow", "Cartouche", None))
#        self.pushButton01.setText(_translate("MainWindow", "Position", None))
        self.pushButton02.setText(_translate("MainWindow", "Quitter", None))
        self.pushButton03.setText(_translate("MainWindow", "Memo", None))
        self.pushButton04.setText(_translate("MainWindow", "Nettoyer", None))
        self.pushButton05.setText(_translate("MainWindow", "Appliquer", None))
        self.pushButton06.setText(_translate("MainWindow", "D.", None))
        self.pushButton07.setText(_translate("MainWindow", "H.", None))
        self.pushButton08.setText(_translate("MainWindow", "D.", None))
        self.pushButton09.setText(_translate("MainWindow", "H.", None))
        self.pushButton10.setText(_translate("MainWindow", "Symbole EU", None))


        self.label_01.setText(_translate("MainWindow", "Designed by :", None))
        self.label_02.setText(_translate("MainWindow", "Date :", None))
        self.label_03.setText(_translate("MainWindow", "Checked by :", None))
        self.label_04.setText(_translate("MainWindow", "Date :", None))
        self.label_05.setText(_translate("MainWindow", "Size :", None))
        self.label_06.setText(_translate("MainWindow", "Scale :", None))
        self.label_07.setText(_translate("MainWindow", "Weight (Kg) :", None))
        self.label_08.setText(_translate("MainWindow", "Drawing number :", None))
        self.label_09.setText(_translate("MainWindow", "Sheet :", None))
        self.label_10.setText(_translate("MainWindow", "A", None))
        self.label_11.setText(_translate("MainWindow", "B", None))
        self.label_12.setText(_translate("MainWindow", "C", None))
        self.label_13.setText(_translate("MainWindow", "D", None))
        self.label_14.setText(_translate("MainWindow", "E", None))
        self.label_15.setText(_translate("MainWindow", "F", None))
        self.label_16.setText(_translate("MainWindow", "G", None))
        self.label_17.setText(_translate("MainWindow", "H", None))
        self.label_18.setText(_translate("MainWindow", "I", None))
        self.label_19.setText(_translate("MainWindow", "Notes", None))
#______________________________________________________________________________________
    # Boutons
    def on_pushButton10_clicked(self):    # Bouton /Symbole
        if self.textEdit_03.toPlainText()=="Symbole US":
            self.pushButton10.setText(_translate("MainWindow", "Symbole US", None))
            self.textEdit_03.setText("Symbole EU")
            symbol_EU(247.5,263.5) #(247.5,263.5)
        else:
            self.pushButton10.setText(_translate("MainWindow", "Symbole EU", None))
            self.textEdit_03.setText("Symbole US")
            symbol_US(247.5,263.5) #(247.5,263.5)
    def on_pushButton09_clicked(self):    # Bouton /heure document
        self.lineEdit_04h.setText(str(heure()))
    def on_pushButton08_clicked(self):    # Bouton date/ document
        if self.textEdit_03.toPlainText()=="Symbole US":
            self.lineEdit_04.setText(str(dateUs()))
        else:
            self.lineEdit_04.setText(str(dateEu()))
    def on_pushButton07_clicked(self):    # Bouton /heure checked
        self.lineEdit_02h.setText(str(heure()))
    def on_pushButton06_clicked(self):    # Bouton date/ checked
        if self.textEdit_03.toPlainText()=="Symbole US":
            self.lineEdit_02.setText(str(dateUs()))
        else:
            self.lineEdit_02.setText(str(dateEu()))
    def on_pushButton05_clicked(self):    # Bouton Appliquer
        DESIGNED_BY = self.lineEdit_01.text()     
        CREATION_DATE = self.lineEdit_02.text()+" - "+self.lineEdit_02h.text()
        CHECKED_BY = self.lineEdit_03.text()
        CHECK_DATE = self.lineEdit_04.text()+" - "+self.lineEdit_04h.text()
        SIZE  = "A3" # self.lineEdit_05.text()
        SCALE = self.lineEdit_06.text()
        WEIGHT = self.lineEdit_07.text()
        DRAWING_NUMBER = self.lineEdit_08.text()
        SHEET = self.lineEdit_09.text()
        TITLE = self.textEdit_01.toPlainText()
        DESCRIPTION = self.textEdit_02.toPlainText()
        SYMBOL = self.textEdit_03.toPlainText()
        try:
            FreeCAD.getDocument (App.ActiveDocument.Name).getObject("Page").EditableTexts = [unicode(DESIGNED_BY, 'utf-8'), unicode(CREATION_DATE, 'utf-8'), unicode(CHECKED_BY, 'utf-8'), unicode(CHECK_DATE, 'utf-8'), unicode(SCALE, 'utf-8'), unicode(WEIGHT, 'utf-8'), unicode(DRAWING_NUMBER, 'utf-8'), unicode(SHEET, 'utf-8'), unicode(TITLE, 'utf-8'), unicode(DESCRIPTION, 'utf-8'),]
        except Exception:
            FreeCAD.getDocument (App.ActiveDocument.Name).getObject("Page").EditableTexts = [DESIGNED_BY.encode('utf-8'), CREATION_DATE.encode('utf-8'), CHECKED_BY.encode('utf-8'), CHECK_DATE.encode('utf-8'), SCALE.encode('utf-8'), WEIGHT.encode('utf-8'), DRAWING_NUMBER.encode('utf-8'), SHEET.encode('utf-8'), TITLE.encode('utf-8'), DESCRIPTION.encode('utf-8'),]

        #print App.ActiveDocument.Name
        try:
            App.activeDocument().removeObject('Note_I')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_H')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_G')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_F')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_E')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_D')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_C')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_B')
        except:
            None
        try:
            App.activeDocument().removeObject('Note_A')
        except:
            None
        try:
            App.activeDocument().removeObject('CopyRight')
        except:
            None
        if self.lineEdit_18.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_I')
            App.activeDocument().Note_I.X = 391.0
            App.activeDocument().Note_I.Y = 232
            App.activeDocument().Note_I.Scale = 3.0
            App.activeDocument().Note_I.Text = str(self.lineEdit_18.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_I)
        if self.lineEdit_17.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_H')
            App.activeDocument().Note_H.X = 391.0
            App.activeDocument().Note_H.Y = 238.8
            App.activeDocument().Note_H.Scale = 3.0
            App.activeDocument().Note_H.Text = str(self.lineEdit_17.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_H)
        if self.lineEdit_16.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_G')
            App.activeDocument().Note_G.X = 391.0
            App.activeDocument().Note_G.Y = 245.4
            App.activeDocument().Note_G.Scale = 3.0
            App.activeDocument().Note_G.Text = str(self.lineEdit_16.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_G)
        if self.lineEdit_15.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_F')
            App.activeDocument().Note_F.X = 391.0
            App.activeDocument().Note_F.Y = 252
            App.activeDocument().Note_F.Scale = 3.0
            App.activeDocument().Note_F.Text = str(self.lineEdit_15.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_F)
        if self.lineEdit_14.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_E')
            App.activeDocument().Note_E.X = 391.0
            App.activeDocument().Note_E.Y = 258.6
            App.activeDocument().Note_E.Scale = 3.0
            App.activeDocument().Note_E.Text = str(self.lineEdit_14.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_E)
        if self.lineEdit_13.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_D')
            App.activeDocument().Note_D.X = 391.0
            App.activeDocument().Note_D.Y = 265.2
            App.activeDocument().Note_D.Scale = 3.0
            App.activeDocument().Note_D.Text = str(self.lineEdit_13.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_D)
        if self.lineEdit_12.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_C')
            App.activeDocument().Note_C.X = 391.0
            App.activeDocument().Note_C.Y = 271.8
            App.activeDocument().Note_C.Scale = 3.0
            App.activeDocument().Note_C.Text =  str(self.lineEdit_12.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_C)
        if self.lineEdit_11.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_B')
            App.activeDocument().Note_B.X = 391.0
            App.activeDocument().Note_B.Y = 278.4
            App.activeDocument().Note_B.Scale = 3.0
            App.activeDocument().Note_B.Text = str(self.lineEdit_11.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_B)
        if self.lineEdit_10.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','Note_A')
            App.activeDocument().Note_A.X = 391.0
            App.activeDocument().Note_A.Y = 285.0
            App.activeDocument().Note_A.Scale = 3.0
            App.activeDocument().Note_A.Text = str(self.lineEdit_10.text())
            App.activeDocument().Page.addObject(App.activeDocument().Note_A)
        if self.lineEdit_20.text() != "":
            App.activeDocument().addObject('Drawing::FeatureViewAnnotation','CopyRight')
            App.activeDocument().CopyRight.X = 221
            App.activeDocument().CopyRight.Y = 286
            App.activeDocument().CopyRight.Scale = 3.0
            App.activeDocument().CopyRight.Text = str(self.lineEdit_20.text())
            App.activeDocument().Page.addObject(App.activeDocument().CopyRight)

        App.ActiveDocument.recompute()

    def on_pushButton04_clicked(self):    # Bouton nettoyer
        try:
            App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_US")
        except:
            None
        try:
            App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_EU")
        except:
            None
        try:
            App.getDocument(App.ActiveDocument.Name).removeObject("SymbolUS")
        except:
            None
        try:
            App.getDocument(App.ActiveDocument.Name).removeObject("SymbolEU")
        except:
            None
        DESIGNED_BY = ""    ;self.lineEdit_01.setText("")
        CREATION_DATE = ""  ;self.lineEdit_02.setText("")
        self.lineEdit_02h.setText("")
        CHECKED_BY = ""     ;self.lineEdit_03.setText("")
        CHECK_DATE = ""     ;self.lineEdit_04.setText("")
        self.lineEdit_04h.setText("")
        SIZE  = "A3"        ;self.lineEdit_05.setText("A3")
        SCALE = ""          ;self.lineEdit_06.setText("")
        WEIGHT = ""         ;self.lineEdit_07.setText("")
        DRAWING_NUMBER = "" ;self.lineEdit_08.setText("")
        SHEET = ""          ;self.lineEdit_09.setText("")
        TITLE = ""          ;self.textEdit_01.setText("")
        DESCRIPTION = ""    ;self.textEdit_02.setText("")
        
        self.lineEdit_10.setText("")
        self.lineEdit_11.setText("")
        self.lineEdit_12.setText("")
        self.lineEdit_13.setText("")
        self.lineEdit_14.setText("")
        self.lineEdit_15.setText("")
        self.lineEdit_16.setText("")
        self.lineEdit_17.setText("")
        self.lineEdit_18.setText("")
        self.lineEdit_20.setText("")

    def on_pushButton03_clicked(self):    # Bouton Memo
        self.lineEdit_01.setText(DESIGNED_BY)
        self.lineEdit_02.setText(CREA_DATE)
        self.lineEdit_02h.setText(CREA_TIME)
        self.lineEdit_03.setText(CHECKED_BY)
        self.lineEdit_04.setText(CHEC_DATE)
        self.lineEdit_04h.setText(CHEC_TIME)
        self.lineEdit_05.setText(SIZE)
        self.lineEdit_06.setText(SCALE)
        self.lineEdit_07.setText(WEIGHT)
        self.lineEdit_08.setText(DRAWING_NUMBER)
        self.lineEdit_09.setText(SHEET)
        self.textEdit_01.setText(TITLE)
        self.textEdit_02.setText(DESCRIPTION)

        self.lineEdit_18.setText(lineEdit18)
        self.lineEdit_17.setText(lineEdit17)
        self.lineEdit_16.setText(lineEdit16)
        self.lineEdit_15.setText(lineEdit15)
        self.lineEdit_14.setText(lineEdit14)
        self.lineEdit_13.setText(lineEdit13)
        self.lineEdit_12.setText(lineEdit12)
        self.lineEdit_11.setText(lineEdit11)
        self.lineEdit_10.setText(lineEdit10)
        self.lineEdit_20.setText(lineEdit20)

    def on_pushButton02_clicked(self):    # Bouton Quitter
        App.Console.PrintMessage("Terminé\r\n")
        self.window.hide()
#    def on_pushButton01_clicked(self):    # Bouton appel de Position
#        MainWindow.resize(210, 480)
#        executer()
#        MainWindow.resize(810, 480)
#______________________________________________________________________________________

MainWindow = QtGui.QMainWindow()
ui = Ui_MainWindow(MainWindow)
MainWindow.show()

}}

## Autre

Les champs n\'ont pas de limite de longueur, vérifiez votre cartouche.

Ce programme crée sur votre projet un dessin représentant le symbole régional de projection, n\'y touchez pas il est enregistré sous forme cachée donc invisible.

Si vous voulez qu\'il soit effacé dé-commentez ces lignes commentées et vice versa


```python

#    App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_EU")
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_EU").Visibility = False
et
#    App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_US")
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_US").Visibility = False
```

(j\'avais quelque fois une erreur à l\'exécution quand le symbole était effacé)

Ce module travaille avec la feuille de mise en plan incluse dans FreeCAD cette feuille s\'appelle **Page**, ne pas modifier le nom de cette feuille !

## Révision

ver 0.3 le 02/07/2014 conversion pour utilisation avec **PyQt4** et **PySide**


</div>


</div>





<div class="mw-collapsible mw-collapsed toccolours">

# Macro CartoucheFC Full 


<div class="mw-collapsible-content">


{{Macro
|Name=Macro_CartoucheFC_Full
|Icon=Macro_CartoucheFC_Full.png
|Description=This macro is a complete application, it allows to fill the cartridge of the drawing sheet with full editabletext (For [Drawing Workbench](Drawing_Workbench.md)).
|Author=Mario52
|Version=00.10
|Date=2017-02-15
|FCVersion=All version using Drawing Workbench
|Download=[https://www.freecadweb.org/wiki/images/6/68/Macro_CartoucheFC_Full.png ToolBar Icon]
}}

## Description 

This macro is a complete application, it allows to fill simply all the fields of the cartridge

Choice in the page Misc_templates_Full

Here the order of filling in the line FreeCAD texteditable. The date and time fields are separated by a **\"space negative space\" \" - \"** and constitute a single line textedit.

<img alt="CartoucheFC_Full" src=images/Macro_CartoucheFC_Full_00.png  style="width:680px;">

## Usage 

**PS: Some characters such as & \$ are not accepted (and possibly other special characters).**

If you have any questions or want to add a function, you can address you on the french forum [Remplir cartouche](http://forum.freecadweb.org/viewtopic.php?f=12&t=2049)

-   The window remains above other Windows, thereby controlling the cartridge without leaving the program.
-   Copy the code into a file named **Macro_CartoucheFC_Full.FCMacro** and place it in your usual macros directory.
-   After you have created your drawing sheet using the Drawing of FreeCAD module, run the macro **Macro_CartoucheFC_Full**.
-   At the opening, the program will register in memory all data already present in the cartridge of the sheet (if they are filled), all these data will be automatically returned to using the button ** Memo** and kept in memory until the closure of the programme.
-   First select your page to work
-   Date button ** D.** and time ** H.** displayed the date and time of the system.

  -The date format depends on the selected symbol **EU** or **US** which determines the regional format. Change does not happen automatically (for the case or you have entered a date manually) you must again click buttons dates if you change the symbol (check before printing).

-   Choice your format page
-   Button **Symbole EU** or US change the meaning of the symbol of projection \"Select your Symbol\" is displayed by default, and then the active symbol appears. Click on the button and check the leaf symbol, click a second time to modify the symbol.

  -The choice of this symbol, affects the date format **EU = dd/MM/yyyy** and **US = MM/dd/yyyy**.

  -**Attention**: this command does not pass through the button **Apply** and immediately changes the symbol to each presses on the key, always check if you have the appropriate symbol on your worksheet.

-   Button **Clean** Clears all fields in the cartridge. You can revert to the original data using the button **Memo**.
-   Button **Apply** saves all fields of the cartridge in the sheet. You can revert to the original data using the button **Memo** (except for the regional symbol that works in independent and is effective immediately).

## Code 

The icon for you toolBar ![](images/Macro_CartoucheFC_Full.png )

**Macro_CartoucheFC_Full.FCMacro**


{{MacroCode|code=
# -*- coding: utf-8 -*-
from __future__ import unicode_literals
"""
***************************************************************************
*   Copyright (c) 2014 2016 2017 <mario52>                                *
*                                                                         *
*   This file is a supplement to the FreeCAD CAx development system.      *
*                                                                         *
*   This program is free software; you can redistribute it and/or modify  *
*   it under the terms of the GNU Lesser General Public License (LGPL)    *
*   as published by the Free Software Foundation; either version 2 of     *
*   the License, or (at your option) any later version.                   *
*   for detail see the LICENCE text file.                                 *
*                                                                         *
*   This software is distributed in the hope that it will be useful,      *
*   but WITHOUT ANY WARRANTY; without even the implied warranty of        *
*   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the         *
*   GNU Library General Public License for more details.                  *
*                                                                         *
*   You should have received a copy of the GNU Library General Public     *
*   License along with this macro; if not, write to the Free Software     *
*   Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  *
*   USA                                                                   *
***************************************************************************
*           WARNING! All changes in this file will be lost and            *  
*                  may cause malfunction of the program                   *
***************************************************************************
"""
#OS: Windows 10
#Word size of OS: 64-bit
#Word size of FreeCAD: 64-bit
#Version: 0.16.6706 (Git)
#Build type: Release
#Branch: releases/FreeCAD-0-16
#Hash: f86a4e411ff7848dea98d7242f43b7774bee8fa0
#Python version: 2.7.8
#Qt version: 4.8.7
#Coin version: 4.0.0a
#OCC version: 6.8.0.oce-0.17

__title__   = "Macro_CartoucheFC_Full"
__author__  = "Mario52"
__url__     = "http://www.freecadweb.org/index-fr.html"
__Wiki__    = "http://www.freecadweb.org/wiki/Macro_CartoucheFC_Full"
__version__ = "00.10"
__date__    = "15/02/2017"

__Requires__ = ("all version and freecad " +
" DESIGNED_BY, CREATION_DATE, CHECKED_BY, CHECK_DATE, SIZE, SCALE, WEIGHT, DRAWING_NUMBER, SHEET, " +
" TITLE, DESCRIPTION, COMPANY, COPYRIGHT, Note_A, Note_B, Note_C, Note_D, Note_E, Note_F, Note_G, Note_H, Note_I" )
__Template__ = " A3_Landscape_xx_FULL.svg, A3_Portrait_xx_FULL, A4_Landscape_xx_FULL.svg, A4_Portrait_xx_FULL"
__Template_Link__ = "http://www.freecadweb.org/wiki/index.php?title=Misc_templates_Full"

import PySide
from PySide import QtCore, QtGui

import Draft, Part, FreeCAD, math, PartGui, FreeCADGui
from math import sqrt, pi, sin, cos, asin
from FreeCAD import Base

def utf8(unio):
    return unicode(unio).encode('UTF8')

global path
#path = FreeCAD.ConfigGet("AppHomePath")
path = FreeCAD.ConfigGet("UserAppData")

global PageActive      ; PageActive  = "Select your page" # essais 
#global PageActive      ; PageActive  = "Page" # page active
global DESIGNED_BY     ; DESIGNED_BY = ""     # lineEdit01 DESIGNED_BY
global MDESIGNED_BY    ; MDESIGNED_BY = ""    # 
global CREATION_DATE   ; CREATION_DATE = ""   # lineEdit02 CREATION_DATE date
global MCREATION_DATE  ; MCREATION_DATE = ""  # 
global CREA_DATE       ; CREA_DATE = ""       # lineEdit02h date
global MCREA_DATE      ; MCREA_DATE = ""      # 
global CREA_TIME       ; CREA_TIME = ""       # lineEdit02h heure
global MCREA_TIME      ; MCREA_TIME = ""      # 
global CHECKED_BY      ; CHECKED_BY = ""      # lineEdit03
global MCHECKED_BY     ; MCHECKED_BY = ""     # 
global CHECK_DATE      ; CHECK_DATE = ""      # lineEdit04 date
global MCHECK_DATE     ; MCHECK_DATE = ""     # 
global CHEC_DATE       ; CHEC_DATE = ""       # lineEdit04 date
global MCHEC_DATE      ; MCHEC_DATE = ""      # 
global CHEC_TIME       ; CHEC_TIME = ""       # lineEdit04h heure
global MCHEC_TIME      ; MCHEC_TIME = ""      # 
global SIZE            ; SIZE = ""            # lineEdit05
global MSIZE           ; MSIZE = ""           # 
global SCALE           ; SCALE =  ""          # lineEdit06
global MSCALE          ; MSCALE =  ""         # 
global WEIGHT          ; WEIGHT =  ""         # lineEdit07
global MWEIGHT         ; MWEIGHT =  ""        # 
global DRAWING_NUMBER  ; DRAWING_NUMBER = ""  # lineEdit08
global MDRAWING_NUMBER ; MDRAWING_NUMBER = "" # 
global SHEET           ; SHEET =  ""          # lineEdit09
global MSHEET          ; MSHEET =  ""         # 
global TITLE           ; TITLE =  ""          # textEdit_01
global MTITLE          ; MTITLE =  ""         # 
global DESCRIPTION     ; DESCRIPTION =  ""    # textEdit_02
global MDESCRIPTION    ; MDESCRIPTION = ""    # 
global COMPANY         ; COMPANY = ""         # textEdit_02b
global MCOMPANY        ; MCOMPANY = ""        # 
global COPYRIGHT       ; COPYRIGHT = ""       # lineEdit_20
global MCOPYRIGHT      ; MCOPYRIGHT = ""      # 
global Note_A          ; Note_A = ""          # lineEdit_10
global MNote_A         ; MNote_A = ""         # 
global Note_B          ; Note_B = ""          # lineEdit_11
global MNote_B         ; MNote_B = ""         # 
global Note_C          ; Note_C = ""          # lineEdit_12
global MNote_C         ; MNote_C = ""         # 
global Note_D          ; Note_D = ""          # lineEdit_13
global MNote_D         ; MNote_D = ""         # 
global Note_E          ; Note_E = ""          # lineEdit_14
global MNote_E         ; MNote_E = ""         # 
global Note_F          ; Note_F = ""          # lineEdit_15
global MNote_F         ; MNote_F = ""         # 
global Note_G          ; Note_G = ""          # lineEdit_16
global MNote_G         ; MNote_G = ""         # 
global Note_H          ; Note_H = ""          # lineEdit_17
global MNote_H         ; MNote_H = ""         # 
global Note_I          ; Note_I = ""          # lineEdit_18
global MNote_I         ; MNote_I = ""         # 

global SymbolSwitch    ; SymbolSwitch = 1     # 0=US 1=EU
global ui              ; ui     = ""

def heure():
    return QtCore.QTime().currentTime().toString('hh:mm:ss')
def dateEu():
    return QtCore.QDate().currentDate().toString('dd/MM/yyyy') # forme euro
def dateUK():
    return QtCore.QDate().currentDate().toString('yyyy/MM/dd') # forme UK
def dateUs():
    return QtCore.QDate().currentDate().toString('MM/dd/yyyy') # forme US
def dateComp():
    return QtCore.QDate().currentDate().toString('dddd d MMMM yyyy') # Retourne "dimanche 20 Juillet 77"

try:
    _fromUtf8 = QtCore.QString.fromUtf8
except AttributeError:
    def _fromUtf8(s):
        return s
try:
    _encoding = QtGui.QApplication.UnicodeUTF8
    def _translate(context, text, disambig):
        return QtGui.QApplication.translate(context, text, disambig, _encoding)
except AttributeError:
    def _translate(context, text, disambig):
        return QtGui.QApplication.translate(context, text, disambig)

def errorDialog(msg):
    diag = QtGui.QMessageBox(QtGui.QMessageBox.Critical,u"Error Message",msg)
    diag.setWindowFlags(PySide.QtCore.Qt.WindowStaysOnTopHint) # cette fonction met la fenetre en avant
    diag.exec_()

def symbol_EU(depx, depy, scale):    #symbol_EU =O
    global PageActive
    global ui

    try:
        page = App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0]
    except Exception:
        page = App.activeDocument().getObjectsByLabel(PageActive)[0]if len(str(page)) != 2:
        comP   = []
        nameL  = []
        if "Page" in (page.Name):
            for ii in (page.Group):
                if ((ii.Label) == "Symbol_EU") or ((ii.Label) == "Symbol_US") :
                    App.activeDocument().removeObject(ii.Name)

        points=[FreeCAD.Vector(-7.5,0.0,0.0),FreeCAD.Vector(20.0,0.0,0.0)]
        i = Draft.makeWire(points,closed=False,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        points=[FreeCAD.Vector(12.5,7.5,0.0),FreeCAD.Vector(12.5,-7.5,0.0)]
        i = Draft.makeWire(points,closed=False,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        points=[FreeCAD.Vector(-5,2.5,0.0),FreeCAD.Vector(5.0,5.0,0.0),FreeCAD.Vector(5.0,-5.0,0.0),FreeCAD.Vector(-5.0,-2.5,0.0)]
        i = Draft.makeWire(points,closed=True,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        pl=FreeCAD.Placement()
        pl.Rotation.Q=(0.0,-0.0,-0.0,1.0)
        pl.Base=FreeCAD.Vector(12.5,-0.0,0.0)
        i = Draft.makeCircle(radius=2.5,placement=pl,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        i = Draft.makeCircle(radius=5.0,placement=pl,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)    comp = Part.makeCompound(comP)
        Part.show(comp)
        App.ActiveDocument.ActiveObject.Label = "Symbol_EU"    obj = FreeCAD.ActiveDocument.ActiveObject
        obj.ViewObject.LineColor = (0.0,0.0,0.0)
        obj.ViewObject.Visibility = False
        
        obj2 = Draft.makeDrawingView(obj, page) 
        obj2.X = depx
        obj2.Y = depy
        obj2.Scale = scale #0.8    # A3
        obj2.Label = "Symbol_EU"    for i in nameL: App.activeDocument().removeObject(i)    App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0].addObject(obj)
        App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0].addObject(obj2)
        App.ActiveDocument.recompute()
    else:
        ui.pushButton05.setStyleSheet("background-color: red")       # This function gives a color button
        FreeCAD.Console.PrintError("Error selected page [ " + PageActive + " ]" + "\n")

def symbol_US(depx, depy, scale):    #symbol_US O=
    global PageActive
    global ui

    try:
        page = App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0]
    except Exception:
        page = App.activeDocument().getObjectsByLabel(PageActive)[0]

    if len(str(page)) != 2:
        comP   = []
        nameL  = []    if "Page" in (page.Name):
            for ii in (page.Group):
                if ((ii.Label) == "Symbol_EU") or ((ii.Label) == "Symbol_US") :
                    App.activeDocument().removeObject(ii.Name)

        points=[FreeCAD.Vector(-7.5,0.0,0.0),FreeCAD.Vector(20.0,0.0,0.0)]
        i = Draft.makeWire(points,closed=False,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        points=[FreeCAD.Vector(0.0,7.5,0.0),FreeCAD.Vector(0.0,-7.5,0.0)]
        i = Draft.makeWire(points,closed=False,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        points=[FreeCAD.Vector(7.5,2.5,0.0),FreeCAD.Vector(17.5,5.0,0.0),FreeCAD.Vector(17.5,-5.0,0.0),FreeCAD.Vector(7.5,-2.5,0.0)]
        i = Draft.makeWire(points,closed=True,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        pl=FreeCAD.Placement()
        pl.Rotation.Q=(0.0,-0.0,-0.0,1.0)
        pl.Base=FreeCAD.Vector(0.0,-0.0,0.0)
        i = Draft.makeCircle(radius=2.5,placement=pl,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        i = Draft.makeCircle(radius=5.0,placement=pl,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)    comp = Part.makeCompound(comP)
        Part.show(comp)
        App.ActiveDocument.ActiveObject.Label = "Symbol_US"    obj = FreeCAD.ActiveDocument.ActiveObject
        obj.ViewObject.LineColor = (0.0,0.0,0.0)
        obj.ViewObject.Visibility = False    obj2 = Draft.makeDrawingView(obj, page) 
        obj2.X = depx
        obj2.Y = depy
        obj2.Scale = scale #0.8    # A3
        obj2.Label = "Symbol_US"    for i in nameL: App.activeDocument().removeObject(i)    App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0].addObject(obj)
        App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0].addObject(obj2)
        App.ActiveDocument.recompute()
    else:
        ui.pushButton05.setStyleSheet("background-color: red")       # This function gives a color button
        FreeCAD.Console.PrintError("Error selected page [ " + PageActive + " ]" + "\n")

def memoEntree():
    global MDESIGNED_BY, MCREATION_DATE, MCREA_DATE  , MCREA_TIME, MCHECKED_BY, MCHECK_DATE
    global MCHEC_DATE  , MCHEC_TIME    , MSIZE       , MSCALE    , MWEIGHT    ,MDRAWING_NUMBER
    global MSHEET      , MTITLE        , MDESCRIPTION, MCOMPANY  , MCOPYRIGHT
    global MNote_A, MNote_B, MNote_C, MNote_D, MNote_E, MNote_F, MNote_G, MNote_H, MNote_I
    global PageActive

    try:
        page = App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0].Name
    except Exception:
        page = App.activeDocument().getObjectsByLabel(PageActive)[0]

    try:
        MDESIGNED_BY   = App.activeDocument().getObject(page).EditableTexts[0]  # lineEdit01 DESIGNED_BY
        MCREATION_DATE = App.activeDocument().getObject(page).EditableTexts[1]  # lineEdit02 CREATION_DATE date

        MCREA_DATE = MCREA_TIME = MCHEC_DATE = MCHEC_TIME = ""

        try:
            MCREA_DATE = MCREATION_DATE.split(" - ")[0]                         # lineEdit02h date
        except:
            MCREA_DATE = MCREATION_DATE
        try:
            MCREA_TIME = MCREATION_DATE.split(" - ")[1]                         # lineEdit02h heure
        except: None    

        MCHECKED_BY = App.activeDocument().getObject(page).EditableTexts[2]     # lineEdit03
        MCHECK_DATE = App.activeDocument().getObject(page).EditableTexts[3]     # lineEdit04 date

        try:
            MCHEC_DATE = MCHECK_DATE.split(" - ")[0]                            # lineEdit04 date
        except:
            MCHEC_DATE = MCHECK_DATE
        try:
            MCHEC_TIME = MCHECK_DATE.split(" - ")[1]                            # lineEdit04h heure
        except: None    

        MSIZE = App.activeDocument().getObject(page).EditableTexts[4]           # lineEdit05
        MSCALE = App.activeDocument().getObject(page).EditableTexts[5]          # lineEdit06
        MWEIGHT = App.activeDocument().getObject(page).EditableTexts[6]         # lineEdit07
        MDRAWING_NUMBER = App.activeDocument().getObject(page).EditableTexts[7] # lineEdit08
        MSHEET = App.activeDocument().getObject(page).EditableTexts[8]          # lineEdit09
        MTITLE = App.activeDocument().getObject(page).EditableTexts[9]          # textEdit_01

        try:
            MDESCRIPTION = App.activeDocument().getObject(page).EditableTexts[10]   # textEdit_02
            MCOMPANY = App.activeDocument().getObject(page).EditableTexts[11]       # textEdit_02b
            MCOPYRIGHT = App.activeDocument().getObject(page).EditableTexts[12]     # lineEdit_20
            MNote_A = App.activeDocument().getObject(page).EditableTexts[13]        # lineEdit_10
            MNote_B = App.activeDocument().getObject(page).EditableTexts[14]        # lineEdit_11
            MNote_C = App.activeDocument().getObject(page).EditableTexts[15]        # lineEdit_12
            MNote_D = App.activeDocument().getObject(page).EditableTexts[16]        # lineEdit_13
            MNote_E = App.activeDocument().getObject(page).EditableTexts[17]        # lineEdit_14
            MNote_F = App.activeDocument().getObject(page).EditableTexts[18]        # lineEdit_15
            MNote_G = App.activeDocument().getObject(page).EditableTexts[19]        # lineEdit_16
            MNote_H = App.activeDocument().getObject(page).EditableTexts[20]        # lineEdit_17
            MNote_I = App.activeDocument().getObject(page).EditableTexts[21]        # lineEdit_18
        except Exception:
            App.Console.PrintError("Erreur cartouche level DESCRIPTION (Missing field)"+"\n"
                        "You may be using an inadequate template. Try with this template"+"\n")
            App.Console.PrintMessage("http://www.freecadweb.org/wiki/index.php?title=Misc_templates_Full"+"\n\n")
            App.Console.PrintError("Or for the original FreeCAD template use this macro"+"\n")
            App.Console.PrintMessage("http://www.freecadweb.org/wiki/index.php?title=Macro_CartoucheFC"+"\n")        errorDialog("Erreur cartouche level DESCRIPTION (Missing field)"+"\n"
                        "You may be using an inadequate template. Try with this template"+"\n"
                        "http://www.freecadweb.org/wiki/index.php?title=Misc_templates_Full"+"\n\n"
                        "Or for the original FreeCAD template use this macro"+"\n"
                        "http://www.freecadweb.org/wiki/index.php?title=Macro_CartoucheFC"+"\n\n")

    except:
        errorDialog("Erreur cartouche")

class Ui_MainWindow(object):

    def __init__(self, MainWindow):
        global path
        global PageActive
        self.window = MainWindow

        MainWindow.setObjectName(_fromUtf8("MainWindow"))
        MainWindow.resize(810, 400)
        MainWindow.setMaximumSize(QtCore.QSize(810, 400))
        self.centralWidget = QtGui.QWidget(MainWindow)
        self.centralWidget.setObjectName(_fromUtf8("centralWidget"))

#        self.pushButton01 = QtGui.QPushButton(self.centralWidget)
#        self.pushButton01.setGeometry(QtCore.QRect(115, 360, 93, 28))
#        self.pushButton01.setObjectName(_fromUtf8("pushButton01"))
#        self.pushButton01.clicked.connect(self.on_pushButton01_clicked) #connection pushButton01

        self.pushButton02 = QtGui.QPushButton(self.centralWidget)
        self.pushButton02.setGeometry(QtCore.QRect(225, 360, 93, 28))
        self.pushButton02.setObjectName(_fromUtf8("pushButton02"))
        self.pushButton02.clicked.connect(self.on_pushButton02_clicked) #connection pushButton02

        self.pushButton03 = QtGui.QPushButton(self.centralWidget)
        self.pushButton03.setGeometry(QtCore.QRect(335, 360, 93, 28))
        self.pushButton03.setToolTip("The memo button work only with the first Page")
        self.pushButton03.setObjectName(_fromUtf8("pushButton03"))
        self.pushButton03.clicked.connect(self.on_pushButton03_clicked) #connection pushButton03

        self.pushButton04 = QtGui.QPushButton(self.centralWidget)
        self.pushButton04.setGeometry(QtCore.QRect(445, 360, 93, 28))
        self.pushButton04.setObjectName(_fromUtf8("pushButton04"))
        self.pushButton04.clicked.connect(self.on_pushButton04_clicked) #connection pushButton04

        self.pushButton05 = QtGui.QPushButton(self.centralWidget)
        self.pushButton05.setGeometry(QtCore.QRect(555, 360, 93, 28))
#        self.pushButton05.setStyleSheet("background-color: red")       # This function gives a color button
        self.pushButton05.setObjectName(_fromUtf8("pushButton05"))
        self.pushButton05.clicked.connect(self.on_pushButton05_clicked) #connection pushButton05

        #####
        self.groupBox = QtGui.QGroupBox(self.centralWidget)
        self.groupBox.setGeometry(QtCore.QRect(20, 159, 190, 101))
        self.groupBox.setObjectName(_fromUtf8("groupBox"))

        self.label_20 = QtGui.QLabel(self.groupBox)
        self.label_20.setGeometry(QtCore.QRect(115, 5, 61, 17))
        self.label_20.setObjectName(_fromUtf8("label_20"))
        ############### font and color Label
        font = QtGui.QFont()
        font.setBold(True)
        self.label_20.setFont(font)
        self.label_20.setStyleSheet("color : #ff0000")
        ############### font and color
        self.label_20.setVisible(False)

        self.radioButton_0 = QtGui.QRadioButton(self.groupBox)
        self.radioButton_0.setGeometry(QtCore.QRect(95, 1, 91, 17))
        self.radioButton_0.setChecked(True)
        self.radioButton_0.setEnabled(False)
        self.radioButton_0.setVisible(False)
        self.radioButton_0.setObjectName(_fromUtf8("radioButton_0"))

        self.radioButton_1 = QtGui.QRadioButton(self.groupBox)
        self.radioButton_1.setGeometry(QtCore.QRect(95, 20, 91, 17))
        self.radioButton_1.setObjectName(_fromUtf8("radioButton_1"))
        self.radioButton_1.clicked.connect(self.on_radioButton_A3_clicked)# connect radioButton_A3

        self.radioButton_2 = QtGui.QRadioButton(self.groupBox)
        self.radioButton_2.setGeometry(QtCore.QRect(95, 39, 91, 17))
        self.radioButton_2.setObjectName(_fromUtf8("radioButton_2"))
        self.radioButton_2.clicked.connect(self.on_radioButton_A3_clicked)# connect radioButton_A3

        self.radioButton_3 = QtGui.QRadioButton(self.groupBox)
        self.radioButton_3.setGeometry(QtCore.QRect(95, 58, 91, 17))
        self.radioButton_3.setObjectName(_fromUtf8("radioButton_3"))
        self.radioButton_3.clicked.connect(self.on_radioButton_A4_clicked)# connect radioButton_A4

        self.radioButton_4 = QtGui.QRadioButton(self.groupBox)
        self.radioButton_4.setGeometry(QtCore.QRect(95, 76, 91, 17))
        self.radioButton_4.setObjectName(_fromUtf8("radioButton_4"))
        self.radioButton_4.clicked.connect(self.on_radioButton_A4_clicked)# connect radioButton_A4

        self.lineEdit_05 = QtGui.QLineEdit(self.groupBox)
        self.lineEdit_05.setGeometry(QtCore.QRect(10, 16, 75, 41))
        font = QtGui.QFont()
        font.setPointSize(25)
        font.setBold(False)
        font.setWeight(50)
        self.lineEdit_05.setFont(font)
        self.lineEdit_05.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_05.setObjectName(_fromUtf8("lineEdit_05"))
        self.lineEdit_05.setText(SIZE)

        self.frame = QtGui.QFrame(self.groupBox)
        self.frame.setGeometry(QtCore.QRect(10, 58, 74, 41))
        self.frame.setFrameShape(QtGui.QFrame.StyledPanel)
        self.frame.setFrameShadow(QtGui.QFrame.Raised)
        self.frame.setObjectName(_fromUtf8("frame"))

        self.radioButton_EU = QtGui.QRadioButton(self.frame)
        self.radioButton_EU.setGeometry(QtCore.QRect(0, 1, 41, 17))
        self.radioButton_EU.setChecked(True)
        self.radioButton_EU.setObjectName(_fromUtf8("radioButton_EU"))
        self.radioButton_EU.clicked.connect(self.on_radioButton_EU_clicked) #connection radioButton_EU

        self.radioButton_US = QtGui.QRadioButton(self.frame)
        self.radioButton_US.setGeometry(QtCore.QRect(37, 1, 41, 17))
        self.radioButton_US.setObjectName(_fromUtf8("radioButton_US"))
        self.radioButton_US.clicked.connect(self.on_radioButton_US_clicked) #connection radioButton_US

        self.pushButton10 = QtGui.QPushButton(self.frame)
        self.pushButton10.setGeometry(QtCore.QRect(0, 18, 75, 23))
        self.pushButton10.setToolTip("Create the symbol EU or US"+"\n"
                                     "This button is Independent of the Write button"+"\n"
                                     "If you desire modify the symbol in the cartouche,"+"\n"
                                     "delete the inadequate symbol manualy.")
        self.pushButton10.setEnabled(False)
        self.pushButton10.setObjectName(_fromUtf8("pushButton10"))
        self.pushButton10.clicked.connect(self.on_pushButton10_clicked)     #connection pushButton10

        #####

        self.pushButton06 = QtGui.QPushButton(self.centralWidget)
        self.pushButton06.setGeometry(QtCore.QRect(170, 57, 20, 20))
        self.pushButton06.setObjectName(_fromUtf8("pushButton06"))
        self.pushButton06.clicked.connect(self.on_pushButton06_clicked) #connection pushButton06

        self.pushButton07 = QtGui.QPushButton(self.centralWidget)
        self.pushButton07.setGeometry(QtCore.QRect(190, 57, 20, 20))
        self.pushButton07.setObjectName(_fromUtf8("pushButton07"))
        self.pushButton07.clicked.connect(self.on_pushButton07_clicked) #connection pushButton07

        self.pushButton08 = QtGui.QPushButton(self.centralWidget)
        self.pushButton08.setGeometry(QtCore.QRect(170, 137, 20, 20))
        self.pushButton08.setObjectName(_fromUtf8("pushButton08"))
        self.pushButton08.clicked.connect(self.on_pushButton08_clicked) #connection pushButton08

        self.pushButton09 = QtGui.QPushButton(self.centralWidget)
        self.pushButton09.setGeometry(QtCore.QRect(190, 137, 20, 20))
        self.pushButton09.setObjectName(_fromUtf8("pushButton09"))
        self.pushButton09.clicked.connect(self.on_pushButton09_clicked) #connection pushButton09

        self.lineEdit_01 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_01.setGeometry(QtCore.QRect(20, 20, 190, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_01.setFont(font)
        self.lineEdit_01.setObjectName(_fromUtf8("lineEdit_01"))
        self.lineEdit_01.setText(DESIGNED_BY)

        self.lineEdit_02 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_02.setGeometry(QtCore.QRect(20, 60, 82, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_02.setFont(font)
        self.lineEdit_02.setObjectName(_fromUtf8("lineEdit_02"))
        self.lineEdit_02.setText(CREA_DATE)

        self.lineEdit_02h = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_02h.setGeometry(QtCore.QRect(98, 60, 72, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_02h.setFont(font)
        self.lineEdit_02h.setObjectName(_fromUtf8("lineEdit_02h"))
        self.lineEdit_02h.setText(CREA_TIME)

        self.lineEdit_03 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_03.setGeometry(QtCore.QRect(20, 100, 190, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_03.setFont(font)
        self.lineEdit_03.setObjectName(_fromUtf8("lineEdit_03"))
        self.lineEdit_03.setText(CHECKED_BY)

        self.lineEdit_04 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_04.setGeometry(QtCore.QRect(20, 140, 82, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_04.setFont(font)
        self.lineEdit_04.setObjectName(_fromUtf8("lineEdit_04"))
        self.lineEdit_04.setText(CHEC_DATE)

        self.lineEdit_04h = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_04h.setGeometry(QtCore.QRect(98, 140, 72, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_04h.setFont(font)
        self.lineEdit_04h.setObjectName(_fromUtf8("lineEdit_04h"))
        self.lineEdit_04h.setText(CHEC_TIME)

        self.lineEdit_06 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_06.setGeometry(QtCore.QRect(20, 280, 61, 41))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_06.setFont(font)
        self.lineEdit_06.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_06.setObjectName(_fromUtf8("lineEdit_06"))
        self.lineEdit_06.setText(SCALE)

        self.lineEdit_07 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_07.setGeometry(QtCore.QRect(100, 280, 101, 41))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_07.setFont(font)
        self.lineEdit_07.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_07.setObjectName(_fromUtf8("lineEdit_07"))
        self.lineEdit_07.setText(WEIGHT)

        self.lineEdit_08 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_08.setGeometry(QtCore.QRect(220, 280, 341, 41))
        self.lineEdit_08.setObjectName(_fromUtf8("lineEdit_08"))
        self.lineEdit_08.setText(DRAWING_NUMBER)

        self.lineEdit_09 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_09.setGeometry(QtCore.QRect(570, 280, 81, 41))
        self.lineEdit_09.setObjectName(_fromUtf8("lineEdit_09"))
        self.lineEdit_09.setText(SHEET)

        self.lineEdit_20 = QtGui.QLineEdit(self.centralWidget) # Copyright
        self.lineEdit_20.setGeometry(QtCore.QRect(20, 330, 771, 22))
        self.lineEdit_20.setObjectName(_fromUtf8("lineEdit_20"))
        self.lineEdit_20.setText(COPYRIGHT)

        self.lineEdit_10 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_10.setGeometry(QtCore.QRect(690, 290, 101, 30))
        self.lineEdit_10.setObjectName(_fromUtf8("lineEdit_10"))
        self.lineEdit_10.setText(Note_A)

        self.lineEdit_11 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_11.setGeometry(QtCore.QRect(690, 260, 101, 30))
        self.lineEdit_11.setObjectName(_fromUtf8("lineEdit_11"))
        self.lineEdit_11.setText(Note_B)

        self.lineEdit_12 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_12.setGeometry(QtCore.QRect(690, 230, 101, 30))
        self.lineEdit_12.setObjectName(_fromUtf8("lineEdit_12"))
        self.lineEdit_12.setText(Note_C)

        self.lineEdit_13 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_13.setGeometry(QtCore.QRect(690, 200, 101, 30))
        self.lineEdit_13.setObjectName(_fromUtf8("lineEdit_13"))
        self.lineEdit_13.setText(Note_D)

        self.lineEdit_14 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_14.setGeometry(QtCore.QRect(690, 170, 101, 30))
        self.lineEdit_14.setObjectName(_fromUtf8("lineEdit_14"))
        self.lineEdit_14.setText(Note_E)

        self.lineEdit_15 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_15.setGeometry(QtCore.QRect(690, 140, 101, 30))
        self.lineEdit_15.setObjectName(_fromUtf8("lineEdit_15"))
        self.lineEdit_15.setText(Note_F)

        self.lineEdit_16 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_16.setGeometry(QtCore.QRect(690, 110, 101, 30))
        self.lineEdit_16.setObjectName(_fromUtf8("lineEdit_16"))
        self.lineEdit_16.setText(Note_G)

        self.lineEdit_17 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_17.setGeometry(QtCore.QRect(690, 80, 101, 30))
        self.lineEdit_17.setObjectName(_fromUtf8("lineEdit_17"))
        self.lineEdit_17.setText(Note_H)

        self.lineEdit_18 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_18.setGeometry(QtCore.QRect(690, 50, 101, 30))
        self.lineEdit_18.setObjectName(_fromUtf8("lineEdit_18"))
        self.lineEdit_18.setText(Note_I)
##
        self.lineEdit_page = QtGui.QLineEdit(self.centralWidget)         # nom de page
        self.lineEdit_page.setGeometry(QtCore.QRect(20, 365, 181, 20))
        self.lineEdit_page.setToolTip("Name page to work"+"\n"
                                      "The name of the first page is always named 'Page'"
                                      "Select the new page in the Combo view")
        self.lineEdit_page.setObjectName(_fromUtf8("lineEdit_page"))
        self.lineEdit_page.setEnabled(False)
        self.lineEdit_page.setStyleSheet("color: red")
        self.lineEdit_page.setText(PageActive)
        self.lineEdit_page.textChanged.connect(self.on_lineEdit_page_Pressed) # 

        self.label_01T = QtGui.QLabel(self.centralWidget)
        self.label_01T.setGeometry(QtCore.QRect(220, 0, 91, 16))
        self.label_01T.setObjectName(_fromUtf8("label_01T"))

        self.textEdit_01 = QtGui.QTextEdit(self.centralWidget)            # Title
        self.textEdit_01.setGeometry(QtCore.QRect(220, 20, 431,55 ))
        font = QtGui.QFont()
        font.setPointSize(15)
        font.setBold(True)
        font.setWeight(75)
        self.textEdit_01.setFont(font)
        self.textEdit_01.setObjectName(_fromUtf8("textEdit_01"))
        self.textEdit_01.setText(TITLE)

        self.label_02T = QtGui.QLabel(self.centralWidget)
        self.label_02T.setGeometry(QtCore.QRect(220, 80, 101, 16))
        self.label_02T.setObjectName(_fromUtf8("label_02T"))

        self.textEdit_02 = QtGui.QTextEdit(self.centralWidget)            # DESCRIPTION
        self.textEdit_02.setGeometry(QtCore.QRect(220, 100, 431, 55))
        self.textEdit_02.setObjectName(_fromUtf8("textEdit_02"))
        self.textEdit_02.setText(DESCRIPTION)

        self.label_02bT = QtGui.QLabel(self.centralWidget)
        self.label_02bT.setGeometry(QtCore.QRect(220, 160, 90, 16))
        self.label_02bT.setObjectName(_fromUtf8("label_02bT"))

        self.textEdit_02b = QtGui.QTextEdit(self.centralWidget)            # COMPANY
        self.textEdit_02b.setGeometry(QtCore.QRect(220, 180, 340, 60))
        self.textEdit_02b.setObjectName(_fromUtf8("textEdit_02b"))
        self.textEdit_02b.setText(COMPANY)

        self.label_01 = QtGui.QLabel(self.centralWidget)
        self.label_01.setGeometry(QtCore.QRect(20, 0, 91, 16))
        self.label_01.setObjectName(_fromUtf8("label_01"))

        self.label_02 = QtGui.QLabel(self.centralWidget)
        self.label_02.setGeometry(QtCore.QRect(20, 40, 53, 16))
        self.label_02.setObjectName(_fromUtf8("label_02"))

        self.label_03 = QtGui.QLabel(self.centralWidget)
        self.label_03.setGeometry(QtCore.QRect(20, 80, 101, 16))
        self.label_03.setObjectName(_fromUtf8("label_03"))

        self.label_04 = QtGui.QLabel(self.centralWidget)
        self.label_04.setGeometry(QtCore.QRect(20, 120, 91, 16))
        self.label_04.setObjectName(_fromUtf8("label_04"))

        self.label_06 = QtGui.QLabel(self.centralWidget)
        self.label_06.setGeometry(QtCore.QRect(20, 260, 53, 16))
        self.label_06.setObjectName(_fromUtf8("label_06"))

        self.label_07 = QtGui.QLabel(self.centralWidget)
        self.label_07.setGeometry(QtCore.QRect(100, 260, 101, 16))
        self.label_07.setObjectName(_fromUtf8("label_07"))

        self.label_08 = QtGui.QLabel(self.centralWidget)
        self.label_08.setGeometry(QtCore.QRect(220, 260, 121, 16))
        self.label_08.setObjectName(_fromUtf8("label_08"))

        self.label_09 = QtGui.QLabel(self.centralWidget)
        self.label_09.setGeometry(QtCore.QRect(570, 260, 53, 16))
        self.label_09.setObjectName(_fromUtf8("label_09"))

        self.label_10 = QtGui.QLabel(self.centralWidget)
        self.label_10.setGeometry(QtCore.QRect(670, 290, 16, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_10.setFont(font)
        self.label_10.setObjectName(_fromUtf8("label_10"))

        self.label_11 = QtGui.QLabel(self.centralWidget)
        self.label_11.setGeometry(QtCore.QRect(670, 260, 16, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_11.setFont(font)
        self.label_11.setObjectName(_fromUtf8("label_11"))

        self.label_12 = QtGui.QLabel(self.centralWidget)
        self.label_12.setGeometry(QtCore.QRect(670, 230, 16, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_12.setFont(font)
        self.label_12.setObjectName(_fromUtf8("label_12"))

        self.label_13 = QtGui.QLabel(self.centralWidget)
        self.label_13.setGeometry(QtCore.QRect(670, 200, 18, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_13.setFont(font)
        self.label_13.setObjectName(_fromUtf8("label_13"))

        self.label_14 = QtGui.QLabel(self.centralWidget)
        self.label_14.setGeometry(QtCore.QRect(670, 170, 15, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_14.setFont(font)
        self.label_14.setObjectName(_fromUtf8("label_14"))

        self.label_15 = QtGui.QLabel(self.centralWidget)
        self.label_15.setGeometry(QtCore.QRect(670, 140, 14, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_15.setFont(font)
        self.label_15.setObjectName(_fromUtf8("label_15"))

        self.label_16 = QtGui.QLabel(self.centralWidget)
        self.label_16.setGeometry(QtCore.QRect(670, 110, 18, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_16.setFont(font)
        self.label_16.setObjectName(_fromUtf8("label_16"))

        self.label_17 = QtGui.QLabel(self.centralWidget)
        self.label_17.setGeometry(QtCore.QRect(670, 80, 18, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_17.setFont(font)
        self.label_17.setObjectName(_fromUtf8("label_17"))

        self.label_18 = QtGui.QLabel(self.centralWidget)
        self.label_18.setGeometry(QtCore.QRect(670, 50, 10, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_18.setFont(font)
        self.label_18.setObjectName(_fromUtf8("label_18"))

        self.label_19 = QtGui.QLabel(self.centralWidget)
        self.label_19.setGeometry(QtCore.QRect(720, 15, 100, 33))
        self.label_19.setObjectName(_fromUtf8("label_19"))

        self.label_page = QtGui.QLabel(self.centralWidget)
        self.label_page.setGeometry(QtCore.QRect(20, 350, 181, 16))
        self.label_page.setObjectName(_fromUtf8("label_page"))

        self.label_Version = QtGui.QLabel(self.centralWidget)        # Version
        self.label_Version.setGeometry(QtCore.QRect(685, 383, 121, 20))
        self.label_Version.setObjectName(_fromUtf8("label_Version"))

        MainWindow.setCentralWidget(self.centralWidget)

        self.retranslateUi(MainWindow)
        QtCore.QMetaObject.connectSlotsByName(MainWindow)

    def retranslateUi(self, MainWindow):
        MainWindow.setWindowFlags(PySide.QtCore.Qt.WindowStaysOnTopHint) # cette fonction met la fenetre en avant
        MainWindow.setWindowTitle("Cartouche (Full)")
#        self.pushButton01.setText("Position")
        self.pushButton02.setText("Quit") #Quitter
        self.pushButton03.setText("Memo")
        self.pushButton04.setText("Clean")#Nettoyer
        self.pushButton05.setText("Write")#Appliquer
        self.pushButton06.setText("D.")
        self.pushButton07.setText("H.")
        self.pushButton08.setText("D.")
        self.pushButton09.setText("H.")
        self.pushButton10.setText("Create Symb.")

        self.label_01.setText("Designed by :")
        self.label_02.setText("Date :")
        self.label_03.setText("Checked by :")
        self.label_04.setText("Date :")
        self.label_06.setText("Scale :")
        self.label_07.setText("Weight (Kg) :")
        self.label_08.setText("Drawing number :")
        self.label_01T.setText("Title :")
        self.label_02T.setText("Description :")
        self.label_02bT.setText("Company :")
        self.label_09.setText("Sheet :")

        self.label_10.setText("A")
        self.label_11.setText("B")
        self.label_12.setText("C")
        self.label_13.setText("D")
        self.label_14.setText("E")
        self.label_15.setText("F")
        self.label_16.setText("G")
        self.label_17.setText("H")
        self.label_18.setText("I")
        self.label_19.setText("Notes")
        self.label_20.setText("Warning")
        self.label_page.setText("Name page to work")
        self.label_Version.setText("Ver: 00.10 15/02/2017")        # Version
        self.groupBox.setTitle("Size :")
        self.radioButton_1.setText("A3 Landscape")
        self.radioButton_2.setText("A3 Portrait")
        self.radioButton_3.setText("A4 Landscape")
        self.radioButton_4.setText("A4 Portrait")
        self.radioButton_EU.setText("EU")
        self.radioButton_US.setText("US")
        self.lineEdit_05.setText("?")

#______________________________________________________________________________________
    # Radio Boutons
    def on_radioButton_A3_clicked(self):  # connect radioButton_A3
        self.label_20.setVisible(False)
        self.pushButton10.setEnabled(True)
        self.lineEdit_05.setText("A3")
        self.pushButton10.setStyleSheet("color: QPalette.Base")           # origin system

    def on_radioButton_A4_clicked(self):  # connect radioButton_A4
        self.label_20.setVisible(False)
        self.pushButton10.setEnabled(True)
        self.lineEdit_05.setText("A4")
        self.pushButton10.setStyleSheet("color: QPalette.Base")           # origin system
    # Radio Boutons

    def on_radioButton_EU_clicked(self):    # Bouton /Symbole EU
        global SymbolSwitch
        SymbolSwitch = 1

    def on_radioButton_US_clicked(self):    # Bouton /Symbole US
        global SymbolSwitch
        SymbolSwitch = 0

    def on_pushButton10_clicked(self):      # Bouton /Symbole EU US disposition dans le cartouche
        global SymbolSwitch
        global PageActive
        self.label_20.setVisible(False)

        if self.radioButton_0.isChecked():
            self.label_20.setVisible(True)
            self.pushButton10.setEnabled(False)
            self.pushButton10.setStyleSheet("color: red")
            self.lineEdit_page.setStyleSheet("color: red")
            FreeCAD.Console.PrintError("Select one format A3 or A4 for the Symbole" + "\n")
        else:
            self.pushButton10.setEnabled(True)
            self.pushButton10.setStyleSheet("background-color: #FF5B2B")
            self.pushButton10.setText("Wait.")
            FreeCADGui.updateGui()                # rafraichi l'ecran
            if SymbolSwitch == 1:
                if self.radioButton_1.isChecked():
                    symbol_EU(247.5, 263.5, 0.8)  # A3 Landscape
                elif self.radioButton_2.isChecked():
                    symbol_EU(124.55, 386.3, 0.8) # A3 Portrait
                elif self.radioButton_3.isChecked():
                    symbol_EU(158.7, 181.35, 0.6) # A4 Landscape
                elif self.radioButton_4.isChecked():
                    symbol_EU(71.9, 269.0, 0.6)   # A4 Portrait
            else:
                if self.radioButton_1.isChecked():
                    symbol_US(247.5, 263.5, 0.8)  # A3 Landscape
                elif self.radioButton_2.isChecked():
                    symbol_US(124.55, 386.3, 0.8) # A3 Portrait
                elif self.radioButton_3.isChecked():
                    symbol_US(158.7, 181.35, 0.6) # A4 Landscape
                elif self.radioButton_4.isChecked():
                    symbol_US(71.9, 269.0, 0.6)   # A4 Portrait
            self.pushButton10.setStyleSheet("color: QPalette.Base")           # origin system
            self.pushButton10.setText("Create Symb.")
            FreeCADGui.updateGui()                                 # rafraichi l'ecran
        
    def on_lineEdit_page_Pressed(self):   # Name page
        global PageActive
        PageActive = self.lineEdit_page.text()

    def on_pushButton09_clicked(self):    # Bouton /heure document
        self.lineEdit_04h.setText(str(heure()))

    def on_pushButton08_clicked(self):    # Bouton date/ document
        global SymbolSwitch
        if SymbolSwitch==0:
            self.lineEdit_04.setText(str(dateUs()))
        else:
            self.lineEdit_04.setText(str(dateEu()))

    def on_pushButton07_clicked(self):    # Bouton /heure checked
        self.lineEdit_02h.setText(str(heure()))

    def on_pushButton06_clicked(self):    # Bouton date/ checked
        global SymbolSwitch
        if SymbolSwitch==0:
            self.lineEdit_02.setText(str(dateUs()))
        else:
            self.lineEdit_02.setText(str(dateEu()))

    def on_pushButton05_clicked(self):    # Bouton Appliquer
        try:
            global DESIGNED_BY, CREATION_DATE, CREA_DATE  , CREA_TIME, CHECKED_BY, CHECK_DATE
            global CHEC_DATE  , CHEC_TIME    , SIZE       , SCALE    , WEIGHT    ,DRAWING_NUMBER
            global SHEET      , TITLE        , DESCRIPTION, COMPANY  , COPYRIGHT
            global Note_A, Note_B, Note_C, Note_D, Note_E, Note_F, Note_G, Note_H, Note_I
            global ui
            global SymbolSwitch
            global PageActive

            try:
                page = App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0]
            except Exception:
                page = App.activeDocument().getObjectsByLabel(PageActive)[0]        if len(str(page)) != 2:            self.pushButton05.setStyleSheet("background-color: #FF5B2B")
                self.pushButton05.setText("Wait.")
                FreeCADGui.updateGui()                # rafraichi l'ecran

                DESIGNED_BY = (self.lineEdit_01.text())
                CREATION_DATE = (self.lineEdit_02.text())+" - "+(self.lineEdit_02h.text())
                CHECKED_BY = (self.lineEdit_03.text())
                CHECK_DATE = (self.lineEdit_04.text())+" - "+(self.lineEdit_04h.text())
                SIZE = (self.lineEdit_05.text())
                SCALE = (self.lineEdit_06.text())
                WEIGHT = (self.lineEdit_07.text())
                DRAWING_NUMBER = (self.lineEdit_08.text())
                SHEET = (self.lineEdit_09.text())
                TITLE = (self.textEdit_01.toPlainText())
                DESCRIPTION = (self.textEdit_02.toPlainText())
                COMPANY = (self.textEdit_02b.toPlainText())
                COPYRIGHT = (self.lineEdit_20.text())            Note_A = (self.lineEdit_10.text())
                Note_B = (self.lineEdit_11.text())
                Note_C = (self.lineEdit_12.text())
                Note_D = (self.lineEdit_13.text())
                Note_E = (self.lineEdit_14.text())
                Note_F = (self.lineEdit_15.text())
                Note_G = (self.lineEdit_16.text())
                Note_H = (self.lineEdit_17.text())
                Note_I = (self.lineEdit_18.text())            try:
                    FreeCAD.getDocument(App.ActiveDocument.Name).getObject(page.Name).EditableTexts = [DESIGNED_BY, CREATION_DATE, CHECKED_BY, CHECK_DATE, SIZE, SCALE, WEIGHT, DRAWING_NUMBER, SHEET, TITLE, DESCRIPTION, COMPANY, COPYRIGHT, Note_A, Note_B, Note_C, Note_D, Note_E, Note_F, Note_G, Note_H, Note_I, ]
#old                    FreeCAD.getDocument(App.ActiveDocument.Name).getObjectsByLabel(PageActive.encode('utf-8'))[0].EditableTexts = [DESIGNED_BY, CREATION_DATE, CHECKED_BY, CHECK_DATE, SIZE, SCALE, WEIGHT, DRAWING_NUMBER, SHEET, TITLE, DESCRIPTION, COMPANY, COPYRIGHT, Note_A, Note_B, Note_C, Note_D, Note_E, Note_F, Note_G, Note_H, Note_I, ]
                    App.ActiveDocument.recompute()
                    FreeCAD.Console.PrintMessage("Write done to ( " + page.Label + " )" + "\n")
                    self.pushButton05.setStyleSheet("color: QPalette.Base")
                except Exception:
                    FreeCAD.Console.PrintError("Error write cartouche or verify the selected page ( " + page.Label + " )" + "\n")
                    self.pushButton05.setStyleSheet("background-color: red")
            else:
                FreeCAD.Console.PrintError("Error selected page ( " + Page.Label + " )" + "\n")
                self.pushButton05.setStyleSheet("background-color: red")

        except Exception:
            self.pushButton05.setStyleSheet("background-color: red")
            FreeCAD.Console.PrintError("Error or not page " + "\n")
        self.pushButton05.setText("Write")
        App.ActiveDocument.recompute()

    def on_pushButton04_clicked(self):    # Bouton nettoyer

        self.lineEdit_01.setText("")
        self.lineEdit_02.setText("")
        self.lineEdit_02h.setText("")
        self.lineEdit_03.setText("")
        self.lineEdit_04.setText("")
        self.lineEdit_04h.setText("")
        self.lineEdit_05.setText("?")
        self.lineEdit_06.setText("")
        self.lineEdit_07.setText("")
        self.lineEdit_08.setText("")
        self.lineEdit_09.setText("")
        self.textEdit_01.setText("")
        self.textEdit_02.setText("")
        self.textEdit_02b.setText("")
        self.lineEdit_20.setText("")
        self.lineEdit_10.setText("")
        self.lineEdit_11.setText("")
        self.lineEdit_12.setText("")
        self.lineEdit_13.setText("")
        self.lineEdit_14.setText("")
        self.lineEdit_15.setText("")
        self.lineEdit_16.setText("")
        self.lineEdit_17.setText("")
        self.lineEdit_18.setText("")

        self.pushButton10.setStyleSheet("color: QPalette.Base")                # origin system
        self.label_20.setVisible(False)
        self.radioButton_0.setChecked(True)
        self.pushButton05.setEnabled(True)
        self.pushButton05.setStyleSheet("background-color: QPalette.Base")     # origin system
        self.groupBox.setEnabled(True)

    def on_pushButton03_clicked(self):    # Bouton Memo
        global MDESIGNED_BY, MCREATION_DATE, MCREA_DATE  , MCREA_TIME, MCHECKED_BY, MCHECK_DATE
        global MCHEC_DATE  , MCHEC_TIME    , MSIZE       , MSCALE    , MWEIGHT    ,MDRAWING_NUMBER
        global MSHEET      , MTITLE        , MDESCRIPTION, MCOMPANY  , MCOPYRIGHT
        global MNote_A, MNote_B, MNote_C, MNote_D, MNote_E, MNote_F, MNote_G, MNote_H, MNote_I
        
        self.lineEdit_01.setText(MDESIGNED_BY)
        self.lineEdit_02.setText(MCREA_DATE)
        self.lineEdit_02h.setText(MCREA_TIME)
        self.lineEdit_03.setText(MCHECKED_BY)
        self.lineEdit_04.setText(MCHEC_DATE)
        self.lineEdit_04h.setText(MCHEC_TIME)
        self.lineEdit_05.setText("?") #(SIZE)
        self.lineEdit_06.setText(MSCALE)
        self.lineEdit_07.setText(MWEIGHT)
        self.lineEdit_08.setText(MDRAWING_NUMBER)
        self.lineEdit_09.setText(MSHEET)
        self.textEdit_01.setText(MTITLE)
        self.textEdit_02.setText(MDESCRIPTION)
        self.textEdit_02b.setText(MCOMPANY)
        self.lineEdit_20.setText(MCOPYRIGHT)
        self.lineEdit_10.setText(MNote_A)
        self.lineEdit_11.setText(MNote_B)
        self.lineEdit_12.setText(MNote_C)
        self.lineEdit_13.setText(MNote_D)
        self.lineEdit_14.setText(MNote_E)
        self.lineEdit_15.setText(MNote_F)
        self.lineEdit_16.setText(MNote_G)
        self.lineEdit_17.setText(MNote_H)
        self.lineEdit_18.setText(MNote_I)
#        self.lineEdit_page.setText(PageActive)
        self.radioButton_0.setChecked(True)

    def on_pushButton02_clicked(self):    # Bouton Quitter
        App.Console.PrintMessage("End CartoucheFC_Full\r\n")
        self.window.hide()
        FreeCADGui.Selection.removeObserver(s)           # Uninstalls the resident function
        App.Console.PrintMessage("removeObserver"+"\n")

#    def on_pushButton01_clicked(self):    # Bouton appel de Position
#        MainWindow.resize(210, 480)
#        executer()
#        MainWindow.resize(810, 480)
#______________________________________________________________________________________

class SelObserver:
    print "run.."
    def setSelection(self,document):                     # Selection in ComboView
        global PageActive
        global ui
        if len(Gui.Selection.getSelection(document)) == 1:

            ff = ui
            ff.lineEdit_page.setStyleSheet("color: QPalette.Base")           # origin system
            ff.pushButton05.setEnabled(True)
            ff.pushButton05.setStyleSheet("background-color: QPalette.Base") # origin system
            ff.groupBox.setEnabled(True)

            if (str(Gui.Selection.getSelection(document)[0].Name[0:4]) == "Page"):
                PageActive = str(Gui.Selection.getSelection(document)[0].Label.encode('utf-8'))
                try:
                    ff.lineEdit_page.setText(unicode(PageActive,'utf-8'))    # convert if accent
                except Exception:
                    ff.lineEdit_page.setText(PageActive)                     # normal

                memoEntree()                    # entree memo click mouse
                ff.on_pushButton03_clicked()    # Bouton Memo
            else:
                FreeCAD.Console.PrintError("Select a valid Page__________________________" + "\n")
                ff.lineEdit_page.setStyleSheet("color: red")
                ff.lineEdit_page.setText("Select a valid Page")              # 
                ff.pushButton05.setEnabled(False)
                ff.pushButton05.setStyleSheet("background-color: red")       # This function gives a color button
                ff.groupBox.setEnabled(False)

                FreeCAD.Console.PrintMessage("                 " + "Name            Label" + "\n")
                for i in App.ActiveDocument.Objects:
                    if i.Name[0:4] == "Page":
                        name = i.Name + "                 "
                        labe = i.Label+ "                 "
                        FreeCAD.Console.PrintMessage("    Valid Page : " + name[:15] + "," + labe[:25] + "\n")
                FreeCAD.Console.PrintError("_____________________________________________" + "\n")

for obj in FreeCAD.ActiveDocument.Objects:        # deslectionne
        FreeCADGui.Selection.removeSelection(obj)

s=SelObserver()
FreeCADGui.Selection.addObserver(s)               # install the function mode resident 

MainWindow = QtGui.QMainWindow()
ui = Ui_MainWindow(MainWindow)
MainWindow.show()
}}

## Other 

The fields have no length limit, check your cartouche.

This program creates a drawing representing the regional projection symbol on your project, do not touch it is registered therefore hidden form invisible.

If you want it to be cleared uncomment the commented lines and vice versa


```python

#    App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_EU")
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_EU").Visibility = False
```

et 
```python

#    App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_US")
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_US").Visibility = False
``` (I had some times an error in execution when the symbol was erased)

This module works with the drawing sheet included in FreeCAD this sheet is called **Page**, do not change the name of this sheet!

## Revision 

ver \"00.10\" : 15/02/2017 : tuning page multiple (It is possible to lose a page if there are too many)

ver \"00.09\" : 10/02/2017 : add radio button for choice symbol and correct the placement symbol in the separate page

ver \"00.08 : 06/02/2017 : the dialog box name page accept the accent

ver \"00.07 : 05/02/2017 : add save cartouche with name page (for multi page in projects) ps: not for character accentuate \"àùé \...\"

ver 00.06 : 13/10/2016 : selection format page and position for the symbol convention (for FreeCAD ver 0.17)

ver 5 : 08/08/2014 PyQt4 and PySide


</div>


</div>





<div class="mw-collapsible mw-collapsed toccolours">

# Macro CartoucheFC Full/fr 


<div class="mw-collapsible-content">


{{Macro/fr
|Name=Macro_CartoucheFC_Full
|Icon=Macro_CartoucheFC_Full.png
|Description=Cette macro est une application complète, elle permet de remplir le cartouche de la feuille de dessin avec tous les champs éditables (Pour l'[atelier Drawing](Drawing_Workbench/fr.md)).
|Author=Mario52
|Version=00.10
|Date=2017-02-15
|FCVersion=Toutes les versions utilisant l'atelier Drawing
|Download=[https://www.freecadweb.org/wiki/images/6/68/Macro_CartoucheFC_Full.png Icône de la barre d'outils]
}}

## Description 

Cette macro est une application complète, elle permet de remplir simplement tous les champs du cartouche.

Téléchargez les feuilles Misc_templates_Full

Voici l\'ordre de remplissage de la ligne éditable de FreeCAD. Les champs date et heure sont séparés par un \'*\'espace négatif espace* \" - \"\'\'\' et constituent une seule ligne éditable.

<img alt="CartoucheFC_Full" src=images/Macro_CartoucheFC_Full_00.png  style="width:680px;">

## Utilisation 

**PS : certains caractères comme & \$ ne sont pas acceptés (et peut être d\'autres caractères spéciaux).**

Si vous avez des questions ou si vous voulez ajouter une fonction, vous pouvez vous adresser au forum français [Remplir cartouche](http://forum.freecadweb.org/viewtopic.php?f=12&t=2049)

-   La fenêtre reste au dessus des autres fenêtres et permet ainsi de contrôler le cartouche sans quitter le programme.

-   Copiez le code dans un fichier nommé **Macro_CartoucheFC_Full.py** et placez le dans votre répertoire de macros habituelle.

-   Après avoir créé votre feuille de dessin à l\'aide du module Drawing de FreeCAD, lancez la macro **Macro_CartoucheFC_Full**.

-   A l\'ouverture, le programme enregistrera en mémoire toutes les données déjà présente dans le cartouche de la feuille (s\'ils sont remplis), toutes ces données seront automatiquement restituées à l\'aide du bouton **Memo** et tenus en mémoire jusqu'à la fermeture du programme.

-   Les boutons de date ** D.** et heure ** H.** affichent la date et heure du système.

  -Le format de la date est tributaire du symbole sélectionné **EU** ou **US** qui détermine le format régional. Le changement ne se fait pas automatiquement (pour le cas ou vous avez entré une date manuellement) il faut cliquer à nouveau sur les boutons dates si vous changez le symbole (vérifiez avant d\'imprimer).

-   Premièrement sélectionnez votre page de travail.

-   Choice : choisissez le format de page utilisé.

-   Le bouton **Symbole EU** ou US change le sens du symbole de projection \"Select your Symbol\" est affiché par défaut, puis le symbole actif s\'affiche. Cliquez sur le bouton et vérifiez sur la feuille le symbole, cliquez une seconde fois pour modifier le symbole.

  -Le choix de ce symbole, influe le format de la date **EU = dd/MM/yyyy** et **US = MM/dd/yyyy**.

  -**Attention** : Cette commande ne passe pas par le bouton **Appliquer** et modifie immédiatement le symbole à chaque appuis sur la touche, vérifiez toujours si vous avez sur votre feuille le symbole approprié.

-   Le bouton **Nettoyer** efface tous les champs du cartouche. Vous pouvez revenir aux données d\'origine à l\'aide du bouton **Memo**.

-   Le bouton **Appliquer** enregistre tous les champs du cartouche dans la feuille. Vous pouvez revenir aux données d\'origine à l\'aide du bouton **Memo** (sauf pour le symbole régional qui travaille en indépendant et est effectif immédiatement).

## Code 

L\' icône pour votre barre d\'outils ![](images/Macro_CartoucheFC_Full.png )

**Macro_CartoucheFC_Full.FCMacro**


{{MacroCode|code=
# -*- coding: utf-8 -*-
from __future__ import unicode_literals
"""
***************************************************************************
*   Copyright (c) 2014 2016 2017 <mario52>                                *
*                                                                         *
*   This file is a supplement to the FreeCAD CAx development system.      *
*                                                                         *
*   This program is free software; you can redistribute it and/or modify  *
*   it under the terms of the GNU Lesser General Public License (LGPL)    *
*   as published by the Free Software Foundation; either version 2 of     *
*   the License, or (at your option) any later version.                   *
*   for detail see the LICENCE text file.                                 *
*                                                                         *
*   This software is distributed in the hope that it will be useful,      *
*   but WITHOUT ANY WARRANTY; without even the implied warranty of        *
*   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the         *
*   GNU Library General Public License for more details.                  *
*                                                                         *
*   You should have received a copy of the GNU Library General Public     *
*   License along with this macro; if not, write to the Free Software     *
*   Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  *
*   USA                                                                   *
***************************************************************************
*           WARNING! All changes in this file will be lost and            *  
*                  may cause malfunction of the program                   *
***************************************************************************
"""
#OS: Windows 10
#Word size of OS: 64-bit
#Word size of FreeCAD: 64-bit
#Version: 0.16.6706 (Git)
#Build type: Release
#Branch: releases/FreeCAD-0-16
#Hash: f86a4e411ff7848dea98d7242f43b7774bee8fa0
#Python version: 2.7.8
#Qt version: 4.8.7
#Coin version: 4.0.0a
#OCC version: 6.8.0.oce-0.17

__title__   = "Macro_CartoucheFC_Full"
__author__  = "Mario52"
__url__     = "http://www.freecadweb.org/index-fr.html"
__Wiki__    = "http://www.freecadweb.org/wiki/Macro_CartoucheFC_Full"
__version__ = "00.10"
__date__    = "15/02/2017"

__Requires__ = ("all version and freecad " +
" DESIGNED_BY, CREATION_DATE, CHECKED_BY, CHECK_DATE, SIZE, SCALE, WEIGHT, DRAWING_NUMBER, SHEET, " +
" TITLE, DESCRIPTION, COMPANY, COPYRIGHT, Note_A, Note_B, Note_C, Note_D, Note_E, Note_F, Note_G, Note_H, Note_I" )
__Template__ = " A3_Landscape_xx_FULL.svg, A3_Portrait_xx_FULL, A4_Landscape_xx_FULL.svg, A4_Portrait_xx_FULL"
__Template_Link__ = "http://www.freecadweb.org/wiki/index.php?title=Misc_templates_Full"

import PySide
from PySide import QtCore, QtGui

import Draft, Part, FreeCAD, math, PartGui, FreeCADGui
from math import sqrt, pi, sin, cos, asin
from FreeCAD import Base

def utf8(unio):
    return unicode(unio).encode('UTF8')

global path
#path = FreeCAD.ConfigGet("AppHomePath")
path = FreeCAD.ConfigGet("UserAppData")

global PageActive      ; PageActive  = "Select your page" # essais 
#global PageActive      ; PageActive  = "Page" # page active
global DESIGNED_BY     ; DESIGNED_BY = ""     # lineEdit01 DESIGNED_BY
global MDESIGNED_BY    ; MDESIGNED_BY = ""    # 
global CREATION_DATE   ; CREATION_DATE = ""   # lineEdit02 CREATION_DATE date
global MCREATION_DATE  ; MCREATION_DATE = ""  # 
global CREA_DATE       ; CREA_DATE = ""       # lineEdit02h date
global MCREA_DATE      ; MCREA_DATE = ""      # 
global CREA_TIME       ; CREA_TIME = ""       # lineEdit02h heure
global MCREA_TIME      ; MCREA_TIME = ""      # 
global CHECKED_BY      ; CHECKED_BY = ""      # lineEdit03
global MCHECKED_BY     ; MCHECKED_BY = ""     # 
global CHECK_DATE      ; CHECK_DATE = ""      # lineEdit04 date
global MCHECK_DATE     ; MCHECK_DATE = ""     # 
global CHEC_DATE       ; CHEC_DATE = ""       # lineEdit04 date
global MCHEC_DATE      ; MCHEC_DATE = ""      # 
global CHEC_TIME       ; CHEC_TIME = ""       # lineEdit04h heure
global MCHEC_TIME      ; MCHEC_TIME = ""      # 
global SIZE            ; SIZE = ""            # lineEdit05
global MSIZE           ; MSIZE = ""           # 
global SCALE           ; SCALE =  ""          # lineEdit06
global MSCALE          ; MSCALE =  ""         # 
global WEIGHT          ; WEIGHT =  ""         # lineEdit07
global MWEIGHT         ; MWEIGHT =  ""        # 
global DRAWING_NUMBER  ; DRAWING_NUMBER = ""  # lineEdit08
global MDRAWING_NUMBER ; MDRAWING_NUMBER = "" # 
global SHEET           ; SHEET =  ""          # lineEdit09
global MSHEET          ; MSHEET =  ""         # 
global TITLE           ; TITLE =  ""          # textEdit_01
global MTITLE          ; MTITLE =  ""         # 
global DESCRIPTION     ; DESCRIPTION =  ""    # textEdit_02
global MDESCRIPTION    ; MDESCRIPTION = ""    # 
global COMPANY         ; COMPANY = ""         # textEdit_02b
global MCOMPANY        ; MCOMPANY = ""        # 
global COPYRIGHT       ; COPYRIGHT = ""       # lineEdit_20
global MCOPYRIGHT      ; MCOPYRIGHT = ""      # 
global Note_A          ; Note_A = ""          # lineEdit_10
global MNote_A         ; MNote_A = ""         # 
global Note_B          ; Note_B = ""          # lineEdit_11
global MNote_B         ; MNote_B = ""         # 
global Note_C          ; Note_C = ""          # lineEdit_12
global MNote_C         ; MNote_C = ""         # 
global Note_D          ; Note_D = ""          # lineEdit_13
global MNote_D         ; MNote_D = ""         # 
global Note_E          ; Note_E = ""          # lineEdit_14
global MNote_E         ; MNote_E = ""         # 
global Note_F          ; Note_F = ""          # lineEdit_15
global MNote_F         ; MNote_F = ""         # 
global Note_G          ; Note_G = ""          # lineEdit_16
global MNote_G         ; MNote_G = ""         # 
global Note_H          ; Note_H = ""          # lineEdit_17
global MNote_H         ; MNote_H = ""         # 
global Note_I          ; Note_I = ""          # lineEdit_18
global MNote_I         ; MNote_I = ""         # 

global SymbolSwitch    ; SymbolSwitch = 1     # 0=US 1=EU
global ui              ; ui     = ""

def heure():
    return QtCore.QTime().currentTime().toString('hh:mm:ss')
def dateEu():
    return QtCore.QDate().currentDate().toString('dd/MM/yyyy') # forme euro
def dateUK():
    return QtCore.QDate().currentDate().toString('yyyy/MM/dd') # forme UK
def dateUs():
    return QtCore.QDate().currentDate().toString('MM/dd/yyyy') # forme US
def dateComp():
    return QtCore.QDate().currentDate().toString('dddd d MMMM yyyy') # Retourne "dimanche 20 Juillet 77"

try:
    _fromUtf8 = QtCore.QString.fromUtf8
except AttributeError:
    def _fromUtf8(s):
        return s
try:
    _encoding = QtGui.QApplication.UnicodeUTF8
    def _translate(context, text, disambig):
        return QtGui.QApplication.translate(context, text, disambig, _encoding)
except AttributeError:
    def _translate(context, text, disambig):
        return QtGui.QApplication.translate(context, text, disambig)

def errorDialog(msg):
    diag = QtGui.QMessageBox(QtGui.QMessageBox.Critical,u"Error Message",msg)
    diag.setWindowFlags(PySide.QtCore.Qt.WindowStaysOnTopHint) # cette fonction met la fenetre en avant
    diag.exec_()

def symbol_EU(depx, depy, scale):    #symbol_EU =O
    global PageActive
    global ui

    try:
        page = App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0]
    except Exception:
        page = App.activeDocument().getObjectsByLabel(PageActive)[0]if len(str(page)) != 2:
        comP   = []
        nameL  = []
        if "Page" in (page.Name):
            for ii in (page.Group):
                if ((ii.Label) == "Symbol_EU") or ((ii.Label) == "Symbol_US") :
                    App.activeDocument().removeObject(ii.Name)

        points=[FreeCAD.Vector(-7.5,0.0,0.0),FreeCAD.Vector(20.0,0.0,0.0)]
        i = Draft.makeWire(points,closed=False,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        points=[FreeCAD.Vector(12.5,7.5,0.0),FreeCAD.Vector(12.5,-7.5,0.0)]
        i = Draft.makeWire(points,closed=False,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        points=[FreeCAD.Vector(-5,2.5,0.0),FreeCAD.Vector(5.0,5.0,0.0),FreeCAD.Vector(5.0,-5.0,0.0),FreeCAD.Vector(-5.0,-2.5,0.0)]
        i = Draft.makeWire(points,closed=True,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        pl=FreeCAD.Placement()
        pl.Rotation.Q=(0.0,-0.0,-0.0,1.0)
        pl.Base=FreeCAD.Vector(12.5,-0.0,0.0)
        i = Draft.makeCircle(radius=2.5,placement=pl,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        i = Draft.makeCircle(radius=5.0,placement=pl,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)    comp = Part.makeCompound(comP)
        Part.show(comp)
        App.ActiveDocument.ActiveObject.Label = "Symbol_EU"    obj = FreeCAD.ActiveDocument.ActiveObject
        obj.ViewObject.LineColor = (0.0,0.0,0.0)
        obj.ViewObject.Visibility = False
        
        obj2 = Draft.makeDrawingView(obj, page) 
        obj2.X = depx
        obj2.Y = depy
        obj2.Scale = scale #0.8    # A3
        obj2.Label = "Symbol_EU"    for i in nameL: App.activeDocument().removeObject(i)    App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0].addObject(obj)
        App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0].addObject(obj2)
        App.ActiveDocument.recompute()
    else:
        ui.pushButton05.setStyleSheet("background-color: red")       # This function gives a color button
        FreeCAD.Console.PrintError("Error selected page [ " + PageActive + " ]" + "\n")

def symbol_US(depx, depy, scale):    #symbol_US O=
    global PageActive
    global ui

    try:
        page = App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0]
    except Exception:
        page = App.activeDocument().getObjectsByLabel(PageActive)[0]

    if len(str(page)) != 2:
        comP   = []
        nameL  = []    if "Page" in (page.Name):
            for ii in (page.Group):
                if ((ii.Label) == "Symbol_EU") or ((ii.Label) == "Symbol_US") :
                    App.activeDocument().removeObject(ii.Name)

        points=[FreeCAD.Vector(-7.5,0.0,0.0),FreeCAD.Vector(20.0,0.0,0.0)]
        i = Draft.makeWire(points,closed=False,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        points=[FreeCAD.Vector(0.0,7.5,0.0),FreeCAD.Vector(0.0,-7.5,0.0)]
        i = Draft.makeWire(points,closed=False,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        points=[FreeCAD.Vector(7.5,2.5,0.0),FreeCAD.Vector(17.5,5.0,0.0),FreeCAD.Vector(17.5,-5.0,0.0),FreeCAD.Vector(7.5,-2.5,0.0)]
        i = Draft.makeWire(points,closed=True,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        pl=FreeCAD.Placement()
        pl.Rotation.Q=(0.0,-0.0,-0.0,1.0)
        pl.Base=FreeCAD.Vector(0.0,-0.0,0.0)
        i = Draft.makeCircle(radius=2.5,placement=pl,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)
        i = Draft.makeCircle(radius=5.0,placement=pl,face=False,support=None)
        comP.append(i.Shape)
        nameL.append(i.Name)    comp = Part.makeCompound(comP)
        Part.show(comp)
        App.ActiveDocument.ActiveObject.Label = "Symbol_US"    obj = FreeCAD.ActiveDocument.ActiveObject
        obj.ViewObject.LineColor = (0.0,0.0,0.0)
        obj.ViewObject.Visibility = False    obj2 = Draft.makeDrawingView(obj, page) 
        obj2.X = depx
        obj2.Y = depy
        obj2.Scale = scale #0.8    # A3
        obj2.Label = "Symbol_US"    for i in nameL: App.activeDocument().removeObject(i)    App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0].addObject(obj)
        App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0].addObject(obj2)
        App.ActiveDocument.recompute()
    else:
        ui.pushButton05.setStyleSheet("background-color: red")       # This function gives a color button
        FreeCAD.Console.PrintError("Error selected page [ " + PageActive + " ]" + "\n")

def memoEntree():
    global MDESIGNED_BY, MCREATION_DATE, MCREA_DATE  , MCREA_TIME, MCHECKED_BY, MCHECK_DATE
    global MCHEC_DATE  , MCHEC_TIME    , MSIZE       , MSCALE    , MWEIGHT    ,MDRAWING_NUMBER
    global MSHEET      , MTITLE        , MDESCRIPTION, MCOMPANY  , MCOPYRIGHT
    global MNote_A, MNote_B, MNote_C, MNote_D, MNote_E, MNote_F, MNote_G, MNote_H, MNote_I
    global PageActive

    try:
        page = App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0].Name
    except Exception:
        page = App.activeDocument().getObjectsByLabel(PageActive)[0]

    try:
        MDESIGNED_BY   = App.activeDocument().getObject(page).EditableTexts[0]  # lineEdit01 DESIGNED_BY
        MCREATION_DATE = App.activeDocument().getObject(page).EditableTexts[1]  # lineEdit02 CREATION_DATE date

        MCREA_DATE = MCREA_TIME = MCHEC_DATE = MCHEC_TIME = ""

        try:
            MCREA_DATE = MCREATION_DATE.split(" - ")[0]                         # lineEdit02h date
        except:
            MCREA_DATE = MCREATION_DATE
        try:
            MCREA_TIME = MCREATION_DATE.split(" - ")[1]                         # lineEdit02h heure
        except: None    

        MCHECKED_BY = App.activeDocument().getObject(page).EditableTexts[2]     # lineEdit03
        MCHECK_DATE = App.activeDocument().getObject(page).EditableTexts[3]     # lineEdit04 date

        try:
            MCHEC_DATE = MCHECK_DATE.split(" - ")[0]                            # lineEdit04 date
        except:
            MCHEC_DATE = MCHECK_DATE
        try:
            MCHEC_TIME = MCHECK_DATE.split(" - ")[1]                            # lineEdit04h heure
        except: None    

        MSIZE = App.activeDocument().getObject(page).EditableTexts[4]           # lineEdit05
        MSCALE = App.activeDocument().getObject(page).EditableTexts[5]          # lineEdit06
        MWEIGHT = App.activeDocument().getObject(page).EditableTexts[6]         # lineEdit07
        MDRAWING_NUMBER = App.activeDocument().getObject(page).EditableTexts[7] # lineEdit08
        MSHEET = App.activeDocument().getObject(page).EditableTexts[8]          # lineEdit09
        MTITLE = App.activeDocument().getObject(page).EditableTexts[9]          # textEdit_01

        try:
            MDESCRIPTION = App.activeDocument().getObject(page).EditableTexts[10]   # textEdit_02
            MCOMPANY = App.activeDocument().getObject(page).EditableTexts[11]       # textEdit_02b
            MCOPYRIGHT = App.activeDocument().getObject(page).EditableTexts[12]     # lineEdit_20
            MNote_A = App.activeDocument().getObject(page).EditableTexts[13]        # lineEdit_10
            MNote_B = App.activeDocument().getObject(page).EditableTexts[14]        # lineEdit_11
            MNote_C = App.activeDocument().getObject(page).EditableTexts[15]        # lineEdit_12
            MNote_D = App.activeDocument().getObject(page).EditableTexts[16]        # lineEdit_13
            MNote_E = App.activeDocument().getObject(page).EditableTexts[17]        # lineEdit_14
            MNote_F = App.activeDocument().getObject(page).EditableTexts[18]        # lineEdit_15
            MNote_G = App.activeDocument().getObject(page).EditableTexts[19]        # lineEdit_16
            MNote_H = App.activeDocument().getObject(page).EditableTexts[20]        # lineEdit_17
            MNote_I = App.activeDocument().getObject(page).EditableTexts[21]        # lineEdit_18
        except Exception:
            App.Console.PrintError("Erreur cartouche level DESCRIPTION (Missing field)"+"\n"
                        "You may be using an inadequate template. Try with this template"+"\n")
            App.Console.PrintMessage("http://www.freecadweb.org/wiki/index.php?title=Misc_templates_Full"+"\n\n")
            App.Console.PrintError("Or for the original FreeCAD template use this macro"+"\n")
            App.Console.PrintMessage("http://www.freecadweb.org/wiki/index.php?title=Macro_CartoucheFC"+"\n")        errorDialog("Erreur cartouche level DESCRIPTION (Missing field)"+"\n"
                        "You may be using an inadequate template. Try with this template"+"\n"
                        "http://www.freecadweb.org/wiki/index.php?title=Misc_templates_Full"+"\n\n"
                        "Or for the original FreeCAD template use this macro"+"\n"
                        "http://www.freecadweb.org/wiki/index.php?title=Macro_CartoucheFC"+"\n\n")

    except:
        errorDialog("Erreur cartouche")

class Ui_MainWindow(object):

    def __init__(self, MainWindow):
        global path
        global PageActive
        self.window = MainWindow

        MainWindow.setObjectName(_fromUtf8("MainWindow"))
        MainWindow.resize(810, 400)
        MainWindow.setMaximumSize(QtCore.QSize(810, 400))
        self.centralWidget = QtGui.QWidget(MainWindow)
        self.centralWidget.setObjectName(_fromUtf8("centralWidget"))

#        self.pushButton01 = QtGui.QPushButton(self.centralWidget)
#        self.pushButton01.setGeometry(QtCore.QRect(115, 360, 93, 28))
#        self.pushButton01.setObjectName(_fromUtf8("pushButton01"))
#        self.pushButton01.clicked.connect(self.on_pushButton01_clicked) #connection pushButton01

        self.pushButton02 = QtGui.QPushButton(self.centralWidget)
        self.pushButton02.setGeometry(QtCore.QRect(225, 360, 93, 28))
        self.pushButton02.setObjectName(_fromUtf8("pushButton02"))
        self.pushButton02.clicked.connect(self.on_pushButton02_clicked) #connection pushButton02

        self.pushButton03 = QtGui.QPushButton(self.centralWidget)
        self.pushButton03.setGeometry(QtCore.QRect(335, 360, 93, 28))
        self.pushButton03.setToolTip("The memo button work only with the first Page")
        self.pushButton03.setObjectName(_fromUtf8("pushButton03"))
        self.pushButton03.clicked.connect(self.on_pushButton03_clicked) #connection pushButton03

        self.pushButton04 = QtGui.QPushButton(self.centralWidget)
        self.pushButton04.setGeometry(QtCore.QRect(445, 360, 93, 28))
        self.pushButton04.setObjectName(_fromUtf8("pushButton04"))
        self.pushButton04.clicked.connect(self.on_pushButton04_clicked) #connection pushButton04

        self.pushButton05 = QtGui.QPushButton(self.centralWidget)
        self.pushButton05.setGeometry(QtCore.QRect(555, 360, 93, 28))
#        self.pushButton05.setStyleSheet("background-color: red")       # This function gives a color button
        self.pushButton05.setObjectName(_fromUtf8("pushButton05"))
        self.pushButton05.clicked.connect(self.on_pushButton05_clicked) #connection pushButton05

        #####
        self.groupBox = QtGui.QGroupBox(self.centralWidget)
        self.groupBox.setGeometry(QtCore.QRect(20, 159, 190, 101))
        self.groupBox.setObjectName(_fromUtf8("groupBox"))

        self.label_20 = QtGui.QLabel(self.groupBox)
        self.label_20.setGeometry(QtCore.QRect(115, 5, 61, 17))
        self.label_20.setObjectName(_fromUtf8("label_20"))
        ############### font and color Label
        font = QtGui.QFont()
        font.setBold(True)
        self.label_20.setFont(font)
        self.label_20.setStyleSheet("color : #ff0000")
        ############### font and color
        self.label_20.setVisible(False)

        self.radioButton_0 = QtGui.QRadioButton(self.groupBox)
        self.radioButton_0.setGeometry(QtCore.QRect(95, 1, 91, 17))
        self.radioButton_0.setChecked(True)
        self.radioButton_0.setEnabled(False)
        self.radioButton_0.setVisible(False)
        self.radioButton_0.setObjectName(_fromUtf8("radioButton_0"))

        self.radioButton_1 = QtGui.QRadioButton(self.groupBox)
        self.radioButton_1.setGeometry(QtCore.QRect(95, 20, 91, 17))
        self.radioButton_1.setObjectName(_fromUtf8("radioButton_1"))
        self.radioButton_1.clicked.connect(self.on_radioButton_A3_clicked)# connect radioButton_A3

        self.radioButton_2 = QtGui.QRadioButton(self.groupBox)
        self.radioButton_2.setGeometry(QtCore.QRect(95, 39, 91, 17))
        self.radioButton_2.setObjectName(_fromUtf8("radioButton_2"))
        self.radioButton_2.clicked.connect(self.on_radioButton_A3_clicked)# connect radioButton_A3

        self.radioButton_3 = QtGui.QRadioButton(self.groupBox)
        self.radioButton_3.setGeometry(QtCore.QRect(95, 58, 91, 17))
        self.radioButton_3.setObjectName(_fromUtf8("radioButton_3"))
        self.radioButton_3.clicked.connect(self.on_radioButton_A4_clicked)# connect radioButton_A4

        self.radioButton_4 = QtGui.QRadioButton(self.groupBox)
        self.radioButton_4.setGeometry(QtCore.QRect(95, 76, 91, 17))
        self.radioButton_4.setObjectName(_fromUtf8("radioButton_4"))
        self.radioButton_4.clicked.connect(self.on_radioButton_A4_clicked)# connect radioButton_A4

        self.lineEdit_05 = QtGui.QLineEdit(self.groupBox)
        self.lineEdit_05.setGeometry(QtCore.QRect(10, 16, 75, 41))
        font = QtGui.QFont()
        font.setPointSize(25)
        font.setBold(False)
        font.setWeight(50)
        self.lineEdit_05.setFont(font)
        self.lineEdit_05.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_05.setObjectName(_fromUtf8("lineEdit_05"))
        self.lineEdit_05.setText(SIZE)

        self.frame = QtGui.QFrame(self.groupBox)
        self.frame.setGeometry(QtCore.QRect(10, 58, 74, 41))
        self.frame.setFrameShape(QtGui.QFrame.StyledPanel)
        self.frame.setFrameShadow(QtGui.QFrame.Raised)
        self.frame.setObjectName(_fromUtf8("frame"))

        self.radioButton_EU = QtGui.QRadioButton(self.frame)
        self.radioButton_EU.setGeometry(QtCore.QRect(0, 1, 41, 17))
        self.radioButton_EU.setChecked(True)
        self.radioButton_EU.setObjectName(_fromUtf8("radioButton_EU"))
        self.radioButton_EU.clicked.connect(self.on_radioButton_EU_clicked) #connection radioButton_EU

        self.radioButton_US = QtGui.QRadioButton(self.frame)
        self.radioButton_US.setGeometry(QtCore.QRect(37, 1, 41, 17))
        self.radioButton_US.setObjectName(_fromUtf8("radioButton_US"))
        self.radioButton_US.clicked.connect(self.on_radioButton_US_clicked) #connection radioButton_US

        self.pushButton10 = QtGui.QPushButton(self.frame)
        self.pushButton10.setGeometry(QtCore.QRect(0, 18, 75, 23))
        self.pushButton10.setToolTip("Create the symbol EU or US"+"\n"
                                     "This button is Independent of the Write button"+"\n"
                                     "If you desire modify the symbol in the cartouche,"+"\n"
                                     "delete the inadequate symbol manualy.")
        self.pushButton10.setEnabled(False)
        self.pushButton10.setObjectName(_fromUtf8("pushButton10"))
        self.pushButton10.clicked.connect(self.on_pushButton10_clicked)     #connection pushButton10

        #####

        self.pushButton06 = QtGui.QPushButton(self.centralWidget)
        self.pushButton06.setGeometry(QtCore.QRect(170, 57, 20, 20))
        self.pushButton06.setObjectName(_fromUtf8("pushButton06"))
        self.pushButton06.clicked.connect(self.on_pushButton06_clicked) #connection pushButton06

        self.pushButton07 = QtGui.QPushButton(self.centralWidget)
        self.pushButton07.setGeometry(QtCore.QRect(190, 57, 20, 20))
        self.pushButton07.setObjectName(_fromUtf8("pushButton07"))
        self.pushButton07.clicked.connect(self.on_pushButton07_clicked) #connection pushButton07

        self.pushButton08 = QtGui.QPushButton(self.centralWidget)
        self.pushButton08.setGeometry(QtCore.QRect(170, 137, 20, 20))
        self.pushButton08.setObjectName(_fromUtf8("pushButton08"))
        self.pushButton08.clicked.connect(self.on_pushButton08_clicked) #connection pushButton08

        self.pushButton09 = QtGui.QPushButton(self.centralWidget)
        self.pushButton09.setGeometry(QtCore.QRect(190, 137, 20, 20))
        self.pushButton09.setObjectName(_fromUtf8("pushButton09"))
        self.pushButton09.clicked.connect(self.on_pushButton09_clicked) #connection pushButton09

        self.lineEdit_01 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_01.setGeometry(QtCore.QRect(20, 20, 190, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_01.setFont(font)
        self.lineEdit_01.setObjectName(_fromUtf8("lineEdit_01"))
        self.lineEdit_01.setText(DESIGNED_BY)

        self.lineEdit_02 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_02.setGeometry(QtCore.QRect(20, 60, 82, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_02.setFont(font)
        self.lineEdit_02.setObjectName(_fromUtf8("lineEdit_02"))
        self.lineEdit_02.setText(CREA_DATE)

        self.lineEdit_02h = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_02h.setGeometry(QtCore.QRect(98, 60, 72, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_02h.setFont(font)
        self.lineEdit_02h.setObjectName(_fromUtf8("lineEdit_02h"))
        self.lineEdit_02h.setText(CREA_TIME)

        self.lineEdit_03 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_03.setGeometry(QtCore.QRect(20, 100, 190, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_03.setFont(font)
        self.lineEdit_03.setObjectName(_fromUtf8("lineEdit_03"))
        self.lineEdit_03.setText(CHECKED_BY)

        self.lineEdit_04 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_04.setGeometry(QtCore.QRect(20, 140, 82, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_04.setFont(font)
        self.lineEdit_04.setObjectName(_fromUtf8("lineEdit_04"))
        self.lineEdit_04.setText(CHEC_DATE)

        self.lineEdit_04h = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_04h.setGeometry(QtCore.QRect(98, 140, 72, 16))
        font = QtGui.QFont()
        font.setPointSize(7)
        self.lineEdit_04h.setFont(font)
        self.lineEdit_04h.setObjectName(_fromUtf8("lineEdit_04h"))
        self.lineEdit_04h.setText(CHEC_TIME)

        self.lineEdit_06 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_06.setGeometry(QtCore.QRect(20, 280, 61, 41))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_06.setFont(font)
        self.lineEdit_06.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_06.setObjectName(_fromUtf8("lineEdit_06"))
        self.lineEdit_06.setText(SCALE)

        self.lineEdit_07 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_07.setGeometry(QtCore.QRect(100, 280, 101, 41))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_07.setFont(font)
        self.lineEdit_07.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_07.setObjectName(_fromUtf8("lineEdit_07"))
        self.lineEdit_07.setText(WEIGHT)

        self.lineEdit_08 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_08.setGeometry(QtCore.QRect(220, 280, 341, 41))
        self.lineEdit_08.setObjectName(_fromUtf8("lineEdit_08"))
        self.lineEdit_08.setText(DRAWING_NUMBER)

        self.lineEdit_09 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_09.setGeometry(QtCore.QRect(570, 280, 81, 41))
        self.lineEdit_09.setObjectName(_fromUtf8("lineEdit_09"))
        self.lineEdit_09.setText(SHEET)

        self.lineEdit_20 = QtGui.QLineEdit(self.centralWidget) # Copyright
        self.lineEdit_20.setGeometry(QtCore.QRect(20, 330, 771, 22))
        self.lineEdit_20.setObjectName(_fromUtf8("lineEdit_20"))
        self.lineEdit_20.setText(COPYRIGHT)

        self.lineEdit_10 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_10.setGeometry(QtCore.QRect(690, 290, 101, 30))
        self.lineEdit_10.setObjectName(_fromUtf8("lineEdit_10"))
        self.lineEdit_10.setText(Note_A)

        self.lineEdit_11 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_11.setGeometry(QtCore.QRect(690, 260, 101, 30))
        self.lineEdit_11.setObjectName(_fromUtf8("lineEdit_11"))
        self.lineEdit_11.setText(Note_B)

        self.lineEdit_12 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_12.setGeometry(QtCore.QRect(690, 230, 101, 30))
        self.lineEdit_12.setObjectName(_fromUtf8("lineEdit_12"))
        self.lineEdit_12.setText(Note_C)

        self.lineEdit_13 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_13.setGeometry(QtCore.QRect(690, 200, 101, 30))
        self.lineEdit_13.setObjectName(_fromUtf8("lineEdit_13"))
        self.lineEdit_13.setText(Note_D)

        self.lineEdit_14 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_14.setGeometry(QtCore.QRect(690, 170, 101, 30))
        self.lineEdit_14.setObjectName(_fromUtf8("lineEdit_14"))
        self.lineEdit_14.setText(Note_E)

        self.lineEdit_15 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_15.setGeometry(QtCore.QRect(690, 140, 101, 30))
        self.lineEdit_15.setObjectName(_fromUtf8("lineEdit_15"))
        self.lineEdit_15.setText(Note_F)

        self.lineEdit_16 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_16.setGeometry(QtCore.QRect(690, 110, 101, 30))
        self.lineEdit_16.setObjectName(_fromUtf8("lineEdit_16"))
        self.lineEdit_16.setText(Note_G)

        self.lineEdit_17 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_17.setGeometry(QtCore.QRect(690, 80, 101, 30))
        self.lineEdit_17.setObjectName(_fromUtf8("lineEdit_17"))
        self.lineEdit_17.setText(Note_H)

        self.lineEdit_18 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_18.setGeometry(QtCore.QRect(690, 50, 101, 30))
        self.lineEdit_18.setObjectName(_fromUtf8("lineEdit_18"))
        self.lineEdit_18.setText(Note_I)
##
        self.lineEdit_page = QtGui.QLineEdit(self.centralWidget)         # nom de page
        self.lineEdit_page.setGeometry(QtCore.QRect(20, 365, 181, 20))
        self.lineEdit_page.setToolTip("Name page to work"+"\n"
                                      "The name of the first page is always named 'Page'"
                                      "Select the new page in the Combo view")
        self.lineEdit_page.setObjectName(_fromUtf8("lineEdit_page"))
        self.lineEdit_page.setEnabled(False)
        self.lineEdit_page.setStyleSheet("color: red")
        self.lineEdit_page.setText(PageActive)
        self.lineEdit_page.textChanged.connect(self.on_lineEdit_page_Pressed) # 

        self.label_01T = QtGui.QLabel(self.centralWidget)
        self.label_01T.setGeometry(QtCore.QRect(220, 0, 91, 16))
        self.label_01T.setObjectName(_fromUtf8("label_01T"))

        self.textEdit_01 = QtGui.QTextEdit(self.centralWidget)            # Title
        self.textEdit_01.setGeometry(QtCore.QRect(220, 20, 431,55 ))
        font = QtGui.QFont()
        font.setPointSize(15)
        font.setBold(True)
        font.setWeight(75)
        self.textEdit_01.setFont(font)
        self.textEdit_01.setObjectName(_fromUtf8("textEdit_01"))
        self.textEdit_01.setText(TITLE)

        self.label_02T = QtGui.QLabel(self.centralWidget)
        self.label_02T.setGeometry(QtCore.QRect(220, 80, 101, 16))
        self.label_02T.setObjectName(_fromUtf8("label_02T"))

        self.textEdit_02 = QtGui.QTextEdit(self.centralWidget)            # DESCRIPTION
        self.textEdit_02.setGeometry(QtCore.QRect(220, 100, 431, 55))
        self.textEdit_02.setObjectName(_fromUtf8("textEdit_02"))
        self.textEdit_02.setText(DESCRIPTION)

        self.label_02bT = QtGui.QLabel(self.centralWidget)
        self.label_02bT.setGeometry(QtCore.QRect(220, 160, 90, 16))
        self.label_02bT.setObjectName(_fromUtf8("label_02bT"))

        self.textEdit_02b = QtGui.QTextEdit(self.centralWidget)            # COMPANY
        self.textEdit_02b.setGeometry(QtCore.QRect(220, 180, 340, 60))
        self.textEdit_02b.setObjectName(_fromUtf8("textEdit_02b"))
        self.textEdit_02b.setText(COMPANY)

        self.label_01 = QtGui.QLabel(self.centralWidget)
        self.label_01.setGeometry(QtCore.QRect(20, 0, 91, 16))
        self.label_01.setObjectName(_fromUtf8("label_01"))

        self.label_02 = QtGui.QLabel(self.centralWidget)
        self.label_02.setGeometry(QtCore.QRect(20, 40, 53, 16))
        self.label_02.setObjectName(_fromUtf8("label_02"))

        self.label_03 = QtGui.QLabel(self.centralWidget)
        self.label_03.setGeometry(QtCore.QRect(20, 80, 101, 16))
        self.label_03.setObjectName(_fromUtf8("label_03"))

        self.label_04 = QtGui.QLabel(self.centralWidget)
        self.label_04.setGeometry(QtCore.QRect(20, 120, 91, 16))
        self.label_04.setObjectName(_fromUtf8("label_04"))

        self.label_06 = QtGui.QLabel(self.centralWidget)
        self.label_06.setGeometry(QtCore.QRect(20, 260, 53, 16))
        self.label_06.setObjectName(_fromUtf8("label_06"))

        self.label_07 = QtGui.QLabel(self.centralWidget)
        self.label_07.setGeometry(QtCore.QRect(100, 260, 101, 16))
        self.label_07.setObjectName(_fromUtf8("label_07"))

        self.label_08 = QtGui.QLabel(self.centralWidget)
        self.label_08.setGeometry(QtCore.QRect(220, 260, 121, 16))
        self.label_08.setObjectName(_fromUtf8("label_08"))

        self.label_09 = QtGui.QLabel(self.centralWidget)
        self.label_09.setGeometry(QtCore.QRect(570, 260, 53, 16))
        self.label_09.setObjectName(_fromUtf8("label_09"))

        self.label_10 = QtGui.QLabel(self.centralWidget)
        self.label_10.setGeometry(QtCore.QRect(670, 290, 16, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_10.setFont(font)
        self.label_10.setObjectName(_fromUtf8("label_10"))

        self.label_11 = QtGui.QLabel(self.centralWidget)
        self.label_11.setGeometry(QtCore.QRect(670, 260, 16, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_11.setFont(font)
        self.label_11.setObjectName(_fromUtf8("label_11"))

        self.label_12 = QtGui.QLabel(self.centralWidget)
        self.label_12.setGeometry(QtCore.QRect(670, 230, 16, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_12.setFont(font)
        self.label_12.setObjectName(_fromUtf8("label_12"))

        self.label_13 = QtGui.QLabel(self.centralWidget)
        self.label_13.setGeometry(QtCore.QRect(670, 200, 18, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_13.setFont(font)
        self.label_13.setObjectName(_fromUtf8("label_13"))

        self.label_14 = QtGui.QLabel(self.centralWidget)
        self.label_14.setGeometry(QtCore.QRect(670, 170, 15, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_14.setFont(font)
        self.label_14.setObjectName(_fromUtf8("label_14"))

        self.label_15 = QtGui.QLabel(self.centralWidget)
        self.label_15.setGeometry(QtCore.QRect(670, 140, 14, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_15.setFont(font)
        self.label_15.setObjectName(_fromUtf8("label_15"))

        self.label_16 = QtGui.QLabel(self.centralWidget)
        self.label_16.setGeometry(QtCore.QRect(670, 110, 18, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_16.setFont(font)
        self.label_16.setObjectName(_fromUtf8("label_16"))

        self.label_17 = QtGui.QLabel(self.centralWidget)
        self.label_17.setGeometry(QtCore.QRect(670, 80, 18, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_17.setFont(font)
        self.label_17.setObjectName(_fromUtf8("label_17"))

        self.label_18 = QtGui.QLabel(self.centralWidget)
        self.label_18.setGeometry(QtCore.QRect(670, 50, 10, 33))
        font = QtGui.QFont()
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.label_18.setFont(font)
        self.label_18.setObjectName(_fromUtf8("label_18"))

        self.label_19 = QtGui.QLabel(self.centralWidget)
        self.label_19.setGeometry(QtCore.QRect(720, 15, 100, 33))
        self.label_19.setObjectName(_fromUtf8("label_19"))

        self.label_page = QtGui.QLabel(self.centralWidget)
        self.label_page.setGeometry(QtCore.QRect(20, 350, 181, 16))
        self.label_page.setObjectName(_fromUtf8("label_page"))

        self.label_Version = QtGui.QLabel(self.centralWidget)        # Version
        self.label_Version.setGeometry(QtCore.QRect(685, 383, 121, 20))
        self.label_Version.setObjectName(_fromUtf8("label_Version"))

        MainWindow.setCentralWidget(self.centralWidget)

        self.retranslateUi(MainWindow)
        QtCore.QMetaObject.connectSlotsByName(MainWindow)

    def retranslateUi(self, MainWindow):
        MainWindow.setWindowFlags(PySide.QtCore.Qt.WindowStaysOnTopHint) # cette fonction met la fenetre en avant
        MainWindow.setWindowTitle("Cartouche (Full)")
#        self.pushButton01.setText("Position")
        self.pushButton02.setText("Quit") #Quitter
        self.pushButton03.setText("Memo")
        self.pushButton04.setText("Clean")#Nettoyer
        self.pushButton05.setText("Write")#Appliquer
        self.pushButton06.setText("D.")
        self.pushButton07.setText("H.")
        self.pushButton08.setText("D.")
        self.pushButton09.setText("H.")
        self.pushButton10.setText("Create Symb.")

        self.label_01.setText("Designed by :")
        self.label_02.setText("Date :")
        self.label_03.setText("Checked by :")
        self.label_04.setText("Date :")
        self.label_06.setText("Scale :")
        self.label_07.setText("Weight (Kg) :")
        self.label_08.setText("Drawing number :")
        self.label_01T.setText("Title :")
        self.label_02T.setText("Description :")
        self.label_02bT.setText("Company :")
        self.label_09.setText("Sheet :")

        self.label_10.setText("A")
        self.label_11.setText("B")
        self.label_12.setText("C")
        self.label_13.setText("D")
        self.label_14.setText("E")
        self.label_15.setText("F")
        self.label_16.setText("G")
        self.label_17.setText("H")
        self.label_18.setText("I")
        self.label_19.setText("Notes")
        self.label_20.setText("Warning")
        self.label_page.setText("Name page to work")
        self.label_Version.setText("Ver: 00.10 15/02/2017")        # Version
        self.groupBox.setTitle("Size :")
        self.radioButton_1.setText("A3 Landscape")
        self.radioButton_2.setText("A3 Portrait")
        self.radioButton_3.setText("A4 Landscape")
        self.radioButton_4.setText("A4 Portrait")
        self.radioButton_EU.setText("EU")
        self.radioButton_US.setText("US")
        self.lineEdit_05.setText("?")

#______________________________________________________________________________________
    # Radio Boutons
    def on_radioButton_A3_clicked(self):  # connect radioButton_A3
        self.label_20.setVisible(False)
        self.pushButton10.setEnabled(True)
        self.lineEdit_05.setText("A3")
        self.pushButton10.setStyleSheet("color: QPalette.Base")           # origin system

    def on_radioButton_A4_clicked(self):  # connect radioButton_A4
        self.label_20.setVisible(False)
        self.pushButton10.setEnabled(True)
        self.lineEdit_05.setText("A4")
        self.pushButton10.setStyleSheet("color: QPalette.Base")           # origin system
    # Radio Boutons

    def on_radioButton_EU_clicked(self):    # Bouton /Symbole EU
        global SymbolSwitch
        SymbolSwitch = 1

    def on_radioButton_US_clicked(self):    # Bouton /Symbole US
        global SymbolSwitch
        SymbolSwitch = 0

    def on_pushButton10_clicked(self):      # Bouton /Symbole EU US disposition dans le cartouche
        global SymbolSwitch
        global PageActive
        self.label_20.setVisible(False)

        if self.radioButton_0.isChecked():
            self.label_20.setVisible(True)
            self.pushButton10.setEnabled(False)
            self.pushButton10.setStyleSheet("color: red")
            self.lineEdit_page.setStyleSheet("color: red")
            FreeCAD.Console.PrintError("Select one format A3 or A4 for the Symbole" + "\n")
        else:
            self.pushButton10.setEnabled(True)
            self.pushButton10.setStyleSheet("background-color: #FF5B2B")
            self.pushButton10.setText("Wait.")
            FreeCADGui.updateGui()                # rafraichi l'ecran
            if SymbolSwitch == 1:
                if self.radioButton_1.isChecked():
                    symbol_EU(247.5, 263.5, 0.8)  # A3 Landscape
                elif self.radioButton_2.isChecked():
                    symbol_EU(124.55, 386.3, 0.8) # A3 Portrait
                elif self.radioButton_3.isChecked():
                    symbol_EU(158.7, 181.35, 0.6) # A4 Landscape
                elif self.radioButton_4.isChecked():
                    symbol_EU(71.9, 269.0, 0.6)   # A4 Portrait
            else:
                if self.radioButton_1.isChecked():
                    symbol_US(247.5, 263.5, 0.8)  # A3 Landscape
                elif self.radioButton_2.isChecked():
                    symbol_US(124.55, 386.3, 0.8) # A3 Portrait
                elif self.radioButton_3.isChecked():
                    symbol_US(158.7, 181.35, 0.6) # A4 Landscape
                elif self.radioButton_4.isChecked():
                    symbol_US(71.9, 269.0, 0.6)   # A4 Portrait
            self.pushButton10.setStyleSheet("color: QPalette.Base")           # origin system
            self.pushButton10.setText("Create Symb.")
            FreeCADGui.updateGui()                                 # rafraichi l'ecran
        
    def on_lineEdit_page_Pressed(self):   # Name page
        global PageActive
        PageActive = self.lineEdit_page.text()

    def on_pushButton09_clicked(self):    # Bouton /heure document
        self.lineEdit_04h.setText(str(heure()))

    def on_pushButton08_clicked(self):    # Bouton date/ document
        global SymbolSwitch
        if SymbolSwitch==0:
            self.lineEdit_04.setText(str(dateUs()))
        else:
            self.lineEdit_04.setText(str(dateEu()))

    def on_pushButton07_clicked(self):    # Bouton /heure checked
        self.lineEdit_02h.setText(str(heure()))

    def on_pushButton06_clicked(self):    # Bouton date/ checked
        global SymbolSwitch
        if SymbolSwitch==0:
            self.lineEdit_02.setText(str(dateUs()))
        else:
            self.lineEdit_02.setText(str(dateEu()))

    def on_pushButton05_clicked(self):    # Bouton Appliquer
        try:
            global DESIGNED_BY, CREATION_DATE, CREA_DATE  , CREA_TIME, CHECKED_BY, CHECK_DATE
            global CHEC_DATE  , CHEC_TIME    , SIZE       , SCALE    , WEIGHT    ,DRAWING_NUMBER
            global SHEET      , TITLE        , DESCRIPTION, COMPANY  , COPYRIGHT
            global Note_A, Note_B, Note_C, Note_D, Note_E, Note_F, Note_G, Note_H, Note_I
            global ui
            global SymbolSwitch
            global PageActive

            try:
                page = App.activeDocument().getObjectsByLabel(PageActive.encode('utf-8'))[0]
            except Exception:
                page = App.activeDocument().getObjectsByLabel(PageActive)[0]        if len(str(page)) != 2:            self.pushButton05.setStyleSheet("background-color: #FF5B2B")
                self.pushButton05.setText("Wait.")
                FreeCADGui.updateGui()                # rafraichi l'ecran

                DESIGNED_BY = (self.lineEdit_01.text())
                CREATION_DATE = (self.lineEdit_02.text())+" - "+(self.lineEdit_02h.text())
                CHECKED_BY = (self.lineEdit_03.text())
                CHECK_DATE = (self.lineEdit_04.text())+" - "+(self.lineEdit_04h.text())
                SIZE = (self.lineEdit_05.text())
                SCALE = (self.lineEdit_06.text())
                WEIGHT = (self.lineEdit_07.text())
                DRAWING_NUMBER = (self.lineEdit_08.text())
                SHEET = (self.lineEdit_09.text())
                TITLE = (self.textEdit_01.toPlainText())
                DESCRIPTION = (self.textEdit_02.toPlainText())
                COMPANY = (self.textEdit_02b.toPlainText())
                COPYRIGHT = (self.lineEdit_20.text())            Note_A = (self.lineEdit_10.text())
                Note_B = (self.lineEdit_11.text())
                Note_C = (self.lineEdit_12.text())
                Note_D = (self.lineEdit_13.text())
                Note_E = (self.lineEdit_14.text())
                Note_F = (self.lineEdit_15.text())
                Note_G = (self.lineEdit_16.text())
                Note_H = (self.lineEdit_17.text())
                Note_I = (self.lineEdit_18.text())            try:
                    FreeCAD.getDocument(App.ActiveDocument.Name).getObject(page.Name).EditableTexts = [DESIGNED_BY, CREATION_DATE, CHECKED_BY, CHECK_DATE, SIZE, SCALE, WEIGHT, DRAWING_NUMBER, SHEET, TITLE, DESCRIPTION, COMPANY, COPYRIGHT, Note_A, Note_B, Note_C, Note_D, Note_E, Note_F, Note_G, Note_H, Note_I, ]
#old                    FreeCAD.getDocument(App.ActiveDocument.Name).getObjectsByLabel(PageActive.encode('utf-8'))[0].EditableTexts = [DESIGNED_BY, CREATION_DATE, CHECKED_BY, CHECK_DATE, SIZE, SCALE, WEIGHT, DRAWING_NUMBER, SHEET, TITLE, DESCRIPTION, COMPANY, COPYRIGHT, Note_A, Note_B, Note_C, Note_D, Note_E, Note_F, Note_G, Note_H, Note_I, ]
                    App.ActiveDocument.recompute()
                    FreeCAD.Console.PrintMessage("Write done to ( " + page.Label + " )" + "\n")
                    self.pushButton05.setStyleSheet("color: QPalette.Base")
                except Exception:
                    FreeCAD.Console.PrintError("Error write cartouche or verify the selected page ( " + page.Label + " )" + "\n")
                    self.pushButton05.setStyleSheet("background-color: red")
            else:
                FreeCAD.Console.PrintError("Error selected page ( " + Page.Label + " )" + "\n")
                self.pushButton05.setStyleSheet("background-color: red")

        except Exception:
            self.pushButton05.setStyleSheet("background-color: red")
            FreeCAD.Console.PrintError("Error or not page " + "\n")
        self.pushButton05.setText("Write")
        App.ActiveDocument.recompute()

    def on_pushButton04_clicked(self):    # Bouton nettoyer

        self.lineEdit_01.setText("")
        self.lineEdit_02.setText("")
        self.lineEdit_02h.setText("")
        self.lineEdit_03.setText("")
        self.lineEdit_04.setText("")
        self.lineEdit_04h.setText("")
        self.lineEdit_05.setText("?")
        self.lineEdit_06.setText("")
        self.lineEdit_07.setText("")
        self.lineEdit_08.setText("")
        self.lineEdit_09.setText("")
        self.textEdit_01.setText("")
        self.textEdit_02.setText("")
        self.textEdit_02b.setText("")
        self.lineEdit_20.setText("")
        self.lineEdit_10.setText("")
        self.lineEdit_11.setText("")
        self.lineEdit_12.setText("")
        self.lineEdit_13.setText("")
        self.lineEdit_14.setText("")
        self.lineEdit_15.setText("")
        self.lineEdit_16.setText("")
        self.lineEdit_17.setText("")
        self.lineEdit_18.setText("")

        self.pushButton10.setStyleSheet("color: QPalette.Base")                # origin system
        self.label_20.setVisible(False)
        self.radioButton_0.setChecked(True)
        self.pushButton05.setEnabled(True)
        self.pushButton05.setStyleSheet("background-color: QPalette.Base")     # origin system
        self.groupBox.setEnabled(True)

    def on_pushButton03_clicked(self):    # Bouton Memo
        global MDESIGNED_BY, MCREATION_DATE, MCREA_DATE  , MCREA_TIME, MCHECKED_BY, MCHECK_DATE
        global MCHEC_DATE  , MCHEC_TIME    , MSIZE       , MSCALE    , MWEIGHT    ,MDRAWING_NUMBER
        global MSHEET      , MTITLE        , MDESCRIPTION, MCOMPANY  , MCOPYRIGHT
        global MNote_A, MNote_B, MNote_C, MNote_D, MNote_E, MNote_F, MNote_G, MNote_H, MNote_I
        
        self.lineEdit_01.setText(MDESIGNED_BY)
        self.lineEdit_02.setText(MCREA_DATE)
        self.lineEdit_02h.setText(MCREA_TIME)
        self.lineEdit_03.setText(MCHECKED_BY)
        self.lineEdit_04.setText(MCHEC_DATE)
        self.lineEdit_04h.setText(MCHEC_TIME)
        self.lineEdit_05.setText("?") #(SIZE)
        self.lineEdit_06.setText(MSCALE)
        self.lineEdit_07.setText(MWEIGHT)
        self.lineEdit_08.setText(MDRAWING_NUMBER)
        self.lineEdit_09.setText(MSHEET)
        self.textEdit_01.setText(MTITLE)
        self.textEdit_02.setText(MDESCRIPTION)
        self.textEdit_02b.setText(MCOMPANY)
        self.lineEdit_20.setText(MCOPYRIGHT)
        self.lineEdit_10.setText(MNote_A)
        self.lineEdit_11.setText(MNote_B)
        self.lineEdit_12.setText(MNote_C)
        self.lineEdit_13.setText(MNote_D)
        self.lineEdit_14.setText(MNote_E)
        self.lineEdit_15.setText(MNote_F)
        self.lineEdit_16.setText(MNote_G)
        self.lineEdit_17.setText(MNote_H)
        self.lineEdit_18.setText(MNote_I)
#        self.lineEdit_page.setText(PageActive)
        self.radioButton_0.setChecked(True)

    def on_pushButton02_clicked(self):    # Bouton Quitter
        App.Console.PrintMessage("End CartoucheFC_Full\r\n")
        self.window.hide()
        FreeCADGui.Selection.removeObserver(s)           # Uninstalls the resident function
        App.Console.PrintMessage("removeObserver"+"\n")

#    def on_pushButton01_clicked(self):    # Bouton appel de Position
#        MainWindow.resize(210, 480)
#        executer()
#        MainWindow.resize(810, 480)
#______________________________________________________________________________________

class SelObserver:
    print "run.."
    def setSelection(self,document):                     # Selection in ComboView
        global PageActive
        global ui
        if len(Gui.Selection.getSelection(document)) == 1:

            ff = ui
            ff.lineEdit_page.setStyleSheet("color: QPalette.Base")           # origin system
            ff.pushButton05.setEnabled(True)
            ff.pushButton05.setStyleSheet("background-color: QPalette.Base") # origin system
            ff.groupBox.setEnabled(True)

            if (str(Gui.Selection.getSelection(document)[0].Name[0:4]) == "Page"):
                PageActive = str(Gui.Selection.getSelection(document)[0].Label.encode('utf-8'))
                try:
                    ff.lineEdit_page.setText(unicode(PageActive,'utf-8'))    # convert if accent
                except Exception:
                    ff.lineEdit_page.setText(PageActive)                     # normal

                memoEntree()                    # entree memo click mouse
                ff.on_pushButton03_clicked()    # Bouton Memo
            else:
                FreeCAD.Console.PrintError("Select a valid Page__________________________" + "\n")
                ff.lineEdit_page.setStyleSheet("color: red")
                ff.lineEdit_page.setText("Select a valid Page")              # 
                ff.pushButton05.setEnabled(False)
                ff.pushButton05.setStyleSheet("background-color: red")       # This function gives a color button
                ff.groupBox.setEnabled(False)

                FreeCAD.Console.PrintMessage("                 " + "Name            Label" + "\n")
                for i in App.ActiveDocument.Objects:
                    if i.Name[0:4] == "Page":
                        name = i.Name + "                 "
                        labe = i.Label+ "                 "
                        FreeCAD.Console.PrintMessage("    Valid Page : " + name[:15] + "," + labe[:25] + "\n")
                FreeCAD.Console.PrintError("_____________________________________________" + "\n")

for obj in FreeCAD.ActiveDocument.Objects:        # deslectionne
        FreeCADGui.Selection.removeSelection(obj)

s=SelObserver()
FreeCADGui.Selection.addObserver(s)               # install the function mode resident 

MainWindow = QtGui.QMainWindow()
ui = Ui_MainWindow(MainWindow)
MainWindow.show()
}}

## Autre 

Les champs n\'ont pas de limite de longueur, vérifiez l\'affichage dans votre cartouche.

Ce programme crée sur votre projet un dessin représentant le symbole régional de projection, n\'y touchez pas, il est enregistré sous forme cachée donc invisible.

Si vous voulez qu\'il soit effacée dé-commentez les lignes commentées et vice versa.


```python

#    App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_EU")
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_EU").Visibility = False
```

et 
```python

#    App.getDocument(App.ActiveDocument.Name).removeObject("Symbol_US")
    FreeCADGui.getDocument(App.ActiveDocument.Name).getObject("Symbol_US").Visibility = False
``` (j\'avais quelque fois une erreur à l\'exécution quand le symbole était effacé)

Vous pouvez aussi utiliser une feuille avec le symbole présent dans le cartouche et ne pas utiliser cette fonction.

Ce module travaille avec le module de mise en plan de FreeCAD la feuille s\'appelle **Page**, ne pas modifier le nom de cette page !

## Version

ver \"00.10\" : 15/02/2017 : réglage pour pages multiples (Il est possible de perdre une page s\'il y en a trop ! )

ver \"00.09\" : 10/02/2017 : ajout de boutons radio pour le choix du type de symbole et correction de la position du symbole dans les pages (la précédente version effaçait le symbole d\'une page pour le reconstruire dans la nouvelle page) et ajout sélection par souris et de tests sur le choix des pages

ver \"00.08 : 06/02/2017 : La boîte de dialoguenom de la page accepteles accents et autres caractères

ver \"00.07 : 05/02/2017 : ajout d\'une fenêtre \"Nom\" pour pouvoir remplir le cartouche de différentes feuilles dans le même projet PS: les caracteres accentué ne sont pas acceptés \"àùé \...\"

ver 00.06 : 13/10/2016 : sélection du format de la page et position automatique du symbole de convention (pour FreeCAD ver 0.17)

ver 5 : 08/08/2014 PyQt4 and PySide


</div>


</div>





<div class="mw-collapsible mw-collapsed toccolours">

# Macro CartoucheFC 2 


<div class="mw-collapsible-content">


{{Macro
|Name=Macro CartoucheFC 2
|Icon=Macro_CartoucheFC_2.png
|Description=This macro is a complete application, it allows to fill the cartridge of the drawing sheet with full editabletext (Only For [Drawing Workbench](Drawing_Workbench.md)).
|Author=Mario52
|Version=5.0
|Date=2014-08-08
|FCVersion=All version using Drawing WorkBench
|Download=[https://www.freecadweb.org/wiki/images/0/00/Macro_CartoucheFC_2.png ToolBar Icon]
}}

## Description 

This macro is a complete application, it allows to fill simply all the fields of the cartridge A3 Landscape english

<img alt="Macro CartoucheFC Modele 2" src=images/Macro_CartoucheFC_Modele_02.png  style="width:680px;">

The picture represents the hierarchy of filling the fields occupied in the \"textEditable\" window in FreeCAD

## Utilisation 

Usage is very easy, run the macro and modify the fields.

-   The **Quit** button to exit the application.
-   The **Memo** button renders the contents of the cartridge at the opening of the macro.
-   The **Clear** button clean all the fields in the macro (fields are rendered by pressing on the **Memo**).
-   The **Apply** button applies the changes to the template.

The window stays above all windows to visualize the changes (this function can be unpleasant if you decide to open a new window and remains unavailable)

**PS: Some characters such as & \$ are not accepted (and possibly other special characters).**

If you have any questions or want to add a function, you can address you on the french forum [Remplir cartouche](http://forum.freecadweb.org/viewtopic.php?f=12&t=2049)

## Code 

ToolBar Icon ![](images/Macro_CartoucheFC_2.png )

**Macro_CartoucheFC_2.FcMacro**


{{MacroCode|code=

# -*- coding: utf-8 -*-
"""
***************************************************************************
*   Copyright (c) 2014 <mario52>                                          *
*                                                                         *
*   This file is a supplement to the FreeCAD CAD development system.      *
*                                                                         *
*   This program is free software; you can redistribute it and/or modify  *
*   it under the terms of the GNU Lesser General Public License (LGPL)    *
*   as published by the Free Software Foundation; either version 2 of     *
*   the License, or (at your option) any later version.                   *
*   for detail see the LICENCE text file.                                 *
*                                                                         *
*   This software is distributed in the hope that it will be useful,      *
*   but WITHOUT ANY WARRANTY; without even the implied warranty of        *
*   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the         *
*   GNU Library General Public License for more details.                  *
*                                                                         *
*   You should have received a copy of the GNU Library General Public     *
*   License along with this macro; if not, write to the Free Software     *
*   Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  *
*   USA                                                                   *
***************************************************************************
*           WARNING! All changes in this file will be lost and            *  
*                  may cause malfunction of the program                   *
***************************************************************************
"""
# Macro_CartoucheFC_2.FcMacro
# 
# il faut que la page (drawing viewer) s'appelle " Page " qui est le nom par défaut du module Drawing
# cette macro fonctionne avec la feuille A3_Landscape_ qui possede tous les champs EditableTexts
# 
# http://www.freecadweb.org/wiki/index.php?title=Drawing_templates
# Fill the area of the cartridge
# It is necessary that the page (drawing viewer) is called "Page", which is the default name of the Drawing module
# Python 2.6
# 08/08/2014 ver 5.0 (pour cartouche modèle 2 (A3 Landscape english)) # PyQt and PySide 
# Created:  by mario52
# PyQt and PySide 

#OS: Windows Vista
#Word size: 32-bit
#Version: 0.14.3700 (Git)
#Branch: releases/FreeCAD-0-14
#Hash: 32f5aae0a64333ec8d5d160dbc46e690510c8fe1
#Python version: 2.6.2
#Qt version: 4.5.2
#Coin version: 3.1.0
#SoQt version: 1.4.1

try:
    import PyQt4                        # PyQt4
    from PyQt4 import QtCore, QtGui     # PyQt4
except Exception:
    import PySide                       # PySide
    from PySide import QtCore, QtGui    # PySide

import Draft, Part, FreeCAD, math, PartGui, FreeCADGui
from math import sqrt, pi, sin, cos, asin
from FreeCAD import Base

def utf8(unio):
    return unicode(unio).encode('UTF8')

global path
global Drawn_by               ; Drawn_by       = ""   # lineEdit_001
global DRAWN_BY               ; DRAWN_BY       = ""   # lineEdit_002
global Controlled_by          ; Controlled_by  = ""   # lineEdit_003
global CONTROLLED_BY          ; CONTROLLED_BY  = ""   # lineEdit_004
global Date                   ; Date           = ""   # lineEdit_005
global DATE                   ; DATE           = ""   # lineEdit_006
global Controlled_2           ; Controlled_2   = ""   # lineEdit_007
global CONTROLLED_2           ; CONTROLLED_2   = ""   # lineEdit_008
global Controlled_3           ; Controlled_3   = ""   # lineEdit_009
global CONTROLLED_3           ; CONTROLLED_3   = ""   # lineEdit_010
global SCALE                  ; SCALE          = ""   # lineEdit_011
global MOD                    ; MOD            = ""   # lineEdit_012
global COMPANY                ; COMPANY        = ""   # lineEdit_013
global ADRESS                 ; ADRESS         = ""   # lineEdit_014
global COUNTRY                ; COUNTRY        = ""   # lineEdit_015
global PART_NAME              ; PART_NAME      = ""   # lineEdit_016
global Project_number         ; Project_number = ""   # lineEdit_017
global A_                     ; A_             = ""   # lineEdit_018
global A__                    ; A__            = ""   # lineEdit_019
global B_                     ; B_             = ""   # lineEdit_020
global B__                    ; B__            = ""   # lineEdit_021
global C_                     ; C_             = ""   # lineEdit_022
global C__                    ; C__            = ""   # lineEdit_023
global D_                     ; D_             = ""   # lineEdit_024
global D__                    ; D__            = ""   # lineEdit_025
global E_                     ; E_             = ""   # lineEdit_026
global E__                    ; E__            = ""   # lineEdit_027
global Quantity               ; Quantity       = ""   # lineEdit_028
global Part_ID_number         ; Part_ID_number = ""   # lineEdit_029
global Fabrication_tolerances ; Fabrication_tolerance = "" #lineEdit_030
global Material               ; Material       = ""   # lineEdit_031
global _01                    ; _01            = ""   # lineEdit_032
global _001_001               ; _001_001       = ""   # lineEdit_033
global ISO2768_fh             ; ISO2768_fh     = ""   # lineEdit_034
global IRON                   ; IRON           = ""   # lineEdit_035

path = FreeCAD.ConfigGet("AppHomePath")

try:
    _fromUtf8 = QtCore.QString.fromUtf8
except AttributeError:
    def _fromUtf8(s):
        return s
try:
    _encoding = QtGui.QApplication.UnicodeUTF8
    def _translate(context, text, disambig):
        return QtGui.QApplication.translate(context, text, disambig, _encoding)
except AttributeError:
    def _translate(context, text, disambig):
        return QtGui.QApplication.translate(context, text, disambig)

def errorDialog(msg):
    # Create a simple dialog QMessageBox
    # The first argument indicates the icon used: one of QtGui.QMessageBox.{NoIcon, Information, Warning, Critical, Question} 
    diag = QtGui.QMessageBox(QtGui.QMessageBox.Critical,u"Error Message",msg)
    try:
        diag.setWindowFlags(PyQt4.QtCore.Qt.WindowStaysOnTopHint)  # PyQt4 cette fonction met la fenêtre en avant
    except Exception:
        diag.setWindowFlags(PySide.QtCore.Qt.WindowStaysOnTopHint) # PySide cette fonction met la fenêtre en avant
    #diag.setWindowModality(QtCore.Qt.ApplicationModal) # la fonction a été désactivée pour favoriser "WindowStaysOnTopHint"
    diag.exec_()

try:
    Drawn_by = App.activeDocument().getObject("Page").EditableTexts[0]          # lineEdit_001
    DRAWN_BY = App.activeDocument().getObject("Page").EditableTexts[1]          # lineEdit_002
    Controlled_by = App.activeDocument().getObject("Page").EditableTexts[2]     # lineEdit_003
    CONTROLLED_BY = App.activeDocument().getObject("Page").EditableTexts[3]     # lineEdit_004
    Date = App.activeDocument().getObject("Page").EditableTexts[4]              # lineEdit_005
    DATE = App.activeDocument().getObject("Page").EditableTexts[5]              # lineEdit_006
    Controlled_2 = App.activeDocument().getObject("Page").EditableTexts[6]      # lineEdit_007
    CONTROLLED_2 = App.activeDocument().getObject("Page").EditableTexts[7]      # lineEdit_008
    Controlled_3 = App.activeDocument().getObject("Page").EditableTexts[8]      # lineEdit_009
    CONTROLLED_3 = App.activeDocument().getObject("Page").EditableTexts[9]      # lineEdit_010
    SCALE = App.activeDocument().getObject("Page").EditableTexts[10]            # lineEdit_011
    MOD = App.activeDocument().getObject("Page").EditableTexts[11]              # lineEdit_012
    COMPANY = App.activeDocument().getObject("Page").EditableTexts[12]          # lineEdit_013
    ADRESS = App.activeDocument().getObject("Page").EditableTexts[13]           # lineEdit_014
    COUNTRY = App.activeDocument().getObject("Page").EditableTexts[14]          # lineEdit_015
    PART_NAME = App.activeDocument().getObject("Page").EditableTexts[15]        # lineEdit_016
    Project_number = App.activeDocument().getObject("Page").EditableTexts[16]   # lineEdit_017
    A_ = App.activeDocument().getObject("Page").EditableTexts[17]               # lineEdit_018
    A__ = App.activeDocument().getObject("Page").EditableTexts[18]              # lineEdit_019
    B_ = App.activeDocument().getObject("Page").EditableTexts[19]               # lineEdit_020
    B__ = App.activeDocument().getObject("Page").EditableTexts[20]              # lineEdit_021
    C_ = App.activeDocument().getObject("Page").EditableTexts[21]               # lineEdit_022
    C__ = App.activeDocument().getObject("Page").EditableTexts[22]              # lineEdit_023
    D_ = App.activeDocument().getObject("Page").EditableTexts[23]               # lineEdit_024
    D__ = App.activeDocument().getObject("Page").EditableTexts[24]              # lineEdit_025
    E_ = App.activeDocument().getObject("Page").EditableTexts[25]               # lineEdit_026
    E__ = App.activeDocument().getObject("Page").EditableTexts[26]              # lineEdit_027
    Quantity= App.activeDocument().getObject("Page").EditableTexts[27]          # lineEdit_028
    Part_ID_number = App.activeDocument().getObject("Page").EditableTexts[28]   # lineEdit_029
    Fabrication_tolerance = App.activeDocument().getObject("Page").EditableTexts[29] #lineEdit_030
    Material = App.activeDocument().getObject("Page").EditableTexts[30]         # lineEdit_031
    _01 = App.activeDocument().getObject("Page").EditableTexts[31]              # lineEdit_032
    _001_001 = App.activeDocument().getObject("Page").EditableTexts[32]         # lineEdit_033
    ISO2768_fh = App.activeDocument().getObject("Page").EditableTexts[33]       # lineEdit_034
    IRON = App.activeDocument().getObject("Page").EditableTexts[34]             # lineEdit_035

except:
    errorDialog("Error read cartridge")

class Ui_MainWindow(object):

    def __init__(self, MainWindow):
        self.window = MainWindow

        MainWindow.setObjectName(_fromUtf8("MainWindow"))
        MainWindow.resize(849, 462)
        MainWindow.setMaximumSize(QtCore.QSize(849, 462))
        self.centralWidget = QtGui.QWidget(MainWindow)
        self.centralWidget.setObjectName(_fromUtf8("centralWidget"))

        self.pushButton02 = QtGui.QPushButton(self.centralWidget)
        self.pushButton02.setGeometry(QtCore.QRect(210, 420, 93, 28))
        self.pushButton02.setObjectName(_fromUtf8("pushButton_2"))
        self.pushButton02.clicked.connect(self.on_pushButton02_clicked) # Bouton Quitter # Quit

        self.pushButton03 = QtGui.QPushButton(self.centralWidget)
        self.pushButton03.setGeometry(QtCore.QRect(320, 420, 93, 28))
        self.pushButton03.setObjectName(_fromUtf8("pushButton_3"))
        self.pushButton03.clicked.connect(self.on_pushButton03_clicked) # Bouton Memo # Memo

        self.pushButton04 = QtGui.QPushButton(self.centralWidget)
        self.pushButton04.setGeometry(QtCore.QRect(430, 420, 93, 28))
        self.pushButton04.setObjectName(_fromUtf8("pushButton_4"))
        self.pushButton04.clicked.connect(self.on_pushButton04_clicked) # Bouton nettoyer # Clear

        self.pushButton01 = QtGui.QPushButton(self.centralWidget)
        self.pushButton01.setGeometry(QtCore.QRect(540, 420, 93, 28))
        self.pushButton01.setObjectName(_fromUtf8("pushButton"))
        self.pushButton01.clicked.connect(self.on_pushButton01_clicked) # Bouton Appliquer # Apply

        self.lineEdit_001 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_001.setGeometry(QtCore.QRect(540, 100, 101, 22))
        self.lineEdit_001.setObjectName(_fromUtf8("lineEdit_001"))
        self.lineEdit_001.setText(Drawn_by)

        self.lineEdit_002 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_002.setGeometry(QtCore.QRect(650, 100, 121, 22))
        self.lineEdit_002.setObjectName(_fromUtf8("lineEdit_002"))
        self.lineEdit_002.setText(DRAWN_BY)

        self.lineEdit_003 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_003.setGeometry(QtCore.QRect(540, 140, 101, 22))
        self.lineEdit_003.setObjectName(_fromUtf8("lineEdit_003"))
        self.lineEdit_003.setText(Controlled_by)

        self.lineEdit_004 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_004.setGeometry(QtCore.QRect(650, 140, 121, 22))
        self.lineEdit_004.setObjectName(_fromUtf8("lineEdit_004"))
        self.lineEdit_004.setText(CONTROLLED_BY)

        self.lineEdit_005 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_005.setGeometry(QtCore.QRect(540, 180, 101, 22))
        self.lineEdit_005.setObjectName(_fromUtf8("lineEdit_005"))
        self.lineEdit_005.setText(Date)

        self.lineEdit_006 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_006.setGeometry(QtCore.QRect(650, 180, 121, 22))
        self.lineEdit_006.setObjectName(_fromUtf8("lineEdit_006"))
        self.lineEdit_006.setText(DATE)

        self.lineEdit_007 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_007.setGeometry(QtCore.QRect(540, 220, 101, 22))
        self.lineEdit_007.setObjectName(_fromUtf8("lineEdit_007"))
        self.lineEdit_007.setText(Controlled_2)

        self.lineEdit_008 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_008.setGeometry(QtCore.QRect(650, 220, 121, 22))
        self.lineEdit_008.setObjectName(_fromUtf8("lineEdit_008"))
        self.lineEdit_008.setText(CONTROLLED_2)

        self.lineEdit_009 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_009.setGeometry(QtCore.QRect(540, 260, 101, 22))
        self.lineEdit_009.setObjectName(_fromUtf8("lineEdit_009"))
        self.lineEdit_009.setText(Controlled_3)

        self.lineEdit_010 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_010.setGeometry(QtCore.QRect(650, 260, 121, 22))
        self.lineEdit_010.setObjectName(_fromUtf8("lineEdit_010"))
        self.lineEdit_010.setText(CONTROLLED_3)

        self.lineEdit_011 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_011.setGeometry(QtCore.QRect(780, 100, 61, 61))
        self.lineEdit_011.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_011.setObjectName(_fromUtf8("lineEdit_011"))
        self.lineEdit_011.setText(SCALE)

        self.lineEdit_012 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_012.setGeometry(QtCore.QRect(10, 100, 131, 181))
        font = QtGui.QFont()
        font.setPointSize(20)
        self.lineEdit_012.setFont(font)
        self.lineEdit_012.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_012.setObjectName(_fromUtf8("lineEdit_012"))
        self.lineEdit_012.setText(MOD)

        self.lineEdit_013 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_013.setGeometry(QtCore.QRect(10, 300, 261, 22))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_013.setFont(font)
        self.lineEdit_013.setObjectName(_fromUtf8("lineEdit_013"))
        self.lineEdit_013.setText(COMPANY)

        self.lineEdit_014 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_014.setGeometry(QtCore.QRect(10, 340, 261, 22))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_014.setFont(font)
        self.lineEdit_014.setObjectName(_fromUtf8("lineEdit_014"))
        self.lineEdit_014.setText(ADRESS)

        self.lineEdit_015 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_015.setGeometry(QtCore.QRect(10, 380, 261, 22))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_015.setFont(font)
        self.lineEdit_015.setObjectName(_fromUtf8("lineEdit_015"))
        self.lineEdit_015.setText(COUNTRY)

        self.lineEdit_016 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_016.setGeometry(QtCore.QRect(280, 300, 301, 101))
        font = QtGui.QFont()
        font.setPointSize(14)
        self.lineEdit_016.setFont(font)
        self.lineEdit_016.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_016.setObjectName(_fromUtf8("lineEdit_016"))
        self.lineEdit_016.setText(PART_NAME)

        self.lineEdit_017 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_017.setGeometry(QtCore.QRect(590, 300, 251, 101))
        self.lineEdit_017.setMinimumSize(QtCore.QSize(0, 0))
        font = QtGui.QFont()
        font.setPointSize(8)
        self.lineEdit_017.setFont(font)
        self.lineEdit_017.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_017.setObjectName(_fromUtf8("lineEdit_017"))
        self.lineEdit_017.setText(Project_number)

        self.lineEdit_018 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_018.setGeometry(QtCore.QRect(150, 260, 71, 22))
        self.lineEdit_018.setObjectName(_fromUtf8("lineEdit_018"))
        self.lineEdit_018.setText(A_)

        self.lineEdit_019 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_019.setGeometry(QtCore.QRect(230, 260, 301, 22))
        self.lineEdit_019.setObjectName(_fromUtf8("lineEdit_019"))
        self.lineEdit_019.setText(A__)

        self.lineEdit_020 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_020.setGeometry(QtCore.QRect(150, 220, 71, 22))
        self.lineEdit_020.setObjectName(_fromUtf8("lineEdit_020"))
        self.lineEdit_020.setText(B_)

        self.lineEdit_021 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_021.setGeometry(QtCore.QRect(230, 220, 301, 22))
        self.lineEdit_021.setObjectName(_fromUtf8("lineEdit_021"))
        self.lineEdit_021.setText(B__)

        self.lineEdit_022 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_022.setGeometry(QtCore.QRect(150, 180, 71, 22))
        self.lineEdit_022.setObjectName(_fromUtf8("lineEdit_022"))
        self.lineEdit_022.setText(C_)

        self.lineEdit_023 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_023.setGeometry(QtCore.QRect(230, 180, 301, 22))
        self.lineEdit_023.setObjectName(_fromUtf8("lineEdit_023"))
        self.lineEdit_023.setText(C__)

        self.lineEdit_024 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_024.setGeometry(QtCore.QRect(150, 140, 71, 22))
        self.lineEdit_024.setObjectName(_fromUtf8("lineEdit_024"))
        self.lineEdit_024.setText(D_)

        self.lineEdit_025 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_025.setGeometry(QtCore.QRect(230, 140, 301, 22))
        self.lineEdit_025.setObjectName(_fromUtf8("lineEdit_025"))
        self.lineEdit_025.setText(D__)

        self.lineEdit_026 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_026.setGeometry(QtCore.QRect(150, 100, 71, 22))
        self.lineEdit_026.setObjectName(_fromUtf8("lineEdit_026"))
        self.lineEdit_026.setText(E_)

        self.lineEdit_027 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_027.setGeometry(QtCore.QRect(230, 100, 301, 22))
        self.lineEdit_027.setObjectName(_fromUtf8("lineEdit_027"))
        self.lineEdit_027.setText(E__)

        self.lineEdit_028 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_028.setGeometry(QtCore.QRect(10, 60, 101, 22))
        self.lineEdit_028.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_028.setObjectName(_fromUtf8("lineEdit_028"))
        self.lineEdit_028.setText(Quantity)

        self.lineEdit_029 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_029.setGeometry(QtCore.QRect(120, 60, 131, 22))
        self.lineEdit_029.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_029.setObjectName(_fromUtf8("lineEdit_029"))
        self.lineEdit_029.setText(Part_ID_number)

        self.lineEdit_030 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_030.setGeometry(QtCore.QRect(260, 60, 381, 22))
        self.lineEdit_030.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_030.setObjectName(_fromUtf8("lineEdit_030"))
        self.lineEdit_030.setText(Fabrication_tolerance)

        self.lineEdit_031 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_031.setGeometry(QtCore.QRect(650, 60, 191, 22))
        self.lineEdit_031.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_031.setObjectName(_fromUtf8("lineEdit_031"))
        self.lineEdit_031.setText(Material)

        self.lineEdit_032 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_032.setGeometry(QtCore.QRect(10, 20, 101, 22))
        self.lineEdit_032.setObjectName(_fromUtf8("lineEdit_032"))
        self.lineEdit_032.setText(_01)

        self.lineEdit_033 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_033.setGeometry(QtCore.QRect(120, 20, 131, 22))
        self.lineEdit_033.setObjectName(_fromUtf8("lineEdit_033"))
        self.lineEdit_033.setText(_001_001)

        self.lineEdit_034 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_034.setGeometry(QtCore.QRect(260, 20, 381, 22))
        self.lineEdit_034.setObjectName(_fromUtf8("lineEdit_034"))
        self.lineEdit_034.setText(ISO2768_fh)

        self.lineEdit_035 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_035.setGeometry(QtCore.QRect(650, 20, 191, 22))
        self.lineEdit_035.setObjectName(_fromUtf8("lineEdit_035"))
        self.lineEdit_035.setText(IRON)

        self.label_1 = QtGui.QLabel(self.centralWidget)
        self.label_1.setGeometry(QtCore.QRect(790, 85, 41, 16))
        self.label_1.setObjectName(_fromUtf8("label"))
        self.label_2 = QtGui.QLabel(self.centralWidget)
        self.label_2.setGeometry(QtCore.QRect(10, 325, 53, 16))
        self.label_2.setObjectName(_fromUtf8("label_2"))
        self.label_3 = QtGui.QLabel(self.centralWidget)
        self.label_3.setGeometry(QtCore.QRect(10, 365, 53, 16))
        self.label_3.setObjectName(_fromUtf8("label_3"))
        self.label_4 = QtGui.QLabel(self.centralWidget)
        self.label_4.setGeometry(QtCore.QRect(10, 285, 161, 16))
        self.label_4.setObjectName(_fromUtf8("label_4"))
        self.label_5 = QtGui.QLabel(self.centralWidget)
        self.label_5.setGeometry(QtCore.QRect(280, 285, 151, 16))
        self.label_5.setObjectName(_fromUtf8("label_5"))
        self.label_6 = QtGui.QLabel(self.centralWidget)
        self.label_6.setGeometry(QtCore.QRect(590, 285, 191, 16))
        self.label_6.setObjectName(_fromUtf8("label_6"))
        self.label_7 = QtGui.QLabel(self.centralWidget)
        self.label_7.setGeometry(QtCore.QRect(10, 85, 53, 16))
        self.label_7.setObjectName(_fromUtf8("label_7"))
        self.label_8 = QtGui.QLabel(self.centralWidget)
        self.label_8.setGeometry(QtCore.QRect(150, 85, 53, 16))
        self.label_8.setObjectName(_fromUtf8("label_8"))
        self.label_9 = QtGui.QLabel(self.centralWidget)
        self.label_9.setGeometry(QtCore.QRect(540, 85, 61, 16))
        self.label_9.setObjectName(_fromUtf8("label_9"))
        self.label_10 = QtGui.QLabel(self.centralWidget)
        self.label_10.setGeometry(QtCore.QRect(540, 125, 101, 16))
        self.label_10.setObjectName(_fromUtf8("label_10"))
        self.label_11 = QtGui.QLabel(self.centralWidget)
        self.label_11.setGeometry(QtCore.QRect(540, 165, 53, 16))
        self.label_11.setObjectName(_fromUtf8("label_11"))
        self.label_12 = QtGui.QLabel(self.centralWidget)
        self.label_12.setGeometry(QtCore.QRect(540, 205, 81, 16))
        self.label_12.setObjectName(_fromUtf8("label_12"))
        self.label_13 = QtGui.QLabel(self.centralWidget)
        self.label_13.setGeometry(QtCore.QRect(540, 245, 81, 16))
        self.label_13.setObjectName(_fromUtf8("label_13"))
        self.label_14 = QtGui.QLabel(self.centralWidget)
        self.label_14.setGeometry(QtCore.QRect(10, 45, 71, 16))
        self.label_14.setObjectName(_fromUtf8("label_14"))
        self.label_15 = QtGui.QLabel(self.centralWidget)
        self.label_15.setGeometry(QtCore.QRect(120, 45, 121, 16))
        self.label_15.setObjectName(_fromUtf8("label_15"))
        self.label_16 = QtGui.QLabel(self.centralWidget)
        self.label_16.setGeometry(QtCore.QRect(260, 45, 141, 16))
        self.label_16.setObjectName(_fromUtf8("label_16"))
        self.label_17 = QtGui.QLabel(self.centralWidget)
        self.label_17.setGeometry(QtCore.QRect(650, 45, 71, 16))
        self.label_17.setObjectName(_fromUtf8("label_17"))

        self.graphicsView = QtGui.QGraphicsView(self.centralWidget)     # Fenêtre pour logo # Logo windows
        self.graphicsView.setGeometry(QtCore.QRect(780, 220, 61, 61))
        self.graphicsView.setObjectName(_fromUtf8("graphicsView"))
        self.label_18 = QtGui.QLabel(self.centralWidget)
        self.label_18.setGeometry(QtCore.QRect(790, 205, 41, 16))
        self.label_18.setObjectName(_fromUtf8("label_18"))
        MainWindow.setCentralWidget(self.centralWidget)

        self.retranslateUi(MainWindow)
        QtCore.QMetaObject.connectSlotsByName(MainWindow)

    def retranslateUi(self, MainWindow):
        try:
            MainWindow.setWindowFlags(PyQt4.QtCore.Qt.WindowStaysOnTopHint)  # PyQt4
        except Exception:
            MainWindow.setWindowFlags(PySide.QtCore.Qt.WindowStaysOnTopHint) # PySide

        MainWindow.setWindowTitle(_translate("MainWindow", "Cartouche mod 2", None))

        self.pushButton01.setText(_translate("MainWindow", "Apply", None))
        self.pushButton02.setText(_translate("MainWindow", "Quit", None))
        self.pushButton03.setText(_translate("MainWindow", "Memo", None))
        self.pushButton04.setText(_translate("MainWindow", "Clear", None))

        self.lineEdit_001.setText(_translate("MainWindow", "Drawn_by", None))
        self.lineEdit_002.setText(_translate("MainWindow", "DRAWN_BY", None))
        self.lineEdit_003.setText(_translate("MainWindow", "Controlled_by", None))
        self.lineEdit_004.setText(_translate("MainWindow", "CONTROLLED_BY", None))
        self.lineEdit_005.setText(_translate("MainWindow", "Date", None))
        self.lineEdit_006.setText(_translate("MainWindow", "DATE", None))
        self.lineEdit_007.setText(_translate("MainWindow", "Controlled_2", None))
        self.lineEdit_008.setText(_translate("MainWindow", "CONTROLLED_2", None))
        self.lineEdit_009.setText(_translate("MainWindow", "Controlled_3", None))
        self.lineEdit_010.setText(_translate("MainWindow", "CONTROLLED_3", None))
        self.lineEdit_011.setText(_translate("MainWindow", "SCALE", None))
        self.lineEdit_012.setText(_translate("MainWindow", "MOD", None))
        self.lineEdit_013.setText(_translate("MainWindow", "COMPANY", None))
        self.lineEdit_014.setText(_translate("MainWindow", "ADRESS", None))
        self.lineEdit_015.setText(_translate("MainWindow", "COUNTRY", None))
        self.lineEdit_016.setText(_translate("MainWindow", "PART_NAME", None))
        self.lineEdit_017.setText(_translate("MainWindow", "Project_number", None))
        self.lineEdit_018.setText(_translate("MainWindow", "A_", None))
        self.lineEdit_019.setText(_translate("MainWindow", "A__", None))
        self.lineEdit_020.setText(_translate("MainWindow", "B_", None))
        self.lineEdit_021.setText(_translate("MainWindow", "B__", None))
        self.lineEdit_022.setText(_translate("MainWindow", "C_", None))
        self.lineEdit_023.setText(_translate("MainWindow", "C__", None))
        self.lineEdit_024.setText(_translate("MainWindow", "D_", None))
        self.lineEdit_025.setText(_translate("MainWindow", "D__", None))
        self.lineEdit_026.setText(_translate("MainWindow", "E_", None))
        self.lineEdit_027.setText(_translate("MainWindow", "E__", None))
        self.lineEdit_028.setText(_translate("MainWindow", "Quantity", None))
        self.lineEdit_029.setText(_translate("MainWindow", "Part_ID_number", None))
        self.lineEdit_030.setText(_translate("MainWindow", "Fabrication_tolerance", None))
        self.lineEdit_031.setText(_translate("MainWindow", "Material", None))
        self.lineEdit_032.setText(_translate("MainWindow", "_01", None))
        self.lineEdit_033.setText(_translate("MainWindow", "_001_001", None))
        self.lineEdit_034.setText(_translate("MainWindow", "ISO2768_fh", None))
        self.lineEdit_035.setText(_translate("MainWindow", "IRON", None))

        self.label_1.setText(_translate("MainWindow", "Scale :", None))
        self.label_2.setText(_translate("MainWindow", "Address :", None))
        self.label_3.setText(_translate("MainWindow", "Country :", None))
        self.label_4.setText(_translate("MainWindow", "Company name :", None))
        self.label_5.setText(_translate("MainWindow", "Part name :", None))
        self.label_6.setText(_translate("MainWindow", "Project number / id :", None))
        self.label_7.setText(_translate("MainWindow", "Size :", None))
        self.label_8.setText(_translate("MainWindow", "Notes :", None))
        self.label_9.setText(_translate("MainWindow", "Draw by :", None))
        self.label_10.setText(_translate("MainWindow", "Controlled by :", None))
        self.label_11.setText(_translate("MainWindow", "Date :", None))
        self.label_12.setText(_translate("MainWindow", "Controlled 2 :", None))
        self.label_13.setText(_translate("MainWindow", "Controlled 3 :", None))
        self.label_14.setText(_translate("MainWindow", "Quantity :", None))
        self.label_15.setText(_translate("MainWindow", "Part ID / Number :", None))
        self.label_16.setText(_translate("MainWindow", "Fabrication tolerance :", None))
        self.label_17.setText(_translate("MainWindow", "Material :", None))
        self.label_18.setText(_translate("MainWindow", "Logo :", None))

    def on_pushButton01_clicked(self):    # Bouton Appliquer # Appli buttom
        Drawn_by = utf8(self.lineEdit_001.text())
        DRAWN_BY = utf8(self.lineEdit_002.text())
        Controlled_by = utf8(self.lineEdit_003.text())
        CONTROLLED_BY = utf8(self.lineEdit_004.text())
        Date = utf8(self.lineEdit_005.text())
        DATE = utf8(self.lineEdit_006.text())
        Controlled_2 = utf8(self.lineEdit_007.text())
        CONTROLLED_2 = utf8(self.lineEdit_008.text())
        Controlled_3 = utf8(self.lineEdit_009.text())
        CONTROLLED_3 = utf8(self.lineEdit_010.text())
        SCALE = utf8(self.lineEdit_011.text())
        MOD = utf8(self.lineEdit_012.text())
        COMPANY = utf8(self.lineEdit_013.text())
        ADRESS = utf8(self.lineEdit_014.text())
        COUNTRY = utf8(self.lineEdit_015.text())
        PART_NAME = utf8(self.lineEdit_016.text())
        Project_number = utf8(self.lineEdit_017.text())
        A_ = utf8(self.lineEdit_018.text())
        A__ = utf8(self.lineEdit_019.text())
        B_ = utf8(self.lineEdit_020.text())
        B__ = utf8(self.lineEdit_021.text())
        C_ = utf8(self.lineEdit_022.text())
        C__ = utf8(self.lineEdit_023.text())
        D_ = utf8(self.lineEdit_024.text())
        D__ = utf8(self.lineEdit_025.text())
        E_ = utf8(self.lineEdit_026.text())
        E__ = utf8(self.lineEdit_027.text())
        Quantity = utf8(self.lineEdit_028.text())
        Part_ID_number = utf8(self.lineEdit_029.text())
        Fabrication_tolerance = utf8(self.lineEdit_030.text())
        Material = utf8(self.lineEdit_031.text())
        _01 = utf8(self.lineEdit_032.text())
        _001_001 = utf8(self.lineEdit_033.text())
        ISO2768_fh = utf8(self.lineEdit_034.text())
        IRON = utf8(self.lineEdit_035.text())

        try:
            FreeCAD.getDocument (App.ActiveDocument.Name).getObject("Page").EditableTexts =[unicode(Drawn_by,'utf-8'), unicode(DRAWN_BY,'utf-8'), unicode(Controlled_by,'utf-8'), unicode(CONTROLLED_BY,'utf-8'), unicode(Date,'utf-8'), unicode(DATE,'utf-8'), unicode(Controlled_2, 'utf-8'), unicode(CONTROLLED_2,'utf-8'), unicode(Controlled_3,'utf-8'), unicode(CONTROLLED_3,'utf-8'), unicode(SCALE,'utf-8'), unicode(MOD,'utf-8'), unicode(COMPANY,'utf-8'), unicode(ADRESS,'utf-8'), unicode(COUNTRY, 'utf-8'), unicode(PART_NAME,'utf-8'), unicode(Project_number,'utf-8'), unicode(A_,'utf-8'), unicode(A__,'utf-8'), unicode(B_,'utf-8'), unicode(B__,'utf-8'), unicode(C_,'utf-8'), unicode(C__,'utf-8'), unicode(D_,'utf-8'), unicode(D__,'utf-8'), unicode(E_,'utf-8'), unicode(E__,'utf-8'), unicode(Quantity,'utf-8'), unicode(Part_ID_number,'utf-8'), unicode(Fabrication_tolerance,'utf-8'), unicode(Material,'utf-8'), unicode(_01,'utf-8'), unicode(_001_001,'utf-8'), unicode(ISO2768_fh,'utf-8'), unicode(IRON,'utf-8'),]  # PyQt4
            App.ActiveDocument.recompute()
        except Exception:#
            FreeCAD.getDocument (App.ActiveDocument.Name).getObject("Page").EditableTexts =[Drawn_by.encode('utf-8'), DRAWN_BY.encode('utf-8'), Controlled_by.encode('utf-8'), CONTROLLED_BY.encode('utf-8'), Date.encode('utf-8'), DATE.encode('utf-8'), Controlled_2.encode('utf-8'), CONTROLLED_2.encode('utf-8'), Controlled_3.encode('utf-8'), CONTROLLED_3.encode('utf-8'), SCALE.encode('utf-8'), MOD.encode('utf-8'), COMPANY.encode('utf-8'), ADRESS.encode('utf-8'), COUNTRY.encode('utf-8'), PART_NAME.encode('utf-8'), Project_number.encode('utf-8'), A_.encode('utf-8'), A__.encode('utf-8'), B_.encode('utf-8'), B__.encode('utf-8'), C_.encode('utf-8'), C__.encode('utf-8'), D_.encode('utf-8'), D__.encode('utf-8'), E_.encode('utf-8'), E__.encode('utf-8'), Quantity.encode('utf-8'), Part_ID_number.encode('utf-8'), Fabrication_tolerance.encode('utf-8'), Material.encode('utf-8'), _01.encode('utf-8'), _001_001.encode('utf-8'), ISO2768_fh.encode('utf-8'), IRON.encode('utf-8'),]                                       # PySide
            App.ActiveDocument.recompute()

    def on_pushButton04_clicked(self):    # Bouton nettoyer # Clear buttom

        Drawn_by = ""             ;self.lineEdit_001.setText("")
        DRAWN_BY = ""             ;self.lineEdit_002.setText("")
        Controlled_by = ""        ;self.lineEdit_003.setText("")
        CONTROLLED_BY = ""        ;self.lineEdit_004.setText("")
        Date  = ""                ;self.lineEdit_005.setText("")
        DATE = ""                 ;self.lineEdit_006.setText("")
        Controlled_2 = ""         ;self.lineEdit_007.setText("")
        CONTROLLED_2 = ""         ;self.lineEdit_008.setText("")
        Controlled_3 = ""         ;self.lineEdit_009.setText("")
        CONTROLLED_3 = ""         ;self.lineEdit_010.setText("")
        SCALE = ""                ;self.lineEdit_011.setText("")
        MOD = ""                  ;self.lineEdit_012.setText("")
        COMPANY = ""              ;self.lineEdit_013.setText("")
        ADRESS = ""               ;self.lineEdit_014.setText("")
        COUNTRY = ""              ;self.lineEdit_015.setText("")
        PART_NAME = ""            ;self.lineEdit_016.setText("")
        Project_number = ""       ;self.lineEdit_017.setText("")
        A_ = ""                   ;self.lineEdit_018.setText("")
        A__ = ""                  ;self.lineEdit_019.setText("")
        B_ = ""                   ;self.lineEdit_020.setText("")
        B__ = ""                  ;self.lineEdit_021.setText("")
        C_ = ""                   ;self.lineEdit_022.setText("")
        C__ = ""                  ;self.lineEdit_023.setText("")
        D_ = ""                   ;self.lineEdit_024.setText("")
        D__ = ""                  ;self.lineEdit_025.setText("")
        E_ = ""                   ;self.lineEdit_026.setText("")
        E__ = ""                  ;self.lineEdit_027.setText("")
        Quantity = ""             ;self.lineEdit_028.setText("")
        Part_ID_number = ""       ;self.lineEdit_029.setText("")
        Fabrication_tolerance = "";self.lineEdit_030.setText("")
        Material = ""             ;self.lineEdit_031.setText("")
        _01 = ""                  ;self.lineEdit_032.setText("")
        _001_001 = ""             ;self.lineEdit_033.setText("")
        ISO2768_fh = ""           ;self.lineEdit_034.setText("")
        IRON = ""                 ;self.lineEdit_035.setText("")

    def on_pushButton03_clicked(self):    # Bouton Memo # Memo buttom
        self.lineEdit_001.setText(Drawn_by)
        self.lineEdit_002.setText(DRAWN_BY)
        self.lineEdit_003.setText(Controlled_by)
        self.lineEdit_004.setText(CONTROLLED_BY)
        self.lineEdit_005.setText(Date)
        self.lineEdit_006.setText(DATE)
        self.lineEdit_007.setText(Controlled_2)
        self.lineEdit_008.setText(CONTROLLED_2)
        self.lineEdit_009.setText(Controlled_3)
        self.lineEdit_010.setText(CONTROLLED_3)
        self.lineEdit_011.setText(SCALE)
        self.lineEdit_012.setText(MOD)
        self.lineEdit_013.setText(COMPANY)
        self.lineEdit_014.setText(ADRESS)
        self.lineEdit_015.setText(COUNTRY)
        self.lineEdit_016.setText(PART_NAME)
        self.lineEdit_017.setText(Project_number)
        self.lineEdit_018.setText(A_)
        self.lineEdit_019.setText(A__)
        self.lineEdit_020.setText(B_)
        self.lineEdit_021.setText(B__)
        self.lineEdit_022.setText(C_)
        self.lineEdit_023.setText(C__)
        self.lineEdit_024.setText(D_)
        self.lineEdit_025.setText(D__)
        self.lineEdit_026.setText(E_)
        self.lineEdit_027.setText(E__)
        self.lineEdit_028.setText(Quantity)
        self.lineEdit_029.setText(Part_ID_number)
        self.lineEdit_030.setText(Fabrication_tolerance)
        self.lineEdit_031.setText(Material)
        self.lineEdit_032.setText(_01)
        self.lineEdit_033.setText(_001_001)
        self.lineEdit_034.setText(ISO2768_fh)
        self.lineEdit_035.setText(IRON)

    def on_pushButton02_clicked(self):    # Bouton Quitter # Quit buttom
        App.Console.PrintMessage("End cartridge mod 2\r\n")
        self.window.hide()

MainWindow = QtGui.QMainWindow()
ui = Ui_MainWindow(MainWindow)
MainWindow.show()

}}

## Version 

5.0 : 08/08/2014


</div>


</div>





<div class="mw-collapsible mw-collapsed toccolours">

# Macro CartoucheFC 2/fr 


<div class="mw-collapsible-content">


{{Macro/fr
|Name=Macro_CartoucheFC_2
|Icon=Macro_CartoucheFC_2.png
|Description=Cette macro est une application complète, il permet de remplir le cartouche de la feuille de dessin avec texteditable (Seulement pour l'[atelier Drawing](Drawing_Workbench/fr.md)).
|Author=Mario52
|Version=5.0
|Date=2014-08-08
|FCVersion=Toutes versions utilisant l'atelier Drawing
|Download=[https://www.freecadweb.org/wiki/images/0/00/Macro_CartoucheFC_2.png ToolBar Icon]
}}


<div class="mw-translate-fuzzy">

## Description 

Cette macro est une application complète, elle permet de remplir simplement tous les champs du cartouche A3 Landscape english


</div>

<img alt="Macro CartoucheFC Modele 2" src=images/Macro_CartoucheFC_Modele_02.png  style="width:680px;">

La photo représente la hiérarchie de remplissage des champs tels qu\'ils sont dans la fenêtre \"textEditable\" de FreeCAD.

## Utilisation 

Son utilisation est très facile, exécutez la macro et modifier les champs.

-   Cliquez sur le bouton **Quit** pour quitter l\'application.
-   Cliquez sur le bouton **Memo** restitue le contenu de la cartouche lors de l\'ouverture de la macro.
-   Cliquez sur le bouton **Clear** nettoyer tous les champs de la macro (champs sont restitués en appuyant sur le **Mémo**).
-   Cliquez sur le bouton **Apply** bouton applique les modifications au modèle.

La fenêtre reste au dessus des autres fenêtres pour permettre de visualiser les changements (cette fonction peut être désagréable si vous décidez d\'ouvrir une nouvelle fenêtre et reste inaccessible)

**PS : certains caractères comme & \$ ne sont pas acceptés (et peut être d\'autres caractères spéciaux) !**

Si vous avez des questions ou désirez ajouter une fonction, vous pouvez vous adresse sur le forum [Remplir cartouche](http://forum.freecadweb.org/viewtopic.php?f=12&t=2049)

## Code 

ToolBar Icon ![](images/Macro_CartoucheFC_2.png )

**Macro_CartoucheFC_2.FcMacro**


{{MacroCode|code=

# -*- coding: utf-8 -*-
"""
***************************************************************************
*   Copyright (c) 2014 <mario52>                                          *
*                                                                         *
*   This file is a supplement to the FreeCAD CAD development system.      *
*                                                                         *
*   This program is free software; you can redistribute it and/or modify  *
*   it under the terms of the GNU Lesser General Public License (LGPL)    *
*   as published by the Free Software Foundation; either version 2 of     *
*   the License, or (at your option) any later version.                   *
*   for detail see the LICENCE text file.                                 *
*                                                                         *
*   This software is distributed in the hope that it will be useful,      *
*   but WITHOUT ANY WARRANTY; without even the implied warranty of        *
*   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the         *
*   GNU Library General Public License for more details.                  *
*                                                                         *
*   You should have received a copy of the GNU Library General Public     *
*   License along with this macro; if not, write to the Free Software     *
*   Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  *
*   USA                                                                   *
***************************************************************************
*           WARNING! All changes in this file will be lost and            *  
*                  may cause malfunction of the program                   *
***************************************************************************
"""
# Macro_CartoucheFC_2.FcMacro
# 
# il faut que la page (drawing viewer) s'appelle " Page " qui est le nom par défaut du module Drawing
# cette macro fonctionne avec la feuille A3_Landscape_ qui possede tous les champs EditableTexts
# 
# http://www.freecadweb.org/wiki/index.php?title=Drawing_templates
# Fill the area of the cartridge
# It is necessary that the page (drawing viewer) is called "Page", which is the default name of the Drawing module
# Python 2.6
# 08/08/2014 ver 5.0 (pour cartouche modèle 2 (A3 Landscape english)) # PyQt and PySide 
# Created:  by mario52
# PyQt and PySide 

#OS: Windows Vista
#Word size: 32-bit
#Version: 0.14.3700 (Git)
#Branch: releases/FreeCAD-0-14
#Hash: 32f5aae0a64333ec8d5d160dbc46e690510c8fe1
#Python version: 2.6.2
#Qt version: 4.5.2
#Coin version: 3.1.0
#SoQt version: 1.4.1

try:
    import PyQt4                        # PyQt4
    from PyQt4 import QtCore, QtGui     # PyQt4
except Exception:
    import PySide                       # PySide
    from PySide import QtCore, QtGui    # PySide

import Draft, Part, FreeCAD, math, PartGui, FreeCADGui
from math import sqrt, pi, sin, cos, asin
from FreeCAD import Base

def utf8(unio):
    return unicode(unio).encode('UTF8')

global path
global Drawn_by               ; Drawn_by       = ""   # lineEdit_001
global DRAWN_BY               ; DRAWN_BY       = ""   # lineEdit_002
global Controlled_by          ; Controlled_by  = ""   # lineEdit_003
global CONTROLLED_BY          ; CONTROLLED_BY  = ""   # lineEdit_004
global Date                   ; Date           = ""   # lineEdit_005
global DATE                   ; DATE           = ""   # lineEdit_006
global Controlled_2           ; Controlled_2   = ""   # lineEdit_007
global CONTROLLED_2           ; CONTROLLED_2   = ""   # lineEdit_008
global Controlled_3           ; Controlled_3   = ""   # lineEdit_009
global CONTROLLED_3           ; CONTROLLED_3   = ""   # lineEdit_010
global SCALE                  ; SCALE          = ""   # lineEdit_011
global MOD                    ; MOD            = ""   # lineEdit_012
global COMPANY                ; COMPANY        = ""   # lineEdit_013
global ADRESS                 ; ADRESS         = ""   # lineEdit_014
global COUNTRY                ; COUNTRY        = ""   # lineEdit_015
global PART_NAME              ; PART_NAME      = ""   # lineEdit_016
global Project_number         ; Project_number = ""   # lineEdit_017
global A_                     ; A_             = ""   # lineEdit_018
global A__                    ; A__            = ""   # lineEdit_019
global B_                     ; B_             = ""   # lineEdit_020
global B__                    ; B__            = ""   # lineEdit_021
global C_                     ; C_             = ""   # lineEdit_022
global C__                    ; C__            = ""   # lineEdit_023
global D_                     ; D_             = ""   # lineEdit_024
global D__                    ; D__            = ""   # lineEdit_025
global E_                     ; E_             = ""   # lineEdit_026
global E__                    ; E__            = ""   # lineEdit_027
global Quantity               ; Quantity       = ""   # lineEdit_028
global Part_ID_number         ; Part_ID_number = ""   # lineEdit_029
global Fabrication_tolerances ; Fabrication_tolerance = "" #lineEdit_030
global Material               ; Material       = ""   # lineEdit_031
global _01                    ; _01            = ""   # lineEdit_032
global _001_001               ; _001_001       = ""   # lineEdit_033
global ISO2768_fh             ; ISO2768_fh     = ""   # lineEdit_034
global IRON                   ; IRON           = ""   # lineEdit_035

path = FreeCAD.ConfigGet("AppHomePath")

try:
    _fromUtf8 = QtCore.QString.fromUtf8
except AttributeError:
    def _fromUtf8(s):
        return s
try:
    _encoding = QtGui.QApplication.UnicodeUTF8
    def _translate(context, text, disambig):
        return QtGui.QApplication.translate(context, text, disambig, _encoding)
except AttributeError:
    def _translate(context, text, disambig):
        return QtGui.QApplication.translate(context, text, disambig)

def errorDialog(msg):
    # Create a simple dialog QMessageBox
    # The first argument indicates the icon used: one of QtGui.QMessageBox.{NoIcon, Information, Warning, Critical, Question} 
    diag = QtGui.QMessageBox(QtGui.QMessageBox.Critical,u"Error Message",msg)
    try:
        diag.setWindowFlags(PyQt4.QtCore.Qt.WindowStaysOnTopHint)  # PyQt4 cette fonction met la fenêtre en avant
    except Exception:
        diag.setWindowFlags(PySide.QtCore.Qt.WindowStaysOnTopHint) # PySide cette fonction met la fenêtre en avant
    #diag.setWindowModality(QtCore.Qt.ApplicationModal) # la fonction a été désactivée pour favoriser "WindowStaysOnTopHint"
    diag.exec_()

try:
    Drawn_by = App.activeDocument().getObject("Page").EditableTexts[0]          # lineEdit_001
    DRAWN_BY = App.activeDocument().getObject("Page").EditableTexts[1]          # lineEdit_002
    Controlled_by = App.activeDocument().getObject("Page").EditableTexts[2]     # lineEdit_003
    CONTROLLED_BY = App.activeDocument().getObject("Page").EditableTexts[3]     # lineEdit_004
    Date = App.activeDocument().getObject("Page").EditableTexts[4]              # lineEdit_005
    DATE = App.activeDocument().getObject("Page").EditableTexts[5]              # lineEdit_006
    Controlled_2 = App.activeDocument().getObject("Page").EditableTexts[6]      # lineEdit_007
    CONTROLLED_2 = App.activeDocument().getObject("Page").EditableTexts[7]      # lineEdit_008
    Controlled_3 = App.activeDocument().getObject("Page").EditableTexts[8]      # lineEdit_009
    CONTROLLED_3 = App.activeDocument().getObject("Page").EditableTexts[9]      # lineEdit_010
    SCALE = App.activeDocument().getObject("Page").EditableTexts[10]            # lineEdit_011
    MOD = App.activeDocument().getObject("Page").EditableTexts[11]              # lineEdit_012
    COMPANY = App.activeDocument().getObject("Page").EditableTexts[12]          # lineEdit_013
    ADRESS = App.activeDocument().getObject("Page").EditableTexts[13]           # lineEdit_014
    COUNTRY = App.activeDocument().getObject("Page").EditableTexts[14]          # lineEdit_015
    PART_NAME = App.activeDocument().getObject("Page").EditableTexts[15]        # lineEdit_016
    Project_number = App.activeDocument().getObject("Page").EditableTexts[16]   # lineEdit_017
    A_ = App.activeDocument().getObject("Page").EditableTexts[17]               # lineEdit_018
    A__ = App.activeDocument().getObject("Page").EditableTexts[18]              # lineEdit_019
    B_ = App.activeDocument().getObject("Page").EditableTexts[19]               # lineEdit_020
    B__ = App.activeDocument().getObject("Page").EditableTexts[20]              # lineEdit_021
    C_ = App.activeDocument().getObject("Page").EditableTexts[21]               # lineEdit_022
    C__ = App.activeDocument().getObject("Page").EditableTexts[22]              # lineEdit_023
    D_ = App.activeDocument().getObject("Page").EditableTexts[23]               # lineEdit_024
    D__ = App.activeDocument().getObject("Page").EditableTexts[24]              # lineEdit_025
    E_ = App.activeDocument().getObject("Page").EditableTexts[25]               # lineEdit_026
    E__ = App.activeDocument().getObject("Page").EditableTexts[26]              # lineEdit_027
    Quantity= App.activeDocument().getObject("Page").EditableTexts[27]          # lineEdit_028
    Part_ID_number = App.activeDocument().getObject("Page").EditableTexts[28]   # lineEdit_029
    Fabrication_tolerance = App.activeDocument().getObject("Page").EditableTexts[29] #lineEdit_030
    Material = App.activeDocument().getObject("Page").EditableTexts[30]         # lineEdit_031
    _01 = App.activeDocument().getObject("Page").EditableTexts[31]              # lineEdit_032
    _001_001 = App.activeDocument().getObject("Page").EditableTexts[32]         # lineEdit_033
    ISO2768_fh = App.activeDocument().getObject("Page").EditableTexts[33]       # lineEdit_034
    IRON = App.activeDocument().getObject("Page").EditableTexts[34]             # lineEdit_035

except:
    errorDialog("Error read cartridge")

class Ui_MainWindow(object):

    def __init__(self, MainWindow):
        self.window = MainWindow

        MainWindow.setObjectName(_fromUtf8("MainWindow"))
        MainWindow.resize(849, 462)
        MainWindow.setMaximumSize(QtCore.QSize(849, 462))
        self.centralWidget = QtGui.QWidget(MainWindow)
        self.centralWidget.setObjectName(_fromUtf8("centralWidget"))

        self.pushButton02 = QtGui.QPushButton(self.centralWidget)
        self.pushButton02.setGeometry(QtCore.QRect(210, 420, 93, 28))
        self.pushButton02.setObjectName(_fromUtf8("pushButton_2"))
        self.pushButton02.clicked.connect(self.on_pushButton02_clicked) # Bouton Quitter # Quit

        self.pushButton03 = QtGui.QPushButton(self.centralWidget)
        self.pushButton03.setGeometry(QtCore.QRect(320, 420, 93, 28))
        self.pushButton03.setObjectName(_fromUtf8("pushButton_3"))
        self.pushButton03.clicked.connect(self.on_pushButton03_clicked) # Bouton Memo # Memo

        self.pushButton04 = QtGui.QPushButton(self.centralWidget)
        self.pushButton04.setGeometry(QtCore.QRect(430, 420, 93, 28))
        self.pushButton04.setObjectName(_fromUtf8("pushButton_4"))
        self.pushButton04.clicked.connect(self.on_pushButton04_clicked) # Bouton nettoyer # Clear

        self.pushButton01 = QtGui.QPushButton(self.centralWidget)
        self.pushButton01.setGeometry(QtCore.QRect(540, 420, 93, 28))
        self.pushButton01.setObjectName(_fromUtf8("pushButton"))
        self.pushButton01.clicked.connect(self.on_pushButton01_clicked) # Bouton Appliquer # Apply

        self.lineEdit_001 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_001.setGeometry(QtCore.QRect(540, 100, 101, 22))
        self.lineEdit_001.setObjectName(_fromUtf8("lineEdit_001"))
        self.lineEdit_001.setText(Drawn_by)

        self.lineEdit_002 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_002.setGeometry(QtCore.QRect(650, 100, 121, 22))
        self.lineEdit_002.setObjectName(_fromUtf8("lineEdit_002"))
        self.lineEdit_002.setText(DRAWN_BY)

        self.lineEdit_003 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_003.setGeometry(QtCore.QRect(540, 140, 101, 22))
        self.lineEdit_003.setObjectName(_fromUtf8("lineEdit_003"))
        self.lineEdit_003.setText(Controlled_by)

        self.lineEdit_004 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_004.setGeometry(QtCore.QRect(650, 140, 121, 22))
        self.lineEdit_004.setObjectName(_fromUtf8("lineEdit_004"))
        self.lineEdit_004.setText(CONTROLLED_BY)

        self.lineEdit_005 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_005.setGeometry(QtCore.QRect(540, 180, 101, 22))
        self.lineEdit_005.setObjectName(_fromUtf8("lineEdit_005"))
        self.lineEdit_005.setText(Date)

        self.lineEdit_006 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_006.setGeometry(QtCore.QRect(650, 180, 121, 22))
        self.lineEdit_006.setObjectName(_fromUtf8("lineEdit_006"))
        self.lineEdit_006.setText(DATE)

        self.lineEdit_007 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_007.setGeometry(QtCore.QRect(540, 220, 101, 22))
        self.lineEdit_007.setObjectName(_fromUtf8("lineEdit_007"))
        self.lineEdit_007.setText(Controlled_2)

        self.lineEdit_008 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_008.setGeometry(QtCore.QRect(650, 220, 121, 22))
        self.lineEdit_008.setObjectName(_fromUtf8("lineEdit_008"))
        self.lineEdit_008.setText(CONTROLLED_2)

        self.lineEdit_009 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_009.setGeometry(QtCore.QRect(540, 260, 101, 22))
        self.lineEdit_009.setObjectName(_fromUtf8("lineEdit_009"))
        self.lineEdit_009.setText(Controlled_3)

        self.lineEdit_010 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_010.setGeometry(QtCore.QRect(650, 260, 121, 22))
        self.lineEdit_010.setObjectName(_fromUtf8("lineEdit_010"))
        self.lineEdit_010.setText(CONTROLLED_3)

        self.lineEdit_011 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_011.setGeometry(QtCore.QRect(780, 100, 61, 61))
        self.lineEdit_011.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_011.setObjectName(_fromUtf8("lineEdit_011"))
        self.lineEdit_011.setText(SCALE)

        self.lineEdit_012 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_012.setGeometry(QtCore.QRect(10, 100, 131, 181))
        font = QtGui.QFont()
        font.setPointSize(20)
        self.lineEdit_012.setFont(font)
        self.lineEdit_012.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_012.setObjectName(_fromUtf8("lineEdit_012"))
        self.lineEdit_012.setText(MOD)

        self.lineEdit_013 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_013.setGeometry(QtCore.QRect(10, 300, 261, 22))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_013.setFont(font)
        self.lineEdit_013.setObjectName(_fromUtf8("lineEdit_013"))
        self.lineEdit_013.setText(COMPANY)

        self.lineEdit_014 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_014.setGeometry(QtCore.QRect(10, 340, 261, 22))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_014.setFont(font)
        self.lineEdit_014.setObjectName(_fromUtf8("lineEdit_014"))
        self.lineEdit_014.setText(ADRESS)

        self.lineEdit_015 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_015.setGeometry(QtCore.QRect(10, 380, 261, 22))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.lineEdit_015.setFont(font)
        self.lineEdit_015.setObjectName(_fromUtf8("lineEdit_015"))
        self.lineEdit_015.setText(COUNTRY)

        self.lineEdit_016 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_016.setGeometry(QtCore.QRect(280, 300, 301, 101))
        font = QtGui.QFont()
        font.setPointSize(14)
        self.lineEdit_016.setFont(font)
        self.lineEdit_016.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_016.setObjectName(_fromUtf8("lineEdit_016"))
        self.lineEdit_016.setText(PART_NAME)

        self.lineEdit_017 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_017.setGeometry(QtCore.QRect(590, 300, 251, 101))
        self.lineEdit_017.setMinimumSize(QtCore.QSize(0, 0))
        font = QtGui.QFont()
        font.setPointSize(8)
        self.lineEdit_017.setFont(font)
        self.lineEdit_017.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_017.setObjectName(_fromUtf8("lineEdit_017"))
        self.lineEdit_017.setText(Project_number)

        self.lineEdit_018 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_018.setGeometry(QtCore.QRect(150, 260, 71, 22))
        self.lineEdit_018.setObjectName(_fromUtf8("lineEdit_018"))
        self.lineEdit_018.setText(A_)

        self.lineEdit_019 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_019.setGeometry(QtCore.QRect(230, 260, 301, 22))
        self.lineEdit_019.setObjectName(_fromUtf8("lineEdit_019"))
        self.lineEdit_019.setText(A__)

        self.lineEdit_020 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_020.setGeometry(QtCore.QRect(150, 220, 71, 22))
        self.lineEdit_020.setObjectName(_fromUtf8("lineEdit_020"))
        self.lineEdit_020.setText(B_)

        self.lineEdit_021 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_021.setGeometry(QtCore.QRect(230, 220, 301, 22))
        self.lineEdit_021.setObjectName(_fromUtf8("lineEdit_021"))
        self.lineEdit_021.setText(B__)

        self.lineEdit_022 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_022.setGeometry(QtCore.QRect(150, 180, 71, 22))
        self.lineEdit_022.setObjectName(_fromUtf8("lineEdit_022"))
        self.lineEdit_022.setText(C_)

        self.lineEdit_023 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_023.setGeometry(QtCore.QRect(230, 180, 301, 22))
        self.lineEdit_023.setObjectName(_fromUtf8("lineEdit_023"))
        self.lineEdit_023.setText(C__)

        self.lineEdit_024 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_024.setGeometry(QtCore.QRect(150, 140, 71, 22))
        self.lineEdit_024.setObjectName(_fromUtf8("lineEdit_024"))
        self.lineEdit_024.setText(D_)

        self.lineEdit_025 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_025.setGeometry(QtCore.QRect(230, 140, 301, 22))
        self.lineEdit_025.setObjectName(_fromUtf8("lineEdit_025"))
        self.lineEdit_025.setText(D__)

        self.lineEdit_026 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_026.setGeometry(QtCore.QRect(150, 100, 71, 22))
        self.lineEdit_026.setObjectName(_fromUtf8("lineEdit_026"))
        self.lineEdit_026.setText(E_)

        self.lineEdit_027 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_027.setGeometry(QtCore.QRect(230, 100, 301, 22))
        self.lineEdit_027.setObjectName(_fromUtf8("lineEdit_027"))
        self.lineEdit_027.setText(E__)

        self.lineEdit_028 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_028.setGeometry(QtCore.QRect(10, 60, 101, 22))
        self.lineEdit_028.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_028.setObjectName(_fromUtf8("lineEdit_028"))
        self.lineEdit_028.setText(Quantity)

        self.lineEdit_029 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_029.setGeometry(QtCore.QRect(120, 60, 131, 22))
        self.lineEdit_029.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_029.setObjectName(_fromUtf8("lineEdit_029"))
        self.lineEdit_029.setText(Part_ID_number)

        self.lineEdit_030 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_030.setGeometry(QtCore.QRect(260, 60, 381, 22))
        self.lineEdit_030.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_030.setObjectName(_fromUtf8("lineEdit_030"))
        self.lineEdit_030.setText(Fabrication_tolerance)

        self.lineEdit_031 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_031.setGeometry(QtCore.QRect(650, 60, 191, 22))
        self.lineEdit_031.setAlignment(QtCore.Qt.AlignCenter)
        self.lineEdit_031.setObjectName(_fromUtf8("lineEdit_031"))
        self.lineEdit_031.setText(Material)

        self.lineEdit_032 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_032.setGeometry(QtCore.QRect(10, 20, 101, 22))
        self.lineEdit_032.setObjectName(_fromUtf8("lineEdit_032"))
        self.lineEdit_032.setText(_01)

        self.lineEdit_033 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_033.setGeometry(QtCore.QRect(120, 20, 131, 22))
        self.lineEdit_033.setObjectName(_fromUtf8("lineEdit_033"))
        self.lineEdit_033.setText(_001_001)

        self.lineEdit_034 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_034.setGeometry(QtCore.QRect(260, 20, 381, 22))
        self.lineEdit_034.setObjectName(_fromUtf8("lineEdit_034"))
        self.lineEdit_034.setText(ISO2768_fh)

        self.lineEdit_035 = QtGui.QLineEdit(self.centralWidget)
        self.lineEdit_035.setGeometry(QtCore.QRect(650, 20, 191, 22))
        self.lineEdit_035.setObjectName(_fromUtf8("lineEdit_035"))
        self.lineEdit_035.setText(IRON)

        self.label_1 = QtGui.QLabel(self.centralWidget)
        self.label_1.setGeometry(QtCore.QRect(790, 85, 41, 16))
        self.label_1.setObjectName(_fromUtf8("label"))
        self.label_2 = QtGui.QLabel(self.centralWidget)
        self.label_2.setGeometry(QtCore.QRect(10, 325, 53, 16))
        self.label_2.setObjectName(_fromUtf8("label_2"))
        self.label_3 = QtGui.QLabel(self.centralWidget)
        self.label_3.setGeometry(QtCore.QRect(10, 365, 53, 16))
        self.label_3.setObjectName(_fromUtf8("label_3"))
        self.label_4 = QtGui.QLabel(self.centralWidget)
        self.label_4.setGeometry(QtCore.QRect(10, 285, 161, 16))
        self.label_4.setObjectName(_fromUtf8("label_4"))
        self.label_5 = QtGui.QLabel(self.centralWidget)
        self.label_5.setGeometry(QtCore.QRect(280, 285, 151, 16))
        self.label_5.setObjectName(_fromUtf8("label_5"))
        self.label_6 = QtGui.QLabel(self.centralWidget)
        self.label_6.setGeometry(QtCore.QRect(590, 285, 191, 16))
        self.label_6.setObjectName(_fromUtf8("label_6"))
        self.label_7 = QtGui.QLabel(self.centralWidget)
        self.label_7.setGeometry(QtCore.QRect(10, 85, 53, 16))
        self.label_7.setObjectName(_fromUtf8("label_7"))
        self.label_8 = QtGui.QLabel(self.centralWidget)
        self.label_8.setGeometry(QtCore.QRect(150, 85, 53, 16))
        self.label_8.setObjectName(_fromUtf8("label_8"))
        self.label_9 = QtGui.QLabel(self.centralWidget)
        self.label_9.setGeometry(QtCore.QRect(540, 85, 61, 16))
        self.label_9.setObjectName(_fromUtf8("label_9"))
        self.label_10 = QtGui.QLabel(self.centralWidget)
        self.label_10.setGeometry(QtCore.QRect(540, 125, 101, 16))
        self.label_10.setObjectName(_fromUtf8("label_10"))
        self.label_11 = QtGui.QLabel(self.centralWidget)
        self.label_11.setGeometry(QtCore.QRect(540, 165, 53, 16))
        self.label_11.setObjectName(_fromUtf8("label_11"))
        self.label_12 = QtGui.QLabel(self.centralWidget)
        self.label_12.setGeometry(QtCore.QRect(540, 205, 81, 16))
        self.label_12.setObjectName(_fromUtf8("label_12"))
        self.label_13 = QtGui.QLabel(self.centralWidget)
        self.label_13.setGeometry(QtCore.QRect(540, 245, 81, 16))
        self.label_13.setObjectName(_fromUtf8("label_13"))
        self.label_14 = QtGui.QLabel(self.centralWidget)
        self.label_14.setGeometry(QtCore.QRect(10, 45, 71, 16))
        self.label_14.setObjectName(_fromUtf8("label_14"))
        self.label_15 = QtGui.QLabel(self.centralWidget)
        self.label_15.setGeometry(QtCore.QRect(120, 45, 121, 16))
        self.label_15.setObjectName(_fromUtf8("label_15"))
        self.label_16 = QtGui.QLabel(self.centralWidget)
        self.label_16.setGeometry(QtCore.QRect(260, 45, 141, 16))
        self.label_16.setObjectName(_fromUtf8("label_16"))
        self.label_17 = QtGui.QLabel(self.centralWidget)
        self.label_17.setGeometry(QtCore.QRect(650, 45, 71, 16))
        self.label_17.setObjectName(_fromUtf8("label_17"))

        self.graphicsView = QtGui.QGraphicsView(self.centralWidget)     # Fenêtre pour logo # Logo windows
        self.graphicsView.setGeometry(QtCore.QRect(780, 220, 61, 61))
        self.graphicsView.setObjectName(_fromUtf8("graphicsView"))
        self.label_18 = QtGui.QLabel(self.centralWidget)
        self.label_18.setGeometry(QtCore.QRect(790, 205, 41, 16))
        self.label_18.setObjectName(_fromUtf8("label_18"))
        MainWindow.setCentralWidget(self.centralWidget)

        self.retranslateUi(MainWindow)
        QtCore.QMetaObject.connectSlotsByName(MainWindow)

    def retranslateUi(self, MainWindow):
        try:
            MainWindow.setWindowFlags(PyQt4.QtCore.Qt.WindowStaysOnTopHint)  # PyQt4
        except Exception:
            MainWindow.setWindowFlags(PySide.QtCore.Qt.WindowStaysOnTopHint) # PySide

        MainWindow.setWindowTitle(_translate("MainWindow", "Cartouche mod 2", None))

        self.pushButton01.setText(_translate("MainWindow", "Apply", None))
        self.pushButton02.setText(_translate("MainWindow", "Quit", None))
        self.pushButton03.setText(_translate("MainWindow", "Memo", None))
        self.pushButton04.setText(_translate("MainWindow", "Clear", None))

        self.lineEdit_001.setText(_translate("MainWindow", "Drawn_by", None))
        self.lineEdit_002.setText(_translate("MainWindow", "DRAWN_BY", None))
        self.lineEdit_003.setText(_translate("MainWindow", "Controlled_by", None))
        self.lineEdit_004.setText(_translate("MainWindow", "CONTROLLED_BY", None))
        self.lineEdit_005.setText(_translate("MainWindow", "Date", None))
        self.lineEdit_006.setText(_translate("MainWindow", "DATE", None))
        self.lineEdit_007.setText(_translate("MainWindow", "Controlled_2", None))
        self.lineEdit_008.setText(_translate("MainWindow", "CONTROLLED_2", None))
        self.lineEdit_009.setText(_translate("MainWindow", "Controlled_3", None))
        self.lineEdit_010.setText(_translate("MainWindow", "CONTROLLED_3", None))
        self.lineEdit_011.setText(_translate("MainWindow", "SCALE", None))
        self.lineEdit_012.setText(_translate("MainWindow", "MOD", None))
        self.lineEdit_013.setText(_translate("MainWindow", "COMPANY", None))
        self.lineEdit_014.setText(_translate("MainWindow", "ADRESS", None))
        self.lineEdit_015.setText(_translate("MainWindow", "COUNTRY", None))
        self.lineEdit_016.setText(_translate("MainWindow", "PART_NAME", None))
        self.lineEdit_017.setText(_translate("MainWindow", "Project_number", None))
        self.lineEdit_018.setText(_translate("MainWindow", "A_", None))
        self.lineEdit_019.setText(_translate("MainWindow", "A__", None))
        self.lineEdit_020.setText(_translate("MainWindow", "B_", None))
        self.lineEdit_021.setText(_translate("MainWindow", "B__", None))
        self.lineEdit_022.setText(_translate("MainWindow", "C_", None))
        self.lineEdit_023.setText(_translate("MainWindow", "C__", None))
        self.lineEdit_024.setText(_translate("MainWindow", "D_", None))
        self.lineEdit_025.setText(_translate("MainWindow", "D__", None))
        self.lineEdit_026.setText(_translate("MainWindow", "E_", None))
        self.lineEdit_027.setText(_translate("MainWindow", "E__", None))
        self.lineEdit_028.setText(_translate("MainWindow", "Quantity", None))
        self.lineEdit_029.setText(_translate("MainWindow", "Part_ID_number", None))
        self.lineEdit_030.setText(_translate("MainWindow", "Fabrication_tolerance", None))
        self.lineEdit_031.setText(_translate("MainWindow", "Material", None))
        self.lineEdit_032.setText(_translate("MainWindow", "_01", None))
        self.lineEdit_033.setText(_translate("MainWindow", "_001_001", None))
        self.lineEdit_034.setText(_translate("MainWindow", "ISO2768_fh", None))
        self.lineEdit_035.setText(_translate("MainWindow", "IRON", None))

        self.label_1.setText(_translate("MainWindow", "Scale :", None))
        self.label_2.setText(_translate("MainWindow", "Address :", None))
        self.label_3.setText(_translate("MainWindow", "Country :", None))
        self.label_4.setText(_translate("MainWindow", "Company name :", None))
        self.label_5.setText(_translate("MainWindow", "Part name :", None))
        self.label_6.setText(_translate("MainWindow", "Project number / id :", None))
        self.label_7.setText(_translate("MainWindow", "Size :", None))
        self.label_8.setText(_translate("MainWindow", "Notes :", None))
        self.label_9.setText(_translate("MainWindow", "Draw by :", None))
        self.label_10.setText(_translate("MainWindow", "Controlled by :", None))
        self.label_11.setText(_translate("MainWindow", "Date :", None))
        self.label_12.setText(_translate("MainWindow", "Controlled 2 :", None))
        self.label_13.setText(_translate("MainWindow", "Controlled 3 :", None))
        self.label_14.setText(_translate("MainWindow", "Quantity :", None))
        self.label_15.setText(_translate("MainWindow", "Part ID / Number :", None))
        self.label_16.setText(_translate("MainWindow", "Fabrication tolerance :", None))
        self.label_17.setText(_translate("MainWindow", "Material :", None))
        self.label_18.setText(_translate("MainWindow", "Logo :", None))

    def on_pushButton01_clicked(self):    # Bouton Appliquer # Appli buttom
        Drawn_by = utf8(self.lineEdit_001.text())
        DRAWN_BY = utf8(self.lineEdit_002.text())
        Controlled_by = utf8(self.lineEdit_003.text())
        CONTROLLED_BY = utf8(self.lineEdit_004.text())
        Date = utf8(self.lineEdit_005.text())
        DATE = utf8(self.lineEdit_006.text())
        Controlled_2 = utf8(self.lineEdit_007.text())
        CONTROLLED_2 = utf8(self.lineEdit_008.text())
        Controlled_3 = utf8(self.lineEdit_009.text())
        CONTROLLED_3 = utf8(self.lineEdit_010.text())
        SCALE = utf8(self.lineEdit_011.text())
        MOD = utf8(self.lineEdit_012.text())
        COMPANY = utf8(self.lineEdit_013.text())
        ADRESS = utf8(self.lineEdit_014.text())
        COUNTRY = utf8(self.lineEdit_015.text())
        PART_NAME = utf8(self.lineEdit_016.text())
        Project_number = utf8(self.lineEdit_017.text())
        A_ = utf8(self.lineEdit_018.text())
        A__ = utf8(self.lineEdit_019.text())
        B_ = utf8(self.lineEdit_020.text())
        B__ = utf8(self.lineEdit_021.text())
        C_ = utf8(self.lineEdit_022.text())
        C__ = utf8(self.lineEdit_023.text())
        D_ = utf8(self.lineEdit_024.text())
        D__ = utf8(self.lineEdit_025.text())
        E_ = utf8(self.lineEdit_026.text())
        E__ = utf8(self.lineEdit_027.text())
        Quantity = utf8(self.lineEdit_028.text())
        Part_ID_number = utf8(self.lineEdit_029.text())
        Fabrication_tolerance = utf8(self.lineEdit_030.text())
        Material = utf8(self.lineEdit_031.text())
        _01 = utf8(self.lineEdit_032.text())
        _001_001 = utf8(self.lineEdit_033.text())
        ISO2768_fh = utf8(self.lineEdit_034.text())
        IRON = utf8(self.lineEdit_035.text())

        try:
            FreeCAD.getDocument (App.ActiveDocument.Name).getObject("Page").EditableTexts =[unicode(Drawn_by,'utf-8'), unicode(DRAWN_BY,'utf-8'), unicode(Controlled_by,'utf-8'), unicode(CONTROLLED_BY,'utf-8'), unicode(Date,'utf-8'), unicode(DATE,'utf-8'), unicode(Controlled_2, 'utf-8'), unicode(CONTROLLED_2,'utf-8'), unicode(Controlled_3,'utf-8'), unicode(CONTROLLED_3,'utf-8'), unicode(SCALE,'utf-8'), unicode(MOD,'utf-8'), unicode(COMPANY,'utf-8'), unicode(ADRESS,'utf-8'), unicode(COUNTRY, 'utf-8'), unicode(PART_NAME,'utf-8'), unicode(Project_number,'utf-8'), unicode(A_,'utf-8'), unicode(A__,'utf-8'), unicode(B_,'utf-8'), unicode(B__,'utf-8'), unicode(C_,'utf-8'), unicode(C__,'utf-8'), unicode(D_,'utf-8'), unicode(D__,'utf-8'), unicode(E_,'utf-8'), unicode(E__,'utf-8'), unicode(Quantity,'utf-8'), unicode(Part_ID_number,'utf-8'), unicode(Fabrication_tolerance,'utf-8'), unicode(Material,'utf-8'), unicode(_01,'utf-8'), unicode(_001_001,'utf-8'), unicode(ISO2768_fh,'utf-8'), unicode(IRON,'utf-8'),]  # PyQt4
            App.ActiveDocument.recompute()
        except Exception:#
            FreeCAD.getDocument (App.ActiveDocument.Name).getObject("Page").EditableTexts =[Drawn_by.encode('utf-8'), DRAWN_BY.encode('utf-8'), Controlled_by.encode('utf-8'), CONTROLLED_BY.encode('utf-8'), Date.encode('utf-8'), DATE.encode('utf-8'), Controlled_2.encode('utf-8'), CONTROLLED_2.encode('utf-8'), Controlled_3.encode('utf-8'), CONTROLLED_3.encode('utf-8'), SCALE.encode('utf-8'), MOD.encode('utf-8'), COMPANY.encode('utf-8'), ADRESS.encode('utf-8'), COUNTRY.encode('utf-8'), PART_NAME.encode('utf-8'), Project_number.encode('utf-8'), A_.encode('utf-8'), A__.encode('utf-8'), B_.encode('utf-8'), B__.encode('utf-8'), C_.encode('utf-8'), C__.encode('utf-8'), D_.encode('utf-8'), D__.encode('utf-8'), E_.encode('utf-8'), E__.encode('utf-8'), Quantity.encode('utf-8'), Part_ID_number.encode('utf-8'), Fabrication_tolerance.encode('utf-8'), Material.encode('utf-8'), _01.encode('utf-8'), _001_001.encode('utf-8'), ISO2768_fh.encode('utf-8'), IRON.encode('utf-8'),]                                       # PySide
            App.ActiveDocument.recompute()

    def on_pushButton04_clicked(self):    # Bouton nettoyer # Clear buttom

        Drawn_by = ""             ;self.lineEdit_001.setText("")
        DRAWN_BY = ""             ;self.lineEdit_002.setText("")
        Controlled_by = ""        ;self.lineEdit_003.setText("")
        CONTROLLED_BY = ""        ;self.lineEdit_004.setText("")
        Date  = ""                ;self.lineEdit_005.setText("")
        DATE = ""                 ;self.lineEdit_006.setText("")
        Controlled_2 = ""         ;self.lineEdit_007.setText("")
        CONTROLLED_2 = ""         ;self.lineEdit_008.setText("")
        Controlled_3 = ""         ;self.lineEdit_009.setText("")
        CONTROLLED_3 = ""         ;self.lineEdit_010.setText("")
        SCALE = ""                ;self.lineEdit_011.setText("")
        MOD = ""                  ;self.lineEdit_012.setText("")
        COMPANY = ""              ;self.lineEdit_013.setText("")
        ADRESS = ""               ;self.lineEdit_014.setText("")
        COUNTRY = ""              ;self.lineEdit_015.setText("")
        PART_NAME = ""            ;self.lineEdit_016.setText("")
        Project_number = ""       ;self.lineEdit_017.setText("")
        A_ = ""                   ;self.lineEdit_018.setText("")
        A__ = ""                  ;self.lineEdit_019.setText("")
        B_ = ""                   ;self.lineEdit_020.setText("")
        B__ = ""                  ;self.lineEdit_021.setText("")
        C_ = ""                   ;self.lineEdit_022.setText("")
        C__ = ""                  ;self.lineEdit_023.setText("")
        D_ = ""                   ;self.lineEdit_024.setText("")
        D__ = ""                  ;self.lineEdit_025.setText("")
        E_ = ""                   ;self.lineEdit_026.setText("")
        E__ = ""                  ;self.lineEdit_027.setText("")
        Quantity = ""             ;self.lineEdit_028.setText("")
        Part_ID_number = ""       ;self.lineEdit_029.setText("")
        Fabrication_tolerance = "";self.lineEdit_030.setText("")
        Material = ""             ;self.lineEdit_031.setText("")
        _01 = ""                  ;self.lineEdit_032.setText("")
        _001_001 = ""             ;self.lineEdit_033.setText("")
        ISO2768_fh = ""           ;self.lineEdit_034.setText("")
        IRON = ""                 ;self.lineEdit_035.setText("")

    def on_pushButton03_clicked(self):    # Bouton Memo # Memo buttom
        self.lineEdit_001.setText(Drawn_by)
        self.lineEdit_002.setText(DRAWN_BY)
        self.lineEdit_003.setText(Controlled_by)
        self.lineEdit_004.setText(CONTROLLED_BY)
        self.lineEdit_005.setText(Date)
        self.lineEdit_006.setText(DATE)
        self.lineEdit_007.setText(Controlled_2)
        self.lineEdit_008.setText(CONTROLLED_2)
        self.lineEdit_009.setText(Controlled_3)
        self.lineEdit_010.setText(CONTROLLED_3)
        self.lineEdit_011.setText(SCALE)
        self.lineEdit_012.setText(MOD)
        self.lineEdit_013.setText(COMPANY)
        self.lineEdit_014.setText(ADRESS)
        self.lineEdit_015.setText(COUNTRY)
        self.lineEdit_016.setText(PART_NAME)
        self.lineEdit_017.setText(Project_number)
        self.lineEdit_018.setText(A_)
        self.lineEdit_019.setText(A__)
        self.lineEdit_020.setText(B_)
        self.lineEdit_021.setText(B__)
        self.lineEdit_022.setText(C_)
        self.lineEdit_023.setText(C__)
        self.lineEdit_024.setText(D_)
        self.lineEdit_025.setText(D__)
        self.lineEdit_026.setText(E_)
        self.lineEdit_027.setText(E__)
        self.lineEdit_028.setText(Quantity)
        self.lineEdit_029.setText(Part_ID_number)
        self.lineEdit_030.setText(Fabrication_tolerance)
        self.lineEdit_031.setText(Material)
        self.lineEdit_032.setText(_01)
        self.lineEdit_033.setText(_001_001)
        self.lineEdit_034.setText(ISO2768_fh)
        self.lineEdit_035.setText(IRON)

    def on_pushButton02_clicked(self):    # Bouton Quitter # Quit buttom
        App.Console.PrintMessage("End cartridge mod 2\r\n")
        self.window.hide()

MainWindow = QtGui.QMainWindow()
ui = Ui_MainWindow(MainWindow)
MainWindow.show()

}}

## Version 

5.0 : 08/08/2014


</div>


</div>



---
⏵ [documentation index](../README.md) > Sandbox:Mario52 Macro Cartouche
