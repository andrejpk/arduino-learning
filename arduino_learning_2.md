### Code Sample 13 -- Using the photoresistor

Read the value of the photoresistor and write the value to the serial monitor

  void setup() {
	  	// initialize serial communication at 9600 bits per second:
  		Serial.begin(9600);
	}

	// the loop routine runs over and over again forever:
	void loop() {
  		// read the input on analog pin 0:
  		int sensorValue = analogRead(A0);
  		// print out the value you read:
  		Serial.println(sensorValue);
  		delay(1);        // delay in between reads for stability
	}


### Code Sample 14 -- Using the servo
Use the servo wired to pin x

	#include <Servo.h>

	Servo myservo;  // create servo object to control a servo 

	void setup() {
      Serial.begin(9600); 
      
      myservo.attach(9);
    }

	void loop() {
      Serial.println("Left");
      myservo.write(0);
      
      delay(500); // wait
      
      Serial.println("Right");
      myservo.write(180);
      
      delay(500); // wait
	}

### Code Sample 15 -- Using the servo with the for loop
Let's use the for statement the control the servo

	#include <Servo.h> 
 
	Servo myservo;  // create servo object to control a servo 

	int pos = 0;    // variable to store the servo position 
 
	void setup() { 
	  myservo.attach(9);  // attaches the servo on pin 9 to the servo object 
	} 
 
 
	void loop() { 
	  for(pos = 0; pos < 180; pos += 1)  // goes from 0 degrees to 180 degrees 
	  {                                  // in steps of 1 degree 
	    myservo.write(pos);              // tell servo to go to position in variable 'pos' 
	    delay(15);                       // waits 15ms for the servo to reach the position 
	  } 
	  for(pos = 180; pos>=1; pos-=1)     // goes from 180 degrees to 0 degrees 
	  {                                
	    myservo.write(pos);              // tell servo to go to position in variable 'pos' 
	    delay(15);                       // waits 15ms for the servo to reach the position 
	  } 
	} 


### Code Sample 16 -- Using the servo with the photoresistor 

	#include <Servo.h> 
	 
	Servo myservo;  // create servo object to control a servo 
	 
	int val;    // variable to read the value from the analog pin 
 
	void setup() { 
  		myservo.attach(9);  // attaches the servo on pin 9 to the servo object 
	} 
 
	void loop() { 
	  val = analogRead(A0);            // reads the value of the potentiometer (value between 0 and 1023) 
	  val = map(val, 0, 250, 0, 179);     // scale it to use it with the servo (value between 0 and 180) 
	  myservo.write(val);                  // sets the servo position according to the scaled value 
	  delay(15);                           // waits for the servo to get there 
	} 

