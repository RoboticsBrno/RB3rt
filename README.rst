Dokumentace k EV3RT C++ API
=============================
EV3RT C++ API vzniklo jako C++ nástavba EV3RT C API (ev3api), které je standardní součástí systému EV3RT_. 

Systém EV3RT je port japonského real-time operačního systém `TOPPERS/HRP2 <http://www.toppers.jp/hrp2-kernel.html>`_ pro stavebnici `LEGO MINDSTORMS EV3 <https://www.lego.com/cs-cz/mindstorms/about-ev3>`_. 

Mezi hlavní přednosti systému EV3RT patří:
 * malá velikost systému (do 5 MB) i uživatelských aplikací (do 1 MB)
 * velmi rychlý start (do 5 sekund) a prakticky okamžité vypnutí
 * jednodušší úprava a doprogramování vlastních funkcí do jádra systému
 * podpora dynamické alokace paměti
 * preemptivní multitasking a rychlé přepínání tasků (do 8 μs)
 * multiplatformní

Hlavním cílem EV3RT C++ API je umožnit jednoduchý přechod uživatelům zvyklým na standardní LEGO vývojové prostředí (`LEGO MINDSTORMS EV3 Software <https://www.lego.com/cs-cz/mindstorms/downloads/download-software>`_) Proto jim je celé API přizpůsobeno a většina funkcí se jmenuje a chová stejně jako v originální vývojovém prostředí.


Kontakt
-------

S jakýmikoliv dotazy se obracejte na: paral.jarek@gmail.com 

Licence
-------

Tato dokumentace je pod `CC BY-SA 4.0`__

.. _CC : https://creativecommons.org/licenses/by-sa/4.0/#

__ CC_
