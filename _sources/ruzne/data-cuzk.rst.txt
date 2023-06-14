.. |vfkPlugin| image:: images/vfkPluginIcon.png
   :width: 1.5em

Práce s daty ČÚZK (RÚIAN, VFK, ...)
-----------------------------------

Tato kapitola pojednává o možnosti pracovat s českými výměnnými
formáty *VFR* (:ref:`Výměnný formát RÚIAN <vfr>`) a *VFK*
(:ref:`Výměnný formát katastru <vfk>`) v prostředí QGIS.

.. _vfr:

Výměnný formát RÚIAN (VFR)
==========================

:wikipedia:`RÚIAN` (*Registr Územní Identifikace, Adres a
Nemovitostí*) patří do systému základních registrů. Poskytuje údaje o
základních územních prvcích jako jsou území státu, katastr, parcela,
nemovitost a další. Více informací najdete na stránkách `ruian.cz
<http://www.ruian.cz>`_.

Data jsou poskytována ve *výměnném formátu RÚIAN* (VFR) službou
`Veřejného dálkového přístupu <http://vdp.cuzk.cz>`_. Datový formát
VFR je podporován knihovnou GDAL. Vzhledem k tomu je můžeme načíst do
QGISu jako každá jiná vektorová souborová data.

.. important:: Formát VFR definuje více geometrických reprezentací na
   prvek, typicky definiční bod, originální a
   generalizovanou hranici. QGIS je v současnosti (3.4)
   schopen zobrazit *pouze první dostupnou geometrii* (tj. většinou
   pouze definiční bod), přestože je knihovna GDAL schopná
   tyto data číst korektně.
   
   .. figure:: images/vfr-vrstvy.png

      Seznam vrstev při načtení v QGISu. U parcel je možné
      načíst pouze definiční body.

Limit QGISu je možné obejít pomocí konverze dat VFR do vhodného
formátu a výběru preferované geometrie. Takto k problému přístupuje i
`RUIAN plugin
<https://ctu-geoforall-lab.github.io/qgis-ruian-plugin/>`__, který
podporuje uložení dat do formátů SQLite, OGC GeoPackage a Esri
Shapefile. Plugin lze nainstalovat běžným způsobem z menu
:menuselection:`Zásuvné moduly --> Spravovat a instalovat zásuvné
moduly`. Je dostupný pro obě verze QGISu 2 i 3.

.. figure:: images/ruian-plugin.png
   :class: large

   Ukázka použití pluginu pro práci s daty RÚIAN.

.. noteadvanced:: Konverzi můžeme provést konzolovými konverzními
   nástroji *vfr2ogr*. Výhoda těchto nástrojů je v tom, že kromě
   jednotlivých vstupních VFR souborů můžeme použít seznam linků
   stažitelný z `VDP <http://vdp.cuzk.cz>`_. V tomto případě budou VFR
   data nástrojem *vfr2ogr* automaticky stažena a naimportována do
   cílového formátu. 

   Konverzní nástroje *vfr2ogr* najdete na serveru GitHub, viz
   `stránka s verzemi
   <https://github.com/ctu-geoforall-lab/gdal-vfr/releases>`_ ke
   stažení.

   Jako příklad si ukážeme stažení dat pro OPR Litoměřice a konverzi dat
   do databáze SQLite.

   .. figure:: images/vfr-vdp-ltm.png
      :class: middle
        
      Na portálu VDP vybereme ORP Litoměřice a stáhneme seznam linků.

   Seznam linků z VDP použijeme jako vstup pro nástroj
   *vfr2ogr*. Seznam z VDP obsahuje data za poslední tři měsíce. Před
   importem vybereme pouze ty nejaktuálnější, např. pomocí unixového
   nástroje *grep*.

   .. code-block:: bash

      grep '20190301' seznamlinku.txt > seznamlinku-aktualni.txt
          
   .. code-block:: bash

      vfr2ogr --file seznamlinku-aktualni.txt --format SQLite --dsn ruian_ltm.db --geom OriginalniHranice

   Jako vstupní soubor do nástroje můžete použít přímo data ve formátu
   VFR. Potom se provede import pouze zvoleného souboru.

   .. code-block:: bash
      
      vfr2ogr --file data/20190301_OB_530506_UKSH.xml.zip --format SQLite --dsn ruian_obec.db --geom OriginalniHranice 
                
   Výsledná databáze potom obsahuje data za celou zvolenou ORP:

   ::

      Layer            obce                 ...         40 features
      Layer            spravniobvody        ...          0 features
      Layer            mop                  ...          0 features
      Layer            momc                 ...          0 features
      Layer            castiobci            ...        142 features
      Layer            katastralniuzemi     ...        128 features
      Layer            zsj                  ...        195 features
      Layer            ulice                ...        445 features
      Layer            parcely              ...     173825 features
      Layer            stavebniobjekty      ...      25727 features
      Layer            adresnimista         ...      17513 features

   Výslednou databázi `ruian_ltm.db` můžeme v QGISu načíst jako běžná
   souborová vektorová data.

   .. figure:: images/vfr-sqlite-vrstvy.png

      Seznam vrstev včetně polygonových vrstev (originální nebo
      generalizované hranice).

   .. figure:: images/vfr-ltm-vizualizace.png
      :class: middle
        
      Příklad vizualizace parcel v ORP Litoměřice.

