Části modelu
============

Název a skupina
---------------

Před samotnou tvorbou modelu je vhodné zadat název a skupinu modelu
(:numref:`modeler_casti`) a uložit jej |mActionFileSave|. Potom
můžeme model při jeho tvorbě průběžně ukládat.

.. figure:: images/modeler_name.png 
   :class: tiny 

   Zadání jména a skupiny modelu.

Vstupní parametry
-----------------

.. _vstupdia:
.. figure:: images/modeler_vstup_dia.png 
   :class: tiny

   Značení vstupního parametru v modelu.
   
Prvním krokem při tvorbě modelu je vložení vstupních parametrů. Tyto parametry 
jsou stejné jako u běžných algoritmů - vrstva, rozsah vrstvy, číslo, text, 
boolean (formou checkboxu) atd. Při spouštění vytvořeného modelu bude 
požadováno vyplnění vložených vstupních parametrů. Tyto parametry potom
budou vstupovat do konkrétních algoritmů v modelu.

.. figure:: images/modeler_vstup.png 
   :class: tiny 

   Možné vstupní parametry.
   
Jednotlivé parametry lze do modelu přidat tažením nebo poklikáním. Po přídání 
se objeví dialogové okno, které je u většiny parametrů jednoduché. Základní 
položkou je zde název parametru. Nastavení parametrů v modelu lze průběžně 
měnit kliknutím na symbol tří teček, nebo lze parametry odstranit kliknutím na 
křížek (:numref:`vstupdia`).

.. figure:: images/modeler_vstup_num.png 
   :class: tiny 

   Dialogové okno při vložení číselného parametru.

- do našeho modelu přidáme vstupy :item:`Rozsah` a :item:`Číslo`.
  Pojmenujeme např. :guilabel:`Rozsah` a :guilabel:`Počet bodů`,
  později můžeme podle potřeby změnit.

Algoritmy
---------

.. figure:: images/modeler_algor_dia.png 
   :class: tiny

   Značení algoritmu v modelu.
   
Hlavní součástí modelů jsou algoritmy. Nalezneme zde většinu algoritmů, které 
jsou v okně nástrojů zpracování.

.. _algor:
.. figure:: images/modeler_algor.png 
   :class: tiny 

   Možné vstupní algoritmy.
   
Algoritmy se přidávají do modelu opět tažením nebo poklikáním. Po přidání se 
otevře dialogové okno konkrétního algoritmu (:numref:`algorrand`). Zde máme 
možnost nastavit výchozí hodnoty parametrů algoritmu, se kterými se bude 
počítat při spuštění modelu. Jesltiže chceme mít parametry při spouštění modelu 
volitelné je třeba nakonfigurovat odpovídající vstupy (:numref:`algorrand2`).
U číselných hodnot lze kromě pevě nastavené hodnoty a hodnoty vstupu,
požít také předpočítanou hodnoty pomocí vzorce nebo hodnotu z výstupu
jiného algoritmu (:numref:`algornum`).

.. _algornum:
.. figure:: images/modeler_algor_num.png 
   :class: middle 

   Možnosti vstupu hodnot u číselných parametrů.

.. _algorrand:
.. figure:: images/modeler_algor_rand.png 
   :class: medium 

   Dialogové okno algoritmu s pevně stanovenými parametry.

- vložíme algoritmus
  |mAlgorithmRandomPointsWithinExtent|:guilabel:`Náhodné body v rozsahu`
  a jako vstupní rozsah zadáme náš vstupní
  parametr :item:`Rozsah`. U počet bodů nastavíme hodnotu pomocí 
  :guilabel:`Model Input` a vybereme vstupní parametr 
  :item:`Počet bodů`. Minimální vzdálenost a výstupní soubor měnit
  prozatím nebudeme, potvrdíme parametry tlačítkem :item:`OK`.


