Tank motory
====================

Pokud chceš řídit robota jako pásový vozidlo, můžeš využít třídu MotorTank

.. code-block:: cpp

   ev3cxx::MotorTank motors(ev3cxx::MotorPort::B, ev3cxx::MotorPort::C);


Vytvořili jsme si objekt ``motors``, kde levý motor je nastaven na port ``B`` a pravý na port ``C``. 
Tankový mód aktuálně podporuje jen ``LARGE`` motory. Ty se tedy nastavuji automaticky.

.. image:: images/lego-soft_motor-tank-on.png
   :height: 90px
   :align: center

.. note:: 
    Pokud nebude řečeno jinak: 
    Při zadání parametru mimo rozsah se automaticky nastavuje maximální/minimální povolená hodnota. 
    Výchozí hodnoty metod odpovídají standardním hodnotám v LEGO Softwaru. 

    Příklad: 
        Rozsah povolených hodnot je v rozmezí od -100 do 100. 
        Při zadání hodnoty -101, dojde k ořezání na hodnotu -100
        Při zadání hodnoty 101, dojde k ořezání na hodnotu 100. 


Výkon a rychlost
*****************

.. note:: 
    Parametry při nastavování rychlosti a výkonu.

        * ``left_speed``: rychlost levého motoru při jízdě; rozsah od -100 do 100
        * ``right_speed``: rychlost pravého motoru při jízdě; rozsah od -100 do 100
        * ``brake``: brzdění; ``true`` - motor brzdí, ``false`` - motor lze volně protáčet

off() 
########

.. image:: images/lego-soft_motor-tank-off.png
   :height: 90px

.. code-block:: cpp
    
    void off(bool brake = true)

Metoda ``off()`` zastavuje motory. Nastavuje rychlost nebo výkon (v závislosti na daném režimu) na 0. 
Jako parametr se předává zda mají být motory zabržděny (``true``) nebo se mají volně protáčet (``false``). 
Ve výchozím stavu brzdí (``true``). 

Použití: ``motors.off();``

on()
########

.. image:: images/lego-soft_motor-tank-on.png
   :height: 90px

.. code-block:: cpp
    
    void on(int left_speed = 50, int right_speed = 50)

Metoda ``on()`` nastavuje rychlost motorů. 
Jako parametry se předávají rychlosti motorů v rozsahu -100 až 100. 
Ve výchozím stavu jsou ``left_speed`` a ``right_speed`` rovny hodnotě 50.

Použití: ``motors.on(50, 50);``

Čas a otáčky
*************

.. note:: 
    Nové parametry při nastavování otáček.

        * ``left_speed``: rychlost levého motoru při jízdě; rozsah od -100 do 100
        * ``right_speed``: rychlost pravého motoru při jízdě; rozsah od -100 do 100
        * ``time_ms``: čas v milisekundách, po který se budou motory točit; 
        * ``degrees``: počet stupňů, o které se má motor otočit; lze otáčet i o více než +- 360 stupňů
        * ``rotations``: počet otáček, které má motor udělat; lze zadávat i desetinná čísla
        * ``brake``: brzdění po otočení o daný počet stupňů; ``true`` - motor po dotočení brzdí, ``false`` - motor lze volně protáčet
        * ``blocking``:  když ``true`` - metoda blokuje další provádění programu, dokud nedokončí svůj úkol
        * ``wait_after_ms``:  parametr, který nastavuje čekání po před zahájením dané akce (jen v případě ``blocking = true``); nechte výchozí hodnotu 

onForSeconds()
################

.. image:: images/lego-soft_motor-tank-onForSeconds.png
   :height: 90px

.. code-block:: cpp
    
    void onForSeconds(int left_speed = 50, 
                      int right_speed = 50,
                      unsigned int time_ms = 1000, 
                      bool brake = true) 

Metoda ``onForSeconds()`` nastavuje čas, jak dlouho se mají motory točit. 
Jako parametry se předávají: ``left_speed``, ``right_speed``, ``time_ms``, ``brake``. 

Použití: ``motors.onForSeconds(50, 50, 1000);``

.. note:: LEGO Software pracuje se sekundami a desetinnými čísly, EV3CXX používá milisekundy a celá čísla

.. warning:: Metoda je vždy blokující. Další příkazy v programu se začnou vykonávat až metoda skončí.  


onForDegrees()
################

.. image:: images/lego-soft_motor-tank-onForDegrees.png
   :height: 90px

.. code-block:: cpp
    
    void onForDegrees(int left_speed = 50, 
                      int right_speed = 50, 
                      int degrees = 360, 
                      bool brake = true, 
                      bool blocking = true, 
                      unsigned int wait_after_ms = 60)

Metoda ``onForDegrees()`` nastavuje počet stupňů, o které se mají motory otočit. 
Jedna otáčka motoru odpovídá 360 stupňům. 
Jako parametry se předávají: ``left_speed``, ``right_speed``, ``degrees``, ``brake``, ``blocking``, ``wait_after_ms``. 

Použití: ``motors.onForDegrees(50, 50, 360);``

onForRotations()
##################

.. image:: images/lego-soft_motor-tank-onForRotations.png
   :height: 90px

.. code-block:: cpp
    
    void onForRotations(int left_speed = 50, 
                        int right_speed = 50 
                        float rotations = 1, 
                        bool brake = true, 
                        bool blocking = true, 
                        unsigned int wait_after_ms = 60)

Metoda ``onForRotations()`` nastavuje počet otáček, o které se mají motory otočit. 
Jako parametry se předávají: ``left_speed``, ``right_speed``, ``rotations``, ``brake``, ``blocking``, ``wait_after_ms``. 

Použití: ``motors.onForDegrees(50, 50, 1);``

leftMotor() a rightMotor()
##########################

.. code-block:: cpp
    
    Motor& rightMotor();

Přes tyto metody, lze ovládat jen jeden motor z páru. 
Nemusíte si tedy vytvářet nový objekt, pokud budete chtít v určitých situacích ovládat jen jeden motor.
Metoda ``leftMotor()`` vrací instanci motoru, který byl při vytvoření objektu předán jako první, ``rightMotor()`` vrací druhý motor v pořadí.

Metody vrací instanci daného motoru a následně nad ní lze volat všechny metody dostupné ve třídě ``Motor``.


Použití: ``motors.rightMotor().onForDegrees(50, 1);``

Dostupné metody
**********************

Po vytvoření objektu ``motor`` lze na něm volat metody:

* ``off()`` - vypne motory a začne brzdit
* ``on()`` - nastaví rychlost na motorech
* ``onForSeconds()`` - jede po zadanou dobu
* ``onForDegrees()`` - otočí se o daný počet stupňů
* ``onForRotations()`` - otočí se o daný počet otáček
* ``leftMotor()`` - vrátí instanci levého motoru
* ``rightMotor()`` - vrátí instanci pravého motoru
