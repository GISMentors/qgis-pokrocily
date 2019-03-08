.. |checkbox| image:: ../images/icon/checkbox.png
   :width: 1.5em
.. |raster-info| image:: ../images/icon/raster-info.png
   :width: 1.5em

.. _nastaveni:

Nastavení, historie, prohlížení výsledků
========================================

Nastavení
---------

Nastavení sady nástrojů nalezneme v hlavním nastavení QGIS v menu
:menuselection:`Nastavení --> Možnosti...` v záložce
|processingAlgorithm| `Zpracování`, nebo přímo z panelu nástrojů
zpracování pomocí tlačítka |iconSettingsConsole| Zde můžeme procházet,
aktivovat a deaktivovat poskytovatele algoritmů, uživatelské skripty a
modely, dále lze přidat jednotlivé funkce do hlavního menu a lišty,
nastavit obecné chování při spouštění algoritmů případně nastavit
chování konkrétních poskytovatelů. Pro prohledávání nastavení lze využít
filtr v horní části okna.

.. figure:: images/geoproc_conf.png 
   :class: middle
        
   Okno nastavení sady nástrojů.

Obecné nastavení
^^^^^^^^^^^^^^^^

V obecném nastavení lze nastavit globální chování všech algoritmů
(nezávisle na poskytovateli).

.. figure:: images/geoproc_obec.png 
   :class: middle
   
   Obecné nastavení zpracování.
   
Vybraná nastavení:

	- :guilabel:`Filtrování neplatných prvků` - nastavení chování z
          hlediska platnosti geometrie

            - Do not Filter (better performence)
            - Ignorovat prvky s neplatnými geometriemi
            - Stop algorithm execution when a geometry is invalid
        
	- :guilabel:`Použít název souboru pro název vrstvy` - pokud je
          neaktivní, tak výstupní vrstva nese vždy automaticky
          vygenerovaný název související s danou funkcí (např. funkce
          :guilabel:`Obalová zóna` ``->`` vrstva
          :guilabel:`S obalovou zónou`). Pokud je aktivní, název vrstvy
          se generuje z vytvořeného výstupního souboru, a v případě kdy
          ukládáme výstup do dočasných souborů, tak se vrstva pojmenuje
          opět automaticky.
	- :guilabel:`Post(Pre)-execution script` - možnost nastavit
          cestu ke skriptům, které se budou automaticky spouštět před
          nebo po spuštění algoritmů.
	- :guilabel:`Styl pro ... vrstvy` - možnost nastavení
          uživatelských stylů (symbologie) u různých typů výstupů. Je
          nutné nastavit cestu k souboru s uloženým stylem.
	- :guilabel:`Warn before executing if parameter CRS's do not match`
          - upozorní pokud chceme provádět analýzy nad daty v
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
možnosti nastavení.

.. figure:: images/geoproc_poskyt.png 
   :class: middle
        
   Nastavení uživatelských skriptů.
   
Přidání tlačítka do nástrojové lišty a hlavního menu
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
V okně nastavení zpracování máme také možnost vytvořit pro jednotlivé
algoritmy položku v hlavním menu, přičemž se nám na liště vytvoří
tlačítko pro rychlé spouštění. To je vhodné pokud používáme k práci
opakovaně několik algoritmů, zejména pak u vytvořených vlastních
nástrojů (skripty, modely). K tlačítku v jde nastavit vlastní ikonka.
Pro zobrazení nové položky v menu a ikonky v liště je nutné QGIS
vypnout a znovu spustit

.. figure:: images/geoproc_menu_add.png 
   :class: middle 

   Přidání tlačítka do nástrojové lišty a hlavního menu
 
.. figure:: images/geoproc_menu_add2.png 
   :class: middle 

   Vzled položky v menu a ikonka v nástrojové liště
 

Historie
--------

V okně historie můžeme procházet historii použitých procesů. Okno lze
spustit z menu :menuselection:`Zpracování --> Historie...` nebo přímo z
panelu nástrojů zpracování pomocí tlačítka
|mIconHistory|:sup:`Historie...` nebo
použitím klávesové zkratky :kbd:`Ctrl+Alt+H`. Ve složce
:item:`ALGORITHM` najdeme seznam spuštěných procesů s vypsaným Python
kódem ve spodní části okna. Poklikáním na konkrétní proces se otevře
okno algoritmu s předvyplněnými parametry. Proces tedy můžeme znovu
spustit, popř. změnit parametry a spustit. V okně se mohou objevit i
další složky: :item:`INFO`, :item:`ERROR`, :item:`WARNINGS`, ve kterých
najdeme další informace nebo chyby ve spouštěných procesech.

.. figure:: images/geoproc_histor.png 
   :class: middle
   
   Okno historie spuštěných algoritmů.
   
Prohlížeč výsledků
------------------

Některé algoritmy generují jako výstup HTML soubor. Pokud takový
algoritmus spouštíme na konci záznamu, tak se nám vypíše text
:guilabel:`Tento algoritmus vytvořil HTML výstup`
(:numref:`htmlfig`). Pro otevření výsledků slouží panel `Prohlížeč
Výsledků`. Otevřeme ho z menu :menuselection:`Zpracování --> Prohlížeč
výsledků...` nebo z panelu nástrojů zpracování tlačítkem ||:sup:`Prohlížeč
výsledků` popř. použitím klávesové zkratky :kbd:`Ctrl+Alt+R`. V panelu
zvolíme výsledek, který chceme zobrazit a klikneme na odkaz ve spodní
části.

.. _htmlfig:

.. figure:: images/geoproc_html.png 
   :class: tiny 

   Informace o vytvoření HTML souboru v záznamu algoritmu.

.. figure:: images/geoproc_vysled.png 
   :class: small

   Ukázka výsledku z funkce :guilabel:`Základní statistiky pro pole`.
   
Ukázky algoritmů generující HTML výstupy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Základní statistiky pro  pole (vektor)
......................................

Pomocí funkce |mAlgorithmBasicStatistics| :guilabel:`Základní statistiky pro pole`
zjistíme základní statistiky týkající se rozlohy *velkoplošných
chráněných území*. Spustíme funkci vybereme požadovanou vrstvu a
parametr podle kterého se budou údaje počítat. Výsledek potom
zkontrolujeme v prohlížeči výsledků :menuselection:`Zpracování -->
Prohlížeč výsledků...`.

.. figure:: images/geoproc_pract_3.png 
   :class: middle 

   Funkce |mAlgorithmBasicStatistics| :guilabel:`Základní statistiky
   pro pole`.

Rastrové informace (rastr)
..........................

Pomocí funkce |raster-info| :guilabel:`Informace` (spouští příkaz 
:guilabel:`gdalinfo`) zjistíme základní informace o rastru. Výsledek potom 
zkontrolujeme v prohlížeči výsledků :menuselection:`Zpracování --> Prohlížeč 
výsledků...`.

.. figure:: images/geoproc_pract_4.png 
   :class: middle 

   Funkce |raster-info| :guilabel:`Informace` (spouští příkaz :guilabel:`gdalinfo`).
