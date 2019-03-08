# WIKI

## HELBURUA

Bi helburu nagusi bereizten ditugu.  

Gure proiektuaren helburu nagusietako bat artistarekin elkar lanean ibiltzea eta koadro dinamikoa bere erakusketara eramatea izango da. 
Bestalde, bigarren helburu nagusia, hemen ikusten duzuen Github plataforman gure proiektuaren dokumentua sortzea izango da eta dokumentu hau edonoren eskura uztea. 
Horrela, guri beste pertsona batzuen proiektuak lagungarri izan zaizkigun bezala, gure proiektua beste pertsona batzuentzat lagungarri izatea gustatuko litzaiguke. 



## MUNTAIAREN PROZEDURA

Muntai prozedurarekin hasteko, arduino  eta serbo batekin hainbat proba egin genituen, proba horien emaitza positiboa lortu ondoren PCA9685[1] txipa arduinora konektatu genuen eta ondoren 16 serboak PCA9685 txipera.

Segidan, Arduinoa erabili ordez ATMega[2] mikrokontrolagailua atera eta PCB[4] plaka bat Proteusen diseinatu  eta honekin batera elikatze iturri plaka bat[3] ere diseinatu genuen plaka eta txip guztiak elikatzeko.

<p align="center">
  <img width="460" height="300" src="https://github.com/endimendizabal/Kuadro-dinamikoa/blob/master/Captura.PNG">
</p>

 <p align="center">1. ATmega proteus eskema

<p align="center">
  <img width="460" height="300" src="https://github.com/endimendizabal/Kuadro-dinamikoa/blob/master/Captura.PNG%202.PNG">
</p>

 <p align="center">2. Elikatze iturri plaka

Honen Ondoren,  Circuitcam programan sartu eta LPKF imprimagailuan imprimitu genituen bi plakak.

 Kontuan izan behar dugu plaka hauek aurpegi batean inprimatuta daudela goiko aldean elementuak jartzeko.
<p align="center">
  <img width="460" height="300" src="https://github.com/endimendizabal/Kuadro-dinamikoa/blob/master/Captura.PNG%203.PNG">
</p>
<p align="center">3. ATmega plaka imprimatuta

<p align="center">
  <img width="460" height="300" src="https://github.com/endimendizabal/Kuadro-dinamikoa/blob/master/Captura.PNG%204.PNG">
</p>
<p align="center"> 4. Elikatze plaka imprimatuta

Bi plaka hauek soldatzean arduino programa egiten hasi ginen eta aldi berean serboak leku finko batean jartzeko aluminiozko txasis bat eraiki genuen.

<p align="center">
  <img width="300" height="400" src="https://github.com/endimendizabal/Kuadro-dinamikoa/blob/master/Captura.PNG%205.PNG">
</p>

<p align="center">5. txasisaren lehenengo prototipoa

Geroago, txukunago eta artistaren nahietara moldatzeko, isis ares programan plano definitibo bat egin genuen erabiliko ditugun pultsadore, led eta sentsore guztien hutsuneak laserrez moztu ahal izateko. 

<p align="center">
  <img width="300" height="400" src="https://github.com/endimendizabal/Kuadro-dinamikoa/blob/master/Captura.PNG%206.PNG">
</p>
<p align="center">
  <img width="300" height="400" src="https://github.com/endimendizabal/Kuadro-dinamikoa/blob/master/Kuadro%20dinamiko%20oinarria.PNG">
</p>

<p align="center">6. IBIL LASER enpresak egindako txasisa

Azkenik  bi plaka, serbo, sakagailu, sensore eta Ledak txasisean jarri eta atzetik beraien konexioa egin genuen. Dena txukun egoteko brida batzuekin kableak lotu genituen.
Kableak ez apurtzeko edo tolesteko atzeko partean metrakilatozko xafla bat jarri genion altuera egoki batean.

<p align="center">
  <img width="460" height="300" src="https://github.com/endimendizabal/Kuadro-dinamikoa/blob/master/Captura.PNG%207.PNG">
</p>

