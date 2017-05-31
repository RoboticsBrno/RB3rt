Instalace vývojového prostředí
===================================

Pro jednodušší používání C++ knihoven je k dispozici předpřipravené vývojového prostředí.

K instalaci prostředí je připraven skript `RB3rt-install.bat <http://files.robotikabrno.cz/RB3rt-install.bat>`_. 

Veškerý software se nainstaluje na diskový oddíl ``C:``.

Po stažení skriptu postupujte podle obrázkového návodu.

.. figure:: /rb3rt-install/rb3rt-installation-01-folder.png
   :align: center

   Nejprve je potřeba spustit instalační skript.

.. warning:: 
   Na novějších verzích Windows (8,10) se zobrazí okno s informací o nerozpoznané aplikaci. 
   Jelikož Windows tento skript nezná, z bezpečnostních důvodů zobrazuje toto okno.
   
   .. figure:: /rb3rt-install/rb3rt-installation-02-windows-warning.png
      :align: center 

   Pro pokračování instalace je potřeba kliknout na ``Další informace``  

   .. figure:: /rb3rt-install/rb3rt-installation-02-windows-warning-next.png
      :align: center
   
   Následně spustit instalaci tlačítkem ``Přesto spustit``.


.. figure:: /rb3rt-install/rb3rt-installation-03-download-wget.png
   :align: center

   Po spuštění začne skript stahovat potřebný software. 
   V průběhu instalace je nutné potvrzovat práva k instalaci u jednotlivých softwaru.
      
.. figure:: /rb3rt-install/rb3rt-installation-04-run.png
   :align: center

   Skript vždy stáhne požadovaný software a spustí jeho instalaci. 
   Po dokončení instalace pokračuje na další software.

   Takto se nainstaluje: 7-Zip, Visual Studio Code, Cygwin, GCC ARM překladač

.. figure:: /rb3rt-install/rb3rt-installation-05-firewall.png
   :align: center
   
   Po nainstalování Visual Studio Code se program otevře a bude potřeba potvrdit přístup na internet.

.. figure:: /rb3rt-install/rb3rt-installation-06-cygwin.png
   :align: center
   
   Další okno, které se vám zobrazí bude instalace software Cygwin. 
   Toto okno je jen informativní a není potřeba s ním cokoliv dělat.
   
.. warning:: Nepostupujte na další krok, dokud se okno s instalací Cygwinu nezavře.

   
.. figure:: /rb3rt-install/rb3rt-installation-07-gcc-arm.png
   :align: center
   
   V následujícím kroku se otevře instalace GCC ARM překladače (GNU Tools for ARM ...).
   Zde je potřeba projít instalačním procesem. Postupně volte vždy krok ``Další`` a ponechejte výchozí nastavení.
   
.. figure:: /rb3rt-install/rb3rt-installation-08-gcc-arm-run.png
   :align: center
   
   Následně se rozběhne instalace.

.. figure:: /rb3rt-install/rb3rt-installation-09-gcc-arm-finish.png
   :align: center
   
   Po dokončení instalace je potřeba vybrat zatržítko ``Add path to environment variable``.

.. figure:: /rb3rt-install/rb3rt-installation-10-gcc-arm-finish-with-path.png
   :align: center
   
   Po vybrání zatržítka ``Add path to environment variable``, klikněte na ``Dokončit``.
   
.. figure:: /rb3rt-install/rb3rt-installation-11-lorris.png
   :align: center
   
   Nyní již automaticky skript dostahuje všechny potřebné soubory a skončí.


Visual Studio Code (VS Code)
*******************************

.. figure:: /rb3rt-install/rb3rt-installation-12-vscode-open.png
   :align: center
   
   Otevřete vývojový editor Visual Studio Code (najdete jej v nabídce ``Start``).

.. note:: Po jeho otevření pravděpodobně proběhne ještě doinstalovaní některých doplňků.

   
.. figure:: /rb3rt-install/rb3rt-installation-13-vscode-open-folder.png
   :align: center
   
   Otevřete nabídku ``File`` a vyberte volbu ``Open Folder...``.

.. figure:: /rb3rt-install/rb3rt-installation-14-vscode-open-folder-select.png
   :align: center
   
   V systémovém oddílu ``C:`` vyberte složku ``RB3rt-project`` a potvrďte ``Vybrat složku``.

.. figure:: /rb3rt-install/rb3rt-installation-15-vscode-project-opened.png
   :align: center
   
   Nyní se otevřel adresář s ukázkovým projektem.

Nastavení klávesových zkratek
*******************************

