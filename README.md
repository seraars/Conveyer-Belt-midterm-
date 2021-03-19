# Conveyer-Belt-midterm-
//set variables
const int en = 10;
const int in1 = 11;
const int in2 = 12;
const int potentio = A5;
const int LEDR = 5;
const int LEDG = 4;
const int time = 1000;
String direction = "";

//set initial values
void setup()
{
  pinMode(4, OUTPUT);//led light
  pinMode(5, OUTPUT);
  pinMode(2, INPUT);//push button
  pinMode(3, INPUT);
  pinMode(potentio, INPUT);
  attachInterrupt(0, setForward, RISING); //trigger when pin goes from low to high
  attachInterrupt(1, setReverse, RISING);
  Serial.begin(9600);//serial monitor
}

void setForward() //foward function
{
  direction = "forward";
}

void setReverse() //reverse function
{
  direction = "reverse";
}

void directionControl() //direction function
{
  if(direction == "forward")
  {
    digitalWrite(11, HIGH);
    digitalWrite(12, LOW);
    digitalWrite(LEDG, HIGH);
    digitalWrite(LEDR, LOW);  
  }
  
  else if(direction == "reverse")
  {
    digitalWrite(11, LOW);
    digitalWrite(12, HIGH);
    digitalWrite(LEDG, LOW);
    digitalWrite(LEDR, HIGH);
  }
}

void contSpeed(int motSpeed) //control speed function
{
  analogWrite(en, motSpeed);
}

void loop() //
{
  int motSpeed = analogRead(A5); //potentiometer
  motSpeed = map(motSpeed, 0, 1023, 0, 255); //range of the boundary
  Serial.print("Motor Speed:"); 
  Serial.println(motSpeed); //print value
  Serial.println("");
  
  directionControl(); //call function
  delay(time);
  contSpeed(motSpeed); //call function 
  delay(time); 
}
