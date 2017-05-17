Senzory
====================

Když už umíme ovládat motory, měli bychom se naučit pracovat se senzory.
Pomocí senzorů můžeme získávat informace z okolí a reagovat na ně.
Lze tak třeba řídit rychlost motorů, podle pozice robota na čáře nebo zastavit robota před překážkou.
V EV3CXX jsou k dispozici všechny základní senzory z LEGO MINDSTORMS EV3.


* ``TouchSensor`` - dotykový senzor (detekce nárazu, překážky, STOP tlačítko)
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

Všechny senzory se inicializují: 

.. code-block:: cpp

    //ev3cxx::nazev_tridy_senzoru nazev_objektu(ev3cxx::SensorPort::cislo_portu);
    ev3cxx::TouchSensor touchS(ev3cxx::SensorPort::1);


Vytvořili jsme tedy objekt ``touchS``, která je nastavena na port číslo ``1``.

Na *Bricku* můžeme využít všechny porty pro senzory: ``1``, ``2``, ``3`` a ``4``. 

TouchSensor
*****************

Metody dostupné ve třídě ``TouchSensor``:

* ``isPressed()`` - vrací ``true`` pokud je senzor zmáčklý 
* ``waitForPress()`` - čekání, dokud se senzor nezmáčkne
* ``waitForRelease()`` - čekání, dokud se senzor neuvolní
* ``waitForClick()`` - čekání na zmáčknutí a uvolnění senzoru


isPressed() 
############

.. image:: images/lego-soft_sensor-touch-state.png
   :height: 90px

.. code-block:: cpp
    
    int isPressed();

Vrací ``true`` v případě, že je dotykový senzor zmáčklý, jinak ``false``.

waitForPress() 
########################

.. image:: images/lego-soft_sensor-touch-waitForPress.png
   :height: 90px

.. code-block:: cpp
    
    void waitForPress();

Program je pozastaven, dokud nebude dotykový senzor zmáčknut.


waitForRelease() 
########################

.. image:: images/lego-soft_sensor-touch-waitForRelease.png
   :height: 90px

.. code-block:: cpp
    
    void waitForRelease();

Program je pozastaven, dokud nebude dotykový senzor uvolněn.

.. warning:: 

    Nezapomínejte, že v běžném stavu může být dotykový senzor uvolněn.
    Volání této metody program pozastaví pouze pokud je v daný okamžik dotykový senzor zmáčknutý.

waitForClick() 
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
* ``getReflectedRawRgb()`` - vrací naměřenou intenzitu odrazu pro jednotlivé barevné složky (RGB - červená, zelená, modrá)
* ``getAmbient()`` - vrací naměřenou intenzitu odrazu bez přisvětlení (vhodné pro kalibraci)
* ``getColor()`` - vrací rozpoznanou barvu

getReflected() 
###############

.. image:: images/lego-soft_sensor-color-getReflected.png
   :height: 90px

.. code-block:: cpp
    
    int getReflected();

Vrací naměřenou intenzitu odraženého světla z povrchu.
Lze tak rozpoznat barvu povrchu a například tak detekovat černou čáru na bílém podkladu.

Rozsah výstupních hodnot je od 0 do 100.

.. note::
    Senzor si při své činnosti snímanou plochu přisvětluje vlastními světly, tak aby mohl lépe určit odrazivost povrchu a nebyl tolik závislý na okolním osvětlení.
    Přes metodu ``getAmbient()`` je možné určit odrazivost při vypnutém přisvětlení.
    Po odečtení této hodnoty od ``getReflected()``  by měly být hodnoty za různých světelných podmínek pro stejné povrchy konstantní. 


getReflectedRawRgb() 
#####################

.. code-block:: cpp
    
    rgb_raw_t getReflectedRawRgb();

Vrací strukturu s naměřenými hodnotami jednotlivých barevných složek. 
Jako návratová hodnota je použita struktura ``rgb_raw_t``, která obsahuje jednotlivé složky (r,g,b). 

.. note:: Tato metoda nemá odpovídající blok v LEGO Softwaru. 

Příklad:

    .. code-block:: cpp
        
        rgb_raw_t rgb_values;
        rgb_values = colorS.getReflectedRawRgb();
        
        rgb_values.r; // RED value
        rgb_values.g; // GREEN value
        rgb_values.b; // BLUE value


getAmbient() 
#####################

.. image:: images/lego-soft_sensor-color-getAmbient.png
   :height: 90px

