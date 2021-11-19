# Import vyřazených publikací z Alephu do Woocommerce

Knihovna vyřazuje zastaralé publikace ze svého fondu. Tyto publikace nabízí k
prodeji jiným knihovnám a čtenářům. Pro zabránění požadavkům na stejné knihy více
zájemci jsme zprovoznili rezervační systém založený na platformě Woocommerce.

Woocommerce umožňuje [import produktů k prodeji](https://docs.woocommerce.com/document/product-csv-importer-exporter/)
pomocí CSV souborů. Tento skript zkonvertuje XML soubor vyexportovaný z Alephu na CSV
s požadovanými údaji.

# Postup v Almě

Potřebujeme nový nástroj na zpracování XML z Almy: https://github.com/Knihovna-PedF-UK/alma-xml

XML stáheme v modulu Analýzy. Vybereme výstup a úplně dole je možnost exportu dat, kde vybereme XML.

Ten zpracujeme pomocí:

     texlua alma-csv cislo_odpisu < xml_soubor > import.csv

Číslo odpisu je důležité, protože XML soubor obsahuje historii všech odpisů.

# Starý postup v Alephu

Nejdříve je třeba vygenerovat XML soubor z Alephu. Ve službě *Obecný formulář pro vyhledávání* zadáme následující hodnoty:

- název: pedf_odpisy_YYYY_MM
- dílčí knihovna: PEDFR PEDFC
- status zpracování: VY 
- datum odpisu: datum ve formátu DD/MM/YYYY

Soubor se stáhne do adresáře ve Wine. Je třeba opravit konce řádků. Např.:

    dos2unix ~/.wine/drive_c/AL500/Circ/files/CKS50/print/pedf_odpisy_2020_10

Pak již můžeme soubor vygenerovat:

    ./eshop-csv  ~/.wine/drive_c/AL500/Circ/files/CKS50/print/pedf_odpisy_2020_10 > import.csv


