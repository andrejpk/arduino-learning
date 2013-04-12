## Arduino Programming Introduction - Code Samples ##
*(c) 2013 Andrej Kyselica - Distributed via Creative Commons CC BY 3.0. 
Your are free to — to copy, distribute and transmit the work 
to Remix — to adapt the work to make commercial use of the work 
with attribution*



### Code Sample 0 - Blank Program ###
This is the simplest Arduino program. It does nothing but lets us test the process of uploading a program and 
learning where to plug our code in.

    void setup() {
      // put your setup code here, to run once:
    
    }
    
    void loop() {
      // put your main code here, to run repeatedly: 
      
    }

### Code Sample 1 - Calling the delay function ###
We're calling a simple function here. When you run it it doesn't appear to do anything yet but
we'll build on it.

    void setup() {
      // put your setup code here, to run once:  
    }
    
    void loop() {
      // put your main code here, to run repeatedly: 
      delay(1000);  // Wait one second
    }

### Code Sample 2 - Using pinMode and digitalWrite ###
Wire an LED with resistor to digital pin 3. 

    void setup() {
      // put your setup code here, to run once:  
      pinMode(3, OUTPUT); 
    }
    
    void loop() {
      // put your main code here, to run repeatedly: 
      digitalWrite(3, HIGH);
      delay(1000);
    }


### Code Sample 3 - Using variables ###
Instead of repeating the pin number throughout the program, we'll create a variable for our LED pin. That helps us
avoid mistakes, make the program easier to understand and makes it easy to change to different pin later.

    int ledPin = 3;
    
    void setup() {
      // put your setup code here, to run once:  
      pinMode(ledPin, OUTPUT); 
    }
    
    void loop() {
      // put your main code here, to run repeatedly: 
      digitalWrite(ledPin, HIGH);
      delay(1000);
    }

### Code Sample 4 - Making it blink ###
We add code to turn the LED on and off with a delay.

    int ledPin = 3;
    
    void setup() {
      // put your setup code here, to run once:  
      pinMode(ledPin, OUTPUT); 
    }
    
    void loop() {
      // put your main code here, to run repeatedly: 
      digitalWrite(ledPin, HIGH);
      delay(1000);
      
      digitalWrite(ledPin, LOW);
      delay(1000);
    }


### Code Sample 5 - Reading input with digitalRead ###
Connect the switch to digital pin 5.

    int ledPin = 3;
    
    void setup() {
      // put your setup code here, to run once:  
      pinMode(ledPin, OUTPUT); 
    }
    
    void loop() {
      // put your main code here, to run repeatedly: 
    
      int buttonValue;
      int buttonValue = digitalRead(5);
    
      digitalWrite(ledPin, buttonValue);
    }


### Code Sample 6 - Using the ! (not) operator ###

    int ledPin = 3;
    
    void setup() {
      // put your setup code here, to run once:  
      pinMode(ledPin, OUTPUT); 
    }
    
    void loop() {
      // put your main code here, to run repeatedly: 
    
      int buttonValue;
      int buttonValue = digitalRead(5);
    
      digitalWrite(ledPin, !buttonValue);  // reverse buttonValue
    }


### Code Sample 7 - Serial Communication ###

	void setup() {
	  Serial.begin(9600); // setup serial communication at 9600 bits per second
	}
	  
	void loop() {
	  Serial.println("My name is Arduino!");
	}

After running program, go to Tools -> Serial Monitor in Arduino to see the output.

### Code Sample 8 - increment (++) operator ###

    int counter = 0;  // declare global variable named counter, set it to 0
    
    void setup() {
      Serial.begin(9600); 
    }
      
    void loop() {
      Serial.print("My name is Arduino! ");   // print but stay on same line
      Serial.println(counter); // print value of variable counter and go to the next line
      
      counter++;   // increase counter by 1
    }

### Code Sample 9 - if Statement ###

	void setup() {
	  Serial.begin(9600); // setup serial communication at 9600 bits per second
	}
	  
	void loop() {
	  int buttonStatus = digitalRead(3);
	  
	  if (buttonStatus == HIGH)
	  {
	    Serial.println("Button DOWN");
	  }
	  else
	  {
	    Serial.println("Button UP");
	  }
	}

### Code Sample 10 - while Statement ###

    void setup() {
      Serial.begin(9600); 
      
      pinMode(5, OUTPUT);
      digitalWrite(5, LOW);
    }
      
    void loop() {
      
      while(digitalRead(3) == LOW)  // keep doing this until button is pressed
      {
    Serial.println(".");
      }
      
      Serial.println("Button Pressed!");
    
      digitalWrite(5, HIGH);
      
      while(digitalRead(3) == HIGH)  // keep doing this until button is released
      {
    Serial.println("x");
      };
      
      Serial.println("Button Released!");
    }

