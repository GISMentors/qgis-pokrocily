.. |vfkPlugin| image:: images/vfkPluginIcon.png
   :width: 1.5em

VFK a RÚIAN
-----------

Tato kapitola pojednává o možnosti pracovat s českými výměnnými
formáty **VFK** (:ref:`Výměnný formát katastru <vfk>`) a **VFR**
(:ref:`Výměnný formát RÚIAN <vfr>`) v prostředí QGIS.

.. _vfk:

Výměnný formát katastru (VFK)
=============================

Výměnný formát (VF) je určen k vzájemnému předávání dat mezi systémem
ISKN a jinými systémy zpracování dat, viz `dokumentace formátu
<http://www.cuzk.cz/Katastr-nemovitosti/Poskytovani-udaju-z-KN/Vymenny-format-KN/Vymenny-format-ISKN-v-textovem-tvaru/Popis_VF_ISKN-v5_1-1-%281%29.aspx>`_.

.. note::
   
   Formát VFK podporuje knihovna GDAL (tuto knihovnu používá QGIS pro
   čtení řady datových formátu včetně formátu VFK) od verze 1.7. Více
   o podpoře formátu VFK v knihovně GDAL `na portálu FreeGIS
   <http://freegis.fsv.cvut.cz/gwiki/VFK_/_GDAL>`_. Pro práci nicméně
   doporučujeme minimálně verzi knihovny GDAL 1.11, ideálně potom GDAL
   2.0 (GDAL 1.11 `nepodporuje křivky
   <http://freegis.fsv.cvut.cz/gwiki/VFK_/_GDAL#K.C5.99ivky.2C_kru.C5.BEnice.2C_kruhov.C3.A9_oblouky>`_,
   což je vzhledem k tomu, že hranice parcel mohou být tvořeny
   kružnicemi či kruhovými oblouky problém. Verzi knihovny GDAL můžete
   zjistit z menu :menuselection:`Nápověda --> O programu`.

   .. figure:: images/vfk-qgis-verze.png

Data ve formátu VFK můžete načíst jako každá jiná vektorová souborová
data. Po načtení dat se objeví dialog pro výběr vrstev, které
odpovídají jednotlivým datovým blokům VFK. Některé mají definovánu
geometrii (např. BUD, PAR, HP a další), jiné obsahují pouze popisné
informace.

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
informace spojovat. To nicméně vyžaduje znalosti vnitřní struktury
formátu VFK. Proto vznikl specializovaný zásuvný modul tzv. **VFK
plugin**, který  pro práci s katastrálními daty výrazně usnadňuje.

.. figure:: images/vfk-join.png
   :class: small
        
   Příklad připojení tabulky druh pozemku (DRUPOZ) k atributové
   tabulce parcel (PAR) ve vlastnostech vrstvy a záložce Připojení.

Po připojení popisných informací můžeme provádět dotazy typu vyhledání
parcel podle druhu pozemku.
   
.. figure:: images/vfk-join-query.png

   Nalezení parcel, které mají druh pozemku chmelnice.

VFK plugin
^^^^^^^^^^

Mnohem větší komfort při práci s daty ve formátu VFK umožňuje v QGISu
specializovaný **VFK plugin**.

.. note:: Tento zásuvný modul byl vyvinut v roce 2011 studenty oboru
          Geoinformatika na ČVUT v Praze, fakulty stavební. Kód byl
          napsán v programovacím jazyku C++, což výrazně stěžovalo
          instalaci pluginu, která nebyla možná standardní
          cestou. Proto byl v roce 2015 a 2016 kód zásuvného modulu
          přepsán do jazyka Python a v něj je i dále vyvíjen. Více
          informací o zásuvném modulu najdete na stránkách `portálu
          FreeGIS
          <http://freegis.fsv.cvut.cz/gwiki/VFK_/_QGIS_plugin>`_.

Instalace
~~~~~~~~~

V současné době není VFK plugin součástí oficiálního repositáře
QGISu. Pro jeho instalaci je nutné do QGISu zaregistrovat nový
repositář, který je dostupný na adrese
*http://geo.fsv.cvut.cz/osgeorel/qgis-plugins.xml*.

V dialogu :menuselection:`Zásuvné moduly --> Spravovat a instalovat
zásuvné moduly` přidáme nový repositář a aktivuje experimentální
moduly.

.. figure:: images/vfk-repo-pridat.png

   Pro instalaci VFK pluginu je nutné aktivovat experimentální zásuvné
   moduly a přidat nový repositář.

.. figure:: images/vfk-repo.png
   :class: small
        
   V dialogu definujeme název a URL 
   http://geo.fsv.cvut.cz/osgeorel/qgis-plugins.xml.

.. figure:: images/vfk-repo-instalace.png

   Poté se již VFK plugin zobrazí v seznamu zásuvných modulů a můžeme
   jej nainstalovat.

Po instalaci se přidá do menu :menuselection:`Zásuvné moduly --> VFK`
a do nástrojové lišty ikonka |vfkPlugin|. Zásuvný modul otevřeme
pomocí této ikonky anebo z menu :menuselection:`Zásuvné moduly --> VFK
--> Otevřít prohlížeč VFK`.

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
   :class: middle
   
   Ukázka využití VFK pluginu pro nalezení parcel s druhem pozemku
   zahrada.

.. _vfr:

Výměnný formát RÚIAN (VFR)
==========================

:wikipedia:`RÚIAN` (Registr Územní Identifikace, Adres a Nemovitostí)
patří do systému základních registrů. Poskytuje údaje o základních
územních prvcích jako jsou území státu, katastr, parcela, nemovitost a
další. Více informací `zde <http://www.ruian.cz>`_.

Data jsou poskytována ve *výměnném formátu RÚIAN* (VFR) službou
`Veřejného dálkového přístupu <http://vdp.cuzk.cz>`_.

Datový formát VFR je podporován knihovnou GDAL od verze 1.11. Vzhledem
k tomu je můžeme načíst do QGISu jako každá jiná vektorová souborová
data.

.. important:: Formát VFR definuje více geometrických reprezentací na
               prvek, typicky definiční bod, originální a
               generalizovanou hranici. QGIS je v současnosti (2.14)
               schopen zobrazit pouze první geometrii (tj. většinou
               pouze definiční bod), přestože je knihovna GDAL schopná
               tyto data číst korektně. Viz porovnání dotazu na data
               pomocí konzolového nástroje *ogrinfo* a QGISu.

               .. code-block:: bash
                   
                  ogrinfo 20160331_OB_564567_UKSH.xml.gz Parcely -so

                  ...
                  Layer name: Parcely
                  Geometry (DefinicniBod): Point
                  Geometry (OriginalniHranice): Polygon
                  ...

               .. figure:: images/vfr-vrstvy.png

                  Seznam vrstev při načtení v QGISu. U parcel je možné
                  načíst pouze definiční body.

Limit QGISu je možné obejít pomocí konverze dat VFR do vhodného
formátu a výběru preferované geometrie. Tuto konverzi můžeme provést
konzolovými konverzními nástroji *vfr2ogr*. Výhoda těchto nástrojů je,
že kromě jednotlivých vstupních VFR souborů můžeme použít seznam linků
stažitelný z `VDP <http://vdp.cuzk.cz>`_. V tomto případě budou VFR
data nástrojem *vfr2ogr* automaticky stažena a naimportována do
cílového formátu. Jako cílový formát doporučujeme
:wikipedia-en:`SpatiaLite` anebo :wikipedia:`PostGIS`.

.. note:: Konverzní nástroje *vfr2ogr* najdete na serveru GitHub, viz
          `stránka s verzemi
          <https://github.com/ctu-osgeorel/gdal-vfr/releases>`_ ke
          stažení.

Jako příklad si ukážeme stažení dat pro OPR Litoměřice a konverzi dat
do databáze SQLite.

.. figure:: images/vfr-vdp-ltm.png
   :class: middle
        
   Na portálu VDP vybereme ORP Litoměřice a stáhneme seznam linků.

Seznam linků z VDP použijeme jako vstup pro nástroj *vfr2ogr*.

.. note:: Seznam z VDP obsahuje data za poslední tři měsíce. Před
          importem vybereme pouze ty nejaktuálnější, např. pomocí
          unixového nástroje *grep*.

          .. code-block:: bash

             grep '20160131' seznamlinku.txt > seznamlinku-aktualni.txt
          
.. code-block:: bash

   vfr2ogr --file seznamlinku-aktualni.txt --format SQLite --dsn ruian_ltm.db --geom OriginalniHranice

.. note:: Jako vstupní soubor do nástroje můžete použít přímo data ve
          formátu VFR. Potom se provede import pouze zvoleného
          souboru.

          .. code-block:: bash
      
             vfr2ogr --file data/20160131_OB_530506_UKSH.xml.gz --format SQLite --dsn ruian_obec.db --geom OriginalniHranice 
                
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
