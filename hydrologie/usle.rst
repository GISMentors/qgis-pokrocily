.. |v.overlay.and| image:: ../hydrologie/images/and.png
   :width: 1em
.. |v.db.join| image:: ../images/gplugin/v.db.join.3.png
   :width: 3em
.. |v.db.update| image:: ../images/gplugin/v.db.update_op.2.png
   :width: 1.5em


2. Priemerná dlhodobá strata pôdy
=================================

Teoretické východiská
---------------------

Pri výpočtoch priemernej dlhodobej straty pôdy sa proces vodnej erózie
popisuje pomocou matematického modelu USLE, tzv. univerzálnej rovnice
straty pôdy:

.. _vzorec-G:

.. math::
   
   G = R \times K \times L \times S \times C \times P

Základné symboly
----------------

 * G - priemerná dlhodobá strata pôdy (:math:`t.ha^{-1} . rok^{-1}`)
 * R - faktor eróznej účinnosti dažďa (:math:`MJ.ha^{-1} .cm.h^{-1}`)
 * K - faktor erodovateľnosti pôdy (:math:`t.h.MJ^{-1} .cm^{-1} .rok^{-1}`) 
 * L - faktor dĺžky svahu (:math:`-`)
 * S - faktor sklonu svahu (:math:`-`)
 * C - faktor ochranného vplyvu vegetačného krytu (:math:`-`) 
 * P - faktor účinnosti protieróznych opatrení (:math:`-`) 
          
Vstupné dáta
------------

 * :map:`dmt.rst` - digitálny model terénu v rozlišení 10 x 10 m
 * :map:`hpj.shp` - vektorová vrstva hlavných pôdnych jednotiek (z kódov BPEJ),
 * :map:`kpp.shp` - vektorová vrstva komplexného prieskumu pôd,
 * :map:`landuse.shp` - vektorová vrstva využitia územia,
 * :map:`povodi.shp` - vektorová vrstva povodí IV. rádu s návrhovými
   zrážkami :math:`H_s` (doba opakovania 2, 5, 10, 20, 50 a 100 rokov)

 * :dbtable:`hpj_k` - číselník s kódom `K` pre hlavné pôdne jednotky,
 * :dbtable:`kpp_k` - číselník s kódom `K` pre pre vrstvu komplexného prieskumu pôd,
 * :dbtable:`lu_c` - číselník s kódom `C` pre vrstvu využitia územia
 * :map:`maska.pack` - oblasť riešeného územia bez líniových a plošných prvkov 
   prerušujúcich odtok
             
Navrhovaný postup
-----------------

1. zjednotenie hlavných pôdnych jednotiek a komplexného prieskumu pôd (:map:`hpj_kpp`)
2. pripojenie kódov `K` k vrstve :map:`hpj_kpp`
3. prienik vrstvy s kódmi `K` s vrstvou využitia územia (:map:`hpj_kpp_landuse`)
4. pripojenie kódov `C` k vrstve :map:`hpj_kpp_landuse`
5. výpočet parametra `KC`
6. vytvorenie rastrovej mapy sklonu a mapy akumulácií toku v každej bunke 
   (:map:`slope` a :map:`accu`)
7. výpočet parametra `LS`
8. výpočet parametra `G`
9. vytvorenie rastrových vrstiev :map:`g.rst`, :map:`g_m.rst` a :map:`ls_m.rst`
10. výpočet priemerných hodnôt `G` pre povodie s maskou a bez masky a vytvorenie rastrových vrstiev :map:`g_avg.rst` a :map:`g_avg_m.rst`

Na :num:`#schema-usle` je prehľadne znázornený navrhovaný postup. 

.. _schema-usle:

.. figure:: images/schema_usle.png
   :class: large

   Grafická schéma postupu 

Postup spracovania v QGIS
-------------------------

Znázornenie vstupných vektorových dát spolu s atribútovými tabuľkami je na ...

.. todo:: odkaz na scs-cn (vstupné 4 mapy, obr. 2 a 3.)

Digitálny model reliéfu a oblasť riešeného územia bez líniových a plošných 
prvkov prerušujúcich odtok (maska) je na :num:`#dmr-maska`. Tabuľky s kódmi `K` 
a kódmi `C` sú na :num:`#ciselniky`.

.. _dmr-maska:

.. figure:: images/x.png
   :class: middle

   Vrstva digitálneho modelu reliéfu a oblasť riešeného územia bez prvkov 
   prerušujúcich odtok.

.. _ciselniky:

.. figure:: images/ciselniky_usle.png
   :class: middle

   Číselníky s kódmi *K* a *C*. 

Krok 1
^^^^^^
1. zjednotenie hlavných pôdnych jednotiek a komplexného prieskumu pôd (:map:`hpj_kpp`)

Krok 2
^^^^^^
2. pripojenie kódov `K` k vrstve :map:`hpj_kpp`

.. _ciselniky:

.. figure:: images/usle_join.png
   :class: small

   Pripojenie číselníkov s faktorom *K* v prostredí QGIS. 

``CASE WHEN "hpj_K" IS NULL THEN "kpp_K" ELSE "hpj_K" END``

.. _ciselniky:

.. figure:: images/usle_kalk_k.png
   :class: small

   Vytvorenie atribútu s hodnotami faktora *K*.

.. _ciselniky:

.. figure:: images/usle_k.png
   :class: small

   Faktor *K* elementárnych plôch v záujmovom území. 

Krok 3
^^^^^^
3. prienik vrstvy s kódmi `K` s vrstvou využitia územia (:map:`hpj_kpp_landuse`)

|v.overlay.and| :sup:`v.overlay.and`

Krok 4
^^^^^^
4. pripojenie kódov `C` k vrstve :map:`hpj_kpp_landuse`, :num:`#usle-db-join-c`

|v.db.join| :sup:`v.db.join`

.. _usle-db-join-c:

.. figure:: images/usle_db_join_c.png
   :class: small

   Pripojenie hodnôt faktora `C` k elementárnym plochám. 

Krok 5
^^^^^^
5. výpočet parametra `KC`

Pre ďalšie výpočty je potrebné, aby typ atribútov s faktorom `K` a faktorom `C` 
bol číselný. 

Krok 6
^^^^^^
6. vytvorenie rastrovej mapy sklonu a mapy akumulácií toku v každej bunke 
   (:map:`slope` a :map:`accu`)

Krok 7
^^^^^^
7. výpočet parametra `LS`

Krok 8
^^^^^^
8. výpočet parametra `G`

Krok 9
^^^^^^
9. vytvorenie rastrových vrstiev :map:`g.rst`, :map:`g_m.rst` a :map:`ls_m.rst`

Krok 10
^^^^^^^
10. výpočet priemerných hodnôt `G` pre povodie s maskou a bez masky a vytvorenie rastrových vrstiev :map:`g_avg.rst` a :map:`g_avg_m.rst`


