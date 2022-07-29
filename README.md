# Digital and Analog Sensor
The output of digital sensors is a discrete digital voltage or signal that represents a measurement digitally. Binary sensors display one's and zero's. These sensors are known for their speed and minimal distortion. The following motion sensor is one of the example of digital sensor.

![image](https://user-images.githubusercontent.com/108624020/181852146-f4f43873-d880-44d6-a6af-966370e17f0a.png)

[Click here to visit the webpage for the circuit](https://www.tinkercad.com/things/6GpLUpS7Cun-digitalsensor/editel)

```
int lamp = 13;                // the pin that the lamp is atteched to
int sensor = 3;              // the pin that the sensor is atteched to
int state = LOW;             // by default, no motion detected
int sensorValue = 0;                 // variable to store the sensor status (sensorValue)

int timer = 0;
long timerThreshold = 5; 	// if motion stopped, keep the lamp on for this time period (seconds)
							// it is needed to avoid immediate power off when motion stops


void setup() {
  Serial.println("Starting...");
  pinMode(lamp, OUTPUT);      // initalize lamp as output
  pinMode(sensor, INPUT);    // initialize sensor as input
  Serial.begin(9600);        // initialize serial
}

void loop(){
  
  sensorValue = digitalRead(sensor);   // read sensor sensorValueue
  
  if (sensorValue == HIGH) {           // check if the sensor is HIGH
    Serial.println("Sensor is HIGH");
    timer = 0;
    
    if (state == LOW) {
      Serial.println("Turning light ON!"); 
      state = HIGH;       // update variable state to HIGH
      digitalWrite(lamp, HIGH);   // turn lamp ON      
    }

  } else {      
      
    if(timer >= timerThreshold) {
      timer = 0;  
      if(state == HIGH){
        Serial.println("Turning light OFF!"); 
        state = LOW;
        digitalWrite(lamp, LOW); // turn lamp OFF
      }
    }
  }

  timer+=1;
  delay(1000);
  Serial.println(timer);

}
```

## Analog sensors

Analog sensors create a continuous signal that represents a quantity. In exchange for efficiency, analog sensors produce a more continuous and slightly more accurate signal. In spite of the fact that analog sensors do not provide as many features as digital sensors, you can be more confident in the readings you obtain with an analog sensor. The following photo-sensor is an example of digital sensor

![image](https://user-images.githubusercontent.com/108624020/181852701-85524177-0fb7-4591-959a-778f07e878de.png)

[Click here to visit the webpage for the circuit](https://www.tinkercad.com/things/gJroV8FAOot-photosenseor/editel)

```
/*

//PhotoResistor Pin
//the analog pin the photoresistor is 
                  //connected to
                  //the photoresistor is not calibrated to any units so
                  //this is simply a raw sensor value (relative light)
//LED Pin
int ledPin = 9;   //the pin the LED is connected to
                  //we are controlling brightness so 
                  //we use one of the PWM (pulse width
                  // modulation pins)



       // *********    Challenge:  Use a motor instead of an LED at this pin - light intensity will change motor speed





void setup()
{
  pinMode(ledPin, OUTPUT); //sets the led pin to output
}




void loop()
{
 int lightLevel = analogRead(A0); //Read the amount of light shining on the photoresistor
                                       
 lightLevel = map(lightLevel, 0, 900, 0, 255); 
         //adjust the value 0 to 900 to
         //span 0 to 255



 lightLevel = constrain(lightLevel, 0, 255);//make sure the 
                                           //value is betwween 
                                           //0 and 255
 analogWrite(ledPin, lightLevel);  //write the value
}
```



