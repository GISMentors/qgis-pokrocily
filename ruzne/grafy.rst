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


Znázornenie diagramov
---------------------

Medzi ďalšie možnosti patrí tvorba diagramov a grafov. QGIS nám umožňuje na 
základe dát vytvárať či už koláčové, textové alebo stĺpcové diagramy a následne 
ich zobrazovať v mape.

Mapa celkovej kriminality krajov ČR
===================================
    
Do mapového okna pridáme vektorovú vrstvu vyšších územných samosprávnych celkov
(:map:`vusc_krim`). Pravým kliknutím na mapu v paneli vrstiev zvolíme 
:item:`Otevrít atributovou tabulku` a prezrieme stĺpce a hodnoty v atribútovej 
tabuľke. Nájdeme tam údaje o kriminalite v Českej republike (zdroj:
`Dátová stránka <http://www.mapakriminality.cz/#tabulky>`_). Stĺpec 
:dbcolumn:`krim_2015c` obsahuje údaje o počte celkovej kriminality 
v jednotlivých samosprávnych celkoch Českej republiky od januára 2014 do 
januára 2015. Atribút s názvom :dbcolumn:`krim_2015v` predstavuje počet vrážd 
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
na výraze. Na :num:`#d-pie` sú znázornené informácie o celkovej 
kriminalite pre jednotlivé vyššie územné samosprávne celky Českej republiky.  

.. _d-pie:

.. figure:: images/d_pie.png
   :class: middle
        
   Celková kriminalita vyšších územných samosprávnych celkov Českej republiky.


