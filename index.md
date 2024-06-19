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
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your second milestone, explain what you've worked on since your previous milestone. You can highlight:
- Technical details of what you've accomplished and how they contribute to the final goal
- What has been surprising about the project so far
- Previous challenges you faced that you overcame
- What needs to be completed before your final milestone 

# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/LpYfZG2CoQc?si=ZzSDz-nx_dfO3KKn" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


The goal in my first milestone is to finish assembling the solar tracker and adapt the code to control the solar tracker. 4 of the LDR sensors which are top right, top left, bottom right, and bottom left detect the light. On the code, servo on the top and the other servo on the bottom move using the calculation of the value of 4 LDR sensors. For the vertical servo which is on the top, when the difference of the average top and average of bottom is over 50 which is tolerance on the code, it should be moving on the direction where the value is bigger among the average of top and average of bottom. For the horizontal servo which is on the bottom, it works in the same way as the vertical servo. There are many challenges and some of them are solved and unsolved. First of all, even though the code was compiled well, the servo is not moving at all and it made the wierd sound but I solved it by replacing it with the new one without any noisy sound. However, there is another problem with the servo again. The servo on the bottom doesn't have any problem but the servo on the top is moving to only one direction. It supposed to be moving to another direction depending on the value of LDR sensor. I treid to make servo anlge LimitHigh higher from 120 to 180 and it moves in another direction but not fully. I tried the another statement to set the angle of the servo using "map()" so it rotates fully but it comes back again. I disassembled it to analyze the problem but the servo doesn't move at all while the value of servo anlge is printed on the Serial monitor. I still cannot figure out what's the problem. The last challenge is the value of tolerance changing sudeenly on the code. The tolerance value should be always 50 as the constant value but it's chaning suddenly.
I will fix the problem in the servo so that it can rotate depending on the sensor and combine the solar usb to the solar tracker to add the function to charge the phone after assembling the solar usb. Maybe it would require printed 3D design for solar tracker to hold the solar usb box by itself.



# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 
-->
# Code
<!---Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. -->

```c++
void setup() {
 Serial.begin(9600);
  horizontal.attach(5);
  vertical.attach(6);
  horizontal.write(90);
  vertical.write(45);
  delay(3000);
}

void loop() {
int tr = analogRead(ldrTR); 
  int tl = analogRead(ldrTL); 
  int br = analogRead(ldrBR); 
  int bl = analogRead(ldrBL); 

  int dtime = 0; 
  int tol = 50;

  int avt = (tl + tr) / 2; 
  int avd = (bl + br) / 2; 
  int avl = (tl + bl) / 2; 
  int avr = (tr + br) / 2; 
  int dvert = avt - avd;  
  int dhoriz = avl - avr;
 Serial.print(tl);
  Serial.print(" ");
  Serial.print(tr);
  Serial.print(" ");
  Serial.print(bl);
  Serial.print(" ");
  Serial.print(br);
  Serial.print("  ");
  Serial.print(avt);
  Serial.print(" ");
  Serial.print(avd);
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


  if (-1 * tol > dvert || dvert > tol) {
    if (avt > avd) {
      servov = ++servov;
      if (servov > servovLimitHigh) {
        servov = servovLimitHigh;
      }
    }
    else if (avt < avd) {
      servov = --servov;
      if (servov < servovLimitLow) {
        servov = servovLimitLow;
      }
    }
    vertical.write(servov);
  }

 
  if (-1 * tol > dhoriz || dhoriz > tol) {
    if (avl > avr) {
      servoh = --servoh;
      if (servoh < servohLimitLow) {
        servoh = servohLimitLow;
      }
    }
    else if (avl < avr) {
      servoh = ++servoh;
      if (servoh > servohLimitHigh) {
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
|Solar USB kit 2.0|Solar Tracker USB charger|$40|https://www.browndoggadgets.com/products/solar-usb-kit-2-0|

# Other Resources/Examples
-https://learn.browndoggadgets.com/Guide/Dual+Axis+Solar+Tracker+3.0/382
-https://www.hackster.io/FIELDING/solar-panel-sun-tracker-phone-charger-f669ce
-https://learn.browndoggadgets.com/Guide/Solar+USB+Charger+2.0/6?lang=en
-https://www.hackster.io/FIELDING/solar-panel-sun-tracker-phone-charger-f669ce
-https://www.instructables.com/Dual-Axis-Tracker-V20/
-https://www.instructables.com/Solar-phone-charging-system-featuring-sun-tracking/

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
# Bill of Material
| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Arduino|Arudino|$150| https://www.browndoggadgets.com/products/dual-axis-smart-solar-tracker |
|LED|3mm Red LED| ||
|BreadBoard|Breadboard|||
|5 pin female header|2 of 5 pin female 0.1" header (1x6)|   | |
|Reset S1|6mm tact switch|2 of 6mm tact switch||  |
|Resistor|470-1.0K Resistors for LED Carbon 5% 1/4W | 2 of the resistor| | |

<!---To watch the BSE tutorial on how to create a portfolio, click here. -->
