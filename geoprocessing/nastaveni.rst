.. |checkbox| image:: ../images/icon/checkbox.png
   :width: 1.5em
.. |tileindex| image:: ../images/icon/tileindex.png
   :width: 1.5em

.. _nastaveni:

Nastavení, historie, prohlížení výsledků
========================================

Nastavení
---------

Nastavení sady nástrojů nalezneme v hlavním menu
:menuselection:`Zpracování --> Možnosti...` (:kbd:`Ctrl+Alt+C`). Zde
můžeme procházet, aktivovat a deaktivovat poskytovatele algoritmů,
uživatelské skripty a modely, dále lze nastavit obecné chování při
spouštění algoritmů případně nastavit chování konkrétních
poskytovatelů. Pro prohledávání nastavení lze využít filtr v horní
části okna.

.. figure:: images/geoproc_conf.png 
   :scale: 70%
   :scale-latex: 40 

   Okno nastavení sady nástrojů.


Obecné nastavení
^^^^^^^^^^^^^^^^

V obecném nastavení lze nastavit globální chování všech algoritmů
(nezávisle na poskytovateli).

.. figure:: images/geoproc_obec.png 
   :scale: 70% 
   :scale-latex: 40 

   Obecné nastavení zpracování.
   
Vybrané nastavení:

	- :guilabel:`Použít název souboru pro název vrstvy` - pokud je
          neaktivní výstupní vrstva nese automaticky vygenerovaný
          název, většinou související s danou funkcí (např funkce
          :guilabel:`Obalová vrstva vekt. vrstvy` ``->`` vrstva
          :guilabel:`Obalová zóna`). V případě že máme nastavení
          aktivní, název vrstvy se generuje z vytvořeného výstupního
          souboru, to je vhodné pokud ručně zadáváme název
          souboru. Pokud v tomto případě ukládáme výstup do dočasných
          souborů, bude vrstva přebírat tohoto souboru
          (např. :guilabel:`OUTPUTLAYER.shp` nebo jiný, komplikovaný
          název)
	- :guilabel:`Požít pouze pro vybrané prvky` - výpočet se
          provede jen nad prvky ve výběru
	- :guilabel:`Post(Pre)-execution script` - možnost nastavit
          cestu ke skriptům, které se budou automaticky spouštět před
          nebo po spuštění algoritmů
	- :guilabel:`Styl pro ... vrstvy` - možnost nastavení
          uživatelských stylů (symbologie) u různých typů výstupů. Je
          nutné nastavit cestu k souboru s uloženým stylem
	- :guilabel:`Varovat před spuštěním pokud nesouhlasí SRS
          vrstev` - upozorní pokud chceme provádět analýzy nad daty v
          různých souřadnicových systémech, nutné např. u překryvných
          analýz.
	- :guilabel:`Výstupní složka` - nastavení defaultní výstupní
          složky kam se mohou ukládat výstupy. V případě, že nechceme
          aby se výstup uložil pouze do dočasných souborů, zadáme při
          provádění operace název souboru a ten se uloží do
          přednastavené složky.
	- :guilabel:`Zobrazit definici SRS vrstvy ve výběrových
          boxech` - při výběru vrstev v analýzách uvidíme kromě názvu
          vrstvy i její EPSG kód.


Nastavení poskytovatelů, modeleru aj.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

V nastavení poskytovatelů procesů se hlavně setkáme z možností
aktivace a deaktivace poskytovatelů (:guilabel:`Activate`
|checkbox|). U jednotlivých poskytovatelů potom mohou být další
možnosti nastavení, jako v případě uživatelských skriptů |tileindex|
:item:`Složka skriptů`, kde můžeme nastavit cestu k našim uživatelským
skriptům.

.. figure:: images/geoproc_poskyt.png 
   :scale: 70% 
   :scale-latex: 40 

   Nastavení uživatelských skriptů.
   

Historie
--------

V okně historie můžeme procházet historii použitých procesů. Okno lze
spustit z menu :menuselection:`Zpracování --> Historie...`, nebo
použitím klávesové zkratky :kbd:`Ctrl+Alt+H`. Ve složce
:item:`ALGORITHM` najdeme seznam spuštěných procesů s vypsaným Python
kódem ve spodní části okna. Tyto procesy lze znovu spustit dvojitým
klikem anebo pomocí Python kódu. V okně se mohou objevit i další
složky: :item:`INFO`, :item:`ERROR`, :item:`WARNINGS`, ve kterých
najdeme další informace nebo chyby ve spouštěných procesech.


.. figure:: images/geoproc_histor.png 
   :scale: 70% 
   :scale-latex: 40 

   Okno historie spuštěných algoritmů.
   
.. noteadvanced::
	
	.. todo:: popsat python
	

Prohlížeč výsledků
------------------

Okno výsledků slouží k prohlížení tabulek a HTML výstupů. Otevřeme ho
z menu :menuselection:`Zpracování --> Prohlížeč výsledků...`, nebo
použitím klávesové zkratky :kbd:`Ctrl+Alt+R`.

.. figure:: images/geoproc_vysled.png 
   :scale: 70% 
   :scale-latex: 40 

   Ukázka výsledku z funkce :guilabel:`Základní statistiky pro
   numerická pole`.
   
HTML výstup
^^^^^^^^^^^

..todo:: GDAL statistika,gdalinfo nebo histogram - html output
