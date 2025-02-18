Project 1

Creating a Morse code Using the link data here: ![alt-text](https://en.wikipedia.org/wiki/Morse_code#/media/File:International_Morse_Code.svg)
<a src="https://en.wikipedia.org/wiki/Morse_code#/media/File:International_Morse_Code.svg" href="" alt-text>Here</a>

```cpp
void setup() {
  pinMode(5, OUTPUT);
}
void loop() {
  for(int i = 0; i < 4; i++){
     digitalWrite(5, HIGH);
    delay(500);
    digitalWrite(5, HIGH);
    delay(500);
  } 
}
``` 
The code provided above is ouytputting an H letter,
To Create the letter G, we need two Long lights and then one short.

```cpp
for(int i = 0; i < 2; i++){
     digitalWrite(5, HIGH);
    delay(1000);
    digitalWrite(5, HIGH);
    delay(1000);
  }
  digitalWrite(5, HIGH);
  delay(500);
```

-  a morse code program to indicate your Initials.
Design a lighting effect such the lighting depends on the potentiometer value, (Trailing Lights effect)
- I have 4 LEDs, Switch two on, while leaving 
**--
-**-
--**
-**-
**--
## Make the LEDs be brighter as time increments
