.. |box_yes| image:: ../images/icon/checkbox.png
   :width: 1.5em
.. |npicon| image:: ../images/icon/np_plugin_icon.png
   :width: 1.5em


Vytvorenie zásuvného modulu
---------------------------

Zásuvné moduly, tzv. :wikipedia:`pluginy <https://en.wikipedia.org/wiki/Plug-in_(computing)>` predstavujú doplnkové moduly a ich úlohou je 
rozširovať funkčnosť a širokú škálu použitia QGIS. Úvod a predstavenie tejto 
problematiky je súčasťou Školenia pre začiatočníkov ako kapitola QGIS pluginy, 
kde sa okrem iného píše, že v súčasnosti existuje pre QGIS viac než 300 
zásuvných modulov napísaných v programovacom jazyku `Python 
<https://www.python.org/>`_ alebo `C++ <https://isocpp.org/>`_.


V mnohých prípadoch však môže nastať situácia, kedy ani jeden z existujúcich 
zásuvných modulov nespĺňa funkcionalitu akú by sme práve potrebovali. 
Úroveň rozširovania funkcionality QGIS sa líši. Za pomoci jazyka Python môže 
ísť o pridanie jednoduchého tlačidla až po tvorbu sofistikovaných nástrojov.
V nasledujúcej časti načrtneme návod ako si vlastný plugin vytvoriť 
a postup následne odskúšame na jednoduchom reálnom príklade. Vytvoríme zásuvný 
modul s názvom *Save Views*, ktorý exportuje grafický výstup vo forme `*.png` 
pre každý prvok vo vybranej vektorovej vrstve do zvoleného adresára. 

Potrebné nástroje
=================

I. Qt Creator
^^^^^^^^^^^^^

Pri tvorbe nového pluginu budeme potrebovať `Qt Creator <https://wiki.qt.io/Category:Tools::QtCreator>`_, čo je aplikácia vývojového framework-u s názvom **Qt**. 
Túto aplikáciu využijeme pri tvorbe užívateľského rozhrania nového modulu. 

II. Python 'bindings' pre Qt
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Vzhľadom k tomu, že budeme vyvíjať plugin v programovacom jazyku Python, musíme
nainštalovať niečo ako *python väzby pre Qt*. Pre tvorbu zásuvných modulov je 
potrebný ``pyrcc4``. Spôsob inštalácie sa v tomto 
prípade líši od platformy.
Na Windows možno stiahnuť inštalátor 
`OSGeo4W <http://trac.osgeo.org/osgeo4w/>`_, vybrať *Express Desktop* inštalátor 
a nainštalovať balík **QGIS**. Po inštalácii je nástroj `pyrcc4` prístupný cez 
*OSGeo4W Shell*.
Pre Mac OS je potrebné nainštalovať `Homebrew <http://brew.sh>`_ správcu balíčkov
a nainštalovať **PyQt** balíček. 
V prípade Linux-u je dôležitý **python-qt4** balíček. Pre Ubuntu ho dostaneme 
spustením príkazu ``sudo apt-get install python-qt4`` v príkazovom riadku.

III. Textový editor
^^^^^^^^^^^^^^^^^^^

Správny textový editor alebo integrované vývojové prostredie (IDE) sú dôležité 
pri písaní kódu. Medzi obľúbené editory patria 
napríklad *Sublime Text, Vim, Emacs, Notepad++, TextWrangler, IDLE, Atom, 
Aquamacs, GNU Nano, Kate, gedit* a podobne.

IV. Zásuvný modul Plugin Builder
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Tento veľmi užitočný zásuvný modul nám vytvorí všetky potrebné súbory a 
štandardnú podobu kódu pre budúci plugin. Nainštalujeme ho klasickým spôsobom
pomocou správcu zásuvných modulov, viď. 
`Správca zásuvných modulov <http://training.gismentors.eu/qgis-zacatecnik/ruzne/qgis_pluginy.html#spravce-zasuvnych-modulu>`_