.. figure:: /rb3rt-install/rb3rt-installation-16-vscode-keybinding-open-file.png
   :align: center
   
   V následujících krocích nastavíme klávesové zkratky. Otevřete soubor ``keybindings.json`` z levé nabídky (stačí kliknout).


.. figure:: /rb3rt-install/rb3rt-installation-16-vscode-keybinding-open-file.png
   :align: center
   
   Obsah tohoto souboru budeme za chvíli kopírovat do nastavení VS Code.

.. figure:: /rb3rt-install/rb3rt-installation-17-vscode-keybinding-open-setting.png
   :align: center
   
   Otevřete nabídku: :menuselection:`File --> Preferences --> Keyboard Shortcuts`.

.. figure:: /rb3rt-install/rb3rt-installation-18-vscode-keybinding-opened-setting.png
   :align: center

   Nyní vidíte všechny klávesové zkratky ve VS Code. 
   My potřebujeme ale nastavit vlastní, a proto klikneme na odkaz ``keybindings.json``, který najdete v okně s přehledem zkratek, hned pod vyhledávacím polem a ve větě s textem: For advanced customizations open add edit ``keybindings.json``. 

.. figure:: /rb3rt-install/rb3rt-installation-19-vscode-keybinding-opened-user-setting.png
   :align: center
   
   V právem okně se otevře soubor ``keybindings.json``. 
   Do tohoto souboru je potřeba nakopírovat obsah souboru ``keybindings.json``, který jsme otevírali v úvodu.


.. figure:: /rb3rt-install/rb3rt-installation-20-vscode-keybinding-opened-user-setting-paste.png
   :align: center
   
   Po překopírování nastavení již stačí vše uložit a restartovat VS Code. Pak již budou všechny klávesové zkratky fungovat.


Přeložení programu
*******************************

.. figure:: /rb3rt-install/rb3rt-installation-21-vscode-open-app.png
   :align: center
   
   Pro přeložení programu, po předchozím nastavení klávesových zkratek, stačí otevřít soubor ``app.cpp`` v ukázkovém projektu a zmáčknout ``F5``.

.. figure:: /rb3rt-install/rb3rt-installation-22-vscode-app-compile-start.png
   :align: center
   
   Po zmáčknutí klávesy ``F5`` se zahájí překlad programu. 
   Poznáte to i tak, že se vám otevře ve VS Code nový panel s informacemi o překladu.
   Na obrázku je vidět zahájení překladu.
   
.. figure:: /rb3rt-install/rb3rt-installation-23-vscode-open-app-compile-end.png
   :align: center
   
   Při úspěšném překladu budete vidět následující výstup. 
   Výsledný program je k dispozici ve složce s projektem: soubor ``app``
   

.. note:: 
   Adresář s ukázkovým programem můžete přemístit kamkoliv na vašem PC. Jeho pozice nemusí být fixní. 
   Všechny ostatní adresáře, které se při instalaci prostředí vytvořili, již ale musí zůstat na stejném místě.
 

Systém EV3RT
*******************************

Pro spuštění systému EV3RT na LEGO MINDSTORMS EV3 je potřeba nahrát image systému na micro SDHC kartu.

Image systému po proběhnutí instalačního skriptu, popisovaného v úvodu této kapitoly, k dispozici ve složce ``C:\RB3rt-image``.
Obsah této složku je potřeba překopírovat na SD kartu a následně ji vložit do EV3 Bricku.
Pak již stačí jen spustit Brick. 

.. warning:: 
   Systém EV3RT podporuje jen SDHC karty. 
   Neumí pracovat se staršími SD kartami (do 2 GB).
   Je proto potřeba mít k dispozici kartu alespoň o velikosti 4 GB.


Nahrání programu do EV3RT
*******************************

Nahrání programu je velmi jednoduché. Systém EV3RT se při připojení Bricku k PC chová jako standardní Flash disk.
Stačí tedy vzít přeložený program (soubor ``app``) ze složky s vaším projektem a vložit jej na SD kartu do adresáře ``ev3rt\apps\``.
Tento adresář je již v image systému vytvořen a obsahuje ukázkový projekt ``helloev3``.
Projekty na kartě si můžete přejmenovávat jak chcete.
Názvy souborů a složek ale nesmí obsahovat diakritiku (háčky, čárky), mezery a nebo speciální znaky ($%^&#@). Pro oddělování slov doporučuji použít pomlčku ``-`` nebo podtržítko ``_``.


   
Předdefinované klávesové zkratky
**********************************

* ``F5`` spuštění překladu programu
* ``F8`` otevření programu Lorris (obsahuje terminál pro práci s Bluetooth)
* ``F9`` otevření webové stránky s online dokumentací k EV3RT C++ API
   
   
   
   

   
