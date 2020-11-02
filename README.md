# Pushbutton-Arduino
int ledPin = 9;
boolean estadoLed = false;
const int buttonPin1 = 2;
 
int buttonState1 = 0;
int buttonState2 = 0;
 
String data;

void setup() {
   Serial.begin(9600);
   pinMode(ledPin, OUTPUT);
   pinMode(buttonPin1, INPUT);
   digitalWrite(ledPin,estadoLed);
   pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  buttonState1 = digitalRead(buttonPin1);
  data = normalizeData(buttonState1, buttonState2);
  Serial.println(data);
  delay(20);

   digitalWrite(LED_BUILTIN, HIGH);   // encender LED (HIGH es el nivel de voltaje)
   delay(0001);                       // esperar dos segundos
   digitalWrite(LED_BUILTIN, LOW);    // apagar LED reduciendo voltajee
   delay(0001);                       // esperar un segundo

   if (Serial.available()){
     char Letra = Serial.read();
            if (Letra== 'a'){         //Presionar letra a para enccender y apagar led
                  estadoLed= !estadoLed;
               }
             digitalWrite(ledPin,estadoLed);
            }
 }
 
 String normalizeData(int b1, int b2) {
 
  String B1string = String(b1);
  String B2string = String(b2);
 
  String ret = String("S") + B1string + B2string + String("E");
  return ret;
}