.. _algorrand2:
.. figure:: images/modeler_algor_rand2.png 
   :class: middle 

   Nastavení parametrů na základě vstupů do modelu.

Nastavení algoritmů v modelu lze průběžně editovat kliknutím na symbol
tří teček nebo lze algotritmy odstranit kliknutím na křížek. Také lze
použít tlačítek ``+`` a ``-`` pro náhled propojení vstupů a výstupů.

.. _algorrand3:
.. figure:: images/modeler_algor_rand3.png 
   :class: meduim 
   
   Nastavení volitelných parametrů algoritmu
   |mAlgorithmRandomPointsWithinExtent|:guilabel:`Random points in
   extent` při spouštění modelu.

Jednotlivé algoritmy lze na sebe dále navazovat - to co je výstupem z jednoho 
algoritmu může nějakým způsobem vstupovat do algoritmu druhého 
(:numref:`algorrand4`).

- Vložíme do modelu algoritmus |mAlgorithmBuffer|:guilabel:`Obalová zóna`.
  Jako vstupní vrstvu nastavíme :guilabel:`'Náhodné body' from
  algorithm 'Náhodné body v rozsahu'` a dále nastavíme
  libovolnou fixní vzdálenost v metrech.

.. _algorrand4:
.. figure:: images/modeler_algor_rand4.png 
   :class: middle 

   Náhodné body vygenerované
   |mAlgorithmRandomPointsWithinExtent|:guilabel:`Random points in
   extent` použité jako vstup pro vytvoření obalových zón.

Pravým kliknutím na algoritmus v modelu můžeme vyvolat kontextové menu, 
ve kterém můžeme algoritmus vymazat, deaktivovat nebo spustit jeho editaci 
(:numref:`algkont`).

.. _algkont:
.. figure:: images/modeler_algor_kont.png 
   :class: middle 

   Kontextové menu algoritmu v modelu.

.. tip:: Ve spodní části dialogového okna každého algoritmu je 
        parametr :guilabel:`Dependencies`, pomocí kterého lze nastavit 
        nadřazené algoritmy. Takto vybrané algoritmy se budou vždy spouštět před 
        tímto algoritmem (:numref:`algpar`).

    .. _algpar:
    .. figure:: images/modeler_algor_parent.png 
       :class: middle 

       Nastavení rodičovských algoritmů.
       
Výstupy
-------

.. figure:: images/modeler_out_dia.png 
   :class: tiny

   Značení výstupu v modelu.
   
Výstup slouží k vytvoření souboru (vrstva, HTML stránka atd.). Může
sloužit jako vlastní konečný výsledek modelu, ale také lze nastavit
výstupy průběžně u jednotlivých algoritmů. Výstup se konfiguruje u
každého algoritmu zvlášť, stačí zadat název výstupu do textového pole
ve spodní části dialogového okna algoritmu
(:numref:`modeloutname`). Všeobecně, a především při generování více
výstupů, je vhodné zvolit smysluplný název podle toho jaký je obsah
dat nebo co nám data sdělují.
   
.. _modeloutname:
.. figure:: images/modeler_out_name.png 
   :class: small

   Dialogové okno algoritmu - pole pro zadání názvu výstupu.

- Otevřeme (editace) algoritmus |mAlgorithmBuffer|:guilabel:`Obalová zóna`
  zadáme libovolný název finálního výstupu (např. :item:`Výstup`).

Zadáním jména do textového pole pro výstup, nastavíme model, aby vytvořil 
výstupní soubor. Pokud pole necháme nevyplněné, model žádný soubor nevytvoří. 
Výsledek algoritmu však může dále sloužit jako vstup pro jiné algoritmy.

.. _modelerukaz:
.. figure:: images/modeler_out_model.png 
   :class: middle 

   Model, ve kterém bude výstupem vrstva obalových zón.

.. figure:: images/modeler_out_model2.png 
   :class: middle

   Ukázka modelu z více výstupy.
