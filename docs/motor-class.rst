Motory
====================

Motory jsou jedna z nejzákladnějších komponent robota a proto s nimi začneme. 
Nejprve je potřeba vytvořit si instanci motorů: 

.. code-block:: cpp

   ev3cxx::Motor motor(ev3cxx::MotorPort::A, ev3cxx::MotorType::LARGE);


Vytvořili jsem si tedy isntaci ``motor``, která je nastavena na port ``A`` a na typ ``LARGE``.

K dispozici máme všechny porty na *Bricku* : ``A``, ``B``, ``C`` a ``D``. 
U typů máme 3 volby, které odpovidají stejným blokům v originálním LEGO softwaru: ``UNREGULATED``, ``MEDIUM`` a ``LARGE``.

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
    Defaultní hodnoty odpovídají standardním hodnotám v LEGO Softwaru. 

    Příklad: 
        Rozsah povolených hodnot je v rozmezí od -100 do 100. 
        Při zadání hodnoty -101, dojde k ořezání na hodnotu -100
        Při zadání hodnoty 101, dojde k ořezání na hodnotu 100. 


Výkon a rychlost
*****

.. note:: 
    Parametry při nastavování rychlosti a výkonu.

        * ``speed``: rychlost motoru při jízdě; rozsah od -100 do 100
        * ``brake``: brždění; ``true`` - motor brzdí, ``false`` - motor lze volně protáčet

off() 
########

.. image:: images/lego-soft_motor-medium-off.png
   :width: 50%

.. code-block:: cpp
    
    void off(bool brake = true)

Funkce ``off(bool brake = true)`` zastevuje motor. Nastavuje rychlost nebo výkon (v závislosti na daném režimu) na 0. Jako paremetr se předává zda má motor zároveň brzdit (``true``) nebo se volně protáčet (``false``). Defaultně brzdí (``false``). 


on()
########

.. image:: images/lego-soft_motor-medium.png
   :width: 50%

.. code-block:: cpp
    
    void on(int power = 50)

Funkce ``on(int power = 50)`` nastavuje rychlost motoru. Jako paremetr se předává požadovaná rychlost v rozsahu -100 až 100. Při zadání čísla mimo rozsah je nastavena maximální/minimální povolená hodnota (-101 => -100; 101 => 100). Defaultně hodnota je 50. 

Otáčky
*****

.. note:: 
    Nové parametry při nastavování otáček.

        * ``speed``: rychlost motoru při otáčení o daný počet stupňů; rozsah od -100 do 100
        * ``degrees``: počet stupňů, o které se má motor otočit; rozsah od  -2 147 483 648 do 2 147 483 647
        * ``brake``: brždění po otočení o daný počet stupňů; ``true`` - motor po dotočení brzí, ``false`` - motor lze volně protáčet
        * ``blocking``: brždění po otočení o daný počet stupňů; ``true`` - motor po dotočení brzí, ``false`` - motor lze v

onForDegrees()
########

.. image:: images/lego-soft_motor-medium-onForDegrees.png
   :width: 50%

.. code-block:: cpp
    
    void onForDegrees(int speed = 50, int degrees = 360, bool_t brake = true, bool_t blocking = true, unsigned int wait_after_ms = 60)

Funkce ``onForDegrees()`` nastavuje počet stupňu, o které se má motor otočit. Jako paremetry se předávají: ``speed``, ``degrees``, ``brake``, ``blocking``, ``wait_after_ms``. 


Dostupné funcke - seznam
**********************

Po vytvoření objektu ``motor`` na něm lze volat funkce:

* ``off(bool brake = true)`` - vypne motory a začne brzit, pokud mu jako parametr nepředáte  ``false``
* ``on(int power = 50)`` - nastaví rychlost na motorech (v rozsahu -100 až 100)
* ``onForDegrees(int speed = 50, int degrees = 360, bool_t brake = true, bool_t blocking = true, unsigned int wait_after_ms = 60)`` -
* ``ahoj`` -
* ``ahoj`` -
* ``ahoj`` -
* ``ahoj`` -
* ``ahoj`` -

 
Pro nastavení neregulovaného motoru je potřeba zavolat na objekt funkci ``unregulated(int power)``.

.. code-block:: cpp

   motor.unregulated(50);





.. code-block:: cpp
   :linenos:

   ev3cxx::Motor motor(ev3cxx::MotorPort::A, ev3cxx::MotorType::LARGE);



