.. |raster-clip| image:: ../images/icon/raster-clip.png
   :width: 1.5em
   
.. _davka:

Dávkové zpracování
==================

Dávkové zpracování nám umožní spustit jeden algoritmus vícekrát najednou
s různými parametry. Spustit dávkový proces lze přímo z okna nástrojů
zpracování vyvoláním kontextové nabídky pravým kliknutím na požadovaný
algoritmus a výběrem :guilabel:`Spustit dávkový proces`
(:numref:`batch`). Další možnost jak dávkový proces spustit je přímo
z okna algoritmu, pomocí tlačítka :item:`Spustit jako dávkový proces`
v levém dolním rohu (:numref:`batch2`).

.. _batch:
.. figure:: images/geoproc_batch.png 
   :class: middle

   Spuštění dávkového procesu z okna nástrojů zpracování.

.. _batch2:
.. figure:: images/geoproc_batch2.png 
   :class: small 

   Tlačítko :item:`Spustit jako dávkový proces` v okně algoritmu.

Popis okna
----------

V okně dávkového zpracování máme opět záložky :guilabel:`Parametry` a
:guilabel:`Záznam`. V záložce :guilabel:`Parametry` se nám zobrazí
všechny vstupní parametry vybraného algoritmu v jednom řádku, každý
řádek potom odpovídá samostatnému procesu. Řádky lze přidávat a
odebírat pomocí tlačítek |symbologyAdd| a |symbologyRemove|. Dále lze
nakonfigurovaný dávkový proces uložit |mActionFileSave| do souboru ve
formátu :wikipedia:`JSON` nebo tento typ souboru nahrát
|mActionFileOpen|. U algoritmů, kde je možná volba pokročilého
nastavení se pro aktivaci těchto parametrů ukáže ikonka
|processingAlgorithm|. Záložka záznam má totožnou funkci jako u
samostatného procesu. Pokud chceme výsledné vrstvy načíst do projektu,
je nutné zaškrtnout políčko :guilabel:`Načíst vrstvy po dokončení`.

.. figure:: images/geoproc_batch_win.png 
   :class: middle

   Okno dávkového zpracování.
   
.. warning:: Při odebírání řádků se odebere vždy poslední řádek.
   
Zadávání parametrů
------------------
Zadávání parametrů funguje, až na malé odchylky, stejně jako u
samostatného procesu. Některá specifika si popíšeme níže.

.. tip:: Poklikáním na název sloupce/parametru, se automaticky vyplní
         hodnoty prvního řádku do ostatních řádků.

Výběr vrstev
^^^^^^^^^^^^
Výběr vrstev provádíme za pomocí tlačítka :item:`...`, kdy můžeme buď vybrat 
vrstvy nahrané v projektu (:numref:`batchlay`) nebo vyhledat soubory uložené na 
disku. V obou případech je možné (u některých algoritmů nutné) vybrat více 
vrstev. Pokud se jedná o algoritmus se vstupem jedné vrstvy, při výběru  více 
vrstev se jednotlivé vrstvy přiřadí k vlastním procesům procesům.

.. figure:: images/geoproc_batch_lay.png 
   :class: middle

   Možnosti výběru vrstev.
   
.. _batchlay:
.. figure:: images/geoproc_batch_lay2.png 
   :class: small

   Výběr více vrstev v projektu.
   
   
.. figure:: images/geoproc_batch_lay3.png 
   :class: middle 

   Při výběru více vrstev se každá přiřadí k vlastnímu procesu.
   
Výstupní soubor
^^^^^^^^^^^^^^^
Zde je, oproti samostatnému procesu, nutné zadat cestu k výstupnímu souboru 
pomocí tlačítka :item:`...`. Stačí však zadat uložení prvního výstupního 
souboru a objeví se nám okno pro automatické doplnění výstupních souborů 
(:numref:`batchout`). Zde je možné automaticky vytvořit výstupní soubory s 
příponou pořadového čísla nebo na základě vybraného vstupního parametru 
(název vrstvy, velikost bufferu atd., viz :numref:`batchout2`).

.. warning:: Pokud v obecném nastavení možností zpracování neaktivujeme 
	     |processingAlgorithm|:guilabel:`Použít název souboru pro název vrstvy` budou 
	     výsledné vrstvy v panelu vrstev pojmenovávány podle algoritmu (viz. 
	     :ref:`nastaveni` ). Samotné soubory však budou pojmenované podle naší 
	     konfigurace výstupu.

