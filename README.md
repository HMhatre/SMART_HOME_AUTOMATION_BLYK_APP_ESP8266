

#define D1 5
#define D2 4
#define D3 0

#define BLYNK_TEMPLATE_ID "ENTER_TMPLATE_ID"
#define BLYNK_TEMPLATE_NAME "ENTER_PROJECT_NAME"
#define BLYNK_AUTH_TOKEN "ENTER_TOKEN"

#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>

char ssid[] = "ENTER_WIFI_NAME";  
char pass[] = "";       

#define RELAY1 D1 
#define RELAY2 D2  
#define RELAY3 D3  

void setup()
{
  Serial.begin(9600);
  delay(100);

  Serial.println("🔌 Connecting to Wi-Fi...");
  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);

  pinMode(RELAY1, OUTPUT);
  pinMode(RELAY2, OUTPUT);
  pinMode(RELAY3, OUTPUT);

  // Default: Relays OFF (active LOW)
  digitalWrite(RELAY1, HIGH);
  digitalWrite(RELAY2, HIGH);
  digitalWrite(RELAY3, HIGH);

  Serial.println("✅ Setup complete.");
}

BLYNK_WRITE(V0)
{
  int state = param.asInt();
  digitalWrite(RELAY1, state ? LOW : HIGH);
  Serial.print("Relay 1 is ");
  Serial.println(state ? "ON" : "OFF");
}

BLYNK_WRITE(V1)
{
  int state = param.asInt();
  digitalWrite(RELAY2, state ? LOW : HIGH);
  Serial.print("Relay 2 is ");
  Serial.println(state ? "ON" : "OFF");
}

BLYNK_WRITE(V2)
{
  int state = param.asInt();
  digitalWrite(RELAY3, state ? LOW : HIGH);
  Serial.print("Relay 3 is ");
  Serial.println(state ? "ON" : "OFF");
}

void loop()
{
  Blynk.run();
}
