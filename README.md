This library is "cloned" from here (including this readme-file):  
http://interface.khm.de/index.php/lab/interfaces-advanced/arduino-frequency-counter-library/  
  
---------
  
## Arduino Frequency Counter Library  
  
<a href="https://github.com/BlackBrix/Arduino-Frequency-Counter-Library/raw/master/pics/freqcounter.jpg"><img title="freqcounter" src="https://github.com/BlackBrix/Arduino-Frequency-Counter-Library/raw/master/pics/freqcounter.jpg" alt="freqcounter" width="370" height="295"></a>
  
From our › [Theremin Project](http://interface.khm.de/index.php/lab/interfaces-advanced/theremin-as-a-capacitive-sensing-device/) I derived this Frequency Counter Library. The library makes it possible to measure frequencies with a high resolution and accuracy.  
  
The Frequency input is fixed to digital pin 5. This pin is mapped to the alternate port function T1 which is the input 16 Bit Hardware Counter1. To obtain a higher resolution than 16 Bit,  the counter overflows are counted also and are calculated with the counter value to the final long integer result. The Frequency Source output must have a digital level so that weak Signals have to be amplified for instance by an single transistor or a 74HC14 inverter. The maximum input frequency is about 8 MHz when signal duty cycle is 50%.  
  
If you like to measure higher frequencies you have to use an prescaler or divider circuit which can be used from other counter projects published in the web. The Gate Time for the counting period can be chosen in the start() function where values of 10, 100 or 1000 ms are practicable for a resolution of 100, 10 and 1 Hz  but any value can be used. The internal resolution of the gatetime is 2 ms so that the time can be varied in the increment of 2. If you wish to minimize the indication error the value of  FreqCounter::f_comp variable can compensate slight gatetime errors. Compared to an commercial ACECO counter it is possible to trim the deviation to almost zero over the whole range. For gatetimes of 10,100,1000 the  values 1, 10 and 100 where found to be good for our Duemilanova boards.  
  
### Example Programm  
  
```C++
#include <FreqCounter.h>

void setup() {
  Serial.begin(57600);                    // connect to the serial port
  Serial.println("Frequency Counter");
}

long int frq;
Void loop() {

 FreqCounter::f_comp= 8;             // Set compensation to 12
 FreqCounter::start(100);            // Start counting with gatetime of 100ms
 while (FreqCounter::f_ready == 0)         // wait until counter ready
 
 frq=FreqCounter::f_freq;            // read result
 Serial.println(frq);                // print result
 delay(20);
}
```
### Preamplifier schematics  
  
<a href="https://github.com/BlackBrix/Arduino-Frequency-Counter-Library/raw/master/pics/preamp.gif"><img title="preamp" src="https://github.com/BlackBrix/Arduino-Frequency-Counter-Library/raw/master/pics/preamp.gif" alt="preamp" width="617" height="189"></a>
  
### Source Codes
Updated 10/2010 ; works with atmega328; removed some glitches  
Updated 01/2012 ; Arduino 1.0  
Download (Original from Author) [>FreqCounter](http://interface.khm.de/wp-content/uploads/2009/01/FreqCounter_1_12.zip) Library  
  
### Forum
further questions to this topic can be discussed here:  
http://arduino.cc/forum/index.php/topic,64219.0.html  
http://www.arduino.cc/cgi-bin/yabb2/YaBB.pl?num=1231326297  
  
### Contact
Martin Nawrath, nawrath@khm.de
