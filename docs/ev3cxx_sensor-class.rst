Senzory
====================

Když už umíme ovládat motory, můžeme se naučit pracovat se senzory.
Pomocí senzorů můžeme získávat informace z okolí a reagovat na ně.
Lze tak třeba řídit rychlost motorů, podle pozice robota na čáře nebo zastavit robota před překážkou.
V EV3CXX jsou k dispozici všechny základní senzory z LEGO MINDSTORMS EV3.


* ``TouchSensor`` - dotykový senzory (detekce nárazu, překážky, STOP tlačítko)
* ``ColorSensor`` - barevný senzor (jízda po čáře, třídění dle barvy)
* ``UltrasonicSensor`` - ultrazvukový senzor (měření vzdálenosti od překážky nebo mantinelu)
* ``GyroSensor`` - gyro senzor (určení o kolik stupňů se robot otočil - jízda rovně)

.. image:: images/lego-soft_sensor-touch-state.png
   :width: 24%
.. image:: images/lego-soft_sensor-color-getReflected.png
   :width: 24%
.. image:: images/lego-soft_sensor-ultrasonic-centimetres.png
   :width: 24%
.. image:: images/lego-soft_sensor-gyro-angle.png
   :width: 24%

Inicializace
*****************

Všechny senzory se inicializují 

.. code-block:: cpp

    //ev3cxx::nazev_tridy_senzoru nazev_objektu(ev3cxx::SensorPort::cislo_portu);
    ev3cxx::TouchSensor touchS(ev3cxx::SensorPort::1);


Vytvořili jsme tedy objekt ``touchS``, která je nastavena na port číslo ``1``.

Na *Bricku* můžeme využít všechny porty pro senzory: ``1``, ``2``, ``3`` a ``4``. 

TouchSensor
*****************

Metody dostupné ve třídě ``TouchSensor``:

* ``isPressed()`` - vrací stav senzory 
* ``waitForPress()`` - čekání, dokud se senzor nezmáčkne
* ``waitForRelease()`` - čekání, dokud se senzor neuvolní
* ``waitForClick()`` - čekání na zmáčknutí a uvolnění senzoru


isPressed() 
############

.. image:: images/lego-soft_sensor-touch-state.png
   :height: 90px

.. code-block:: cpp
    
    int isPressed();

Vrací ``true`` v případě, že je dotykový senzor zmáčknut, jinak ``false``.

void waitForPress() 
########################

.. image:: images/lego-soft_sensor-touch-waitForPress.png
   :height: 90px

.. code-block:: cpp
    
    void waitForPress();

Program je pozastaven, dokud nebude dotykový senzor zmáčknut.


void waitForRelease() 
########################

.. image:: images/lego-soft_sensor-touch-waitForRelease.png
   :height: 90px

.. code-block:: cpp
    
    void waitForRelease();

Program je pozastaven, dokud nebude dotykový senzor uvolněn.

.. warning:: 

    Nezapomínejte, že v běžném stavu je dotykový senzor uvolněn a proto nemusí být program při volání této funkce vůbec pozastaven. 
    Je tedy nutné nejprve dotykový senzor zmáčknout a až potom volat tuto funkci.

void waitForClick() 
########################

.. image:: images/lego-soft_sensor-touch-waitForClick.png
   :height: 90px

.. code-block:: cpp
    
    void waitForClick();

Program je pozastaven, dokud neproběhne zmáčknutí a uvolnění dotykového senzoru.


ColorSensor
*****************

Barevný senzor může pracovat v několika režimech: 

* ``getReflected()`` - vrací naměřenou intenzitu odrazu
* ``getReflectedRawRgb()`` - vrací naměřenou intenzitu odrazu pro jednotlivé barevní složky (RGB - červená, zelená, modrá)
* ``getAmbient()`` - vrací naměřenou intenzitu odrazu bez přisvětlení (vhodné pro kalibraci)
* ``getColor()`` - vrací rozpoznanou barvu

getReflected() 
###############

.. image:: images/lego-soft_sensor-color-getReflected.png
   :height: 90px

.. code-block:: cpp
    
    int getReflected();

Vrací naměřenou intenzitu odraženého světla z povrchu.
Lze tak rozpoznat barvu povrchu a například tak detekovat černo čáru na bílém podkladu.

Rozsah výstupních hodnot je od 0 do 100.

.. note::
    Senzor si při své činnosti snímanou plochu přisvětluje vlastními světly, tak aby mohl lépe určit odrazivost povrchu a nebyl tolik závislý na okolním osvětlení.
    Přes funkci ``getAmbient()`` je možné určit odrazivost při vypnutém přisvětlení.
    Po odečtení této hodnoty od ``getReflected()``  by měli být hodnoty za různých světelných podmínek pro stejné povrchy konstantní. 


getReflectedRawRgb() 
#####################

.. code-block:: cpp
    
    rgb_raw_t getReflectedRawRgb();

Vrací strukturu s naměřenými hodnotami jednotlivých barevných složek. 

Tato funkce nemá odpovídající blok v LEGO Softwaru. 

Příklad:

    .. code-block:: cpp
        
        rgb_raw_t rgb_values;
        rgb_values = colorS.getReflectedRawRgb();
        
        rgb_values.r; // RED value


getAmbient() 
#####################

.. image:: images/lego-soft_sensor-color-getAmbient.png
   :height: 90px

.. code-block:: cpp
    
    int getAmbient();

Vrací naměřenou intenzitu odraženého světla od povrchu, ale **bez přisvětlení vlastními světly**.
Vhodné pro kalibraci senzoru pro různá osvětlení. Více informací v poznámce u funkce ``getReflected()``.

Rozsah výstupních hodnot je od 0 do 100.


getColor() 
#####################

.. image:: images/lego-soft_sensor-color-getColor.png
   :height: 90px

.. code-block:: cpp
    
    colorid_t getColor();

Vrací rozpoznanou barvu povrchu z výčtového typu ``enum colorid_t``.

Hodnoty v typu ``colorid_t``:

*  ``COLOR_NONE`` - barva nerozpoznána 
*  ``COLOR_BLACK`` - černá barva  
*  ``COLOR_BLUE``  - modrá barva 
*  ``COLOR_GREEN`` - zelená barva  
*  ``COLOR_YELLOW`` - žlutá barva  
*  ``COLOR_RED`` - červená barva  
*  ``COLOR_WHITE`` - bílá barva    
*  ``COLOR_BROWN`` - hnědá barva  

Příklad:

    .. code-block:: cpp
        
        colorid_t color_value;
        color_value = colorS.getColor();
        
        if (color_value == COLOR_BLACK) 
        {
             // senzor on black color
        }