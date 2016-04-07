Nastavení a orientace v nástrojích
==================================

Aktivace sydy nástrojů
----------------------
Okno sady nástrojů lze aktivovat v hlavním menu :menuselection:`Zpracování --> Sada nástrojů`, nebo použitím klávesové zkratky :kbd:`Ctrl+Alt+T`, nebo stejně jako u vypínání a zapínání ostatních panelů, nástrojových lišt a oken - pravým kliknutím na panel a výběrem z nabídky.

.. figure:: images/geoproc_menu.png
   :scale: 70%

   Aktivace sady nástrojů v hlavním menu :menuselection:`Zpracování --> Sada nástrojů`
   


.. note:: Pokud nemáte možnost aktivovat panel sady nástrojů, je možné, že máte deaktivovaný plugin :item:`Processing`, který tento panel poskytuje.

Nastavení
---------
Nastavení sady nástrojů nalezneme v hlavním menu :menuselection:`Zpracování --> Možnosti...` (:kbd:`Ctrl+Alt+C`). Zde můžeme procházet, aktivovat a deaktivovat poskytovatele algoritmů, uživatelské skripty a modely, dále lze nastavit obecné chování při spouštění algoritmů případně nastavit chování konkrétních poskytovatelů. Pro prohledávání nastavení lze využít filtr v horní části okna.

.. figure:: images/geoproc_conf.png 
   :scale: 70%
   :scale-latex: 40 

   Okno nastavení sady nástrojů


Obecné nastavení
^^^^^^^^^^^^^^^^

Nastavení poskytovatelů, medeleru aj.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Orientace v okně Nástroje zpracování
------------------------------------
Orientace v okně a prohledávání nástrojů je velice intuitivní. Nástroje jsou struktorované podle poskytovatelů a dále zpravidla rozdělené do tematických okruhů (vektorové analýzy, rastrové analýzy atd.). Součástí této struktury je také položka :menuselection:`Naposledy použité algoritmy` kde naleznete naposledy použité funkce.

.. figure:: images/geoproc_orient.png
   :scale: 70%
   :scale-latex: 40 

   Ukázka orientace v okně podle tromové struktury


V horní části panelu je filtr pro rychlé vyhledání funkce. Výhodou tohoto filtru je, že vyhledává i v neaktivních algoritmech a v případě shody se zadaným řetězcem se ukáže ve spodní části upozornění, s možností prohlížení a rychlé aktivace algoritmů.

.. figure:: images/geoproc_filter.png
   :scale: 70%
   :scale-latex: 40 

   Použití filtru a upozornění na výsledky v neaktivních algoritmech

Po kliknutí na odkaz na konci upozornění (:guilabel:`to view item`) se ukáže struktura s výsledky od neaktivních poskytovatelů (šedá barva tetu). Po kliknutí na tlačítko :guilabel:`Activete` se nám poskytovatel aktivuje.

.. figure:: images/geoproc_filter_disa.png
   :scale: 70%
   :scale-latex: 40 

   Zobrazení výsledků neaktivních algoritmů s možností aktivace
   
Historie
--------

Prohlížeč Výsledků
------------------


