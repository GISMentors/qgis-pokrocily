.. |model| image:: ../images/icon/model.png
   :width: 1.5em
.. |qgis| image:: ../images/intro_logo.png
   :width: 1.5em
   
  
   
Úvod
====
Okno grafického modeláře můžeme otevřít z menu :menuselection:`Zpracování --> Grafický modelář...`, klávesovou zkratkou :kbd:`Ctrl+Alt+M` nebo pomocí položky |model| :guilabel:`Vytvořit nový model` v okně nástrojů zpracování.

.. figure:: images/modeler_menu.png 
   :class: small 
   :scale-latex: 40 

   Spouštění okna modeláře z hlahvního menu
   
   
Uložené modely lze nálezt mezi ostatními algoritmy v okně nástrojů zpracování, kde jsou strukturovány podle zadaných skupin při tvorbě modelu. Také lze přidávat modely ze souboru (.model) nebo z online kolekce.

.. figure:: images/modeler_panel.png 
   :class: tiny 
   :scale-latex: 40 

   Modely jako součást okna nástrojů zpracování
   
Popis okna
----------
.. figure:: images/modeler.png 
   :class: middle 
   :scale-latex: 40 

   Okno grafického modeláře

Popis jednotlivých částí okna:

1. V horní části okna máme sadu ikonek pro základní operace (ukládání, export atd.)
2. Levá část okna slouží k přidávání prvků do modelu - vstupních parametrů (záložka :guilabel:`Vstupy`) a Algoritmů (záložka :guilabel:`Algoritmy`)
3. Dvě textové pole složí k zadání názvu a skupiny, do které se model zařadí v rámci nástrojů zpracování (před uložením nutné vyplnit)
4. Hlavní okno modeláře. Zde se skládají, configurují a propojují jednotlivé části modelu
   
Jednotlivé části modelu
-----------------------

Vstupní parametry
^^^^^^^^^^^^^^^^^
.. _vstupdia:
.. figure:: images/modeler_vstup_dia.png 
   :class: tiny
   :scale-latex: 40 

   Značení vstupního parametru v modelu
   
Prvním krokem při tvorbě modelu je vložení vstupních parametrů.Tyto parametry jsou stejné jako u běžných algoritmů - vrstva, rozsah vrstvy, číslo, text, boolean (formou checkboxu) atd. Při spouštění vytvořeného modelu bude požadováno vyplnění vložených vstupních parametrů. Tyto parametry jsou navázany na konkrétní algoritmy v modelu.

.. figure:: images/modeler_vstup.png 
   :class: small 
   :scale-latex: 40 

   Možné vstupní parametry
   
Jednotlivé parametry lze do modelu přidat tažením nebo poklikáním. Po přídání se objeví dialogové okno, které je u většiny parametrů jednoduché, základní položkou je zde název parametru. Nastavení parametrů v modelu lze průběžně měnit kliknutím na symbol tužky, nebo lze parametry odstranit kliknutím na křížek (:num:`#vstupdia`).

.. figure:: images/modeler_vstup_num.png 
   :class: small 
   :scale-latex: 40 

   Dialogové okno při vložení číselného parametru

Algoritmy
^^^^^^^^^
.. figure:: images/modeler_algor_dia.png 
   :class: tiny
   :scale-latex: 40 

   Značení algoritmu v modelu
   
Hlavní součástí modelů jsou algoritmy. Nalezneme zde většinu algoritmů, které jsou v okně nástrojů zpracování. Kromě těchto funkcí jsou zde speciální :guilabel:`Nástroje jen pro modely` (:num:`#algor`)

.. _algor:
.. figure:: images/modeler_algor.png 
   :class: small 
   :scale-latex: 40 

   Možné vstupní algoritmy
   
Algoritmy se přidávají do modelu opět tažením nebo poklikáním. Po přidání se ukáže běžné dialogové okno konkrétního algoritmu (:num:`#algorrand`). Zde máme možnost nastavit výchozí hodnoty parametrů algoritmu, se kterými se bude počítat při spuštění modelu. Jesltiže chceme mít parametry při spouštění modelu volitelné je třeba nakonfigurovat odpovídající vstupy (:num:`#algorrand2`).

.. _algorrand:
.. figure:: images/modeler_algor_rand.png 
   :class: medium 
   :scale-latex: 40 

   Dialogové okno algoritmu s pevně stanpvenými parametry

.. _algorrand2:
.. figure:: images/modeler_algor_rand2.png 
   :class: large 
   :scale-latex: 40 

   Nastavení parametrů na základě vstupů do modelu

Nastavení algoritmů v modelu lze průběžně editovat kliknutím na symbol tužky, nebo lze algotritmy odstranit kliknutím na křížek. Také lze pomocí tlačítek + a -  jaké mohou být vstupy a výstpy algoritmu. 

.. _algorrand3:
.. figure:: images/modeler_algor_rand3.png 
   :class: middle 
   :scale-latex: 40 

   Nastavení volitelných parametrů algoritmu |qgis|:guilabel:`Random points in extent` při spouštění modelu

Jednotlivé algoritmy lze na sebe dále navazovat - to co je výstupem z jednoho algoritmu může nějakým způsobem vstupovat do algoritmu druhého (:num:`#algorrand4`).

.. _algorrand4:
.. figure:: images/modeler_algor_rand4.png 
   :class: middle 
   :scale-latex: 40 

   Náhodné body vygenerované |qgis|:guilabel:`Random points in extent` použité jako vstup pro vytvoření obalových zón

Výstupy
^^^^^^^
.. figure:: images/modeler_out_dia.png 
   :class: tiny
   :scale-latex: 40 

   Značení výstupu v modelu
   
.. todo:: typy výstupu (vrstva,html), jak vytvořit



.. todo:: rodičovské algoritmy

