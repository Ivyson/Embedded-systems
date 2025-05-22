# Practice Questions

## DC Motor & H-Bridge
1. Write a code snippet to rotate a DC motor forward and reverse using an H-bridge motor driver (e.g., L298N).
   - [Question 1](https://www.tinkercad.com/things/2OFeHToP4i2-dc-motor-q1?sharecode=QFyjdrt9Cy-bQ1uJofEwTuVDPSzBDrOF5Oo8wmOsTwM)
2. Write a code to gradually increase the speed of a DC motor from 0 to 255 using analogWrite() and then stop after 5 seconds.
   - [Question 2](https://www.tinkercad.com/things/60O0hrK7IMe-dc-motor-q12?sharecode=T6pF7FZRQdcImo5984ltb43aW_KF6hDzXCk1Fv9qNmY)

## Ultrasonic Sensor
3. Write an Arduino function that reads distance from an HC-SR04 ultrasonic sensor and returns it in centimeters.
   - [Question 3](https://www.tinkercad.com/things/4CJZVTm1xBf-ultrasonic-q3?sharecode=gguxhHk71-o5mcmYuBDyYl60ZndD-UztEQUhE8vQ604)
4. Write code to stop the motor if an object is detected within 10 cm using the ultrasonic sensor.
   - [Question 4](https://www.tinkercad.com/things/d4SGSVoIX76-ultrasonic-q4?sharecode=9EWH3OHXvchF7Gu554qxBOpJks0AhjicdxAUGoF2J34)

## LCD Display
5. Write a code snippet to display "Distance: xx cm" on a 16x2 LCD based on ultrasonic sensor readings.
   - [Question 5](https://www.tinkercad.com/things/3jxwbcWUK7d-ldc-display-q5?sharecode=s27Ud9QrDLAJ96g_B3bqhgDA9iwvmwkRG474Od2zKsE)
6. Modify the above code to show "Obstacle!" on the second line if distance is less than 10 cm.
   - [Question 6](https://www.tinkercad.com/things/j37yBBpjq2A-ldc-display-q6?sharecode=8jcB94dltJAgH1OGsF31nUWSS5wfqx2P5Qhizib7beQ)

## Interrupts
7. Write an Arduino program that uses an external interrupt to toggle a motor ON/OFF with a push button.
   - [Question 7](https://www.tinkercad.com/things/kWTnP55zcQE-interrupt-q7?sharecode=m8aFHu-me8Os_Cz_K8n4i8H8Re71EgEDVgjxQYFKbu4)
8. Modify your interrupt code so that the LCD displays "Motor ON" or "Motor OFF" accordingly.
   - [Question 8](https://www.tinkercad.com/things/9MiRvuHztm2-interrupts-q-8?sharecode=ZMESH770DM0h9yD96YO7YNqNgFItCfUdROcpRgEwWBU)

## Strings
9. Write code to read a value from a sensor, convert it to a string using String(), and print it on the LCD.
   - [Question 9](https://www.tinkercad.com/things/0w23n6oCkRs-string-q9?sharecode=UcfoKbMdYcUSuaNqz7Epwmn0OL2BFgADgjc5I99CNVY)
10. Combine a string message and a numeric sensor value into one string and print it via Serial.println().
   - [Question 10](https://www.tinkercad.com/things/0w23n6oCkRs-string-q9?sharecode=UcfoKbMdYcUSuaNqz7Epwmn0OL2BFgADgjc5I99CNVY)

## Photoresistor
11. Write a code to read the value from a photoresistor and control the brightness of an LED using analogWrite().
    - [Question 11](https://www.tinkercad.com/things/eB3oqGAfCZn-photoresistor-q11-and-q12?sharecode=crBZm8rPSgyM_hAkdMR8GLIHogLH01iOkx6e6gt9Zbo)
12. Modify your code to also show the brightness level on the LCD in percentage.
    - [Question 12](https://www.tinkercad.com/things/eB3oqGAfCZn-photoresistor-q11-and-q12?sharecode=crBZm8rPSgyM_hAkdMR8GLIHogLH01iOkx6e6gt9Zbo)

## Photodiode
13. Write code to detect light intensity using a photodiode and turn a motor on when the light is below a certain threshold.
    - [Question 13](https://www.tinkercad.com/things/bBwu3Ziw1qw-photodiode-q13?sharecode=MO6ieG4awswd1HwiVoBHrZ5aGth5-0iHUDr7E6BKzow)

## map() Function
14. Write a program that reads a photoresistor value (0–1023), maps it to (0–255), and uses it to control motor speed.
    - [Question 14](https://www.tinkercad.com/things/2fFV6LXu1JA-map-q14-and-q15?sharecode=tRgZxIbJDPRU6rFh918mFKX4Kj-IE4V5a_ZsFRVcvao)
15. Modify your code to display the mapped speed value on the LCD.
    - [Question 15](https://www.tinkercad.com/things/2fFV6LXu1JA-map-q14-and-q15?sharecode=tRgZxIbJDPRU6rFh918mFKX4Kj-IE4V5a_ZsFRVcvao)