.. |mActionAddRasterLayer| image:: ../images/icon/mActionAddRasterLayer.png
   :width: 1.5em


Práce s 3D daty
^^^^^^^^^^^^^^^

Zobrazování 3D dat v QGISu bylo možné už v minulosti a to zejména pomocí pluginů
(např. Qgis2threejs  https://plugins.qgis.org/plugins/Qgis2threejs/,).
Od verze 3.0 je základní součástí QGISu také `3D mapové okno 
<https://qgis.org/en/site/forusers/visualchangelog30/index.html#d-features>`_,
které slouží na vizualizaci 3D dat.

Práce s daty, které mají i Z-ovou souřadnici je na vzestupu i díky postupu v
technologii, která umožňuje práci s takovýmito daty zpřístupnit i pro běžné
počítače bez speciálního  vybavení a zvýšených nároků na jejich výkon.


Popis typických dat
===================

Tak jako u běžných mapových podkladů zobrazujeme zemský povrch a jevy, které se
na něm nachází, budeme z tohoto předpokladu vycházet i v případě práce se 
zobrazováním ve 3D.Musíme tedy začít tím, že budeme zobrazovat
**zemský povrch**.

Jednu formu reprezentace povrchu jsme použili již v `začátečnickém kurzu  
<http://training.gismentors.eu/qgis-zacatecnik/rastrova_data/rastr_terenni_analyzy.html>`_.
Jedná se o digitální model terénu, který pokrývá celé území ČR.
Jeho nevýhodou však je, že jeho prostorové rozlišení není dostačující pro řešení úkolů pro jednotlivé části území.
Pro území ČR ČÚZK poskytuje digitální model reliéfu (nejnovější je pátá generace DMR5G) a digitální model povrchu (jediná verze DMP1G).





