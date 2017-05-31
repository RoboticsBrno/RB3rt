Soubory a bluetooth
====================

V rámci C++ API jsou připraveny třídy pro práci se soubory (třída ``File``) i Bluetooth (třída ``Bluetooth``). Obě dvě třídy mají totožné rozhraní (stejné metedy) až metodu ``isConnected()``, která je k dispozici jen pro Bluetooth.

Soupis dostupných metod:

* ``open()`` - otevře soubor/bluetooth
* ``isOpen()`` - vrací, zda je soubor/bluetooth otevřen
* ``isConnected()`` - vrací, zda k bluetooth někdo připojen
* ``close()`` - uzavírá soubor/bluetooth
* ``write()`` - zapíše/odešle znak
* ``readChar()`` - přečte/příjme znak
* ``readNumber()`` - přečte/příjme číslo
* ``rewind()`` - nastaví ukazatel pozice pro čtení/zápis na začátek souboru 
* ``()`` - operátor kulaté závorky vrací file descriptor souboru/bluetooth

Inicializace
*****************

Pro práci se soubory a Bluetooth je nejprve potřeba provést inicializaci (vytvořit instanci třídy).

.. code-block:: cpp

    //ev3cxx::File nazev_objektu{umisteni_souboru};
    ev3cxx::File myFile{"myFile.txt"};

    //ev3cxx::Bluetooth nazev_objektu{};
    ev3cxx::Bluetooth bt{};

Systém EV3RT pracuje se soubory na SD kartě. 
Proto se ``umisteni_souboru`` uvažuje vždy vůči kořenovému adresáři na kartě. 
Pokud chcete umístit soubor do podadresáře, stačí zadat cestu s lomítkem.
Příklad: ``ev3rt/myFile.txt``.

.. warning:: 
   Když zadáváte umístění souboru do podadresářů, ujistěte se, že všechny složky po cestě existují. 
   C++ API sice může vytvořit soubor, pokud ještě na kartě neexistuje, ale nevytváří složky, které jsou uvedeny v cestě k souboru, ale na SD kartě neexistují. 

Následuje podrobnější popis konstruktorů.

File
############

.. code-block:: cpp

    ev3cxx::File(const char * filename, const char * mode = "w+")

Parametr ``filename`` očekává textový řetězec s cestou k danému souboru (viz popis ``umisteni_souboru`` v sekci Inicializace). 
Pokud soubor neexistuje, při ponechání ``mode`` na výchozí hodnotu ``w+``, bude soubor vytvořen.

Parametr ``mode`` udává v jakém režimu se soubor otevře (pro zápis/čtení/obojí), zda se má vytvořit když neexistuje nebo jestli se má soubor vždy přepisovat či dál rozšiřovat.
Popis všech ``mode`` naleznete `ve specifikaci C funkce fopen() <http://www.cplusplus.com/reference/cstdio/fopen/#parameters>`_

.. note:: 
   Při vytváření instance třídy File je soubor automaticky otevřen.


Bluetooth
############

.. code-block:: cpp

    ev3cxx::Bluetooth()

U třídy Bluetooth se při inicializaci nezadávají žádné parametry. Po vytvoření instance je potřeba ještě Bluetooth otevřít => metoda ``open()``.

Metody
*****************

Soupis dostupných metod v třídách ``File`` a ``Bluetooth``.


open() 
############

.. code-block:: cpp
    // File
    bool_t open(const char * filename = "", const char * mode = "w+");

    // Bluetooth
    bool_t open();

Otevře soubor/bluetooth. 
    
Vrací ``true`` v případě, že se soubor/bluetooth podaří otevřít, jinak ``false``.

Parametry metody ``open()`` pro třídu File jsou popsány v sekci inicializace.

Příklad: 

``myFile.open("ev3rt/myFile.txt", "a+");``

``bt.open();``


isOpen() 
########################

.. code-block:: cpp
    
    bool isOpen();

Vrací ``true`` v případě, že je soubor/bluetooth správně otevřen, jinak ``false``.

Příklad: ``myFile.isOpen();``

isConnected() 
########################

.. code-block:: cpp
    
    bool isConnected();

Vrací ``true`` v případě, že je k Bluetooth na EV3 Bricku někdo připojen, jinak ``false``.

Příklad: ``bt.isConnected();``

.. warning:: Tato metoda je dostupná jen pro třídu Bluetooth.


close() 
########################

.. code-block:: cpp
    
    int close();

Zavírá soubor/bluetooth.    
    
Vrací ``true`` v případě, že je soubor/bluetooth správně zavřen, jinak ``false``.

Příklad: ``myFile.close();``


write() 
###############

.. code-block:: cpp
    
    int write(char ch);

Zapíše/odešle jeden znak.

Vrací odeslaný znak, pokud úspěšně odeslán, jinak ``EOF`` (End Of File - signalizace konce souboru nebo chybového stavu).

