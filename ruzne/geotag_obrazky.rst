.. |mActionAddRasterLayer| image:: ../images/icon/mActionAddRasterLayer.png
   :width: 1.5em


Obrazová data jako součást vektorů 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Možnost různě kombinovat různá data je čím dál víc dostupná. Jedním z běžných
požadavků se stává možnost přiřadit obrázek k vektorovým datům jako jakýkoli
jiný atribut. Způsobů jak naložit s takovým požadavkem je vícero. Jednou z
možností je mít atribut, ve kterém je zapsán název souboru, který k jednotlivým
záznamům patří. To umožňuje jednoznčné přiřazení obrázku k záznamu. Pokud je ale
obrázek zdrojem informací a chceme ho vidět, tak ho pak musíme otevřít 
samostatně v prohlížeči obrázků. 
QGIS však nabízí možnost zobrazit přímo v detailu jendotlivého prvku. Jednotlivé
kroky pro nastavení jsou popsány níže.

Využití
=======
Příkladem využití je pořizování geotagovaných fotografií (fotka s určeným místem
jejího pořízení). V současné době je možné dělat takovéto záznamy i s běžnými
mobilními telefony (je však nutné brát v potaz přesnost určení polohy).
Proces zpracování pak pozůstává z načtení dat jako vektorové vrstvy a nastavení
zobrazování daného obrázku jako atributu. Kompletní postup je rozepsán níže.

1. Vstupní obrazová data:
=========================

Pro práci s geotagovanými fotkami je nutné mít nainstalovaný
`ExifTool <http://www.sno.phy.queensu.ca/~phil/exiftool/>`_ který nám umožňuje 
s nimi pracovat.

Instalace na *Linux* je možná pomocí instalačníko balíčku. Pro instalaci na 
*Windows* je nutné stáhnout příslušnou složku (spouští se pomocí `.exe` 
souboru).

.. notecmd:: Instalace ExifTool
   
   .. code-block:: bash

      sudo apt-get install exiftool

.. tip::
  
   Pokud si chcete prohlédnout informace vztažené k danému obrázku, tak obrázek
   jednoduše otevřete v *ExifTool*. 
   Ve *Windows* tak udělále pomocí drag-and-drop v Linuxu například pomocí 
   příkazu :map:`exiftool -a gps:nazev_obrazku.jpg`. 
   Na obrázku :num:`exif-data` je vidět přehled ecidovaných informací.

  .. _exif-data:
   
  .. figure:: images/exif_data.png
     :class: small

     Příklad vypsaných informací u geotagované fotky 'ukazkova.jpg'.


2. instalace pluginu 
====================

Pro možnost tvorby vektorové vrstvy z geotagovaných fotek využijeme plugin
`Geotag and import photos <https://hub.qgis.org/projects/geotagphotos/wiki>`_.
Tento nainstalujeme standardní cestou přes :menuselection:`Zásuvné moduly -->
Spravovat a instalovat zásuvné moduly...`. Potřebný modul je pouze
experimentální, proto musíte být povolené zobrazování experimentálních modulů.

Po instalaci se modul nachází v :menuselection:`Vektor -->Geotag and import
photos` (:num:`menu-geotag`).

.. _menu-geotag:

.. figure:: images/geotag_menu.png
   :class: small

   Umístění nástrojú přidaného pluginu v menu QGIS.

.. note::
   
   Pro práci na na OS Windows je nutné nastavit cestu k ExifTool souboru v 
   :menuselection:`Vetkor --> Geotag and import photos --> Settings`. Na OS
   Linux toto není potřebné.

   #TODO: přidat obrázek z WIN

3. import fotek do vektorové vrstvy
===================================

4. vykreslování obrázku v detailu prvku
=======================================



