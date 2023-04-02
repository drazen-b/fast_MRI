# Rekonstrukcija slika magnetske rezonance putem fastMRI biblioteke

## Uvod

Medicinska dijagnostika je područje medicine koje obuhvaća načine identifikacije zdravstvenih problema. Zbog svojih sposobnosti stvaranja detaljnih slika mekog tkiva magnetska rezonanca je nezamjenjiva metoda dobivanja medicinskih slika. Potpuno je bezbolna metoda koja za stvaranje slike koristi jako magnetsko polje i radiovalove, a time nema štetnog ionizirajućeg zračenja i nuspojava. Postupak dobivanja slike traje od 15 do 90 minuta, a tokom postupka osoba mora mirno ležati unutar stroja. Najmanje kretnje uzrokuju šum i artefakte. S obzirom na trajanje postupka, iskustvo može biti neudobno i klaustrofobično. Dugo trajanje postupka ima i posljedice na povećanje cijene snimanja jer je potrebno više vremena po osobi. No, sposobnost detaljnog slikanja mekog tkiva nije zamjenjiva metodama poput CT snimanja i rendgenskog snimanja. Time, smanjenje trajanja slikanja postupkom magnetske rezonancije je poželjno.

### Magnetska rezonanca

Magnetska rezonancija se temelji na fizikalnoj pojavi nuklearne magnetske rezonancije. U toj pojavi jezgre određenih atoma pokazuju sposobnost upijanja i odašiljanja elektromagnetske energije prilikom stavljanja u magnetsko polje. Ponašaju se kao mali štapičasti magneti, te ukoliko se nalaze u magnetskom polju oni će se poravnati s njim. Zatim, stroj za magnetsku rezonanciju odašilje u njih elektromagnetski puls radio frekvencije, te ih time izbija iz poravnanja s magnetskim poljem. Ovdje djelovanje nuklearne magnetske rezonancije dolazi u utjecaj. Jezgre atoma će se rotirati i time odašiljati rf signal. No, nakon određenog vremena njihova će rotacija stati, te će se ponovno poravnati s magnetskim poljem. Vrijeme da se jezgra atoma prestane rotirati, vrijeme da se ponovno poravna s magnetskim poljem i količina energije koja je ispuštena ovise o kemijskom sastavu molekula. S obzirom na to je moguće razaznati razliku između različitih vrsta tkiva.

Postupak magnetske rezonance uzorkuje područje koje snimamo u Fourierovom prostoru, koji je također poznat kao k-prostor. Uporabom inverzne Diskretne Fourierove Transformacije (DFT) nad k-prostorom slike *y* dobivamo rekonstruiranu sliku *m*. **(Ubaciti formulu (1))**

Kvaliteta slike se određuje trima karakteristikama. Omjerom snage signala i snage šuma (SNR). oblikom piksela (point spread function) i artifaktima. Ukoliko je snaga šuma visoka, dolazi do diskoloracije konačne slike. Oblik piksela bi trebao biti samo jedan piksel, no ukoliko funkcija širenja sadrži više frekvencija doći će do zamućenja piksela. Artifakti nastaju kada su signali povezani uz piksele kojima ne pripadaju. To stvara preklapanja slike i nastanak nepostojećih oblika na slikama. Ukoliko je kvaliteta slike niska, može doći do skrivanja bitnih obilježja na slici što može dovesti do pogrešne dijagnoze, ili u najgorem slučaju slike koju nije moguće iskoristiti.

### Tehnike rekonstrukcije

Uvođenjem paralelnog slikanja u 1990ima skraćena je duljina trajanja postupka. Svaka dodana zavojnica slika zasebnu sliku u k-prostoru. Rekonstruirana slika y_i, zavojnice i od nc dobiva se iz **(Ubaciti formulu (2))** gdje je S_i osjetljivost zavojnice, a g_i njena Fourierova transformacija. Uvođenjem koprimirajuće osjetljivosti (compressed sensing (CS)) doprinijelo je napretku u smanjenju vremena snimanja magnetske rezonance. Tehnike CS ubrzavaju slikanje uzorkovanjem manje količine podataka nego klasičnim metodama. No zbog kršenja Nyquist-Shannonovog teorema uzorkovanja, ono dovodi do nastanka artefakta. Artefakti se prilikom rekonstrukcije moraju ukloniti, a to se postiže uporabom prethodnog znanja tokom rekonstrukcije. ESPIRiT je pristup koji povezuje paralelno slikanje i CS. U slikanju s više zavojnica služi za procjenu osjetljivosti zavojnica i za izvođenje rekonstrukcije slika u kombinaciji s CS korištenjem regularizacije ukupne varijacije.

Najnoviji pokušaji rekonstrukcije se izvode metodama dubokog učenja modela. Kretanje u tom smjeru je potaknuto objavljivanjem javno dostupnog fastMRI skupa podataka.

## fastMRI dataset

fastMRI je zajednički istraživački projekt između *Facebook AI Research* i *NYU Langone Health*. Njihov javno objavljeni skup podataka sastoji se od od četri tipa snimaka mozga i koljena postukom magnetske rezonance:
- Neprocesiranih snimaka k-prostora za višestruke zavojnice
- Emuliranih podataka k-prostora za pojedinačne zavojnice
- (Ground-truth) rekonstruirane slike iz potpuno uzorkovanih snimaka višestrukih zavojnica
- DICOM slika

Podatci su predviđeni kako bi omogućili dva različita zadatka:
- Rekonstrukciju slika uzorkovanih jednom zavojnicom
- Rekonstrukciju slika uzorkovanih s više zavojnica

Za svaki izazov objavljeni su službeni podskupovi za trening, validaciju, test i izazova. Svi podatci su anonimizirani. Sveukupno je 1594 neprocesiranih snimaka k-prostora koljena dobivenih s više zavojnica, 6970 slika k-prostora mozga dobivenih s više zavojnica. Podatci za izazov rekonstrukcije slika uzorkovanih jednom zavojnicom dobiveni su emulacijom podataka iz k-prostora slika dobivenih metodom s više zavojnica. 10000 DICOM slika mozga i koljena dobivenih MRI skenom.

**(Ubaciti sliku-tablicu s količinom podataka)**

U ovom radu se fokusiramo na dataset sa slikama mozga metodom više zavojnica. Prethodno navedenih 6970 MRI slika su dobivene korištenjem 11 magneta na 5 kliničkih lokacija. Kod uporabe ovog skupa podataka vrlo brzo dolazimo do problema. Naime, set za treniranje je veličine ~1.2 TB, set za validaciju je ~500GB, a set za testiranje je ~100GB. DICOM podatci se ne koriste jer ne pružaju neprocesirani k-prostor.

**((UBACITI NEKE SLIKICE OVO ONO))**

## fastMRI

Repozitorij javno dostupne i open-source fastMRI biblioteke dostupan je na GitHub-u. Biblioteka je pisana za programski jezik Python. Sadrži CS, Dino, Unet i VarNet modele za rekonstrukciju, njihov kod, te upute za uporabu.