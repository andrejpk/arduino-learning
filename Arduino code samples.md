## Arduino Programming Introduction - Code Samples ##
* (c) 2013 Andrej Kyselica - Distributed via Creative Commons CC BY 3.0 *
* Your are free to — to copy, distribute and transmit the work 
to Remix — to adapt the work to make commercial use of the work 
with attribution *



### Code Sample 0 - Blank Program ###

    void setup() {
      // put your setup code here, to run once:
    
    }
    
    void loop() {
      // put your main code here, to run repeatedly: 
      
    }

### Code Sample 1 - Calling the delay function ###

    void setup() {
      // put your setup code here, to run once:  
    }
    
    void loop() {
      // put your main code here, to run repeatedly: 
      delay(1000);
    }

### Code Sample 2 - Using pinMode and digitalWrite ###
Write an LED with resistor to digital pin 3

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

### Code Sample 11: Working with 
