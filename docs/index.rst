.. Read the Docs Template documentation master file, created by
   sphinx-quickstart on Tue Aug 26 14:19:49 2014.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Dokumentace k EV3RT C++ API!
==================================================

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

.. image:: images/lego-soft_project.png
    :align: center
    :alt: LEGO MINDSTORMS EV3 originální software
    
    
.. _EV3RT: http://ev3rt-git.github.io/


Contents:

.. toctree::
   :maxdepth: 2
   :glob:

   ev3cxx_motor-class
   ev3cxx_motor-tank-class
   ev3cxx_sensor-class
   ev3cxx_brick-class
   ev3cxx_time-class
   ev3cxx_file-bt
   Robotutoriál <ev3cxx_robotutorial/index>
   Instalace vývojového prostředí <rb3rt-install/index>
   faq
   *



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

