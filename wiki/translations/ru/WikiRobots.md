# WikiRobots/ru
**Robots are intrinsically dangerous as they can automatically do a lot of damage. Use with extreme care!**



## Обзор

Repetitive tasks can be automated using robots or bots, i.e. software programs operating on the wiki by themselves.

The natural and most commonly used robots for wiki sites are provided by MediaWiki, under the package name Pywikibot. See [Manual:Pywikibot](http://www.mediawiki.org/wiki/Manual:Pywikibot) for the full information.

In a nutshell, Pywikibot is a collection of Python scripts able to use the native wiki API to act on wiki sites. To see the API list for the FreeCAD wiki, visit <http://www.freecadweb.org/wiki/api.php>

In order to use Pywikibot, you need to:

1.  install the Pywikibot package
2.  configure Pywikibot to work on the FreeCAD Wiki
3.  launch the scripts you need for the task at hand

There is a wealth of information on how to install, configure and use Pywikibot. However, please be aware that this information, although useful, can be misleading, since it mixes instructions related to two different Pywikibot codebases, and different versions of the Pywikibot scripts collection.

In the following, you will find the basic instructions to set up and use Pywikibot on the FreeCAD wiki. This will allow you to perform the most common tasks. For advanced usage, refer to the [Manual:Pywikibot](http://www.mediawiki.org/wiki/Manual:Pywikibot), and to the Python source code.



## Установка

Перейти к <http://tools.wmflabs.org/pywikibot/> и скачать **package/pywikipedia/core.zip** (проект также находится под github, gerrit и т.д., Но это самый простой способ получить полный автономный пакет).

Распакуйте содержимое в нужный вам каталог.

Unless you want to install the libraries into your Python libs, you are done (if you still want to install them, check the file **INSTALL** in the base directory).

Pywikibot работает с Python 2.6 и 2.7 без каких-либо проблем. Python 3  до сих пор не тестировался с FreeCAD wiki также работает.



## Настройка

You must save the following Python code as a file with the name **user-config.py** in the base directory where you unzipped **package/pywikipedia/core.zip** (to be clear, in the same directory where you already find a file called **user-config.py.sample**).


```python
# -*- coding: cp437  -*-
family = 'freecadwiki'
mylang = 'en'
usernames['freecadwiki']['en'] = u'<<yourWikiUserName>>'
#usernames['freecadwiki']['freecadwiki'] = u'<<yourWikiUserName>>'
console_encoding = 'cp437'
```

In the above code:

-   replace *\<\>* with your Wiki user name
-   replace *cp437* with your *console_encoding*. To find out what is your console encoding, for Windows and Linux, launch the Python interpreter, enter {{SystemInput|import sys}} followed by {{SystemInput|print sys.stdout.encoding}}. Python will write your {{SystemOutput|console_encoding}} on the screen.

Then you must save the following Python code as a file with the name **freecadwiki_family.py** under the sub-directory **/pywikibot/families** (together with the other **family_xxx.py** files).


```python
# -*- coding: utf-8  -*-

__version__ = '$Id: 7f3891c3bbbfbd69c0b005de953514803d783d92 $'

from pywikibot import family


# The MediaWiki family
# user-config.py: usernames['mediawiki']['mediawiki'] = 'User name'
class Family(family.WikimediaFamily):
    def __init__(self):
        super(Family, self).__init__()
        self.name = 'freecadwiki'

        self.langs = {
            'en': 'www.freecadweb.org',
        }

    def scriptpath(self, code):
        return 'wiki'

    def path(self, code):
        return '/index.php' #The path of index.php, look at your wiki address. 
     
    def apipath(self, code):
        return '/api.php' #The path of api.php

    def version(self, code):
        # Replace with the actual version being run on your wiki
        return '1.20.3'

    def protocol(self, code):
        """
        Can be overridden to return 'https'. Other protocols are not supported.
        """
        return 'http'
        #return 'https' # My server uses https
```



## Применение

You are now all set to launch the Pywikibot scripts. The scripts themselves are contained in the **/scripts** subdirectory, from which you can know the names.

To launch the scripts, open a shell and move to the base directory (the installation one, NOT the **/scripts** subdirectory), and write


{{SystemInput|python pwb.py <<scriptname>>.py -<<parameter>>}}

where of course you replace *\<\>* with the name of the script you are interested in, and *\<\>* with the parameter(s) required for the given script.

To have a description of the usage and parameters of any script, simply use the *-help* parameter. For instance, to have a description of the **replace.py** script (one of the most useful), type


{{SystemInput|python pwb.py replace.py -help}}

There is another very useful parameter, valid for all the scripts, called *-simulate*, that allows you to test commands without harming the Wiki. Use it, before going \'live\'.



## Примеры

This command will log into the wiki


{{SystemInput|pwb.py login.py}}

This command will print a list of all the pages containing a link to SourceForge


{{SystemInput|pwb.py listpages.py -weblink:sourceforge.net}}

This command will replace all the links to the old SourceForge Forum with a link to the new freecad.org-hosted Forum


{{SystemInput|pwb.py replace.py -weblink:sourceforge.net/apps/phpbb/free-cad "sourceforge.net/apps/phpbb/free-cad" "forum.freecad.org"}}

This command will print a list of all the pages containing the word \'PartDesign\', starting with the page titled \"2d Drafting Module\" and going on alphabetically


{{SystemInput|pwb.py listpages.py -start:"2d Drafting Module" -grep:PartDesign}}

This command will replace all the secure links to the old SourceForge Forum with a link to the new freecad.org-hosted Forum in the translated pages


{{SystemInput|pwb.py replace.py -start:Translations:! "https://sourceforge.net/apps/phpbb/free-cad" "http://forum.freecad.org"}}

## FreeCAD Wiki Related Commands 

Count all pages that a specific wiki templates is used in


{{SystemInput|python3 pwb.py templatecount -count GuiCommand}}

List all pages that a specific wiki templates is used in


{{SystemInput|python3 pwb.py templatecount -list GuiCommand}}

Replace a string in all the pages listed in the Arch category


{{SystemInput|python3 pwb.py replace.py -cat:Arch}}



---
⏵ [documentation index](../README.md) > [Administration](Category_Administration.md) > [Developer](Category_Developer.md) > WikiRobots/ru
