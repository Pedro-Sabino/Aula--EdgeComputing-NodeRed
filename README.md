# Aula--EdgeComputing-NodeRed

#include<DHT.h>
#include<ArduinoJson.h>


#define dhtpin 2
#define dhttype DHT11
DHT dht(dhtpin, dhttype);
void setup(){
  Serial.begin(9600);
  dht.begin();
}
void loop() {
  int temp = dht.readTemperature();
  int umi = dht.readHumidity();
  //alocando buffer de memora no doc 
  StaticJsonDocument<100>json;


  json["Temperatura"] = temp;
  json["Umidade"] = umi;

  serializeJson(json, Serial);
  Serial.println();
  delay(2000);
}

--------------------------------------------------------------------
Sensor Ultrasonico 

#include <ArduinoJson.h>

#define trigPin 9
#define echoPin 10

void setup() {
  Serial.begin(9600);
  
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  long duration = pulseIn(echoPin, HIGH);
  
  long distance = duration * 0.034 / 2;

  StaticJsonDocument<100> json;
  
  json["Distancia"] = distance;

  serializeJson(json, Serial);
  Serial.println();

  delay(2000);
}
