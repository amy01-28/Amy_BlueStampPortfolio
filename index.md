# Solar Tracker
It is the tracker which detects where the sun light shines so that it can convert from the solar energy to eletric energy. It have the function to charge it, so you can charge the smartphone battery only using the solar energy. Also, you can check the other information about the environment such as the temperature or humidity things. 

<!---This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were.-->


|Name| School name| **Area of Interest** | Grade |
|:--:|:--:|:--:|:--:|
| Amy(Seoyeon) K | Valley Christian High School | Chemical,Mechanical Engineering | Rising Junior

<!---**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.** -->

![Headstone Image](logo.svg)
  
<!---# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE -->



# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/wntJOIwsdMw?si=buplrxJSqPQrK0lx" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

The goal for my second milestone is to solve the issue for the servo. Two of the servos which are on top and the bottom were not working at all. When I get rid of the arduino and connect the servos on the shield, they were working well. However, the sensors are working well on the arduino but not shield so I cannot even use the breadboard to connect them togehter. By using the electrical tester, I tried to find out which connection is weak, and the batteries were the problem so I replaced them with new big one to give bigger power to shield. After that, servo on the top was working well according to the code but the other one is not woring well. It is rotating in the wrong way. It seems to be reading the code for the top servo. The fundamental issue was in the arduino and the battery. Their ground were different, which make the arduino confusing. That's why servos read the code wrongly. 



# First Milestone
<iframe width="560" height="315" src="https://www.youtube.com/embed/JpZ5UY8uZ1I?si=ufLPYo7IaSHPRlNB" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

The goal in my first milestone is to finish assembling the solar tracker and adapt the code to control the solar tracker. 4 of the LDR sensors which are top right, top left, bottom right, and bottom left detect the light. On the code, servo on the top and the other servo on the bottom move using the calculation of the value of 4 LDR sensors. For the vertical servo which is on the top, when the difference of the average top and average of bottom is over 50 which is tolerance on the code, it should be moving on the direction where the value is bigger among the average of top and average of bottom. For the horizontal servo which is on the bottom, it works in the same way as the vertical servo. There are many challenges and some of them are solved and unsolved. First of all, even though the code was compiled well, the servo is not moving at all and it made the wierd sound but I solved it by replacing it with the new one without any noisy sound. However, there is another problem with the servo again. The servo on the bottom doesn't have any problem but the servo on the top is moving to only one direction. It supposed to be moving to another direction depending on the value of LDR sensor. I treid to make servo anlge LimitHigh higher from 120 to 180 and it moves in another direction but not fully. I tried the another statement to set the angle of the servo using "map()" so it rotates fully but it comes back again. I disassembled it to analyze the problem but the servo doesn't move at all while the value of servo anlge is printed on the Serial monitor. I still cannot figure out what's the problem. The last challenge is the value of tolerance changing sudeenly on the code. The tolerance value should be always 50 as the constant value but it's chaning suddenly.
I will fix the problem in the servo so that it can rotate depending on the sensor and combine the solar usb to the solar tracker to add the function to charge the phone after assembling the solar usb. Maybe it would require printed 3D design for solar tracker to hold the solar usb box by itself.



# Schematics 

![Schematics Image](dualaxis.pdf)


# Code
<!---Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. -->

