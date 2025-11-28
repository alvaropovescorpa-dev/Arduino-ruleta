# Arduino-ruleta
#include <Adafruit_NeoPixel.h>

#define PIN 7
#define NUM_LEDS 24
#define BUTTON 2

Adafruit_NeoPixel strip(NUM_LEDS,PIN,NEO_GRB+NEO_KHZ800);

int numerorandom(){
  return random(1,24);
}

int led = 7;

void setup(){
  strip.begin();
  strip.show();
  pinMode(BUTTON, INPUT_PULLUP);
  randomSeed(analogRead(A0));
}

void loop(){
  int num, potValue, ledSelected, nume = 0;
  
  // Lectura del potenciómetro
  potValue = analogRead(A0);
  ledSelected = map(potValue, 0, 1023, 0, NUM_LEDS - 1);

  // LED azul según potenciómetro
  strip.clear();
  strip.setPixelColor(ledSelected, strip.Color(0, 0, 255));
  strip.show();
  delay(20);

  // Secuencia LED rojo
  num = numerorandom();
  if(digitalRead(BUTTON) == LOW){ 
    for(int i = 0; i < 24; i++){
      strip.clear();
      strip.setPixelColor(i, strip.Color(255,0,0));
      strip.show();
      delay(50);
    }

    for(int i = 0; i < 24; i++){
      strip.clear();
      strip.setPixelColor(i, strip.Color(255,0,0));
      strip.show();
      delay(50);
    }

    for(int i = 0; i < num; i++){
      strip.clear();
      strip.setPixelColor(i, strip.Color(255,0,0));
      strip.show();
      delay(100);
      nume = i;
    }

    delay(1000);

    for(int j = 0; j < 3; j++){
      for(int i = 0; i < NUM_LEDS; i++){
        strip.setPixelColor(i, strip.Color(255,0,0));
      }
      strip.show();
      delay(500);

      strip.clear();
      strip.show();
      delay(500);
    }
  }

  
}
