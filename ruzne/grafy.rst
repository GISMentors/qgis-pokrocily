.. |diagram| image:: ../images/icon/diagram.png
   :width: 1.5em
.. |box_no| image:: ../images/icon/checkbox_unchecked.png
   :width: 1.5em
.. |box_yes| image:: ../images/icon/checkbox.png
   :width: 1.5em
.. |histogram| image:: ../images/icon/histogram.png
   :width: 1.5em
.. |pie-chart| image:: ../images/icon/pie-chart.png
   :width: 1.5em
.. |text| image:: ../images/icon/text.png
   :width: 1.5em
.. |plus| image:: ../images/icon/mActionSignPlus.png
   :width: 1.5em
.. |minus| image:: ../images/icon/mActionSignMinus.png
   :width: 1.5em
.. |expression| image:: ../images/icon/mIconExpression.png
   :width: 1.5em
.. |catsymbol| image:: ../images/icon/rendererCategorizedSymbol.png
   :width: 1.5em
.. |q2t| image:: ../images/icon/q2t.png
   :width: 1.5em
.. |mActionCalculateField| image:: ../images/icon/mActionCalculateField.png
   :width: 1.5em






Znázornenie diagramov
---------------------

Medzi ďalšie možnosti patrí tvorba diagramov a grafov. QGIS nám umožňuje na 
základe dát vytvárať či už koláčové, textové alebo stĺpcové diagramy a následne 
ich zobrazovať v mape.

Do mapového okna pridáme vektorovú vrstvu vyšších územných samosprávnych celkov
(:map:`vusc_krim`). Nastavíme štýl, napr. na :num:`#cr-styl` je typ vrstvy 
symbolu nastavený na ``Shapeburst fill``, ide o ``Prevrácené polygóny`` s farbami
prechodu ``modrá`` a ``biela`` s nastaveným tieňovaním do vzdialenosti
5 mm. Popisky predstavujú názvy jednotlivých samosprávnych celkov 
(:dbcolumn:`nazev`), ich veľkosť je nastavná na ``10``, povolená je svetlomodrá 
obalová zóna s veľkosťou ``3 mm`` a umiestnenie je okolo centroidu.

.. _cr-styl:

.. figure:: images/cr_styl.png
   :class: middle
        
   Vyššie územné samosprávne celky Českej republiky.

Mapy kriminality krajov ČR
==========================

Záložka |diagram| :sup:`Diagramy`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Pravým kliknutím na mapu v paneli vrstiev zvolíme 
:item:`Otevrít atributovou tabulku` a prezrieme stĺpce a hodnoty v atribútovej 
tabuľke. Nájdeme tam údaje o kriminalite v Českej republike (zdroj:
`Dátová stránka <http://www.mapakriminality.cz/#tabulky>`_). Konkrétnejšie, 
stĺpec :dbcolumn:`krim_2015c` obsahuje údaje o počte celkovej kriminality 
v jednotlivých samosprávnych celkoch Českej republiky od januára 2014 do 
januára 2015 a stĺpec s názvom :dbcolumn:`krim_2015v` predstavuje počet vrážd 
pre to isté obdobie. Tieto údaje pridáme do mapy vo forme diagramov.

V dialógovom okne *Vlastnosti vrstvy* (pravé tlačidlo myši na mapu a voľba 
:item:`Vlastnosti`) zvolíme záložku |diagram| :sup:`Diagramy`. Zobrazia sa 
nastavenia súvisiace s ich tvorbou.

V prvom kroku zaklikneme |box_no| :sup:`Show diagrams for this 
layer`. Potom vyberieme typ diagramu, pričom môže ísť o 
|pie-chart| :sup:`Koláčový graf`, |text| :sup:`Textový diagram` alebo 
|histogram| :sup:`Histogram`. V rámci tohto okna je možné nastaviť jeho vzhľad, 
formát, viditeľnosť, tlačidlami |plus| a |minus| sa dá pridávať, resp. uberať 
zobrazované atribúty, tlačidlom |expression| možno definovať atribút založený 
na výraze. Na :num:`#d-pie` sú kombináciou koláčového grafu a textového diagramu
znázornené informácie o celkovej kriminalite pre jednotlivé vyššie územné 
samosprávne celky Českej republiky. Je to jeden z najjednoduchších spôsobov
takejto reprezentácie dát (zobrazujeme len jeden atribút).

.. _d-pie:

.. figure:: images/d_pie.png
   :class: middle
        
   Celková kriminalita vyšších územných samosprávnych celkov Českej republiky.


Zásuvný modul Qgis2threejs
^^^^^^^^^^^^^^^^^^^^^^^^^^

Ďalším spôsobom je zobrazenie pomocou pluginu *QGIS2threejs*. Pôjde o informácie
o počte vrážd pre jednotlivé samosprávne kraje (atribút :dbcolumn:`krim_2015v`)
za rok 2015. 

.. note:: Tento plugin sa dá spustiť, len ak je prítomná rastrová vrstva 
	  digitálneho modelu terénu, preto netreba zabudnúť do mapového okna 
	  pridať rastrovú vrstvu :map:`dmt`.

Nastavíme štýlovanie vrstiev, t.j. |catsymbol| :sup:`Kategorizovaný symbol` pre hodnoty
o počte vrážd za rok 2015. Pomocou :menuselection:`Web --> OpenLayers Plugin`
pridáme do mapového okna napríklad aj vrstvu :map:`OpenStreetMap`. Výsledok môže
vyzerať ako to znázorňuje :num:`cr-graf-osm`. 

