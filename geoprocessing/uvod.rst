.. |alg| image:: ../images/icon/alg.png
   :width: 1.5em

Orientace v nástrojích
======================

Aktivace Nástrojů zpracování
----------------------------

Panel *Nástroje zpracování* lze aktivovat pomocí tlačítka |alg|:sup:`Sada nástrojů` v liště nástrojů, v hlavním menu
:menuselection:`Zpracování --> Sada nástrojů`, použitím klávesové
zkratky :kbd:`Ctrl+Alt+T`, nebo stejně jako u vypínání a zapínání
ostatních panelů, nástrojových lišt a oken - pravým kliknutím na panel a výběrem z nabídky.

.. figure:: images/geoproc_menu.png
   :scale: 70%

   Aktivace sady nástrojů v hlavním menu :menuselection:`Zpracování
   --> Sada nástrojů`.
   


.. note:: Pokud nemáte možnost aktivovat panel sady nástrojů, je
          možné, že máte deaktivovaný vestavěný plugin
          :item:`Processing`, který tento panel poskytuje. Aktivovat ho
          lze ve správci zásuvných modulů, viz :skoleni:`školení pro
          začátečníky
          <qgis-zacatecnik/ruzne/qgis_pluginy.html#spravce-zasuvnych-modulu>`.


Orientace v panelu Nástroje zpracování
--------------------------------------

Orientace v panelu a prohledávání nástrojů je velice
intuitivní. Nástroje jsou strukturované podle poskytovatelů a dále
zpravidla rozdělené do tematických okruhů (vektorové analýzy, rastrové
analýzy atd.). Součástí této struktury je také položka
:menuselection:`Naposledy použité algoritmy`, kde naleznete naposledy
použité funkce.

.. figure:: images/geoproc_orient.png
   :scale: 70%
   :scale-latex: 40 

   Ukázka orientace v panelu podle stromové struktury.

V horní části panelu je filtr pro rychlé vyhledání funkce.

..
    Výhodou tohoto filtru je, že vyhledává i v neaktivních algoritmech
    a v případě shody se zadaným řetězcem se ukáže ve spodní části
    upozornění s možností prohlížení a rychlé aktivace algoritmů.

.. _geoproc_filter:

.. figure:: images/geoproc_filter.png
   :scale: 70%
   :scale-latex: 40 

   Použití filtru a upozornění. 

.. note:: Filtr vyhledává jak české tak anglické názvy. Je ale obecně
   výhodnější použít anglické názvy. Někteří poskytovatelé (jako
   např. GRASS GIS) nemusí mít načtenou lokalizaci. Namísto "obal"
   zkuste na :numref:`geoproc_filter` zadat "buffer".

.. Po kliknutí na odkaz na konci upozornění (:guilabel:`to view item`) se
    ukáže struktura s výsledky od neaktivních poskytovatelů (šedá barva
    textu). Po kliknutí na tlačítko :guilabel:`Activate` se nám
    poskytovatel aktivuje.

    .. figure:: images/geoproc_filter_disa.png
       :scale: 70%
       :scale-latex: 40 

       Zobrazení výsledků neaktivních algoritmů s možností aktivace.
       