.. _batchout:
.. figure:: images/geoproc_batch_out.png 
   :class: tiny
   
   Nastavení automatického vyplnění výstupního souboru.
   
.. _batchout2:
.. figure:: images/geoproc_batch_out2.png 
   :class: tiny
   
   Možnosti automatického vytvoření přípon výstupního souboru.

.. note:: U vektorových dat nelze v současné verzi nastavit spuštění
          pouze vybrané prvky.

Praktická ukázka
----------------

V následujících příkladech si ukážeme možné praktické využití dávkového 
zpracování.

Tvorba vícenásobné obalové zóny
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

V případě, že potřebujeme kolem nějakého území vytvořit větší počet
různě velkých obalových zón, je možné využít funkci
|mAlgorithmBuffer|:guilabel:`Obalová zóna` v režimu dávkového procesu. V našem
příkladu vytvoříme z vrstvy velkoplošných chráněných území tři
obalové zóny (1, 5 a 10 km).

Spustíme dávkový proces algoritmu, nastavíme vstupní vrstvu s do tří
řádků (pro každý proces) a požadované hodnoty vzdáleností obalové zóny 
v metrech (1000, 5000, 10000). 

.. figure:: images/geoproc_batch_pract1.png 

   Tvorba vícenásobné obalové zóny vybraného území.

Vybereme výstupní soubor a nastavíme automatickou výpň na základě parametru 
:guilabel:`Vzdálenost` a spustíme dávkový proces tlačítkem :item:`Run`, 
zkontrolujeme záznamy a zavřeme okno. V tomto případě se nám do názvu
souboru vloží i znak čárky (jedná se o číslo s desetinnou čárkou) což
není zrovna ideální. Název můžeme opravit ručně přímo v okně, nebo
v případě potřeby potom soubory hromadně přejmenovat.

.. figure:: images/geoproc_batch_pract1_2.png 
   :class: tiny

   Nastavení automatického vyplnění na základě parametru - Vzdálenost.

.. figure:: images/geoproc_batch_pract1_3.png 
   :class: small 
   :scale-latex: 40 

   Výsledné názvy výstupních souborů
   
.. figure:: images/geoproc_batch_pract1_4.png 
   :class: middle

   Výsledek tvorby vícenásobné obalové zóny.


Ořezání více rastrových vrstev 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
K tomuto úkolu budeme potřebovat více rastrových vrstev, pokud nemáme,
vytvoříme z digitálního modelu terénu (dmt) vrstvu sklonu svahů (Slope) a 
orientace svahů (Aspect). K vytvoření vrstvy sklonu a orientace svahů jsme nyní 
schopni využít více funkcí, mimo vestavěné funkce QGISu to jsou  např. GDAL 
|providerGdal|:guilabel:`Sklon` a |providerGdal|:guilabel:`Aspekt` nebo využít externí 
|providerGrass|:grasscmd:`r.slope.aspect` nebo |providerSaga|:guilabel:`Slope, aspect, 
curvature`.

.. figure:: images/geoproc_batch_pract2.png 

   Rastrové vrstvy.
   
Vytvořili jsme tedy 2 nové rastrové vrstvy. Nyní opět využijeme 
funkci |raster-clip| :guilabel:`Oříznout rastr podle rozsahu`, ale
tentokrát jako dávkový proces na všechny rastrové vrstvy najednou.
  
Jako vstupní vrstvy vybereme rastrové vrstvy, které chceme ořezat (dmt, aspect, 
slope), a zvolíme rozsah ořezu v mapovém okně, hodnotu rozsahu potom 
nakopírujeme do dalších řádků (:numref:`batchclip`). Výstupním souborům necháme 
přidělit příponu podle parametru :guilabel:`Vstupní vrstva` a spustíme proces.


.. _batchclip:
.. figure:: images/geoproc_batch_pract2_3.png 
   :class: middle
        
   Vstupní vrstvy a zvolený rozsah pro dávkový zpracování 
   |raster-clip| :guilabel:`Oříznout rastr podle rozsahu`.
   
.. figure:: images/geoproc_batch_pract2_4.png 
   
   Automatické přidělení přípony výstupním souborům na základě
   vstupních vrstev.
   
.. figure:: images/geoproc_batch_pract2_5.png 
   
   Výsledek hromadného ořezání rastrových vrstev.
   
