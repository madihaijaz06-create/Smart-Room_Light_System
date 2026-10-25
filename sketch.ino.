const int LDR_PIN = A0;
const int PIR_PIN = 2;
const int LIGHT_PIN = 3;
const int BUZZER_PIN = 4;

// Adjust this threshold after testing
const int LIGHT_THRESHOLD = 500;

void setup() {
  Serial.begin(9600);

  pinMode(PIR_PIN, INPUT);
  pinMode(LIGHT_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);

  digitalWrite(LIGHT_PIN, LOW);
  digitalWrite(BUZZER_PIN, LOW);

  Serial.println("Smart Room-Light System Started");
  Serial.println("Allow PIR sensor to initialize...");
}

void loop() {
  int lightLevel = analogRead(LDR_PIN);
  int motion = digitalRead(PIR_PIN);

  // For the Wokwi photoresistor module:
  // Lower readings generally indicate darker conditions.
  bool isDark = lightLevel < LIGHT_THRESHOLD;
  bool motionDetected = (motion == HIGH);

  // Automatic room-light control
  if (isDark && motionDetected) {
    digitalWrite(LIGHT_PIN, HIGH);
  } else {
    digitalWrite(LIGHT_PIN, LOW);
  }

  // Security alert when motion is detected
  if (motionDetected) {
    tone(BUZZER_PIN, 1000);
  } else {
    noTone(BUZZER_PIN);
  }

  // Display sensor readings and system status
  Serial.print("Light Level: ");
  Serial.print(lightLevel);

  Serial.print(" | Motion: ");
  Serial.print(motionDetected ? "DETECTED" : "NONE");

  Serial.print(" | Room Light: ");
  Serial.print((isDark && motionDetected) ? "ON" : "OFF");

  Serial.print(" | Security Alert: ");
  Serial.println(motionDetected ? "ACTIVE" : "INACTIVE");

  delay(500);
}
