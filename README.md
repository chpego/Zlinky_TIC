
# ZLinky_TIC
 Téléinformation Linky autoalimenté communiquant en ZigBee 3.0  
 vous pouvez vous procurer le ZLinky_TIC à l'adresse suivante :  
 [Boutique LiXee](https://lixee.fr/)
 

## Description
![Description ZLinky_TIC](https://github.com/fairecasoimeme/Zlinky_TIC/blob/master/Doc/Images/ZLinky_description.JPG)
<img src="https://github.com/fairecasoimeme/Zlinky_TIC/blob/master/Doc/Images/ZLinky_prototype.jpg" width="400">

## PCB
<img src="https://github.com/fairecasoimeme/Zlinky_TIC/blob/master/Doc/Images/ZLinky_PCB_face.jpg" width="800">
<img src="https://github.com/fairecasoimeme/Zlinky_TIC/blob/master/Doc/Images/ZLinky_PCB_pile.jpg" width="800">

**ZLinky_TIC** est un appareil permettant de transmettre toutes les informations du Linky en ZigBee 3.0.  
**ZLinky_TIC** est alimenté par votre compteur Linky. Il suffit simplement d'enlever le cash (jaune fluo) et de "plugger" l'appareil en pressant sur le bouton orange.  
Au départ, **ZLinky_TIC** est en attente d'appairage mais si vous souhaitez réinitialiser l'appareil, il suffit de rester appuyer sur le bouton "link" pendant 10 secondes. Ensuite, le bouton relâché, la Led s'éteint puis se mettre à clignoter.  
Une fois appairé à votre box domotique par l'intermédiaire d'une ZiGate ou d'un autre coordinateur ZigBee, vous pourrez gérer votre consommation d'électricité.

**Actuellement, l'appareil fonctionne avec le mode Historique et standard du compteur Linky.**  
**Il permet de gérer tous les abonnements en mono ou triphasé et le mode production (uniquement en mode standard)**  

## Installation
Suivre les instructions suivantes :
* Retirer le capot vert du Linky
* Insérer le *ZLinky_TIC* en appuyant sur le bouton au-dessus

<img src="https://github.com/fairecasoimeme/Zlinky_TIC/blob/master/Doc/Images/installation_ZLinky_TIC.png" width="600">  

PS: L'image et l'emplacement des bornes I1 I2 et A peuvent varier en fonction de la marque du Linky

## Voyant lumineux

L'appareil clignote 4 fois. Zlinky_TIC rencontre des erreurs lors de l'acquisition des données du Linky.  
<img src="https://github.com/fairecasoimeme/Zlinky_TIC/blob/master/Doc/Images/manuel_LED_cycle_error.png" width="200">  

La LED de l'appareil reste fixe : Le ZLinky_TIC fonctionne correctement. L'appareil décode correctement le Linky  
<img src="https://github.com/fairecasoimeme/Zlinky_TIC/blob/master/Doc/Images/manuel_LED_send_datas.png" width="200">  

## Clusters

### Clusters List

|Num (Hexa)|Name|I/O| Comment|
|----------|----|---|--------|  
|0x0000|Basic|I||
|0x0003|Identify|I||
|0x0702|Simple Metering|I||
|0x0B01|Meter Identification|I||
|0x0B04|Electric measurement|I||
|0xFF66|LiXee Private|I||
|0x0019|OTA|O|Not used yet|

### Basic Cluster (0x0000)

|attribut|Name|Value|
|------|----------|------|
|0x0000|ZCLVersion|0x0003|  
0x0001 | ApplicationVersion|0x0001|  
0x0002 | StackVersion|0x0002|
0x0003 | HWVersion|0x0001|
0x0004 | ManufacturerName|LiXee|
0x0005 | ModelIdentifier|ZLinky_TIC|
0x0006 | DateCode|20210401|
0x0007 | PowerSource|0x03|
0x4000 | SWBuildID|4000-0001|

### Subscription (OPTARIF Values)

#### Mode historique  
![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) BASE  
![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) HC..  
![#c56615](https://via.placeholder.com/15/c56615/000000?text=+) EJP.  
![#1589F0](https://via.placeholder.com/15/1589F0/000000?text=+) BBRx  


RO= READ only RP= Reportable / RW = Read/Write	

|Commande TIC|CLUSTER|Attribut|Droit|Comment|data type|size max|unit|designation|valeur par defaut|
|------------|-------|--------|-----|--------------|---------|-------|----|-----------|------------|				
|ADC0|0x0702|0x0308|RO||String|12 car|-|	Serial Number|NULL|
|![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) BASE|0x0702|0x0000|RP||Uint32|9 car|Wh| Index Base|0|
|OPTARIF			|0xFF66|	0x0000|		RO||String|4 car|-| Option tarifaire|BASE|	
|ISOUSC			|0x0B01	|0x000D		|RO		||Uint16|2 car|A| Intensité souscrite|0|
|![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) HCHC			|0x0702	|0x0100		|RO			||Uint32|9 car|Wh|Index HCHC|0|
|![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) HCHP			|0x0702	|0x0102		|RO			||Uint32|9 car|Wh|Index HCHP|0|
|![#c56615](https://via.placeholder.com/15/c56615/000000?text=+) EJPHN			|0x0702	|0x0100		|RO			||Uint32|9 car|Wh|Index EJPHN|0|
|![#c56615](https://via.placeholder.com/15/c56615/000000?text=+) EJPHPM			|0x0702	|0x0102		|RO			||Uint32|9 car|Wh|Index EJPHPM|0|
|![#1589F0](https://via.placeholder.com/15/1589F0/000000?text=+) BBRHCJB			|0x0702	|0x0100		|RO			||Uint32|9 car|Wh|Index BBRHCJB|0|
|![#1589F0](https://via.placeholder.com/15/1589F0/000000?text=+) BBRHPJB			|0x0702	|0x0102		|RO			||Uint32|9 car|Wh|Index BBRHPJB|0|
|![#1589F0](https://via.placeholder.com/15/1589F0/000000?text=+) BBRHCJW			|0x0702	|0x0104		|RO			||Uint32|9 car|Wh|Index BBRHCJW|0|
|![#1589F0](https://via.placeholder.com/15/1589F0/000000?text=+) BBRHPJW			|0x0702	|0x0106		|RO			||Uint32|9 car|Wh|Index BBRHPJW|0|
|![#1589F0](https://via.placeholder.com/15/1589F0/000000?text=+) BBRHCJR			|0x0702	|0x0108		|RO			||Uint32|9 car|Wh|Index BBRHCJR|0|
|![#1589F0](https://via.placeholder.com/15/1589F0/000000?text=+) BBRHPJR			|0x0702	|0x010A		|RO			||Uint32|9 car|Wh|Index BBRHPJR|0|
|IINST			|0x0B04	|0x0508		|RP			||Uint16|3 car|A|Courant efficace|0xFFFF|
|IINST1			|0x0B04	|0x0508		|RP			|Triphasé|Uint16|3 car|A|Courant efficace phase 1|0xFFFF|
|IINST2			|0x0B04	|0x0908		|RP			|Triphasé|Uint16|3 car|A|Courant efficace phase 2|0xFFFF|
|IINST3			|0x0B04	|0x0A08		|RP			|Triphasé|Uint16|3 car|A|Courant efficace phase 3|0xFFFF|
|IMAX			|0x0B04	|0x050A		|RO			||Uint16|3 car|A|Intensité maximale|0xFFFF|
|IMAX1			|0x0B04	|0x050A		|RO			|Triphasé|Uint16|3 car|A|Intensité maximale phase 1|0xFFFF|
|IMAX2			|0x0B04	|0x090A		|RO			|Triphasé|Uint16|3 car|A|Intensité maximale phase 2|0xFFFF|
|IMAX3			|0x0B04	|0x0A0A		|RO			|Triphasé|Uint16|3 car|A|Intensité maximale phase 3|0xFFFF|
|PMAX			|0x0B04	|0x050D		|RO			|Triphasé|Uint16|5 car|W|Puissance maximale triphasée atteinte|0x8000|
|PAPP			|0x0B04	|0x050F		|RP			|Triphasé|Uint16|5 car|VA|Puissance apparente|0xFFFF|
|PTEC			|0x0702	|0x0020		|RO	||String|4 car|-|Periode tarifaire en cours|NULL|				
|![#1589F0](https://via.placeholder.com/15/1589F0/000000?text=+) DEMAIN			|0xFF66	|0x0001		|RP||String|4 car|-|Couleur du lendemain|NULL|
|HHPHC			|0xFF66	|0x0002		|RO||Uint8|1 car|-|Horaire Heure Pleines Heures Creuses|0|
|PPOT 			|0xFF66	|0x0003		|RO|Triphasé|Uint8|2 car|-| Présence des potentiels|0|
|![#c56615](https://via.placeholder.com/15/c56615/000000?text=+) PEJP			|0xFF66	|0x0004		|RP||Uint8|2 car|Min|Préavis début EJP(30min)|0|
|ADPS			|0xFF66	|0x0005		|RP||Uint16|3 car|A|Avertissement de Dépassement De Puissance Souscrite|0|
|ADIR1			|0xFF66	|0x0006		|RP|Triphasé|Uint16|3 car|A|Avertissement de Dépassement D'intensité phase 1|0|
|ADIR2			|0xFF66	|0x0007		|RP|Triphasé|Uint16|3 car|A|Avertissement de Dépassement D'intensité phase 2|0|
|ADIR3			|0xFF66	|0x0008		|RP|Triphasé|Uint16|3 car|A|Avertissement de Dépassement D'intensité phase 3|0|

#### Mode standard
|Commande TIC|CLUSTER|Attribut|Droit|Comment|data type|size max|unit|designation|valeur par defaut|
|------------|-------|--------|-----|--------------|---------|-------|----|-----------|------------|				
|ADSC|0x0702|0x0308|RO||String|12 car|-|	Adresse Secondaire du Compteur|NULL|
|NGTF|0xFF66|	0x0000|		RO||String|16 car|-| Nom du calendrier tarifaire fournisseur|-|	
|LTARF|0xFF66|	0x0200|		RO||String|16 car|-| Libellé tarif fournisseur en cours|-|	
|NTARF|0xFF66|	0x0201|		RO||Uint8|2 car|-| Numéro de l’index tarifaire en cours|-|	
|VTIC|0xB01|	0x000A|		RO||Uint16|2 car|-| Version de la TIC|-|	
|DATE|0xFF66|	0x0202|		RO||String|10 car|-| Date et heure courant|EX: E211022162000 |	
|EAST|0x702|	0x0000|		RP||Uint32|9 car|Wh| Energie active soutirée totale|0 |	
|EASF01|0x702|	0x0100|		RP||Uint32|9 car|Wh| Energie active soutirée Fournisseur, index 01|0 |	
|EASF02|0x702|	0x0102|		RP||Uint32|9 car|Wh| Energie active soutirée Fournisseur, index 02|0 |	
|EASF03|0x702|	0x0104|		RP||Uint32|9 car|Wh| Energie active soutirée Fournisseur, index 03|0 |	
|EASF04|0x702|	0x0106|		RP||Uint32|9 car|Wh| Energie active soutirée Fournisseur, index 04|0 |	
|EASF05|0x702|	0x0108|		RP||Uint32|9 car|Wh| Energie active soutirée Fournisseur, index 05|0 |	
|EASF06|0x702|	0x010A|		RP||Uint32|9 car|Wh| Energie active soutirée Fournisseur, index 06|0 |	
|EASF07|0x702|	0x010C|		RP||Uint32|9 car|Wh| Energie active soutirée Fournisseur, index 07|0 |	
|EASF08|0x702|	0x010E|		RP||Uint32|9 car|Wh| Energie active soutirée Fournisseur, index 08|0 |	
|EASF09|0x702|	0x0110|		RP||Uint32|9 car|Wh| Energie active soutirée Fournisseur, index 09|0 |	
|EASF10|0x702|	0x0112|		RP||Uint32|9 car|Wh| Energie active soutirée Fournisseur, index10|0 |	
|EASD01|0xFF66|	0x0203|		RP||Uint32|9 car|Wh| Energie active soutirée Distributeur, index 01|0 |	
|EASD02|0xFF66|	0x0204|		RP||Uint32|9 car|Wh| Energie active soutirée Distributeur, index 02|0 |	
|EASD03|0xFF66|	0x0205|		RP||Uint32|9 car|Wh| Energie active soutirée Distributeur, index 03|0 |	
|EASD04|0xFF66|	0x0206|		RP||Uint32|9 car|Wh| Energie active soutirée Distributeur, index 04|0 |	
|EAIT|0x702|	0x0001|		RP|Production|Uint32|9 car|Wh| Energie active injectée totale|0 |	
|ERQ1|0xB04|	0x0305|		RP|Production|int16|9 car|VArh| Energie réactive Q1 total|0 |	
|ERQ2|0xB04|	0x050E|		RP|Production|int16|9 car|VArh| Energie réactive Q2 total|0 |	
|ERQ3|0xB04|	0x090E|		RP|Production|int16|9 car|VArh| Energie réactive Q3 total|0 |	
|ERQ4|0xB04|	0x0A0E|		RP|Production|int16|9 car|VArh| Energie réactive Q4 total|0 |	
|IRMS1|0xB04|	0x0508|		RP|mono / triphasé|Uint16|3 car|A| Courant efficace, phase 1|0 |	
|IRMS2|0xB04|	0x0908|		RP|Triphasé|Uint16|3 car|A| Courant efficace, phase 21|0 |	
|IRMS3|0xB04|	0x0A08|		RP|Triphasé|Uint16|3 car|A| Courant efficace, phase 3|0 |	
|URMS1|0xB04|	0x0505|		RP|mono / triphasé|Uint16|3 car|V|Tension efficace, phase 1|0 |	
|URMS2|0xB04|	0x0905|		RP|Triphasé|Uint16|3 car|V| Tension efficace, phase 2|0 |	
|URMS3|0xB04|	0x0A05|		RP|Triphasé|Uint16|3 car|V| Tension efficace, phase 3|0 |	
|PREF|0xB01|	0x000D|		RO||Uint16|2 car|kVA| Puissance app. de référence (PREF)|0 |	
|STGE|0xFF66|	0x0217|		RO||String|8 car|-| Registre de Statuts|0 |	
|PCOUP|0xB01|	0x000E|		RO||Uint8|2 car|kVA| Puissance app. de coupure (PCOUP)|0 |	
|SINSTI|0xFF66|	0x0207|		RP|Production|Uint16|5 car|VA| Puissance app. Instantanée injectée|0 |	
|SMAXIN|0xFF66|	0x0208|		RP|Production|int16|5 car|VA| Puissance app max. injectée n|0 |	
|SMAXIN-1|0xFF66|	0x0209|		RO|Production|int16|5 car|VA| Puissance app max. injectée n-1|0 |	
|CCASN|0xB04|	0x050B|		RP||int16|5 car|W| Point n de la courbe de charge active soutirée|0 |	
|CCASN-1|0xB04|	0x090B|		RP||int16|5 car|W| Point n-1 de la courbe de charge active soutirée|0 |	
|CCAIN|0xFF66|	0x0210|		RP|Production|int16|5 car|W| Point n de la courbe de charge active injectée|0 |	
|CCAIN-1|0xFF66|	0x0211|		RO|Production|int16|5 car|W| Point n-1 de la courbe de charge active injectée|0 |	
|UMOY1|0xB04|	0x0511|		RP|mono / triphasé|Uint16|3 car|V|Tension moy. ph. 1|0 |	
|UMOY2|0xB04|	0x0911|		RP|Triphasé|Uint16|3 car|V| Tension moy. ph. 2|0 |	
|UMOY3|0xB04|	0x0A11|		RP|Triphasé|Uint16|3 car|V| Tension moy. ph. 3|0 |	
|SINSTS|0xB04|	0x050F|		RP||Uint16|5 car|VA|Puissance app. Instantanée soutirée|0 |	
|SINSTS1|0xB04|	0x050F|		RP|Triphasé|Uint16|5 car|VA| Puissance app. Instantanée soutirée ph.1|0 |	
|SINSTS2|0xB04|	0x090F|		RP|Triphasé|Uint16|5 car|VA| Puissance app. Instantanée soutirée ph. 2|0 |	
|SINSTS3|0xB04|	0x0A0F|		RP|Triphasé|Uint16|5 car|VA| Puissance app. Instantanée soutirée ph. 3|0 |	
|SMAXN|0xB04|	0x050D|		RP||int16|5 car|VA|Puissance app. max. soutirée n|0 |	
|SMAXN1|0xB04|	0x050D|		RP|Triphasé|int16|5 car|VA| Puissance app. max. soutirée n ph.1|0 |	
|SMAXN2|0xB04|	0x090D|		RP|Triphasé|int16|5 car|VA| Puissance app. max. soutirée n ph. 2|0 |	
|SMAXN3|0xB04|	0x0A0D|		RP|Triphasé|int16|5 car|VA| Puissance app. max. soutirée n ph. 3|0 |	
|SMAXN-1|0xFF66|	0x0212|		RO||int16|5 car|VA|Puissance app. max. soutirée n-1|0 |	
|SMAXN1-1|0xFF66|	0x0212|		RO|Triphasé|int16|5 car|VA| Puissance app. max. soutirée n-1 ph.1|0 |	
|SMAXN2-1|0xFF66|	0x0213|		RO|Triphasé|int16|5 car|VA| Puissance app. max. soutirée n-1 ph. 2|0 |	
|SMAXN3-1|0xFF66|	0x0214|		RO|Triphasé|int16|5 car|VA| Puissance app. max. soutirée n-1 ph. 3|0 |	
|MSG1|0xFF66|	0x0215|		RO||String|32 car|-| Message court|0 |	
|MSG2|0xFF66|	0x0216|		RO||String|16 car|-| Message ultra court|0 |	
|PRM|0x702|	0x0307|		RO||String|14 car|-| PRM|0 |	
|DPM1|0xFF66|	0x0218|		RO||Uint8|2 car|-| Début Pointe Mobile 1|0 |	
|FPM1|0xFF66|	0x0219|		RO||Uint8|2 car|-| Fin Pointe Mobile 1|0 |	
|DPM2|0xFF66|	0x0220|		RO||Uint8|2 car|-| Début Pointe Mobile 2|0 |	
|FPM2|0xFF66|	0x0221|		RO||Uint8|2 car|-| Fin Pointe Mobile 2|0 |	
|DPM3|0xFF66|	0x0222|		RO||Uint8|2 car|-| Début Pointe Mobile 3|0 |	
|FPM3|0xFF66|	0x0223|		RO||Uint8|2 car|-| Fin Pointe Mobile 3|0 |	
|RELAIS|0xFF66|	0x0224|		RO||Uint16|3 car|-| RELAIS|0 |	
|NJOURF|0xFF66|	0x0225|		RO||Uint8|2 car|-| Numéro du jour en cours calendrier fournisseur|0 |	
|NJOURF+1|0xFF66|	0x0226|		RO||Uint8|2 car|-| Numéro du prochain jour calendrier fournisseur|0 |	
|PJOURF+1|0xFF66|	0x0227|		RO||String|98 car|-|Profil du prochain jour calendrier fournisseur|0 |	
|PPOINTE1|0xFF66|	0x0228|		RO||String|98 car|-|Profil du prochain jour de pointe|0 |	

### Synthèse développeur
|Fonctions|CLUSTER|Attribut|
|---------|-------|--------|
|Standard : EAIT (Production)|0x0702|0x0001|
|Histo : PTEC|0x0702|0x0020|
|Histo : <br>- HCHC<br>- BASE<br>- EJPHN<br>- BBRHCJB<br>Standard :<br>- EASF01 |0x0702|0x0100|
|Histo : <br>- HCHP<br>- EJPHPM<br>- BBRHPJB<br>Standard :<br>- EASF02 |0x0702|0x0102|
|Histo : <br>- BBRHCJW<br>Standard :<br>- EASF03 |0x0702|0x0104|
|Histo : <br>- BBRHPJW<br>Standard :<br>- EASF04 |0x0702|0x0106|
|Histo : <br>- BBRHCJR<br>Standard :<br>- EASF05 |0x0702|0x0108|
|Histo : <br>- BBRHPJR<br>Standard :<br>- EASF06 |0x0702|0x010A|
|Standard : EASF07 |0x0702|0x010C|
|Standard : EASF08 |0x0702|0x010E|
|Standard : EASF09 |0x0702|0x0110|
|Standard : EASF10 |0x0702|0x0112|
|Standard : PRM|0x0702|0x0307|
|Histo : <br>- ADC0<br>Standard : <br>- ADSC|0x0702|0x0308|
|Standard: VTIC|0x0B01|0x000A|
|Histo : <br>- ISOUSC<br> Standard :<br>- PREF|0x0B01|0x000D|
|Standard: PCOUP|0x0B01|0x000E|
|Histo: <br>- IINST<br>- IINST1 (Triphasé)<br>Standard :<br>- IRMS1|0x0B04|0x0508|
|Histo: <br>- IINST2 (Triphasé)<br>Standard :<br>- IRMS2 (Triphasé)|0x0B04|0x0908|
|Histo: <br>- IINST3 (Triphasé)<br>Standard :<br>- IRMS3 (Triphasé)|0x0B04|0x0A08|
|Histo: <br>- IMAX<br>- IMAX1(Triphasé)|0x0B04|0x050A|
|Histo: <br>- IMAX2(Triphasé)|0x0B04|0x090A|
|Histo: <br>- IMAX3(Triphasé)|0x0B04|0x0A0A|
|Histo: <br>- PMAX(Triphasé)<br>Standard :<br>- SMAXN<br>- SMAXN1(Triphasé)|0x0B04|0x050D|
|Histo: <br>- PAPP<br>Standard :<br>- SINSTS<br>- SINSTS1(Triphasé)|0x0B04|0x050F|
|Standard : SINSTS2(Triphasé)|0x0B04|0x090F|
|Standard : SINSTS3(Triphasé)|0x0B04|0x0A0F|
|Standard : ERQ1 (Production)|0x0B04|0x0305|
|Standard : ERQ2 (Production)|0x0B04|0x050E|
|Standard : ERQ3 (Production)|0x0B04|0x090E|
|Standard : ERQ4 (Production)|0x0B04|0x0A0E|
|Standard : URMS1(Mono / Triphasé)|0x0B04|0x0505|
|Standard : URMS2(Triphasé)|0x0B04|0x0905|
|Standard : URMS3(Triphasé)|0x0B04|0x0A05|
|Standard : UMOY1(Mono / Triphasé)|0x0B04|0x0511|
|Standard : UMOY2(Triphasé)|0x0B04|0x0911|
|Standard : UMOY3(Triphasé)|0x0B04|0x0A11|
|Standard : CCASN |0x0B04|0x050B|
|Standard : CCASN-1 |0x0B04|0x090B|
|Histo : <br>- OPTARIF <br>Standard :<br>- NGTF|0xFF66|0x0000|
|Histo : DEMAIN|0xFF66|0x0001|
|Histo : HHPHC|0xFF66|0x0002|
|Histo : PPOT|0xFF66|0x0003|
|Histo : PEJP|0xFF66|0x0004|
|Histo : ADPS|0xFF66|0x0005|
|Histo : ADIR1 (Triphasé)|0xFF66|0x0006|
|Histo : ADIR2 (Triphasé)|0xFF66|0x0007|
|Histo : ADIR3 (Triphasé)|0xFF66|0x0008|
|Standard : LTARF|0xFF66|0x0200|
|Standard : NTARF|0xFF66|0x0201|
|Standard : DATE|0xFF66|0x0202|
|Standard : EASD01|0xFF66|0x0203|
|Standard : EASD02|0xFF66|0x0204|
|Standard : EASD03|0xFF66|0x0205|
|Standard : EASD04|0xFF66|0x0206|
|Standard : SINSTI (Production)|0xFF66|0x0207|
|Standard : SMAXIN (Production)|0xFF66|0x0208|
|Standard : SMAXIN-1 (Production)|0xFF66|0x0209|
|Standard : CCAIN (Production)|0xFF66|0x0210|
|Standard : CCAIN-1 (Production)|0xFF66|0x0211|
|Standard : <br>- SMAXN-1 (Monophasé)<br>- SMAXN1-1 (Triphasé)|0xFF66|0x0212|
|Standard : SMAXN1-1 (Triphasé)|0xFF66|0x0212|
|Standard : SMAXN2-1 (Triphasé)|0xFF66|0x0213|
|Standard : SMAXN3-1 (Triphasé)|0xFF66|0x0214|
|Standard : MSG1|0xFF66|0x0215|
|Standard : MSG2|0xFF66|0x0216|
|Standard : STGE|0xFF66|0x0217|
|Standard : DPM1|0xFF66|0x0218|
|Standard : FPM1|0xFF66|0x0219|
|Standard : DPM2|0xFF66|0x0220|
|Standard : FPM2|0xFF66|0x0221|
|Standard : DPM3|0xFF66|0x0222|
|Standard : FPM3|0xFF66|0x0223|
|Standard : RELAIS|0xFF66|0x0224|
|Standard : NJOURF|0xFF66|0x0225|
|Standard : NJOURF+1|0xFF66|0x0226|
|Standard : PJOURF+1|0xFF66|0x0227|
|Standard : PPOINTE1|0xFF66|0x0228|


## Mise à jour du Firmware (non OTA)


Tout d'abord, il faut dévisser le boitier afin de sortir la carte électronique.
Ensuite, il faut brancher le module USB TTL sur le ZLinky_TIC comme sur la photo. 

<img src="https://github.com/fairecasoimeme/Zlinky_TIC/blob/master/Doc/Images/update_ZLinky_TIC_1.jpg" width="400">  

Pour ceux qui n'ont pas ce modèle, voici la correspondance des 5 PINs : 

<img src="https://github.com/fairecasoimeme/Zlinky_TIC/blob/master/Doc/Images/update_ZLinky_TIC_4.jpg" width="400"> 

Une fois que les branchements sont OK, il suffit d'insérer sur votre ordinateur la clef USB en maintenant le bouton **Flash** puis relacher.

<img src="https://github.com/fairecasoimeme/Zlinky_TIC/blob/master/Doc/Images/update_ZLinky_TIC_2.jpg" width="400"> 

Enfin vous pouvez suivre les [instructions suivantes](https://zigate.fr/documentation/mise-a-jour-de-la-zigate-2/) (similaire à la mise à jour d'une ZiGate+ (V2))


## Changelog

### Version 0003

* Fix data type for 0x702 cluster attribut consumption. uint32 to uint48 (For ZiGate v3.21)
* Fix config report bug on cluster 0x702
* Fix PIN Led error
* Fix differents data type value (DATE, HHPHC, VTIC, PREF)
* Fix version size 0x0000 | 0x4000


### Version 0001
Version initiale