V. Zásuvný modul Reloader plugin
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Vďaka tomuto pluginu nemusíme pri každej zmene kódu reštartovať QGIS. Zmeny sa
prejavia po jeho spustení.

Päť základných krokov pre vytvorenie pluginu Save Views
======================================================

:ref:`1.<krok1>` 
Spustenie zásuvného modulu *Plugin Builder* a vyplnenie dialógu

:ref:`2.<krok2>` 
Kompilácia súboru *.qrc príkazom `make` (vlastne spustenie pyrcc4)

:ref:`3.<krok3>` 
Načítanie nového pluginu v správcovi zásuvných modulov

:ref:`4.<krok4>` 
Vytvorenie užívateľského rozhrania pomocou Qt Creator

:ref:`5.<krok5>` 
Pridanie logiky pomocou python kódu a ďalšie úpravy

.. _krok1:

1. Spustenie zásuvného modulu *Plugin Builder* a vyplnenie dialógu
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Po spustení zásuvného modulu na tvorbu pluginov sa objaví dialógové okno, kde 
zadáme základné údaje o našom novom plugine, viď. :num:`#plugin-builder`.
Potom prejdeme tlačidlom `Next` na ďalšie okno, kde vyplníme bližšie informácie
*About*. V tretej časti definojeme template ako `Tool button with dialog`,
zadáme text, ktorý sa bude zobrazovať v menu a nakoniec vyberieme, pod ktorou
položkou v menu náš nový plugin používateľ nájde, napríklad `Vector`.
V ďalších intuitívnych krokoch je možné ovplyvniť vytvorenie niektorých súborov, 
vyplniť povinné a odporúčané informácie napríklad o domovskej stránke, 
repozitári modulu, označiť plugin ako experimentálny a podobne.

Následne sa objaví okno, kde je potrebné zadať cestu, kde bude adresár so 
všetkými súbormi uložený (:num:`#plugin-dir`). Treba nájsť adresár `.qgis2/python/plugins`. Jeho 
umiestnenie sa líši od platformy. 

.. _plugin-builder:

.. figure:: images/np_plugin_builder.png
   :class: small

   Dialógové okno zásuvného modulu na tvorbu pluginov.

.. _plugin-dir:

.. figure:: images/np_plugin_dir.png
   :class: small

   Adresár obsahujúci všetky nainštalované zásuvné moduly QGIS.

Po tomto kroku dostaneme potvrdzujúci dialóg, tzv. `Plugin Builder Results`
so súhrnom rôznych informácií.

.. _krok2:

2. Kompilácia
^^^^^^^^^^^^^

V termináli prejdeme do adresára, kde bol plugin SaveViews vytvorený,
napríklad pre Linux pomocou ``cd .qgis2/python/plugins/SaveViews/`` a spustíme
``make``. Tento príkaz vlastne spustí vyššie spomenutý `pyrcc4`.

.. _krok3:

3. Načítanie nového pluginu v správcovi zásuvných modulov
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Po reštarte QGIS je v :menuselection:`Plugins --> Manage and Install plugins`
viditeľný aj plugin *Save Views*. Zaškrtnutím |box_yes| sa jeho ikona 
|npicon| objaví v hlavnej lište a ako sme zadali, nájdeme ho aj pod
položkou `Vector` (:num:`#plugin-menu`).

.. _plugin-menu:

.. figure:: images/np_plugin_menu.png
   :class: small

   Nový plugin dostupný pod položkou *Vector*.

Spustením otvoríme okno, ktoré obsahuje tlačidlá `Cancel` a `OK` 
(:num:`#plugin-dlg`). 

.. _plugin-dlg:

.. figure:: images/np_plugin_dlg.png
   :class: small

   Dialógové okno modulu *Save Views* po prvom spustení.

.. tip::

	V tejto fáze je dobré premyslieť si, akú funkcionalitu by plugin mal 
	a nemal mať, aký bude typ vstupných dát a podobne. Jednoducho je 
	potrebné plugin priebežne počas vývoja testovať.