### Code Sample 11 -- using a button to toggle a light (first attempt)
Pushbutton wired to Pin 3 and LED on pin 5 (change ledPin or buttonPin for different connections). 


    int ledPin = 5;
    int buttonPin = 3;
    
    void setup() {
      Serial.begin(9600); 
      
      pinMode(ledPin, OUTPUT);
      digitalWrite(ledPin, LOW);
    }
      
    void loop() {
      
      while(digitalRead(buttonPin) == LOW)  // keep doing this until button is pressed
      {
        // nothing
      }
    
      Serial.println("Light turned on");
      digitalWrite(ledPin, HIGH);
      
      while(digitalRead(buttonPin) == LOW)  // keep doing this until button is pressed again
      {
        // nothing    
      };
      
      Serial.println("Light turned off");
      digitalWrite(ledPin, LOW);
    }

Hmm... it runs but the button just blinks like crazy and finishes in a random spot. We need to fix this.

### Code Sample 12 -- using a button to toggle a light (second attempt)
We're adding delay()s before we try to read the button again. This is called a 'debounce' to keep the button value from bouncing when we meant to just press it once.

    int ledPin = 5;
    int buttonPin = 3;
    
    void setup() {
      Serial.begin(9600); 
      
      pinMode(ledPin, OUTPUT);
      digitalWrite(ledPin, LOW);
    }
      
    void loop() {
      
      while(digitalRead(buttonPin) == LOW)  // keep doing this until button is pressed
      {
        // nothing
      }
    
      Serial.println("Light turned on");
      digitalWrite(ledPin, HIGH);
      
      delay(500); // debounce
      
      while(digitalRead(buttonPin) == LOW)  // keep doing this until button is pressed again
      {
        // nothing    
      };
      
      Serial.println("Light turned off");
      digitalWrite(ledPin, LOW);
      
      delay(500); // debounce
    }

It works! Now we have a reliable way to work with buttons and similar binary (on/off) sensors. 

### Code Sample 13 -- Working with a Servo


    #include <Servo.h>

    int buttonPin = 3;
    Servo myservo;  // create servo object to control a servo 
    
    void setup() {
      Serial.begin(9600); 
      
      myservo.attach(11);
    }
      
    void loop() {
      
      while(digitalRead(buttonPin) == LOW)  // keep doing this until button is pressed
      {
        // nothing
      }
    
      Serial.println("Left");
      myservo.write(0);
      
      delay(500); // debounce
      
      while(digitalRead(buttonPin) == LOW)  // keep doing this until button is pressed again
      {
        // nothing    
      };
      
      Serial.println("Right");
      myservo.write(180);
      
      delay(500); // debounce
    }
    
Now we can have the servo swing around just by pressing the button. 


### Code Sample 14 -- Using the Ultrasonic distance sensor

Wire the ultrasonic distance sensor with GND going to GND, Vcc going to 5v, trigger going to IO 9 and echo going to IO 10. *Be careful not to reverse the GND and Vcc connections--this will permanently damage the sensor.*

    #include <Servo.h>
    #include <Ultrasonic.h>

    int buttonPin = 3;
    //Servo myservo;  // create servo object to control a servo 
    
    int triggerPin = 9;
    int echoPin = 10;
    
    Ultrasonic ultrasonic(triggerPin, echoPin);
    
    void setup() {
      Serial.begin(9600); 
      
      //myservo.attach(11);
    }
      
    void loop() {
      long microsec = ultrasonic.timing();   // measure the time the sound takes to travel
      Serial.print("Microsec = ");
      Serial.print(microsec);
      
      float inches = ultrasonic.convert(microsec, Ultrasonic::IN);   // convert to inches
      Serial.print(" inches = ");
      Serial.print(inches);
      
      Serial.println();
      
      delay(500);    // wait before measuring again
    }
    
Run the program and open the Serial Monitor to see the sensor's measurements.

### Code Sample 15 -- Using the Ultrasonic distance sensor with the servo

Use the servo we had wired into IO pin 11 in the prior examples. 

    #include <Servo.h>
    #include <Ultrasonic.h>

    int buttonPin = 3;
    Servo myservo;  // create servo object to control a servo 
    
    int triggerPin = 9;
    int echoPin = 10;
    
    Ultrasonic ultrasonic(triggerPin, echoPin);
    
    void setup() {
      Serial.begin(9600); 
      
      myservo.attach(11);
    }
      
    void loop() {
      long microsec = ultrasonic.timing();   // measure the time the sound takes to travel
      Serial.print("Microsec = ");
      Serial.print(microsec);
      
      float inches = ultrasonic.convert(microsec, Ultrasonic::IN);   // convert to inches
      Serial.print(" inches = ");
      Serial.print(inches);
      
      Serial.println();
      
      if(inches < 30)
      {
        myservo.write(0);
      }
      else
      {
        myservo.write(180);
      }
      
      delay(500);    // wait before measuring again
    }