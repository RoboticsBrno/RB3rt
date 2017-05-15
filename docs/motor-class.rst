Motory
====================

Motory jsou jedna z nejzákladnějších komponent robota a proto s nimi začneme. 
Nejprve je potřeba vytvořit si instanci motorů: 

.. code-block:: cpp

   ev3cxx::Motor motor(ev3cxx::MotorPort::A, ev3cxx::MotorType::LARGE);


Vytvořili jsem si tedy instanci ``motor``, která je nastavena na port ``A`` a na typ ``LARGE``.

K dispozici máme všechny porty na *Bricku* : ``A``, ``B``, ``C`` a ``D``. 
U typů máme 3 volby, které odpovídají stejným blokům v originálním LEGO softwaru: ``UNREGULATED``, ``MEDIUM`` a ``LARGE``.

.. image:: images/lego-soft_motor-unregulated.png
   :width: 25%
.. image:: images/lego-soft_motor-medium.png
   :width: 25%
.. image:: images/lego-soft_motor-large.png
   :width: 25%

* Neregulované motory (``UNREGULATED``): u motorů se nastavuje jen výkon
* Regulované motory střední a velké (``MEDIUM`` a ``LARGE``): u motorů se nastavuje rychlost

Při inicializaci je potřeba se rozhodnout v jakém režimu budete chtít s motorem pracovat.


.. note:: 
    Pokud nebude řečeno jinak: 
    Při zadání parametru mimo rozsah se automaticky nastavuje maximální/minimální povolená hodnota. 
    Výchozí hodnoty funkcí odpovídají standardním hodnotám v LEGO Softwaru. 

    Příklad: 
        Rozsah povolených hodnot je v rozmezí od -100 do 100. 
        Při zadání hodnoty -101, dojde k ořezání na hodnotu -100
        Při zadání hodnoty 101, dojde k ořezání na hodnotu 100. 


Výkon a rychlost
*****************

.. note:: 
    Parametry při nastavování rychlosti a výkonu.

        * ``speed``: rychlost motoru při jízdě; rozsah od -100 do 100
        * ``brake``: brzdění; ``true`` - motor brzdí, ``false`` - motor lze volně protáčet

off() 
########

.. image:: images/lego-soft_motor-medium-off.png
   :height: 90px

.. code-block:: cpp
    
    void off(bool brake = true)

Funkce ``off()`` zastevuje motor. 
Nastavuje rychlost nebo výkon (v závislosti na daném režimu) na 0. 
Jako parametr se předává zda má motor zároveň brzdit (``true``) nebo se volně protáčet (``false``). 
Ve výchozím stavu brzdí (``false``). 


on()
########

.. image:: images/lego-soft_motor-medium.png
   :height: 90px

.. code-block:: cpp
    
    void on(int power = 50)

Funkce ``on()`` nastavuje rychlost motoru. 
Jako parametr se předává požadovaná rychlost v rozsahu -100 až 100.
Ve výchozím stavu je hodnota 50. 

Čas a otáčky
*************

.. note:: 
    Nové parametry při nastavování otáček.

        * ``speed``: rychlost motoru při běhu; rozsah od -100 do 100
        * ``time_ms``: čas v milisekundách, po který se bude motor točit; 
        * ``degrees``: počet stupňů, o které se má motor otočit; lze otáčet i o více než +- 360 stupňů
        * ``rotations``: počet otáček, které má motor udělat; lze zadávat i desetinná čísla
        * ``brake``: brzdění po otočení o daný počet stupňů; ``true`` - motor po dotočení brzdí, ``false`` - motor lze volně protáčet
        * ``blocking``:  když ``true`` - funkce blokuje další provádění programu, dokud nedokončí svůj úkol
        * ``wait_after_ms``:  parametr, který nastavuje čekání po před zahájením dané akce (jen v případě ``blocking = true``); nechte výchozí hodnotu 

onForSeconds()
################

.. image:: images/lego-soft_motor-medium-onForSeconds.png
   :height: 90px

.. code-block:: cpp
    
    void onForSeconds(int speed = 50, 
                      unsigned int time_ms = 1000, 
                      bool_t brake = true) 

Funkce ``onForSeconds()`` nastavuje čas, jak dlouho se má motor točit. 
Jako parametry se předávají: ``speed``, ``time_ms``, ``brake``. 


.. note:: LEGO pracuje se sekundami a desetinnými čísly, EV3CXX používá milisekundy a celá čísla

.. warning:: Funkce je vždy blokující. Další příkazy v programu se začnou vykonávat až funkce skončí.  


onForDegrees()
################

.. image:: images/lego-soft_motor-medium-onForDegrees.png
   :height: 90px

.. code-block:: cpp
    
    void onForDegrees(int speed = 50, 
                      int degrees = 360, 
                      bool_t brake = true, 
                      bool_t blocking = true, 
                      unsigned int wait_after_ms = 60)

Funkce ``onForDegrees()`` nastavuje počet stupňů, o které se má motor otočit. 
Jedna otáčka motoru odpovídá 360 stupňům. 
Jako parametry se předávají: ``speed``, ``degrees``, ``brake``, ``blocking``, ``wait_after_ms``. 

onForRotations()
##################

.. image:: images/lego-soft_motor-medium-onForRotations.png
   :height: 90px

.. code-block:: cpp
    
    void onForRotations(int speed = 50, 
                        float rotations = 1, 
                        bool_t brake = true, 
                        bool_t blocking = true, 
                        unsigned int wait_after_ms = 60)

Funkce ``onForRotations()`` nastavuje počet otáček, o které se má motor otočit. 
Jako parametry se předávají: ``speed``, ``rotations``, ``brake``, ``blocking``, ``wait_after_ms``. 


Dostupné funkce
**********************

Po vytvoření objektu ``motor`` lze na něm volat funkce:

* ``off()`` - vypne motory a začne brzit
* ``on()`` - nastaví rychlost na motorech
* ``onForSeconds()`` - jede po zadanou dobu
* ``onForDegrees()`` - otočí se o daný počet stupňů
* ``onForRotations()`` - otočí se o daný počet otáček
* ``degrees()`` - vrátí aktuální počet stupňů na motoru
* ``rotations()`` - vrátí aktuální počet otáček na motoru
* ``currentPower()`` - vrátí aktuální rychlost motoru
* ``resetPosition()`` - vyresetuje pozici motoru (ovlivní funkce ``degrees()`` a ``rotations()``)
* ``getType()`` - vrátí aktuálně nastavený port v systému EV3RT

