.. only:: latex

   #####
   Obsah
   #####

.. only:: html

   `GISMentors <http://gismentors.cz>`_ | Školení `GRASS GIS
   <http://gismentors.cz/skoleni/grass-gis>`_ | `QGIS
   <http://gismentors.cz/skoleni/qgis>`_ | `PostGIS
   <http://gismentors.cz/skoleni/postgis>`_ | `GeoPython
   <http://gismentors.cz/skoleni/geopython>`_
   
   ****
   Úvod
   ****

.. only:: html

   .. image:: images/qgis_logo.png
      :width: 140px
      :align: left

.. index::
   single: GIS
   single: geografický informační systém

`QGIS <http://qgis.org/en/site/>`_  je open source *geografický informační systém*
(:wikipedia:`GIS`) publikovaný pod všeobecnou licencí GNU GPL.
Projekt QGIS vznikl v roce 2002, verze s označením 1.0 vyšla později v roce 2009.
Mezi hlavní výhody patří zejména rychlost vývoje a rozšiřování jeho funkcionality.
Licence GNU GPL umožňuje používání software i pro komerční účely. Podstatné je, že
umožňuje i modifikaci zdrojového kódu a jeho následné šíření.

.. only:: latex

   .. figure:: images/qgis_logo.png
      :width-latex: 150

      Logo projektu QGIS.

Současným konceptem ve vývoji je pravidelné a intenzivní publikování
nových verzí. Dlouhodobá stabilní verze (LTR) je doplněna dvěma
krátkodobými verzemi (viz `QGIS release schedule
<https://qgis.org/en/site/getinvolved/development/roadmap.html#release-schedule>`__). Krátkodobé
verze mají sloužit pro zveřejňování nových funkcionalit v kratších
intervalech.

Přechod na verzi 3.x je spojen s postupem technologií, konkrétně zejména povýšení:
  * Python 2.7 na Python 3
  * Qt4 na Qt5

S touto změnou přicházejí nejenom novější a lepší technologické nástroje, ale
také jasná zpráva o tom, že QGIS se neustále vyvíjí, drží krok a nezastarává.
Součástí velkých změn je i v tomto případě nutnost se adaptovat na ně, což závisí
hlavně od způsobu jakým QGIS uživatel využívá. Všechny změny ale vycházejí z
dlouhodobého plánování a hlavně z požadavků uživatelů.

.. only:: html

.. important:: Školení je zaměřeno na aktuální LTR verzi **QGIS 3.4
   Madeira**. V jiných verzích není zaručena funkčnost uvedených
   příkladů. Dále předpokládáme zapnutou *českou lokalizaci*,
   :menuselection:`Možnosti --> Obecné`. Obsahově navazuje na školení
   :skoleni:`QGIS pro začátečníky <qgis-zacatecnik>`. K dispozici jsou
   i historické školící materiály k verzím QGIS :skoleni:`2.14
   <qgis-pokrocily/2.14>` a :skoleni:`2.18 <qgis-pokrocily/2.18>`.

.. index::
   pair: datové sady; ke stažení

.. notedata::

   *Data ke školení* jsou stažitelná jako `zip archiv
   <http://training.gismentors.eu/geodata/qgis/data.zip>`__ (614
   MB).

.. only:: html
             
   #####   
   Obsah
   #####

.. toctree::
   :maxdepth: 2

   georeferencovani/index
   geoprocessing/index
   modeler/index
   grass/index
   hydrologie/index
   3d/index
   pokrocile_upravy/index
   ruzne/index
   priklady/index

*******
Dodatky
*******

O dokumentu
===========

Text dokumentu je licencován pod `Creative Commons
Attribution-ShareAlike 4.0 International License
<http://creativecommons.org/licenses/by-sa/4.0/>`_.

.. figure:: images/cc-by-sa.png 
   :width: 130px
   :scale-latex: 120
              
*Verze textu dokumentu:* |release| (sestaveno |today|)

Autoři
------

Za `GISMentors <http://www.gismentors.cz/>`_:

* `Alžbeta Gardoňová <http://www.gismentors.cz/mentors/gardonova/>`_
* `Ľudmila Furtkevičová <http://www.gismentors.cz/mentors/furtkevicova/>`_
* `Oto Kaláb <http://www.gismentors.cz/mentors/kalab/>`_ 
* `Martin Landa <http://www.gismentors.cz/mentors/landa>`_

Text dokumentu
--------------

.. only:: latex

   Online HTML verze textu školení je dostupná na adrese:

   * http://training.gismentors.eu/qgis-pokrocily

Zdrojové texty školení jsou dostupné na adrese:

* https://github.com/GISMentors/qgis-pokrocily

  Případné chyby nebo náměty na vylepšení můžete hlásit:

* https://github.com/GISMentors/qgis-pokrocily/issues
