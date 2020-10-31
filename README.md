# Arduino-Neopixel-Controller-30-effects

//Questo Sketch è basato sulla libreria Adafruit, modificando l'esempio "buttoncycler" aggiungendo un interrupt.
//include 30 diversi effetti switchabili con il pulsante.
//la strip che ho usato è una ws2812b 60 led/metro(5 volt)
//This sketch is based on Adafruit Library, I modified the example "buttoncycler" by adding interrupt.
//Include 30 different switchable effect.
//I used ws2812b strip led 60 led/m(5 volt)


#include <Adafruit_NeoPixel.h>
#include <EEPROM.h>
#define BUTTON 2 // pulsante per switchare modalità / button pin

#define PIXEL_PIN 5   // pin 5 collegato alla strip /strip data pin 
#define NUMPIXELS 41  // Numero dei Led/Pixel / number of pixels/leds on the strip

Adafruit_NeoPixel strip(NUMPIXELS, PIXEL_PIN, NEO_GRB + NEO_KHZ800);

byte selectedEffect = 0; 

void setup() {
  strip.begin(); // Inizializzo la Strip
  strip.show(); // Inizializzo tutti i pixel su OFF
  digitalWrite (BUTTON, HIGH);  // internal pull-up resistor
  attachInterrupt (digitalPinToInterrupt (BUTTON), changeEffect, CHANGE); // premuto / pressed

}
void loop() {
  
  EEPROM.get(0, selectedEffect);

  if (selectedEffect > 30) {

    selectedEffect = 0;
    EEPROM.put(0, 0);

  }
  switch (selectedEffect) {

    case 0  : {

        colorWipe(strip.Color(  0,   0,   0), 50);    // Black/off

        break;
      }
    case 1  : {

        colorWipe(strip.Color(  255,   0,   0), 50);    // Rosso-Red

        break;
      }
    case 2  : {

        colorWipe(strip.Color(  0,   255,   0), 50); // Verde-Green

        break;
      }
    case 3  : {

        colorWipe(strip.Color(  0,   0,   255), 50); // Blu-Blue

        break;
      }

    case 4  : {

        colorWipe(strip.Color(  255,   255,   255), 50); // Bianco-White

        break;
      }

    case 5  : {

        colorWipe(strip.Color(  255,   0,   255), 50); // Magenta

        break;
      }

    case 6  : {

        colorWipe(strip.Color(  255,   30,   255), 50); // Rosa-Pink

        break;
      }

    case 7  : {

        colorWipe(strip.Color(  255,  255,   0), 50); // Giallo-Yellow

        break;
      }

    case 8  : {

        colorWipe(strip.Color( 255,  70,  0), 50); // Arancione-Orange

        break;
      }

    case 9  : {

        colorWipe(strip.Color(  0,  255,   255), 50); // Azzurro-Turchese

        break;
      }

    case 10  : {

        rainbow(20);

        break;
      }

    case 11  : {

        colorWipe(strip.Color(  0,  255,   255), 50); // Azzurro-Turchese
        colorWipe(strip.Color(  255,   0,   255), 50); // Magenta

        break;
      }

    case 12  : {

        colorWipe(strip.Color(  255,  255,   255), 50); // Bianco-White
        colorWipe(strip.Color(  0,   0,   255), 50); // Blue

        break;
      }

    case 13  : {

        colorWipe(strip.Color(  255,  255,   255), 50); // Bianco-White
        colorWipe(strip.Color(  255,   0,   0), 50); // Rosso-Red

        break;
      }

    case 14  : {

        colorWipe(strip.Color(  255,  255,   0), 50); // Giallo-Yellow
        colorWipe(strip.Color( 255,  70,  0), 50); // Arancione-Orange

        break;
      }


    case 15 : {

        theaterChase(strip.Color(  0,   0, 127), 50); // Blue
        break;
      }
    case 16 : {

        theaterChaseRainbow(50);

        break;
      }
    case 17 : {

        rainbowCycle(20);

        break;
      }
    case 18 : {

        RGBLoop();

        break;
      }

      //**************************Cylone************************************//
    //*********************************************************************************//
    // 4 example of Cylone Eye---> Redeye,WhiteEye,GreenEye and BlueEye
    // You can change color on the first 3 value----> ( 0, 0, 0,.....)=( r, g, b,.....)
    // the rest are "size","speed" and "delay" = ( r, g, b, size, speed, delay)
    //*********************************************************************************
    case 19 : {

        Cylone(255,  0,  0, 4, 40, 50); // RedEye

        break;
      }
    case 20 : {

        Cylone(255, 255, 255, 4, 40, 50); // WhiteEye

        break;
      }
    case 21 : {

        Cylone( 0, 255, 0, 4, 40, 50); // GreenEye

        break;
      }
    case 22 : {

        Cylone( 0, 0, 255, 4, 40, 50); // BlueEye

        break;
      }
    case 23: {

        CieloStellato( 0, 0, 10, 20, random(100, 1000));  // ( r, g, b,....)

        break;
      }
    case 24 : {

        CieloStellato( 0, 0, 0, 20, random(100, 1000));  // ( r, g, b,....)


        break;
      }
    //**************************Cylone_Base_Azzurra************************************//
    //*********************************************************************************//
    // 4 example of Cylone_Base_Azzurra with Magenta,Yellow.White and Green
    // You can change color on the first 3 value----> ( 0, 0, 0,.....)=( r, g, b,.....)
    // the rest are "size","speed" and "delay" = ( r, g, b, size, speed, delay)
    //*********************************************************************************
    case 25 : {

        Cylone_Base_Azzurra( 255, 0, 255, 4, 40, 50); // Cylone Magenta Base Azzurra

        break;
      }
    case 26 : {

        Cylone_Base_Azzurra( 255, 255, 0, 4, 40, 50); // Cylone Giallo-Yellow Base Azzurra

        break;
      }
    case 27 : {

        Cylone_Base_Azzurra( 0, 0, 255, 4, 40, 50); //Cylone Verde_Green Base Azzurra

        break;
      }
    case 28 : {

        Cylone_Base_Azzurra( 255, 255, 255, 4, 40, 50); // Cylone Bianco-White Base Azzurra

        break;
      }
    case 29 : {

        Cylone_Cambio_Colore( 255, 255, 255, 4, 40, 50); // Cylone with change base color

        break;
      }
    case 30 : {

        Strobo(255, 255, 255, 10, 100, 1000); //****( r, g, b,......)
        
        break;
      }


  }
}


