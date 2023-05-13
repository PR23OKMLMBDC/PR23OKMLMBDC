# Razmerje Slovencev z avtomobili
Oskar Kocjančič, Miha Lazić, Matija Bajt, David Čadež

## Opis problema
V današnjem svetu je vloga avtomobila pomembna kot še nikoli prej. Vsako jutro se usedemo v avto in odpeljemo v službo, v trgovino, na obisk k sorodnikom, pripeljemo nazaj domov, potem pa spet nekam drugam. Človek si življenja brez njega enostavno ne more več predstavljati.  
Pri tem problemu ne zaostajamo niti mi, Slovenci, saj [statistika](https://siol.net/avtomoto/novice/peto-mesto-v-evropi-tako-odvisni-smo-slovenci-od-avtomobilov-544642) pravi, da  po slovenskih cestah vozi kar 598 avtomobilov na 1000 ljudi, kar nas uvršča na samo peto mesto izmed vseh članic Evropske unije.
Iz zgornjega dejstva lahko sklepamo, da med Slovencem in njegovim avtomobilom obstaja neko razmerje, ki smo ga poskušali na najrazličnejše načine analizirati.

## Opis podatkov
Osnova projektne naloge je bila [**Evidenca registriranih vozil**](https://podatki.gov.si/dataset/evidenca-registriranih-vozil-presek-stanja), ki vsebuje malo morje podatkov o vseh registriranih vozilih *(znamka, število prevoženih kilometrov, moč motorja, ...)* v določenem časovnem obdobju.

Za nas so bili relavantni najaktualnejši podatki, in sicer 2 `.zip` datoteki s podatki o registriranih vozilih iz leta 2022:
- *Vozila_OPSI_30062022*
- *Vozila_OPSI_31.12.2022*

Datoteki vsebujeta vsaka po 3 `.csv` datoteke, kjer ima vsaka cca. 650 000 vrstic in 99 stolpcev, kjer vrstica predstavlja registrirano vozilo, stolpec pa atribut pri registraciji. Za naš projekt smo od vrstic izluščili **avtomobile**, od stolpcev pa naslednje **atribute**:
- *B-Datum prve registracije vozila*
- *C13-Obcina uporabnika vozila (opis)*
- *C2-Starost lastnika vozila*
- *D1-Znamka*
- *J-Kategorija in vrsta vozila (opis)*
- *P12-Nazivna moc*
- *Prevozeni kilometri milje*

Za potrebe vizualizacije smo uporabili datoteko [**obcine.geojson**](https://github.com/stefanb/gurs-rpe/blob/master/data/OB.geojson) za izris občinskih mej in datoteko [**obcine.csv**](https://github.com/stefanb/gurs-rpe/blob/master/data/OB.csv) za rešitev problema s poimenovanjem občin, ki je opisan spodaj.

## Analiza

Najprej smo izbrane stolpce in vrstice prebrali v `Pandas DataFrame`. Želeli smo podatke grupirati po občinah, da bi podatke lažje vizualizirali na zemljevidu. Naleteli smo na težavo s kodiranjem, natančneje s črko `č` ki je bila predstavljena kot `c`, hkrati pa je bilo poimenovanje štirih občin napačno. To je predstavljalo problem, saj se podatki niso izrsiali na zeljevidu (zaradi napačnega imena občine v datoteki obcine.geojson). Težavo smo rešili s **slovarjem preslikav**, kjer ključ predstavlja preslikavo na pravilno ime občine. Sledila je priprava petih vizualizacij, ki so opisane v spodnjih poglavjih.

## Rezultati

Ker smo podatke grupirali po občinah, je bila najboljša oblika vizualizacije **Choropleth zemljevid**, ki se nahaja v orodju `Folium`.

### Povprečna starost lastnika avtomobila

![image](https://user-images.githubusercontent.com/75141731/232854168-3487c3d0-a9bb-4a07-9316-69f0f014409d.png)

Občina z najvišjo povprečno starostjo lastnika avtomobila je občina Šempeter-Vrtojba, s povprečno starostjo `54.99` leta. 
Občina z najnižjo povprečno starostjo lastnika avtomobilav je občina Cerkvenjak, s povprečno starostjo `47.16` leta. 

### Popularna znamka avtomobila

![image](https://user-images.githubusercontent.com/75141731/232854272-abefee86-967d-4372-a943-06608b4e481c.png)

### Povprečna starost avtomobila

![image](https://user-images.githubusercontent.com/75141731/232854462-5529f909-40e9-4c74-93d8-bf714e384096.png)

Občina z najvišjo povprečno starostjo avtomobila je občina Kanal, s povprečno starostjo `14.33` leta. 
Občina z najnižjo povprečno starostjo avtomobila je občina Trzin, s povprečno starostjo `9.5` leta.

### Povprečna moč avtomobila

![image](https://user-images.githubusercontent.com/75141731/232854740-ad682c62-974a-405b-919d-b1e1f58773c5.png)

Občina z najbolj močnimi avtomobili je občina Trzin, kjer ima avtomobil povprečno `127.89` konjskih moči. 
Občina z najšibkejšimi avtomobili je občina Kobilje, kjer ima avtomobil povprečno `103.13` konjskih moči.

### Povprečno število prevoženih kilometrov

![image](https://user-images.githubusercontent.com/75141731/232854914-596a5867-eddd-405a-84be-5dc83962355a.png)

Občina z največ povprečno prevoženimi kilometri je občina Zavrč, kjer posameznik v povprečju prevozi `228035.24` kilometrov s svojim jeklenim konjičkom.
Občina z najmanj povprečno prevoženimi kilometri je občina Trzin, kjer posameznik v povprečju prevozi `145868.85` kilometrov s svojim jeklenim konjičkom.


## Ugotovitve
Ugotavljali smo najrazličnejše razloge za določeno porazdelitev barv na  posameznem zemljevidu. Prišli smo do zanimivih ugotovitev.


### Povprečna starost lastnika avtomobila
 
Iz zgornje vizualizacije lahko razberemo, da se najstarejši vozniki nahajajo na Primorskem. Najverjetnejši razlog je slabo urejen javni prevoz, kar primore k temu, da so starejši Slovenci primorani se voziti z avtom.

### Popularna znamka avtomobila

Najpopularnejša znamka avtomobila v Sloveniji je `Volkswagen`. Najverjetneje zaupanje tej znamki izhaja iz časov Jugoslavije, ko je po slovenskih cestav vozil Golf. Sledi ji francoski `Renault`, ki ga radi vozijo vozniki iz Novega mesta in okolice, kjer se nahaja proizvodnja le-tega. Osamelca sta občini Trzin in Podvelka, kjer prevladuje znamka `BMW` in `Ford`. 

### Povprečna starost avtomobila

Povprečna starost avtomobilov po eni strani nakazuje, kateri vozniki so najboljši, saj avtomobil mora biti redno vzdrževan in lepo vožen, da doseže visoko starost. Najboljši vozniki so po podatkih na `Primorskem`, kjer je tudi najvišja starost lastnika avtomobila, medtem ko najnižja starost avtomobila je pri voznikih iz `Notranjske` (najbrž ne zaradi slabih voznih sposobnosti:)).


### Povprečna moč avtomobila

Iz vizualizacije je razvidno, da Slovenci, ki živijo v "bogatejših" in "strmejših" regijah vozijo močnejše avtomobile. To so občine iz `Notranjske` in `Koroške`. Zanimivo je, da se Povprečna moč avtomobila občine `Trzin` sovpada s popularno znamko (BMW).

### Povprečno število prevoženih kilometrov

Vizualizacija razkriva, da se Slovenci iz manj razvitih krajev dnevno vozijo na delo v oddaljena mesta. Za razliko od le-teh je videti, da Slovenci, ki živijo v razvitejši mestih ne toliko vozijo z avtomobilom na dnevni bazi, temveč raje uporabijo javni prevoz.