Příklad: ``myFile.write('a');``

.. note:: 
   Tuto metodu pravděpodobně nebudete potřebovat, protože veškerý zápis/odesílání dat můžete provádět přes metodu ``format()`` (viz dále).


format() 
###############

Formát je metoda, která není součástí tříd ``File`` a ``Bluetooth``. 
Proto se s ní pracuje trochu odlišně (viz následující příklady).

.. code-block:: cpp
    
    format(objekt_soubor , char const *pattern);
    format(objekt_bluetooth , char const *pattern);
    
Pro zápis/odesílání formátovaného textu slouží metoda ``format``.
Jako první parametr se předává název objektu
Parametr ``pattern`` je text, který se má vypsat.


Příklad: ``ev3cxx::format(myFile ,"Hello world");``

Zapíše text "Hello world".

Ve vypisovaném textu se mohou vyskytovat speciální znaky pro ovládání pozice kurzoru:

* ``\n`` - přesune kurzor na začátek dalšího řádku
* ``\r`` - přesune kurzor na začátek tohoto řádku

Příklad: ``ev3cxx::format(bt, "Ahoj svete! \nJak se mas?");``

Na prvním řádku v souboru (nebo terminálu připojeném k Bluetooth EV3 Bricku) bude po provedení tohoto příkazu text "Ahoj svete!".
Na druhém řádku pak "Jak se mas?".

``format`` také umožňuje vypisovat hodnotu proměnných pomocí znaku ``%``.
Lze vypisovat proměnné a řetězce.

.. warning:: 

    Pozor: znak ``%`` pro výpis proměnné vždy "sežere" znak, následující bezprostředně za ním!
    Z toho důvodu jsou v prvním příkladu s hodinami za znakem ``%`` napsány dvě mezery.
    První mezeru "sežere" ``%``, druhá se vypíše.
    Mít za ``%`` mezeru je nezbytně nutné i v případě, že je ``%`` posledním znakem v řetězci.
    Pokud za ``%`` následuje hned konec řetězce, je chování nedefinované.

    Příklad: |br|\
    ``ev3cxx::format(myFile, "%") % 1;`` číslo "1" se nezobrazí => za % není mezera |br|\
    ``ev3cxx::format(myFile, "% ") % 1;`` při tomto zápisu formátovacího řetězce se již číslo "1" zobrazí normálně

Příklad:

   .. code-block:: cpp

      int hours = 19;
      int minutes = 42;
      ev3cxx::format(myFile, "Je %  hodin a %  minut.") % hours % minutes;

Zapíše do souboru text "Je 19 hodin a 42 minut.".

Také se dá specifikovat zarovnání výpisu proměnné doprava na daný počet znaků.
Například při výpisu hodin je dobré, když jsou hodiny i minuty vždy na stejném místě, bez ohledu na to, jestli jsou zrovna reprezentovány jednomístným, nebo dvoumístným číslem.

.. note:: 
   Zarovnání znaků je podporováno jen u celočíselných typů (``int``, ``long``, ...). Nelze jej nastavovat u čísel s plovoucí čárkou (``float`` a ``double``). U nich bude uživatelem zadané zarovnání ignorováno a použije se vždy výchozí nastavení (``float`` => ``%g`` a ``double`` => ``%f`` `dle standardní specifikace formátování čísel v C <http://www.cplusplus.com/reference/cstdio/printf/#parameters>`_).

Příklad:

   .. code-block:: cpp

      int hours = 8;
      int minutes = 42;
      ev3cxx::format(myFile, "Je %2 hodin a %2 minut.") % hours % minutes;

Zapíše text ``Je  8 hodin a 42 minut.``.
Všimněte si dvou mezer mezi "je" a "8", ale jen jedné mezery mezi "a" a "42".
8 hodin je pouze jednomístné číslo a tudíž ho formát sám doplnil zleva mezerou, aby zabíralo stejně místa, jako dvoumístné číslo a nedocházelo k posunu následujícího textu.
Zarovnání doplňuje zleva mezery, pokud je to potřeba, ale nebrání ve výpisu delších čísel.

Dále je možné vypisovat čísla v dvojkové, nebo šestnáctkové soustavě.

Příklad: ``ev3cxx::format(myFile, "hex: %x4\nbin: %b8\ndec: %3") % 42 % 42 % 42;``

Zapíše text:

.. |br| raw:: html

   <br />

``hex: 002A`` |br|\
``bin: 00101010`` |br|\
``dec:  42``

Šestnáctková a dvojková čísla se při zarovnání doplňují číslicí 0, zatím co desítková mezerami.

Chcete-li mít ve výsledném textu znak %, použijte kombinaci ``%%``:

Příklad: ``ev3cxx::format(myFile, "10%%");``

Zapíše text "10%".