<p align="center">7. Koadroa atzeko partetik muntatu aurretik


## FUNTZIONAMENDUA

Bi funtzionamendu diferente sortu ditugu proiektu honetan.
lehendabizi ikusleak erraz ulertzeko 4 sakagailu jarri ditugu bakoitza led bat eta mugimendu bat edukiko du.
Beste funtzionamendu bat interaktibotasuna handitzeko 2 sensorekin beste mugimendu batzuk egitea izan da.

### PCA9685<sup>1

Plaka honek 16 servoak kontrolatzeko balio du, eta ATMega328p plakara konektatzen da I2C konexioarekin.

### ATmega328p<sup>2

Proiektua karakteristika berezi batzuk dauzka eta honek da horietako bat. Arduino baten ordez erabili dugu bere prozesadorea eta PCB plaka bat diseinatu diogu sarrera irteerak lotzeko.

### Elikatze iturri plaka<sup>3

PCB bat diseinatu egin behar genuen ATmega dagoen PCB plaka eta PCA9685 plaka alimentatzeko, zirkuitu osoa 5 voltiotan alimentatzen dugu. 

### PCB<sup>4

Printed circuit board-eri deritzo ingelesez. Zirkuitu integratuak imprimatzen diren kobreko xaflak dira.

## MARTXAN JARTZEA ETA DOIKETAK

Lehenengo ATMega txipa arduinoarekin konektatu eta programa kargatuko dugu.

Ondoren, ATMega txipa, ATMegarako egin dugun plakan txertatuko dugu.

Gero, PCB elikatze plaka elikatuko dugu. Segundu batzuk itxarongo ditugu eta PCA txiparen led gorria pizten denean prest egongo dela baieztatu dezakegu.

Azkenik, markoan dauden pultsagailuetako bat sakatu ezgero, pultsagailu horri dagokion leda piztu egingo dela ikusiko dugu. Baita pultsagailu bakoitzak programatua duen mugimendua ere.

<p align="center">
  <img width="460" height="300" src="https://github.com/endimendizabal/Kuadro-dinamikoa/blob/master/Captura.PNG%208.PNG">
</p>

<p align="center">8. Koadroa prest eta elikatuta


## AURREKONTUA		

Elementua | Balioa | Kantitatea | Prezioa Unitateko | Balio totala €-tan
------------ | ------------ | ------------- | ------------- | -------------
Servo | 3V-7,3V | 32 | 2,29€ | 91,96€
PCA | 3,3V-6V | 2 | 2,55€ | 5,10€
ATmega | 1,8-5V | 2 | 3,03€ | 6,06€
Konektorea | 300V 16A | 12 | 0,28€ | 3,36€
Elikatze iturria | IN 230V OUT 5V 2,5A | 2 | 7,69€ | 15,38€
Erresistentziak | 220 ohm | 16 | 0,02€ | 4,01€
PCB xafla | Aurpegi bat | 2 | 0,59€ | 10,99€
Sensorea | 5V | 4 | 0,92€ | 4,60€
Led | 1,8V-2V | 8 | 0,06€ | 5,99€
Sakagailua | 250V/5A | 8 | 4,01€ | 32,08€
Elementua | Lana | Orduak | Prezioa orduko | Guztira
M.O. | Hardware & Software | 90 | 8€ | 720€
 | | | | Totala: | 899,53€

## KONKLUSIOAK/ONDORIOAK

### Akatsak:
- Erosi genuen serbo batzuk eta tope batzuk kentzen izorratu genitun.
- txasis bat egin genuen aluminioarekin eta txukunago eta hobeto egoteko proteusen plano bat egin genuen baino oso fina atera zen azkenean.
- sakagailu gehiago behar genituen eta plaka berriro aldatu eta inprimatu  behar genuen.
- elikatze plakan zuloak txikiegi geratu ziren eta plaka berriro egin genuen zuloak bat egiteko.


## ERREFERENTZIAK
ATmegaren konexioak begiratzeko erabili genuen web-a

PCA konexioak jakiteko erabili dugun web-a