Vytvoríme si jednoduchý projekt v QGIS, ktorý bude obsahovať pár vektorových 
vrstiev. Na :num:`#np-project` sú zobrazené napríklad požiarne stanice, 
železnice, kraje Českej republiky, veľkoplošné územia a štátna hranica. 

.. _np-project:

.. figure:: images/np_project.png
   :class: middle

   Príklad projektu s vektorovými vrstvami v QGIS.

.. _krok4:

4. Vytvorenie užívateľského rozhrania pomocou *Qt Creator*
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Vzhľad a elementy dialógového okna pluginu vieme customizovať vďaka aplikácii
Qt Creator. V hlavnej lište prejdeme na :menuselection:`File --> Open File or Project` a otvoríme súbor `*.ui`, v našom prípade `save_views_dialog_base.ui`, ktorý 
nájdeme v adresári vytváraného pluginu. Na :num:`#qtcreator` je znázornené
zatiaľ prázdne okno s objektami `SaveViewsDialogBase` a `button_box`. Spôsobom 
`drag-and-drop` je možné z ľavého panelu pridávať ďalšie objekty a ich názvy 
a vlastnosti meniť v pravej časti okna aplikácie *Qt Creator*.

.. _qtcreator:

.. figure:: images/np_qt_creator.png
   :class: middle

   Dialógové okno vytváraného pluginu v prostredí aplikácie *Qt Creator*.

Prvé dva objekty, ktoré pridáme budú tzv. *Combo Box* z kategórie *Input Widgets*
a tzv. *Label* z kategórie *Display Widgets*. V pravom paneli predvolený text 
objektu *label* zmeníme na `Select a layer` (:num:`#qtlabel`). 

.. _qtlabel:

.. figure:: images/np_qt_label.png
   :class: middle

   Editácia objektov dialógového okna.

Po uložení súboru `*.ui` cez :menuselection:`File --> Save "save_views_dialog_base.ui"` prejdeme do prostredia QGIS, kde použijeme plugin *Plugin Reloader*. V 
`Configure Plugin reloader` nastavíme `SaveViews` (:num:`#qt-plugin-reloader`) 
a plugin spustíme. Po kliknutí na ikonu `Save Views` sa otvorí okno totožné 
s návrhom na :num:`#qtlabel`.

.. _qt-plugin-reloader:

.. figure:: images/np_plugin_reloader.png
   :class: small

   Konfigurácia zásuvného modulu *Plugin Reloader*.

.. _krok5:

5. Pridanie logiky pomocou python kódu a ďalšie úpravy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Povedzme, že chceme, aby sa po spustení pluginu *Combo Box* automaticky naplnil 
vektorovými vrstvami aktuálneho projektu. Hlavným súborom, ktorý sa stará 
o logiku jednotlivých objektov je python kód, v našom prípade súbor 
`save_views.py`. Otvoríme ho v textovom editore a nájdeme metódu `run(self)`.
Táto metóda je spustená pri každom štarte pluginu. Pod jej prvý riadok 
(:num:`#np-run-method`) umiestnime nasledujúci kód. 

.. code::

	# populate the Combo Box with the layers loaded in QGIS
        self.dlg.comboBox.clear()
        layers = self.iface.legendInterface().layers()
        layer_list = []
        for layer in layers:
            layer_list.append(layer.name())
        self.dlg.comboBox.addItems(layer_list)

.. _np-run-method:

.. figure:: images/np_run_method.png
   :class: middle

   Editácia python súboru s cieľom naplniť *Combo Box* vektorovými vrstvami.

Na :num:`#np-cb-filled` je vidieť, že po novom spustení *Save Views* sa 
zmeny prejavia.

.. _np-cb-filled:

.. figure:: images/np_cb_filled.png
   :class: small

   Vzhľad dialógového okna po zmenách v python kóde.




 