void changeEffect() {
  if (digitalRead (BUTTON) == HIGH) {
    selectedEffect++;
    EEPROM.put(0, selectedEffect);
    asm volatile ("  jmp 0");
  }
}
// *************************
// ** LEDEffect Functions **
// *************************

// Fill strip pixels one after another with a color. Strip is NOT cleared
// first; anything there will be covered pixel by pixel. Pass in color
// (as a single 'packed' 32-bit value, which you can get by calling
// strip.Color(red, green, blue) as shown in the loop() function above),
// and a delay time (in milliseconds) between pixels.

void colorWipe(uint32_t color, int wait) {
  for (int i = 0; i < strip.numPixels(); i++) { // For each pixel in strip...
    strip.setPixelColor(i, color);         //  Set pixel's color (in RAM)
    strip.show();                          //  Update strip to match
    delay(wait);                           //  Pause for a moment
  }
}

// Rainbow cycle along whole strip. Pass delay time (in ms) between frames.

void rainbow(int wait) {
  // Hue of first pixel runs 3 complete loops through the color wheel.
  // Color wheel has a range of 65536 but it's OK if we roll over, so
  // just count from 0 to 3*65536. Adding 256 to firstPixelHue each time
  // means we'll make 3*65536/256 = 768 passes through this outer loop:
  for (long firstPixelHue = 0; firstPixelHue < 3 * 65536; firstPixelHue += 256) {
    for (int i = 0; i < strip.numPixels(); i++) { // For each pixel in strip...
      // Offset pixel hue by an amount to make one full revolution of the
      // color wheel (range of 65536) along the length of the strip
      // (strip.numPixels() steps):
      int pixelHue = firstPixelHue + (i * 65536L / strip.numPixels());
      // strip.ColorHSV() can take 1 or 3 arguments: a hue (0 to 65535) or
      // optionally add saturation and value (brightness) (each 0 to 255).
      // Here we're using just the single-argument hue variant. The result
      // is passed through strip.gamma32() to provide 'truer' colors
      // before assigning to each pixel:
      strip.setPixelColor(i, strip.gamma32(strip.ColorHSV(pixelHue)));
    }
    strip.show(); // Update strip with new contents
    delay(wait);  // Pause for a moment
  }
}

// Theater-marquee-style chasing lights. Pass in a color (32-bit value,
// a la strip.Color(r,g,b) as mentioned above), and a delay time (in ms)
// between frames.

void theaterChase(uint32_t color, int wait) {
  for (int a = 0; a < 10; a++) { // Repeat 10 times...
    for (int b = 0; b < 3; b++) { //  'b' counts from 0 to 2...
      strip.clear();         //   Set all pixels in RAM to 0 (off)
      // 'c' counts up from 'b' to end of strip in steps of 3...
      for (int c = b; c < strip.numPixels(); c += 3) {
        strip.setPixelColor(c, color); // Set pixel 'c' to value 'color'
      }
      strip.show(); // Update strip with new contents
      delay(wait);  // Pause for a moment
    }
  }
}

