# Sensoren

## Drucksensoren (Barometer)

### BME680
Alter Bosch-Sensor, für neue Projekte nicht mehr empfohlen. Ich habe ein Watterott-Breakout. Das ist ein Vierfach-Sensor,
eigentlich für Luftqualität, er misst auch Temperatur, Feuchte, und Luftdruck. I2C oder SPI Interface, das Breakout kann
man mit 3.3V oder 5 V betreiben. Die Genauigkeit ist +-3% Feuchte, IAQ (Luftqualität) von 0 bis 500 mit vernünftiger
Genauigkeit. Absolute Genauigkeit des Barometers ist 0.6 mbar, relativ 0.12 mbar, und die Rauschgrenze liegt bei 0.2 Pa
was nur 1,7 cm Höhe entspricht. Der Temperatursensor ist auf 1 Grad genau und misst von -40 bis 85 Grad. Meiner hat I2C Adresse
0x77.

### BMP384
Dieser Sensor ist gelgefüllt und daher feuchtigkeitsunempfindlicher. Absolute Genauigkeit ist 50 Pa (0.5 mbar), Temperaturkoeffizient
1 Pa/K, und relativ 9 Pa (0.09 mbar). Es gibt ein breakout von sparkfun mit Qwiic Konnektoren für ca. 20 Euro (Eckstein). Dieser
ist also der genaueste der drei.

### HP206C
Das ist wohl der verbreitetste Sensor, gibt es zB bei reichelt für 18,20 EUR. Misst absolut auf 1.5 mbar (150 Pa) genau, 
relativ auf 0.5 mbar (50 Pa). Der ist also relativ deutlich ungenauer als die beiden anderen.

### MS5611 
Das ist der Sensor, den ich früher in meine Kopter eingebaut habe. Ein MS5611-BA03 kostet heute ca. 8-11 Euro. Die Auflösung geht
bis 0,012 mbar (1.2 Pa), die Antwortzeit ist sehr kurz (unter 8 ms), die absolute Genauigkeit auf +-1,5 mbar und die Langzeitstabilität
1 mbar pro Jahr.

### BMP180


### BMP280