```c++
#include <Servo.h>

Servo horizontal;   //horizontal servo setting
int servoh = 90;    //initial horizontal servo angle would be 90 degrees you can change any value you want
int servoLimitHigh =180;  //the maximum angle of the horizontal servo angle
int servohLimitLow = 0;   //minimum angle of the horizontal servo angle

Servo vertical;   //vertical servo setting
int servov= 90;   // initial vertical servo angle would be 90 degrees you can change any value you want
int servovLimitHigh =130;  // the maximum anlge of the vertical servo angle
int servovLimitLow = 20;   //the minimum angle of the vertical servo angle

void setup() {
 Serial.begin(9600);   // setting for the computer printing speed
  horizontal.attach(5);   // pin number of the horizontal servo 
  vertical.attach(6);     // pin number of the vertical servo
  horizontal.write(90);   // servo.write(angle) so this setting means the horizontal servo would rotate to 90 degrees
  vertical.write(45);    //the vertical servo would rotate to 45 degrees
  delay(3000);            // rotating for 3 seconds 1000 is a second
}

void loop() {    // setting 4 sensors which are top right top bottom bottom right bottom left
int tr = analogRead(ldrTR); 
int tl = analogRead(ldrTL); 
int br = analogRead(ldrBR); 
int bl = analogRead(ldrBL); 

int dtime = 0; // change for debugging only
int tol = 50;  // tolerance

int avt = (tl + tr) / 2;  //average value top
int avb = (bl + br) / 2; //average value bottom
int avl = (tl + bl) / 2; //average value left
int avr = (tr + br) / 2; //average value right
int dvert = avt - avd;  //difference of top and down
int dhoriz = avl - avr;  //difference of right and left
  Serial.print(tl);   //computer printing the value of them on Serial monitor
  Serial.print(" ");
  Serial.print(tr);
  Serial.print(" ");
  Serial.print(bl);
  Serial.print(" ");
  Serial.print(br);
  Serial.print("  ");
  Serial.print(avt);
  Serial.print(" ");
  Serial.print(avb);
  Serial.print(" ");
  Serial.print(avl);
  Serial.print(" ");
  Serial.print(avr);
  Serial.print("  ");
  Serial.print(dtime);
  Serial.print("   ");
  Serial.print(tol);
  Serial.print("  ");
  Serial.print(servov);
  Serial.print("   ");
  Serial.print(servoh);
  Serial.println(" ");

//vertical servo and sensors
  if (abs(tol)<abs(dvert)) {   //if the absolute value of dvert is bigger than the tolerance
    if (avt > avb) {         
      servov = ++servov;        //servo should be going up
      if (servov > servovLimitHigh) {  // servo angle should not be bigger than the maximum angle
       servov = servovLimitHigh;  
      }
    }
    else if (avt < avb) {  
      servov = --servov;   // servo should be going down
      if (servov < servovLimitLow) {  //servo should not be smaller than the minimum angle
        servov = servovLimitLow;
      }
    }
    else if(avt =avb ) {
    }
    vertical.write(servov);
  }

 
  if (abs(tol)<abs(dhoriz)); { //if the absolute value of dhoriz is bigger than the tolerance
    if (avl > avr){ 
      servoh = --servoh;  //horizontal servo should be going down
      if (servoh < servohLimitLow) {  // servo anlge should not be bigger than the minimum angle
        servoh = servohLimitLow;
      }
    }
    else if (avl < avr) {  
      servoh = ++servoh; //vertical servo should be going up
      if (servoh > servohLimitHigh) {  //servo angle should not be bigger than the maximum anlge
        servoh = servohLimitHigh;
      }
    }
    else if (avl = avr) {
    
    }
    horizontal.write(servoh);
  }
  
  delay(dtime);
  
}
}
```

# Bill of Materials
<!---([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. -->

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Dual Axis Tracker 3.0 Kit |Solar Tracker|$150| https://www.browndoggadgets.com/products/dual-axis-smart-solar-tracker | 
|Charging usb circuit|The part in |$40|https://www.browndoggadgets.com/products/solar-usb-kit-
# Other Resources/Examples
* https://learn.browndoggadgets.com/Guide/Dual+Axis+Solar+Tracker+3.0/382?lang=en -
   instruction for solar tracker kit
* https://www.instructables.com/Dual-Axis-Tracker-V20/
   more information and explanation about solar tracker
* https://www.youtube.com/watch?v=C6vZFio-rkw&t=475s
   solar usb instruction video
* https://learn.browndoggadgets.com/Guide/Solar+USB+Charger+2.0/6?lang=en
  instruction for solar usb box kit
* https://www.hackster.io/FIELDING/solar-panel-sun-tracker-phone-charger-f669ce
   the idea for combining usb charger circuit and solar tracker
* https://chargehq.net/kb/solar-tracking-settings
  blutooth

# Starter Project
 <iframe width="560" height="315" src="https://www.youtube.com/embed/LpYfZG2CoQc?si=6JxsjkRi9CZVnVa_" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

  My starter project is the BlueStamp engineering arduino Beginner. It's necessary part for the robotics, which would be helpful to learn about circuit and coding through this project.
  I had problem for uploading the code I made. When I verify the code I made, it is compiled well but it's not uploaded. I did not use the resistor which should be always together with the LED. When trying to install the resistor with them, it should be 220 ohm but I could not find the resistor with that exactly same number, I replaced two of 110 ohm with 220 ohm one by twisting two of them to make it pretned to be one. Even though the circuit and codes are all correct, it was not working. I tried to figure it out by changing new arduino, new breadboard and disassembling the shield that I soldered. And finally we figure it out what was the probelm, which was the lack of power so we add the wire connect to voltage 5.

# Code
```c++
const int bt = 2; //button pin
const int led = 13; //LED pin
int Btst = 0; //the first button state before starting

void  setup(){
  pinMode(bt, INPUT);
  pinMode(led, OUTPUT);
}

void  loop(){
  btst = digitalRead(bt);
  if (btst == HIGH){
    digitalWrite(led, HIGH);
  } 
  else{
    digitalWrite(led,  LOW);
  }
}
```
# Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Arduino|Arudino|$150| https://www.browndoggadgets.com/products/dual-axis-smart-solar-tracker |
|LED|3mm Red LED| a|a|
|BreadBoard|Breadboard|a|a|
|5 pin female header|2 of 5 pin female 0.1" header (1x6)|  a |  a |
|Reset S1|6mm tact switch|2 of 6mm tact switch|a| a |
|Resistor|470-1.0K Resistors for LED Carbon 5% 1/4W | 2 of the resistor| a| a|


<!---To watch the BSE tutorial on how to create a portfolio, click here. -->