// Rainbow-enhanced theater marquee. Pass delay time (in ms) between frames.

void theaterChaseRainbow(int wait) {
  int firstPixelHue = 0;     // First pixel starts at red (hue 0)
  for (int a = 0; a < 30; a++) { // Repeat 30 times...
    for (int b = 0; b < 3; b++) { //  'b' counts from 0 to 2...
      strip.clear();         //   Set all pixels in RAM to 0 (off)
      // 'c' counts up from 'b' to end of strip in increments of 3...
      for (int c = b; c < strip.numPixels(); c += 3) {
        // hue of pixel 'c' is offset by an amount to make one full
        // revolution of the color wheel (range 65536) along the length
        // of the strip (strip.numPixels() steps):
        int      hue   = firstPixelHue + c * 65536L / strip.numPixels();
        uint32_t color = strip.gamma32(strip.ColorHSV(hue)); // hue -> RGB
        strip.setPixelColor(c, color); // Set pixel 'c' to value 'color'
      }
      strip.show();                // Update strip with new contents
      delay(wait);                 // Pause for a moment
      firstPixelHue += 65536 / 90; // One cycle of color wheel over 90 frames
    }
  }
}


byte * Wheel(byte WheelPos) {
  static byte c[3];

  if (WheelPos < 85) {
    c[0] = WheelPos * 3;
    c[1] = 255 - WheelPos * 3;
    c[2] = 0;
  } else if (WheelPos < 170) {
    WheelPos -= 85;
    c[0] = 255 - WheelPos * 3;
    c[1] = 0;
    c[2] = WheelPos * 3;
  } else {
    WheelPos -= 170;
    c[0] = 0;
    c[1] = WheelPos * 3;
    c[2] = 255 - WheelPos * 3;
  }

  return c;
}

void rainbowCycle(int SpeedDelay) {
  byte *c;
  uint16_t i, j;

  for (j = 0; j < 256 * 5; j++) { // 5 cycles of all colors on wheel
    for (i = 0; i < NUMPIXELS; i++) {
      c = Wheel(((i * 256 / NUMPIXELS) + j) & 255);
      strip.setPixelColor(i, *c, *(c + 1), *(c + 2));
    }
    strip.show();
    delay(SpeedDelay);
  }
}

void RGBLoop() {
  for (int j = 0; j < 3; j++ ) {
    // Fade IN
    for (int k = 0; k < 256; k++) {
      switch (j) {
        case 0: setAll(k, 0, 0); break;
        case 1: setAll(0, k, 0); break;
        case 2: setAll(0, 0, k); break;
      }
      strip.show();
      delay(3);
    }
    // Fade OUT
    for (int k = 255; k >= 0; k--) {
      switch (j) {
        case 0: setAll(k, 0, 0); break;
        case 1: setAll(0, k, 0); break;
        case 2: setAll(0, 0, k); break;
      }
      strip.show();
      delay(3);
    }
  }
}

void Cylone_Base_Azzurra(byte red, byte green, byte blue, int EyeSize, int SpeedDelay, int ReturnDelay) {

  for (int i = 0; i < NUMPIXELS - EyeSize - 2; i++) {
    setAll(0, 255, 255);
    strip.setPixelColor(i, red / 10, green / 10, blue / 10);
    for (int j = 1; j <= EyeSize; j++) {
      strip.setPixelColor(i + j, red, green, blue);
    }
    strip.setPixelColor(i + EyeSize + 1, red / 10, green / 10, blue / 10);
    strip.show();
    delay(SpeedDelay);
  }

  delay(ReturnDelay);

  for (int i = NUMPIXELS - EyeSize - 2; i > 0; i--) {
    setAll(0, 255, 255);
    strip.setPixelColor(i, red / 10, green / 10, blue / 10);
    for (int j = 1; j <= EyeSize; j++) {
      strip.setPixelColor(i + j, red, green, blue);
    }
    strip.setPixelColor(i + EyeSize + 1, red / 10, green / 10, blue / 10);
    strip.show();
    delay(SpeedDelay);
  }

  delay(ReturnDelay);
}

