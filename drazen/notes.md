# Rekonstrukcija MRI slika mozga pomoću fastMRI biblioteke

Zadatak:

- Istražiti i opisati način dobivanja dinamičkih MRI slika te problematiku
rekonstrukcije MRI slika. 
- Istražiti i opisati postupak i važnost rekonstrukcije MRI medicinskih 
slika u kliničkoj praksi.
- Dati kratak pregled prethodnih istraživanja. 
- Opisati fastMRI biblioteku za rekonstrukciju medicinskih slika.
- Odabrati metodu implementiranu unutar fastMRI biblioteke za rekonstrukciju
MRI medicinskih slika, opisati je te prilagoditi za zadatak rekonstrukcije MRI
slika mozga.
- Prikazati i komentirati dobivene rezultate.

---

## Izvori:

- https://www.nibib.nih.gov/science-education/science-topics/magnetic-resonance-imaging-mri
- https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3097694/

---

## Istražiti i opisati način dobivanja dinamičkih MRI slika te problematiku rekonstrukcije MRI slika. 

### Uvod

Magnetska rezonancija je često korištena tehnika dobivanja medicinskih slika. Koristi magnetsko polje i radio valove kako bi stvorila detaljne slike mekog tkiva. Ne emitira ionizirajuće zračenje koje se pronalazi kod CT i rendgenskih slika što ga čini sigurnijim. Strojevi koji provode slikanje magnetskom rezonancijom su zapravo veliki magneti. Tako da jedino emitiraju jako magnetsko zračenje. Iz tog razloga se u okolini stroja ne smiju nalaziti feromagnetici. `UMETNI SLIKU I OPIS`. Postupak dobivanja slike može trajati od 15 do 90 minuta. Prilikom postupka, osoba koje se nalazi u stroju mora biti potpuno mirna. Najmanje kretnje i pokreti stvaraju šum i mutnu sliku. S obzirom na dugo trajanje postupka, iskustvo može biti neudobno i klaustrofobično. Također, dugo trajanje postupka znači da nije moguće brzo slikati velik broj ljudi, čime se i cijena postupka povečava. No, zbog sposobnosti prikaza mekog tkiva, magnetska rezonancija nije zamjenjiva drugim metodama poput CT snimanja i rendgenskih snimanja. TIme, smanjenje trajanja magnetske rezonancije je poželjno. Snimanje je moguće obaviti brže, no posljedica toga su mutne slike pune šuma.

Bitna razlika između magnetske rezonancije i ostalih metoda prikupljanja medicinskih slika je ta što je prilikom izvođenja snimanja moguće upravljati prikupljanjem podataka, te time utjecati na konačnu dobivenu sliku. Moguće je prilagoditi prostornu rezolucije, polje pregleda (FOV), kontrast slike, brzinu prikupljanja, artifakte i još dodatne parametre koji pridonose konačnoj slici.

### Način rada magnetske rezonancije

Magnetska rezonancija se temelji na fizikalnoj pojavi nuklearne magnetske rezonancije. U toj pojavi jezgre određenih atoma pokazuju sposobnost upijanja i odašiljanja elektromagnetske energije prilikom stavljanja u magnetsko polje. Ponašaju se kao mali štapičasti magneti, te ukoliko se nalaze u magnetskom polju oni će se poravnati s njim. Zatim, stroj za magnetsku rezonanciju odašilje u njih elektromagnetski puls radio frekvencije, te ih time izbija iz poravnanja s magnetskim poljem. Ovdje djelovanje nuklearne magnetske rezonancije dolazi u utjecaj. Jezgre atoma će se rotirati i time odašiljati rf signal. No, nakon određenog vremena njihova će rotacija stati, te će se ponovno poravnati s magnetskim poljem. Vrijeme da se jezgra atoma prestane rotirati, vrijeme da se ponovno poravna s magnetskim poljem i količina energije koja je ispuštena ovise o kemijskom sastavu molekula. S obzirom na to je moguće razaznati razliku između različitih vrsta tkiva. 

Prethodno navedene mogućnosti prilagodbe prikupljanja podataka tokom snimanja omogućuje k-prostor. K-prostor je proširenje koncepta Fourierovog prostora. Matrica je koja sadrži sirove podatke prikupljene prilikom snimanja magnetskom rezonancijom. 

Kako bi se dobila slika iz k-prostora potrebno je obaviti više koraka procesiranja. Proces transformiranja k-prostora u konačne slike se naziva rekonstrukcija slike.

Sliku iz k-prostora dobivamo Fourierovom tranformacijom. `POGLEDATI ONAJ VIDEO I OPISATI MAL KAK TO SVE IZGLEDA`



Što je k-prostor? K-prostor je matrica amplituda koje predstavljaju prostorne frekvencije magnetske rezonancije. Razlika je u tome što nije u vremenskoj, već u prostornoj domeni. Tako da iumjesto amplitude i vremena na osima se nalaze kx  ky koji predstavljaju fizički prostor. `DODATI POVEZANOSTI IZMEĐU FREKVENCIJE I FAZORA`. Prostorne frekvencije prikazane su crnom i bijelom bojom ovisno o njihovoj amplitudi. Kada je amplituda niska,
sinusoidalni uzorak biva manje naglašen. To se događa jer se raspon svjetline smanjuje kako vrijednosti amplituda 
postaju manje. Zbrajanjem svih prostornih frekvencija dobivamo konačnu sliku. Frekvencije bliže centru imaju 
veće amplitude nego one bliže rubovima slike. To je DC pomak.
