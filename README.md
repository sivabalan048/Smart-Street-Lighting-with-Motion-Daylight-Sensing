# Smart-Street-Lighting-with-Motion-Daylight-Sensing
This project saves energy by automatically controlling the street lights based on ambient light and motion detection.
// Smart Street Lighting with Motion + Daylight sensing
int LDR = A0;        // LDR sensor pin
int PIR = 2;         // PIR sensor pin
int Light = 13;      // Street light (LED)

void setup() {
  pinMode(Light, OUTPUT);
  pinMode(PIR, INPUT);
  Serial.begin(9600);
}

void loop() {
  int ldrValue = analogRead(LDR);     // Read LDR value
  int motion = digitalRead(PIR);      // Read PIR value

  Serial.print("LDR: ");
  Serial.print(ldrValue);
  Serial.print("  Motion: ");
  Serial.println(motion);

  if (ldrValue < 500) {  // Dark condition (adjust threshold as needed)
    if (motion == HIGH) {
      digitalWrite(Light, HIGH);   // Turn ON light when motion detected
    } else {
      digitalWrite(Light, LOW);    // Keep OFF when no motion
    }
  } else {
    digitalWrite(Light, LOW);      // Daytime → light always OFF
  }
}