.. code-block:: cpp
    
    int getAmbient();

Vrací naměřenou intenzitu světla dopadajícího na senzor, ale **bez přisvětlení vlastními světly**.
Vhodné např. pro kalibraci senzoru pro různá osvětlení. Více informací v poznámce u metody ``getReflected()``.

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
             // sensor on black color
        }


UltrasonicSensor
*****************

Ultrazvukový senzor je primárně určen na měření vzdálenosti. Můžeme jej využít pro detekci překážky, určení vzdálenosti od mantinelu nebo i pro korekci jízdy. 


.. note:: Šíření ultrazvukových vln v prostoru

    .. figure:: images/Ultrasonic-measure-range.jpg
       :height: 286px
       :align: center

       Ultrazvukové vlny se od vysílače šíří v kuželu.
       To znamená, že s rostoucí vzdáleností od senzoru pokrývají větší plochu. 
       Zároveň s tím ale klesá rozlišovací schopnost, proto senzor při větších vzdálenostech nedokáže zachytit předměty, které na blízko zachytí.
       To je podstatný rozdíl v porovnání s infra senzorem, jehož paprsky se šíří prakticky přímo (s mnohem menším rozptylem do stran).

       Zdroj obrázku: http://arcbotics.com/products/sparki/parts/ultrasonic-range-finder/


Ultrazvuk v EV3CXX poskytuje tyto metody:


* ``centimeters()`` - vrací naměřenou vzdálenost v centimetrech
* ``millimeters()`` - vrací naměřenou vzdálenost v milimetrech
* ``inches()`` - vrací naměřenou vzdálenost v palcích
* ``inchesLine()`` - vrací naměřenou vzdálenost v line (1/12 palce)
* ``listen()`` - vrací zda přijímá signál z jiného ultrazvukového vysílače

.. warning:: 
   Ultrazvuk v EV3 umí měřit v rozsahu od 3 do 255 centimetrů. 
   Pokud se budete pohybovat na hranici 3 centimetrů, může se stát, že ultrazvuk nedokáže danou vzdálenost změřit a místo hodnoty blízké 3 cm vrátí hodnotu rovnou maximální vzdálenosti => 255 cm.
   
   Pamatujte na tuto vlastnosti při návrhu a programování vašich robotů. Nejbezpečnějším řešením je umístit ultrazvuk tak, aby samotná konstrukce nedovolila menší vzdálenost než 4 a více centimetrů.

centimeters() 
###############

.. image:: images/lego-soft_sensor-ultrasonic-centimetres.png
   :height: 90px

.. code-block:: cpp
    
    int centimeters();

Vrací naměřenou vzdálenost v centimetrech. 

Rozsah měření je od 3 do 255.

.. warning:: 
   Na rozdíl od LEGO Softwaru, v EV3CXX tato metoda pracuje v celých číslech. Pokud chcete vyšší přesnost použijte metodu ``millimeters()``.


millimeters() 
###############

.. code-block:: cpp
    
    int millimeters();

Vrací naměřenou vzdálenost v milimetrech. 

Rozsah měření je od 30 do 2550.

.. note:: 
   Tato metoda nemá odpovídající blok v LEGO Softwaru. 
   Jelikož ultrazvuk v EV3 má rozlišení na milimetry a v LEGO Softwaru to řeší pomocí desetinných čísel, je v EV3CXX implementována tato metoda.



inches() 
###############

.. image:: images/lego-soft_sensor-ultrasonic-inches.png
   :height: 90px

.. code-block:: cpp
    
    int inches();

Vrací naměřenou vzdálenost v palcích (1 palec = 2,54 cm). 

Rozsah měření je od 1 do 100.

.. warning:: 
   Na rozdíl od LEGO Softwaru, v EV3CXX tato metoda pracuje v celých číslech. Pokud chcete vyšší přesnost použijte metodu ``inchesLine()``.


inchesLine() 
###############

.. code-block:: cpp
    
    int inchesLine();

Vrací naměřenou vzdálenost v linech (1 line = 1/12 palce). 

Rozsah měření je od 10 do 1200.

.. note:: 
   Tato metoda nemá odpovídající blok v LEGO Softwaru. 
   Jelikož ultrazvuk v EV3 má rozlišení na milimetry a v LEGO Softwaru to řeší pomocí desetinných čísel, je v EV3CXX implementována tato metoda.


listen() 
###############

.. image:: images/lego-soft_sensor-ultrasonic-listen.png
   :height: 90px

