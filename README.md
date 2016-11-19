# Tanuló Adminisztrációs Rendszer (TAR)
#### Készítette: Szántó Attila

##1. Követelményanalízis

###1.1. Célkitűzés, projektindító dokumentum

A program legfőbb célja, hogy jól átláthatóan, és egyértelműen nyomon követhető legyen a kutyaiskola tanulói, és kutyáik egy webes vastagkliens, azaz egyoldali alkalmazás felhasználásával. Az adatok védelme érdekében legyen lehetőség regisztrációra, majd bejelentkezésre. Két felhasználó típus létezik, tanuló és oktató. Ezek közül, csak tanuló típusú felhasználó regisztrálható        

###Funkcionális követelmények:

1.	Regisztráció
2.	Bejelentkezés
3.	Minden bejelentkezett felhasználó által elérhető funkciók
  1. rögzített adatok megtekintése
4.	Csak bejelentkezett „oktató” típusú felhasználók által elérhető funkciók
  1.	új tanuló felvitele
  2.	új kutya felvitele
  3.	meglévő tanuló szerkesztése
  4.	meglévő kutya szerkesztése
  5.	meglévő tanuló törlése
  6.	meglévő kutya törlése

###Nem funkcionális követelmények:

1. Könnyű áttekinthetőség: Színekkel típus szerint csoportosítás
2. Használhatóság: Könnyű áttekinthetőség, ésszerű elrendezés, könnyen kezelhetőség
3. Megbízhatóság: jelszóval védett funkciók, és a jelszavak védelme a háttérben. Hibásan bevitt adatok esetén a program jól láthatóan jelezzen a felhasználónak, és emelje ki a hibás beviteli mezőket. A jól bevitt adatok maradjanak az űrlapban.
4. Karbantarthatóság: könnyen lehessen bővíteni, a különböző típusú fájlok külön csoportosítva, ésszerűen legyenek felbontva, a könnyebb fejleszthetőség miatt

###1.2. Szakterületi fogalomjegyzék

1. Oktató: A kutya képzéséért és az adatok karbantartásáért felel
2. Tanuló: Az oktatásra járó kutya gazdája
3. Kutya: Az oktatásra járó kutya

###1.3. Használatieset-modell, funkcionális követelmények

####Vendég: Csak a publikus oldalakat éri el

1. Főoldal
2. Bejelentkezés
3. Regisztráció

####Bejelentkezett felhasználó (tanuló): A publikus oldalak elérésén felül egyéb funkciókhoz is hozzáfér.

1. Tanulók listája
2. Kutyák listája
3. Tanulói adatlap
4. Kutya adatlap

####Bejelentkezett felhasználó (oktató): A publikus oldalak és a „tanuló” típusú felhasználó elérésén felül egyéb funkciókhoz is hozzáfér.

1. Új tanuló felvitele
2. Új kutya felvitele
3. Meglévő tanuló szerkesztése
4. Meglévő kutya szerkesztése
5. Meglévő tanuló törlése
6. Meglévő kutya törlése

![Kép felirata](docs/images/uml.jpg)

Vegyünk példának egy egyszerű folyamatot:

####Meglévő tanuló szerkesztése:

1.	A felhasználó az oldalra érkezve, bejelentkezik egy oktató jogkörrel rendelkező felhasználóval
2.	Regisztráció után megtekintheti a tanulókat listázó oldalt, ahol kiválaszthatja a szerkeszteni kívánt tanulót.
3.	Megnyomja a „Megtekintés” feliratú gombot
4.	A megtekintés oldalon kiválaszthatja a „Szerkesztés” gombot
5.	Szerkesztés oldalon felviszi az új adatokat
6.	Submit gombra kattintva elmenti a változásokat

![Kép felirata](docs/images/workflow.jpg)

##2. Tervezés

###2.1. Architektúra terv

####2.1.1. Komponensdiagram
        
![Kép felirata](docs/images/modela.png)

####2.1.2. Oldaltérkép:
#####Publikus:
1. Főoldal
2. Bejelentkezés
3. Regisztráció

#####Bejelentkezett (tanuló):
1. Főoldal
2. Tanuló listaoldal
	1. Tanuló adatlap
3. Kutya listaoldal
	1. Kutya adatlap

#####Bejelentkezett (oktató):
1. Főoldal
2. Tanuló listaoldal
	1. Új 
	2. Adatlap
		1. Törlés
		2. Szerkesztés
3. Kutya listaoldal
	1. Új 
	2. Adatlap
		1. Törlés
		2. Szerkesztés

####2.1.3. Végpontok
1. GET/: főoldal
2. GET/login: bejelentkező oldal
3. POST/login: bejelentkező adatok felküldése
4. GET/login/signup: regisztrációs oldal
5. POST/login/signup: regisztrációs adatok felküldése
6. GET/logout: kijelentkező oldal
7. GET/student/list: tanulólista oldal
8. GET/student/new: új tanuló felvétele
9. POST/student/new: új tanuló felvételéhez szükséges adatok felküldése
10. GET/student/id: tanuló adatok
11. GET/student/delete=id: tanuló törlése
12. GET/student/edit=id: tanuló módosítása
13. POST/student/edit=id: tanuló módosítása, adatok felküldése
14. GET/dog/list: kutyalista oldal
15. GET/dog/new: új kutya felvétele
16. POST/dog/new: új kutya felvételéhez szükséges adatok felküldése
17. GET/dog/id: kutya adatok
18. GET/dog/delete=id: kutya törlése
19. GET/dog/edit=id: kutya módosítása
20. POST/dog/edit=id: kutya módosítása, adatok felküldése

###2.2. Felhasználói-felület modell

####2.2.1.Oldalvázlatok:

#####Főoldal

![Kép felirata](docs/images/maina.png) 

#####Regisztrációs oldal

![Kép felirata](docs/images/reg.png) 

#####Bejelentkező  oldal

![Kép felirata](docs/images/login.png) 

#####Példa listázó

![Kép felirata](docs/images/tanlist.png)

#####Új tanuló felvétele

![Kép felirata](docs/images/newTan.png)

#####Tanuló megtekintése

![Kép felirata](docs/images/tanAdat.png)

#####Tanuló szerkesztése     

![Kép felirata](docs/images/editTan.png)

####2.2.3. Dinamikus működés

#####Szekvenciadiagram

![Kép felirata](docs/images/seqgiag.png)

#####Vegyünk példának a regisztrációt, majd egy új elem felvételét, szerkesztését, törlését, mindezt szekvenciadiagrammon.
 
###3. Implementáció

#####3.1.1. Fejlesztőkörnyezet

IDE: VS Code

1. Github account szükséges
2. Belépés után új workspace létrehozása (node.js)
3. Ezután elkezdhetjük a kód írását
4. git add paranccsal kiválaszthatunk egy fájlt verzionálásra, vagy git add . paranccsal az összes fájlt kiválaszthatjuk
5. git commit -m "commit" paranccsal feltehetjük a fájlokat a cloud9 helyi tárolójába. Az így megjelölt verziókhoz a későbbiekben visszatérhetünk, különbségüket megtekinthetjük.
6. git push origin master paranccsal a lokális tárolóból feltölthetjük a tartalmat a Github-ra.
7. Végezetül a Github oldalán leellenőrizhetjük a munkánkat.

###6. Irodalomjegyzék:

http://webprogramozas.inf.elte.hu/alkfejl.php

http://ade.web.elte.hu/wabp/lecke2_lap1.html

http://webprogramozas.inf.elte.hu/alkfejl/A_dokumentacio_felepitese.pdf

\ No newline at end of file





