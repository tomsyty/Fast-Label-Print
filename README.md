## Szybkie drukowanie etykiet adresowych
Ten skrypt do programu AutoHotkey pozwala na automatyzację drukowania etykiet adresowych poprzez uruchamianie wydruku w tle za pomocą skrótu klawaturowego oraz usuwanie pliku etykiety bez dodatkowej ingerencji ze strony użytkownika. Pozwala zaoszczędzić sporo czasu gdyż eliminuje konieczność wykonywania kilku czynności: 
1. Otwórz plik etykiety
2. Wybierz Plik - Drukuj, kliknij ikonę drukowania albo użyj skrótu klawiaturowego Ctrl+P
3. Upewnij się że wybrałeś właściwą drukarkę i zatwierdź drukowanie
4. Zamknij plik
5. Usuń etykietę
   
To wszystko sprowadzić można do jednej czynności - wciśnięcie zdefiniowanego skrótu klawiaturowego. Oprócz tego skrypt umożliwia też skalowanie kodu kreskowego etykiet eCommerce Poczty Polskiej (Allegro Mini Przesyłka i Allegro Przesyłka polecona). Istnieje już do tego rozszerzenie do przeglądarki Chrome (https://github.com/tomsyty/Scale-PP-barcode) jednak gdyby ktoś korzystał z innej a potrzebował tej funkcjonalności (poczytaj o tej funkcji pod wspomnianym linkiem) to niniejszy skrypt daje taką możliwość.

Skrypt do działania wymaga kilku darmowych narzędzi znanych i wypróbowanych w środowisku programistycznym od wielu lat:
- Ghostscript: interpreter PDF do odczytu i renderowania plików
- ImageMagick: zestaw narzędzi do tworzenia, modyfikowania, konwersji grafiki w wielu formatach
- SumatraPDF: program do plików PDF z obsługą z wiersza poleceń
- Autohotkey: skryptowy język programowania  pozwalający na tworzenie programów bez potrzeby ich kompilacji

**Sposób użycia:**
1. Pobierz plik "FastLabelPrint.zip" z listy plików widocznej powyżej i rozpakuj go tam gdzie zamierzasz go trzymać. Zawiera on plik skryptu oraz wzorzec etykiety eCommerce (mały jej fragment który pozwala zidentyfikować że drukowana etykieta jest tą którą trzeba przetworzyć).
2. Zainstaluj (jeśli jeszcze ich nie posiadasz) wymagane programy (wymagany Windows 64 bit): (okresowo wychodzą nowe wersje, podane są wersje dla których działanie zostało sprawdzone, każda nowsza powinna być w porządku)
    - AutoHotkey (https://www.autohotkey.com) v2.0.10
    - SumatraPDF (https://sumatrapdfreader.org) SumatraPDF-3.4.6-64-install.exe<br/>
    
    oraz jeśli planujesz korzystać z funkcjonalności skalowania etykiet eCommerce Poczty Polskiej
   - Ghostscript (https://ghostscript.com) Ghostscript 10.02.0 for Windows (64 bit) Ghostscript AGPL Release
   - ImageMagick (https://imagemagick.org) ImageMagick-7.1.1-19-Q8-x64-static.exe

3. Uruchom plik "script.ahk". Przy pierwszym uruchomieniu zostanie otwarte okno z informacjami o programie oraz instrukcją instalacji. Po jego zamknięciu należy wskazać tryb działania programu: tylko drukowanie etykiet lub drukowanie z autowykrywaniem i modyfikacją etykiet przesyłek eCommerce Poczty Polskiej.
   W kolejnych krokach ustawisz:
   - skrót klawiaturowy aktywujący wydruk<br/>
     ![shortcut_keys_selection](https://github.com/tomsyty/Fast-Label-Print/assets/41838854/62ef1db0-4176-44f7-b9ab-3c91d2e2ee1e)

   - folder pobieranych etykiet: folder do którego przeglądarka zapisuje etykiety żeby program wiedział gdzie ich szukać
   - ścieżka do programu SumatraPDF: program wymagany jest do wydruku etykiet więc musi być zainstalowany, inaczej jego działanie mija się z celem
   - drukarka która jest używana do wydruku etykiet<br/>
     ![select_printer](https://github.com/tomsyty/Fast-Label-Print/assets/41838854/641a4c29-87c4-4f33-9ce4-8cfa5486dba4)

    oraz jeśli chcesz wykorzystywać program do modyfikacji etykiet adresowych Poczty Polskiej musisz ustawić opcje:
   - ścieżka do programu Ghostscript
   - ścieżka do programu ImageMagick
   - włączyć opcję "Modyfikuj etykiety Poczty Polskiej"

    Aby uruchamiać program przy włączeniu systemu zaznacz opcję "Uruchamiaj automatycznie przy starcie systemu" (działa ona dla aktualnie zalogowanego użytkownia).
4. W dowolnym momencie możesz zmienić ustawienia klikając prawym przyciskiem myszy ikonę programu AutoHotkey i wybierając "Ustawienia"<br/>
   ![settings](https://github.com/tomsyty/Fast-Label-Print/assets/41838854/8da8b71d-3f6a-4193-8eab-91c0c2a41135)


To już wszystko. Skrypt po wciśnięciu zdefiniowanego skrótu klawiaturowego wyszuka w folderze pobieranych plików wszystkie etykiety .pdf zawierającej w nazwie pliku datę w formacie YYYY-MM-DD_HH-MM-SS, a więc zarówno te które zawierają przedrostek "label-" (lub "labels-") jak i bez niego (etykietę na Allegro można pobrać w kilku miejscach, w zależności od tego miejsca nazwa pliku zawiera przedrostek lub nie). **Przed pierwszym uruchomieniem usuń wszystkie pobrane wcześniej etykiety przechowywane bezpośrednio w tym folderze aby uniknąć niepotrzebnego ich wydruku.**

Przetwarzanie etykiet eCommerce Poczty Polskiej mozliwe jest tylko gdy plik zawiera jedną etykietę. Jeśli potrzebujesz przetwarzać tego typu etykiety, drukuj je pojedynczo. W przypadku gdy skrypt wykryje plik zawierajacy więcej niż jedną etykietę i włączony jest tryb pracy programu z przetwarzaniem etykiet eCommerce, poinformuje o braku możliwości jej ewentualnego przetworzenia i zapyta czy chcesz wydrukować ją tak jak jest (to może być plik zawierający inne etykiety)<br/>
![multiple_labels_question](https://github.com/tomsyty/Fast-Label-Print/assets/41838854/e2d9af7c-7e58-4547-8a4f-c368cc6c732a)<br/>
Gdy masz wyłączony tryb przetwarzania etykiet eCommerce, takiego pytania nie będzie, wydrukuje plik bez pytania.


W razie problemów z usunięciem etykiety (np. jeżeli zostanie ona otwarta w momencie drukowania i okno z nią nie zostanie zamknięte przez co nie będzie można usunąć otwartego pliku) program poinformuje o tym stosownym komunikatem oraz zakończy działanie, otwierając okno eksploratora plików i zaznaczając plik do usunięcia. Ma to na celu ochronę przed sytuacją gdy odruchowo pobieramy kolejne etykiety, drukujemy, naklejamy na kolejne paczki nie zwracając większej uwagi na to czy wydrukowaliśmy właściwą etykietę, gdyby np. nie usunęło pliku etykiety ze wspomnianego wcześniej powodu to pomimo pobrania kolejnej mogłoby dojść do sytuacji że ponowny wydruk nie wydrukowałby nowo pobranej etykiety tylko kolejny raz tą samą pobraną wcześniej. Zakończenie działania programu wskazuje jednoznacznie że coś poszło nie tak i trzeba zwrócić na to szczególną uwagę żeby nie nakleić złej czy zdublowanej etykiety.  
    