.. _vfk:

Výměnný formát katastru (VFK)
=============================

Výměnný formát (VF) je určen k vzájemnému předávání dat mezi systémem
ISKN a jinými systémy zpracování dat, viz `dokumentace formátu
<https://www.cuzk.cz/Katastr-nemovitosti/Poskytovani-udaju-z-KN/Vymenny-format-KN/Vymenny-format-NVF.aspx>`_.

Díky tomu, že je formát VFK podporován `knihovnou GDAL
<https://www.gdal.org/drv_vfk.html>`__, tak je můžete v prostředí
QGISu načíst jako každá jiná vektorová souborová data. Po načtení dat
se objeví dialog pro výběr vrstev, které odpovídají jednotlivým
datovým blokům VFK. Některé mají definovánu geometrii (např. BUD, PAR,
HP a další), jiné obsahují pouze popisné informace.

.. _vfk-vrstvy:

.. figure:: images/vfk-vrstvy.png

   V dialogu vrstev vybereme vrstvy, které chceme přidat do QGISu.
   
.. important:: Knihovna GDAL při prvním načítání dat vytváří v
               adresáři, ve kterém je umístěn soubor VFK, interní
               :wikipedia:`SQLite` databázi. To znamená, že musíte mít
               v tomto adresáři **právo zápisu**. S tím také souvisí
               fakt, že první načtení dat trvá vždy *delší dobu*,
               neboť dochází k vytvoření interní databáze. Při dalším
               čtení jsou již data načítána přímo z interní databáze,
               což vede k mnohonásobnému zrychlení přístupu k datům.

Po načtení můžeme v QGISu jednotlivé vrstvy s geometrií a popisnými
informace propojovat pomocí standardního |join| :sup:`Připojení`, viz
:skoleni:`QGIS pro začátečníky
<qgis-zacatecnik/vektorova_data/join.html>`. To nicméně vyžaduje
znalosti vnitřní struktury formátu VFK. Proto vznikl specializovaný
zásuvný modul tzv. **VFK plugin**, který pro práci s katastrálními
daty výrazně usnadňuje.

.. figure:: images/vfk-join.png
   :class: small
        
   Příklad připojení tabulky druh pozemku (DRUPOZ) k atributové
   tabulce parcel (PAR) ve vlastnostech vrstvy a záložce Připojení.

Po připojení popisných informací můžeme provádět dotazy typu vyhledání
parcel podle druhu pozemku.
   
.. figure:: images/vfk-join-query.png
   :class: middle
   
   Nalezení parcel, které mají druh pozemku chmelnice.

VFK plugin
^^^^^^^^^^

Mnohem větší komfort při práci s daty ve formátu VFK umožňuje v QGISu
specializovaný **VFK plugin**.

.. note:: Tento zásuvný modul byl vyvinut v roce 2011 a posléze
   významně aktualizován v letech 2015 a 2016 studenty oboru Geomatika
   na ČVUT v Praze, fakulty stavební. Více informací o zásuvném modulu
   najdete na stránkách `portálu FreeGIS
   <http://freegis.fsv.cvut.cz/gwiki/VFK_/_QGIS_plugin>`__ anebo v
   jeho `dokumentaci
   <https://ctu-geoforall-lab.github.io/qgis-vfk-plugin/>`__.

.. warning:: **V současné době je plugin dostupný pouze pro verzi
   QGIS 2.**

   Bohužel kvůli změně distribuovaní informací o vlastnických
   vztazích, ke které byl ČÚZK donucen v rámci aplikace GDPR, neumí v
   současné době VFK plugin tyto informace získávat. Jeho
   funkcionalita je tím poměrně výzmnamně omezena.

.. _geoforall-instalace:
          
Instalace
~~~~~~~~~

V současné době není VFK plugin součástí oficiálního repositáře
QGISu. Pro jeho instalaci je nutné do QGISu zaregistrovat nový
repositář, který je dostupný na adrese
*http://geo.fsv.cvut.cz/geoforall/qgis-plugins.xml*. Postup instalace
je podrobně popsán v `dokumentaci pluginu
<https://ctu-geoforall-lab.github.io/qgis-vfk-plugin/instalace.html>`__.

Zásuvný modul otevřeme pomocí ikonky |vfkPlugin anebo z menu
:menuselection:`Zásuvné moduly --> VFK --> Otevřít prohlížeč VFK`.

Práce se zásuvným modulem
~~~~~~~~~~~~~~~~~~~~~~~~~

Panel nástroje pro práci s katastrálními daty má 3 části:

.. figure:: images/vfk-panel.png
   :class: middle
        
   Panel nástroje a jeho části: část pro vstupní parametry načítání a
   dotazování dat (1), nástrojová lišta (2) a část pro nápovědu a
   výstup dotazů.

Nejprve zadáme VFK soubor, který chceme načíst a poté stiskneme
tlačítko :item:`Načíst`. Po načtení dat se v mapovém okně objeví
vrstvy parcel (PAR) a budov (BUD). Pomocí nástroje může v datech
vyhledávat, postupovat podle listů vlastnictví a mnoho dalších funkcí.

.. figure:: images/vfk-plugin.png
   :class: large
   
   Ukázka využití VFK pluginu pro nalezení parcel s druhem pozemku
   zahrada.
