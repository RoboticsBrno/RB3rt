Motory
====================

Motory jsou jedna z nejzákladnějších komponent robota a proto s nimi začneme.

.. code-block:: cpp
   :linenos:

   ev3cxx::Motor motor(ev3cxx::MotorPort::A, ev3cxx::MotorType::LARGE);
   
Nejprve je potřeba vytvořit si instanci motorů: 


.. literalinclude:: excode/motor-init.cpp
   :language: cpp

Vytvořil se objekt ``motor``, který je nastaven na port ``A`` a na typ ``LARGE``.

.. |logo| image:: images/Advanced_Palette_UnregulatedMotor_1.png


.. table:: Truth table for "not"
   :align : center
+---------+---------+
| |logo|  | |logo|  |
+---------+---------+



.. |logo1| image:: images/lego-soft_motor-unregulated.png

.. |logo2| image:: images/lego-soft_motor-regulated.png


.. table:: Truth table for "not"
   :align : center
+---------+---------+
| |logo1| | |logo2| |
+---------+---------+


Pokus na druho

.. table:: Truth table for "not"
   :widths: auto
   :align : center

   =====  =====
     A    not A
   =====  =====
   False  True
   True   False
   =====  =====



.. figure:: images/Advanced_Palette_UnregulatedMotor_1.png
   :width: 25%
.. figure:: images/Action_Palette_LargeMotor_On.png
   :width: 25%

LEGO poskytuje dva způsoby obsluhy motorů. 
Lze řídit čistě výkon motorů (neregulované/modré motory v LEGO Softwaru) a nebo můžete nastavovat rychlost (zelené motory).

.. image:: images/lego-soft_motor-unregulated.png
   :width: 25%
   :align: right
.. image:: images/lego-soft_motor-regulated.png
   :width: 25%
   :align: left

Po vytvoření objektu ``motor`` na něm lze volat funkce. Pro nastavení neregulovaného motoru je potřeba zavolat na objekt funkci ``unregulated(int power)``.

.. code-block:: cpp

   motor.unregulated(50);

.. image:: images/lego-soft_motor-unregulated.png
   :width: 25%
.. image:: images/lego-soft_motor-regulated.png
   :width: 25%

Test



Po vytvoření objektu ``motor`` na něm lze volat funkce. Pro nastavení neregulovaného motoru je potřeba zavolat na objekt funkci ``unregulated(int power)``.

.. image:: images/lego-soft_motor-unregulated.png
   :width: 25%
   :align: center
.. image:: images/lego-soft_motor-regulated.png
   :width: 25%
   :align: center


Pokus

