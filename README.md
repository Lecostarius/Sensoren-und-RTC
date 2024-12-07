# RTC (real time clocks)
RX8111CE
RX4111CE
RV-8803-C7
CBC921xx
M41T62
RV2123
RV3049 (SPI)
RV3029 (I2C)
PCF8563/83
PCF2123 (small power: 100 nA at 1.5 V)
PCF8523 (wie PCF2123, mit battery backup)

DS3231M
DS3232
DS3234
DS1307
DS1302
MCP7940
DS1387

vermutlich am besten: DS3231 und RV3029. Beide sind temperaturstabilisiert. Der DS1307 ist die nicht temperaturstabilisierte Variante des DS3231 (?).
RV3029: 3 ppm accuracy; vermutlich gerade noch handlötbar (keine Pins, immerhin 1 mm Abstand der Löt-Seiten).

DS3231: 1.5 ppm accuracy; kommt im 16-SO package (16 pins, davon 8 not connected, mit 1.27 mm Pinabstand)

Vom DS3231 gibt es eine Menge breakout boards. Ausserdem ist er lötfreundlicher und genauer. Der Stromverbrauch des RV3029 liegt bei 800 nA, der des DS3231
bei 110 uA, also mehr als 100 mal höher.






# Sensoren

## Drucksensoren (Barometer)

Zusammenfassung: Der BMP390 von Bosch ist der beste von allen, kostet aber knapp 20 Euro als breakout. Alternativ ist der BMP280
zu nennen, den gibt es für 2-3 Euro und er ist immer noch besser als der MS5611 den ich damals für die Kopter genommen habe und 
von dem ich so begeistert war. Für Außeneinsätze sollte man auch den BMP384 in Betracht ziehen. Der ist besser als der BMP280
(und schlechter als der BMP390), aber gelgefüllt und daher feuchtigkeitsunempfindlicher.


### BME680 (und BME688)
Alter Bosch-Sensor, für neue Projekte nicht mehr empfohlen. Ich habe ein Watterott-Breakout. Das ist ein Vierfach-Sensor,
eigentlich für Luftqualität, er misst auch Temperatur, Feuchte, und Luftdruck. I2C oder SPI Interface, das Breakout kann
man mit 3.3V oder 5 V betreiben. Die Genauigkeit ist +-3% Feuchte, IAQ (Luftqualität) von 0 bis 500 mit vernünftiger
Genauigkeit. Absolute Genauigkeit des Barometers ist 0.6 mbar, relativ 0.12 mbar, und die Rauschgrenze liegt bei 0.2 Pa
was nur 1,7 cm Höhe entspricht. Man kann das Baro mit 150 sps samplen. Der Temperatursensor ist auf 1 Grad genau und misst 
von -40 bis 85 Grad. Meiner hat I2C Adresse 0x77.
Die neue Version heisst BME688 und hat eingebaute KI.

### BMP384
Dieser Sensor ist gelgefüllt und daher feuchtigkeitsunempfindlicher. Absolute Genauigkeit ist 50 Pa (0.5 mbar), Temperaturkoeffizient
1 Pa/K, und relativ 9 Pa (0.09 mbar). Es gibt ein breakout von sparkfun mit Qwiic Konnektoren für ca. 20 Euro (Eckstein). Dieser
ist also der genaueste der drei. Die Rauschgrenze liegt bei 1,2 Pa bei maximaler Geschwindigkeit und 0,03 Pa bei niedrigster
Geschwindigkeit und eingeschaltetem Filter.

### HP206C
Das ist wohl der verbreitetste Sensor, gibt es zB bei reichelt für 18,20 EUR. Misst absolut auf 1.5 mbar (150 Pa) genau, 
relativ auf 0.5 mbar (50 Pa). Der ist also relativ deutlich ungenauer als die beiden anderen.

### MS5611 
Das ist der Sensor, den ich früher in meine Kopter eingebaut habe. Ein MS5611-BA03 kostet heute ca. 8-11 Euro. Die Auflösung geht
bis 0,012 mbar (1.2 Pa), die Antwortzeit ist sehr kurz (unter 8 ms), die absolute Genauigkeit auf +-1,5 mbar und die Langzeitstabilität
1 mbar pro Jahr. Dieser Sensor funktioniert schon ab 10 mbar Druck, die Boschsensoren typisch erst ab 300. RMS noise liegt bei 1,2 Pa 
bei langsamer Messung (110 sps).


### BMP180
Nachfolger des BMP085, spottbillig. Absolute Genauigkeit -4 bis +2 mbar, relativ +-0.12 mbar. Rauschen in ultra high res 0,03 mbar (3 Pa).
Der BMP280 ist in allen Parametern besser als der BMP180 und kostet ebenfalls fast nichts, es gibt also keinen Grund, einen BMP180 zu kaufen,
wenn man nicht gerade 100000 Stück braucht.

### BMP280
Absolute Genauigkeit +-1 mbar. Temperaturkoeffizient 1,5 Pa/K. Relative Genauigkeit 0,12 mbar (12 Pa). Rauschen minimal 1,3 Pa. Bis zu 157 sps
schnell, Temperatursensor mit 0,01 Grad Auflösung. Der BMP280 ist ein rundum verbesserter BMP180. Der Preis ist ebenfalls superbillig,
amazon bietet 5 Stück für unter 10 Euro an. Ich habe ein Board von Eckstein gekauft, von QITA. Dabei musste ich feststellen, dass man zwar
Pin CSB auf High ziehen muss (Chip Select), aber beim Pin SDO, was laut allen Beschreibungen die I2C-Adresse zwischen 0x76 und 0x77 umschaltet,
führt das Anlegen von +3,3V zur Zerstörung des Chips: ab da gibt er nur noch 0 aus (meldet sich aber brav über I2C). Wenn ich es unbeschaltet
lasse, tut der Sensor auf I2C-Adresse 0x76, obwohl das Datenblatt sagt, man müsse das Pin beschalten und laut Ohmmeter das Breakout auch
keine Pullups oder Pulldowns verwendet. Rätselhaft!

### BMP390 (Vorgänger ist der BMP388)
Absolut +-50 Pa, relativ +-3 Pa, Temperaturkoeffizient 0,6 Pa/K, Nachfolger des BMP380. Rauschen 0,9 Pa bis minimal mit Filter 0,02 Pa.
Driftet 0,16 mbar/Jahr. Es gibt den von adafruit. Der BMP388 ist der Vorgänger, nicht mehr für neue Designs empfohlen.

### BMP380
Nicht empfohlen f. neue Designs, man soll den BMP390 nehmen. Absolut 50 Pa, relativ 6 Pa, 200 sps.

### DPS310
Barometer von infineon. Es gibt ein adafruit-Breakout. Absolut 1 mbar, relativ 6 Pa (0,06 mbar) genau. Temperaturkoeffizient 0,5 Pa/K. 
Macht nur 35 sps bei höchster Genauigkeit. Messrauschen (dort pressure precision genannt) ist 0,35 Pa Standard, 0,2 Pa high precision.


