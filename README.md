# line-follower-bot
#define LEFT_SENSOR 2
#define RIGHT_SENSOR 3

#define ENA 9  // Left Motor Speed
#define ENB 10 // Right Motor Speed
#define IN1 5  // Left Motor Forward
#define IN2 6  // Left Motor Backward
#define IN3 7  // Right Motor Forward
#define IN4 8  // Right Motor Backward

void setup() {
    pinMode(LEFT_SENSOR, INPUT);
    pinMode(RIGHT_SENSOR, INPUT);
    
    pinMode(ENA, OUTPUT);
    pinMode(ENB, OUTPUT);
    pinMode(IN1, OUTPUT);
    pinMode(IN2, OUTPUT);
    pinMode(IN3, OUTPUT);
    pinMode(IN4, OUTPUT);

    analogWrite(ENA, 150); // Set motor speed (0-255)
    analogWrite(ENB, 150);

    Serial.begin(9600);
}

void loop() {
    int leftSensor = digitalRead(LEFT_SENSOR);
    int rightSensor = digitalRead(RIGHT_SENSOR);

    Serial.print("Left: "); Serial.print(leftSensor);
    Serial.print(" | Right: "); Serial.println(rightSensor);

    if (leftSensor == 0 && rightSensor == 0) {
        moveForward();  // Both sensors on line → Move Forward
    } 
    else if (leftSensor == 0 && rightSensor == 1) {
        turnLeft();  // Right sensor off → Turn Left
    } 
    else if (leftSensor == 1 && rightSensor == 0) {
        turnRight(); // Left sensor off → Turn Right
    } 
    else {
        stopBot();  // Both off-line → Stop
    }
}

// Functions for motor control
void moveForward() {
    digitalWrite(IN1, HIGH);
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, HIGH);
    digitalWrite(IN4, LOW);
}

void turnLeft() {
    digitalWrite(IN1, LOW);
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, HIGH);
    digitalWrite(IN4, LOW);
}

void turnRight() {
    digitalWrite(IN1, HIGH);
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, LOW);
    digitalWrite(IN4, LOW);
}

void stopBot() {
    digitalWrite(IN1, LOW);
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, LOW);
    digitalWrite(IN4, LOW);
}