void Cylone_Cambio_Colore(byte red, byte green, byte blue, int EyeSize, int SpeedDelay, int ReturnDelay) {

  for (int i = 0; i < NUMPIXELS - EyeSize - 2; i++) {
    setAll(255, 0, 0);
    strip.setPixelColor(i, red / 10, green / 10, blue / 10);
    for (int j = 1; j <= EyeSize; j++) {
      strip.setPixelColor(i + j, red, green, blue);
    }
    strip.setPixelColor(i + EyeSize + 1, red / 10, green / 10, blue / 10);
    strip.show();
    delay(SpeedDelay);
  }

  delay(ReturnDelay);

  for (int i = NUMPIXELS - EyeSize - 2; i > 0; i--) {
    setAll(255, 70, 0);
    strip.setPixelColor(i, red / 10, green / 10, blue / 10);
    for (int j = 1; j <= EyeSize; j++) {
      strip.setPixelColor(i + j, red, green, blue);
    }
    strip.setPixelColor(i + EyeSize + 1, red / 10, green / 10, blue / 10);
    strip.show();
    delay(SpeedDelay);
  }

  delay(ReturnDelay);

  for (int i = 0; i < NUMPIXELS - EyeSize - 2; i++) {
    setAll(255, 255, 0);
    strip.setPixelColor(i, red / 10, green / 10, blue / 10);
    for (int j = 1; j <= EyeSize; j++) {
      strip.setPixelColor(i + j, red, green, blue);
    }
    strip.setPixelColor(i + EyeSize + 1, red / 10, green / 10, blue / 10);
    strip.show();
    delay(SpeedDelay);
  }

  delay(ReturnDelay);

  for (int i = NUMPIXELS - EyeSize - 2; i > 0; i--) {
    setAll(0, 255, 255);
    strip.setPixelColor(i, red / 10, green / 10, blue / 10);
    for (int j = 1; j <= EyeSize; j++) {
      strip.setPixelColor(i + j, red, green, blue);
    }
    strip.setPixelColor(i + EyeSize + 1, red / 10, green / 10, blue / 10);
    strip.show();
    delay(SpeedDelay);
  }

  delay(ReturnDelay);

  for (int i = 0; i < NUMPIXELS - EyeSize - 2; i++) {
    setAll(0, 0, 255);
    strip.setPixelColor(i, red / 10, green / 10, blue / 10);
    for (int j = 1; j <= EyeSize; j++) {
      strip.setPixelColor(i + j, red, green, blue);
    }
    strip.setPixelColor(i + EyeSize + 1, red / 10, green / 10, blue / 10);
    strip.show();
    delay(SpeedDelay);
  }

  delay(ReturnDelay);

  for (int i = NUMPIXELS - EyeSize - 2; i > 0; i--) {
    setAll(255, 0, 255);
    strip.setPixelColor(i, red / 10, green / 10, blue / 10);
    for (int j = 1; j <= EyeSize; j++) {
      strip.setPixelColor(i + j, red, green, blue);
    }
    strip.setPixelColor(i + EyeSize + 1, red / 10, green / 10, blue / 10);
    strip.show();
    delay(SpeedDelay);
  }

  delay(ReturnDelay);
}

void Cylone(byte red, byte green, byte blue, int EyeSize, int SpeedDelay, int ReturnDelay) {

  for (int i = 0; i < NUMPIXELS - EyeSize - 2; i++) {
    setAll(0, 0, 0);
    strip.setPixelColor(i, red / 10, green / 10, blue / 10);
    for (int j = 1; j <= EyeSize; j++) {
      strip.setPixelColor(i + j, red, green, blue);
    }
    strip.setPixelColor(i + EyeSize + 1, red / 10, green / 10, blue / 10);
    strip.show();
    delay(SpeedDelay);
  }

  delay(ReturnDelay);

  for (int i = NUMPIXELS - EyeSize - 2; i > 0; i--) {
    setAll(0, 0, 0);
    strip.setPixelColor(i, red / 10, green / 10, blue / 10);
    for (int j = 1; j <= EyeSize; j++) {
      strip.setPixelColor(i + j, red, green, blue);
    }
    strip.setPixelColor(i + EyeSize + 1, red / 10, green / 10, blue / 10);
    strip.show();
    delay(SpeedDelay);
  }

  delay(ReturnDelay);
}


void Strobo(byte red, byte green, byte blue, int StrobeCount, int FlashDelay, int EndPause) {
  for (int j = 0; j < StrobeCount; j++) {
    setAll(red, green, blue);
    strip.show();
    delay(FlashDelay);
    setAll(0, 0, 0);
    strip.show();
    delay(FlashDelay);
  }

  delay(EndPause);
}

void CieloStellato(byte red, byte green, byte blue, int SparkleDelay, int SpeedDelay) {
  setAll(red, green, blue);

  int Pixel = random(NUMPIXELS);
  strip.setPixelColor(Pixel, 0xff, 0xff, 0xff);
  strip.show();
  delay(SparkleDelay);
  strip.setPixelColor(Pixel, red, green, blue);
  strip.show();
  delay(SpeedDelay);
}

void setAll(byte red, byte green, byte blue) {
  for (int i = 0; i < NUMPIXELS ; i++ ) {
    strip.setPixelColor(i, red, green, blue);
  }
  strip.show();
}
