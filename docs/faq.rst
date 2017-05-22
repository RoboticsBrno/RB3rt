FAQ
==================================================

Zda naleznete soupis chyb a jejich řešení, na které můžete při programování narazit.


Práce s projektem
**********************************
 
Vytvoření nového projektu
###############################################################

Pokud chcete založit nový projekt, stačí jen zkopírovat složku s ukázkovým projektem ``RB3rt-project`` z ``C:\RB3rt-project``, přejmenovat jej a umístit kamkoliv budete chtít.

.. note:: 
   Název složky nesmí obsahovat diakritiku (háčky, čárky), mezery a nebo speciální znaky ($%^&#@). Pro oddělování slov doporučuji použít pomlčku ``-`` nebo podtržítko ``_``.


Chyby při překladu programu
**********************************

Nadpisy podkapitol jsou buď celé nebo zkrácené chybové hlášky, které se mohou během překladu zobrazit. 


error: expected unqualified-id before numeric constant
###############################################################

Chyba může nastat, když například špatně zadáte označení portu u senzoru:

.. code-block:: cpp

   ev3cxx::TouchSensor touchS(ev3cxx::SensorPort::1); 
   // spatne oznaceni portu senzory

Senzory v EV3CXX jsou označovány: ``S1``, ``S2``, ``S3`` a ``S4``.

.. code-block:: cpp

   ev3cxx::TouchSensor touchS(ev3cxx::SensorPort::S1); 
   // takhle je to spravne


error: ambiguous overload for 'operator%' (operand types are 'ev3cxx::detail::format_impl
###########################################################################################

Chyba může nastat, když například předáte strukturu ``colorid_t`` do metody ``format()`` přes ``%``.

Příklad:

.. code-block:: cpp

   colorid_t col = colorS.color();
   display.format("Color: % \n") % col;

Metoda ``format()`` neumí pracovat se strukturou ``colorid_t``. Pokud si chceme zobrazit danou barvu, musíme například použít podmínku:

.. code-block:: cpp

   colorid_t col = colorS.color();

   if (col == COLOR_BLACK) {
      display.format("Black color\n");
   }