.. _cr-graf-osm:

.. figure:: images/cr_graf_osm.png
   :class: middle
        
   Počet vrážd pre vyššie územné samosprávne celky Českej republiky.

V dialógovom okne zásuvného modulu |q2t| :sup:`Qgis2threejs` na zobrazovanie dát 
v prostredí web-u nastavíme v záložke ``World`` rozsah, mierku, farbu pozadia, 
typ zobrazovaných súradníc, ... v záložke ``DEM`` predovšetkým vstupný 
digitálny model terénu, prípadne rozlíšenie či nastavenie transparentnosti a 
nakoniec v záložke ``Polygon`` použijeme vrstvu :map:`vusc_krim` a jej atribút 
:dbcolumn:`krim_2015v` prenásobený hodnotou napr. ``3000``. 
Potvrdíme stlačením :item:`Run` a počkáme na automatické otvorenie výsledku 
vo webovom prehliadači. Tu môžeme zapínať, resp. vypínať vrstvy, meniť 
transparentnosť ako vrstiev, tak pozadia, viď. :num:`cr-graf-g2t`.

.. _cr-graf-g2t:

.. figure:: images/cr_graf_g2t.png
   :class: middle
        
   Počet vrážd pre vyššie územné samosprávne celky Českej republiky.

Štatistika dopravných prostriedkov
==================================

Do mapového okna pridáme vrstvy ako železníce (:map:`zeleznice`), 
diaľnice (:map:`silnice_1`), rýchlostné cesty (:map:`silnice_2`), cesty 1. a 2. 
triedy (:map:`silnice_3`, map:`silnice_4` a :map:`silnice_5`). 
Skontrolujeme či všetky vrstvy majú rovnaký súradnicový systém, t.j. 
:menuselection:`Vlastnosti --> Obecné --> Souradnicový referenčný systém`). 
Potom z menu lišty vyberieme :menuselection:`Vektor --> Analytické nástroje -->
Součet délek čar`. Otvorí sa dialógové okno, kde nastavíme vstupnú polygónovú
a líniovú vektorovú vrstvu a názov výstupnej vrstvy (:num:`#soucet-silnice-okno`). 
Urobíme to pre všetky dopravné komunikácie, tak, že výstupnú plošnú vrstvu
použijeme ako vstup pre ďalšiu, viď. :num:`cr-silnice`. Takto nám nakoniec 
vznikne vektorová vrstva krajov s informáciami o dĺžke vybraných komunikácií,
viď. atribútová tabuľka poslednej mapy :map:`sum_z` na :num:`#at-sum`. 

.. _soucet-silnice-okno:

.. figure:: images/soucet_silnice_okno.png
   :scale: 55%
        
   Dialógové okno pre sčítanie dĺžky dopravných komunikácií v rámci krajov.

.. _cr-silnice:

.. figure:: images/cr_silnice.png
   :class: middle
        
   Vybrané dopravné cesty Českej republiky a panel vrstiev po sčítaní ich dĺžok.

.. _at-sum:

.. figure:: images/at_sum.png
   :scale: 55%
        
   Atribútová tabuľka s dĺžkou vybraných komunikácií.

Potom pomocou kalkulačky polí |mActionCalculateField| :sup:`Otvoriť kalkulátor polí`
zaokrúhlime hodnoty na celé čísla. Najprv zaklikneme 
|box_yes| :sup:`Aktualizovať existujúce pole` a následne do okna *Výraz*
zadáme ``round("sum_s1"/1000)``, viď. :num:`kalk-poli`. Postupujeme obdobne
pri stĺpcoch :dbcolumn:`sum_s2`, :dbcolumn:`sum_s3`, :dbcolumn:`sum_s4`, 
:dbcolumn:`sum_s5` a :dbcolumn:`sum_z`. Na záver zmeny uložíme. 

.. _kalk-poli:

.. figure:: images/kalk_poli.png
   :scale: 60%
        
   Zaokrúhlenie dĺžok v atribútovej tabuľke pomocou kalkulačky polí.

.. note:: Mapu :map:`sum_z` premenujeme na :map:`vusc_silnice`.

Potom postupujeme obdobne ako pri mape celkovej kriminality záložkou 
|diagram| :sup:`Diagramy`. Nastavíme priehľadnú výplň a umiestnenie 
``Inside polgon``. Výsledok prekryjeme s vrstvou :map:`vusc` 
(:num:`#silnice-graf-all`)

.. _silnice-graf:

.. figure:: images/silnice_graf.png
   :class: middle
        
   Vytvorenie diagramov predstavujúcich podiel komunikácií v krajoch ČR.

.. _silnice-graf-all:

.. figure:: images/silnice_graf_all.png
   :class: middle
        
   Grafické znázornenie počtu diaľnic, rýchlostných ciest, 
   ciest 1., 2. a 3. formou diagramov.

Ďalej môžeme vrstvu :map:`vusc-silnice` duplikovať a namiesto koláčového grafu 
znázorniť textové diagramy. V prípade, že všetky vrstvy prekryjeme, výsledok
môže byť ako na :num:`#silnice-graf-text`.

.. _silnice-graf-text:

.. figure:: images/silnice_graf_text.png
   :class: small
        
   Grafické znázornenie informácií formou diagramov spolu s textom.