.. code-block:: cpp
    
    int listen();

Senzor poslouchá a pokud zachytí ultrazvukový signál, od jiného vysílače, vrací ``true``, jinak ``false``.



GyroSensor
*****************


Gyroskop umožňuje změřit o kolik stupňů se robot otočil nebo jak rychle se otáčí. 
EV3 obsahuje jednoosý gyroskop a tak si při stavbě musíte vybrat v jaké rovině chcete měřit.


Gyroskop v EV3CXX poskytuje tyto metody:

* ``angle()`` - vrací aktuální úhel natočení ve stupních
* ``rate()`` - vrací aktuální rychlost otáčení ve stupních za vteřinu
* ``reset()`` - nastavuje počáteční polohu gyroskopu
* ``resetHard()`` - provádí úplný restart senzoru


.. warning:: 
   Gyroskop v EV3 se občas zasekne a začne měnit aktuální úhel (ujíždět), i když se robot nehýbe. 
   Většinou nepomůže standardní ``reset()`` a proto je v těchto případech potřeba provést ``resetHard()``.
   
   Při každém vytváření objektu ze třídy GyroSensor se provádí ``resetHard()``. V tento moment se nesmí gyroskop pohybovat, jinak bude měřit špatně.  

angle() 
###############

.. image:: images/lego-soft_sensor-gyro-angle.png
   :height: 90px

.. code-block:: cpp
    
    int angle();

Vrací aktuální úhel natočení vůči počáteční pozici (odchylku od počáteční pozice). Počáteční pozice se nastavuje při vytváření objektu nebo pomocí metody ``reset()``.

Rozsah měření je od -32768 do 32767. Při překročení maximální nebo minimální hodnoty (např. 32767 + 1) začne gyroskop vracet hodnotu z druhého konce rozsahu (=> -32768).

.. warning:: 
   Při použití metody ``rate()`` dochází k restartu počáteční polohy u metody ``angle()``. Ta pak ukazuje opět od nuly.


rate() 
###############

.. image:: images/lego-soft_sensor-gyro-rate.png
   :height: 90px

.. code-block:: cpp
    
    int rate();

Vrací aktuální rychlost změny polohy ve stupních za sekundu.



reset() 
###############

.. image:: images/lego-soft_sensor-gyro-reset.png
   :height: 90px

.. code-block:: cpp
    
    void reset();

Nastavuje počáteční polohu gyroskopu pro metodu ``angle()`` a také kalibruje senzor.
Při volání metody ``reset()`` by se Gyro senzor neměl vůbec hýbat. Jinak bude špatně měřit. Dejte pozor na vibrace a dojezdy setrvačností.

Metoda může v některých případech odstranit *ujíždění* aktuálního úhlu gyroskopu pro metodu ``angle()``, ale ne vždy funguje.


resetHard() 
###############

.. code-block:: cpp
    
    void resetHard();


Provádí úplný restart senzoru. Měl by odstranit problém s ujížděním, kdy ačkoliv se Gyro senzor vůbec nehýbe, jeho poloha má konstantní přírůstek. 
V tento moment gyroskop nelze využívat a je potřeba jej restartovat.

.. note:: Tato metoda nemá odpovídající blok v LEGO Softwaru. 

.. warning:: 
   Počítejte s tím, že ``resetHard()`` může trvat i několik sekund a po tuto dobu bude zastaven běh programu. 
   Je tedy potřeba provádět úplný reset jen v nutných případech a na místech v programu, kde tato prodleva nebude vadit.

   Během restartu se nesmi gyroskop pohybovat, jinak nebude měřit správně.

.. note::
   Implementace úplného restartu je v celku jednoduchá. 
   Aby došlo k restartu, je potřeba přepnout gyroskop mezi režimy v jakých  pracuje. 
   První režim je měří úhel natočení (``angle()``) a druhý režim  měří rychlost otáčení (``rate()``). 
   Při přepínání mezi těmito režimy dochází k úplnému restartu gyroskopu. 
   Pro stoprocentní funkčnost se v metodě ``resetHard()`` provádí vícenásobné přepínání (``angle()`` => ``reset()`` => ``rate()`` => ``reset()`` => ``angle()``).

   Zdroj 1: https://bricks.stackexchange.com/questions/7115/how-can-ev3-gyro-sensor-drift-be-handled

   Zdroj 2: https://www.us.lego.com/en-us/mindstorms/community/robot?projectid=96894a3a-45db-48f9-9544-abf66f481b32