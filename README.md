# Esp32-Firebase

```c++
#include <WiFi.h>
#include "FirebaseESP32.h"

// Credenciales wifi
#define WIFI_SSID "Wifi hogar"
#define WIFI_PASSWORD "panconpalta"

// Credenciales Proyecto Firebase
#define FIREBASE_HOST "https://esp32-3a5e9-default-rtdb.firebaseio.com/"
#define FIREBASE_AUTH "ic9zqUP4bM0hsmFQXJPyc0Yy8a2FJTGPGHZlcTOG"

// Firebase Data object
FirebaseData firebaseData;

// Si deseamos una ruta especifica
String nodo = "/Sensores";

void setup()
{
  Serial.begin(115200);
  Serial.println();

  WiFi.begin(WIFI_SSID, WIFI_PASSWORD);
  Serial.print("Conectado al Wi-Fi");
  while (WiFi.status() != WL_CONNECTED)
  {
    Serial.print(".");
    delay(300);
  }
  Serial.println();

  Firebase.begin(FIREBASE_HOST, FIREBASE_AUTH);
  Firebase.reconnectWiFi(true);
}

void loop()
{
  //Para leer datos sensor1
  Firebase.getInt(firebaseData, nodo + "/sensor1");
  Serial.println(firebaseData.intData());

  //Para leer datos sensor2
  Firebase.getString(firebaseData, nodo + "/sensor2");
  Serial.println(firebaseData.stringData());

  //Para escribir datos
  Firebase.setInt(firebaseData, nodo + "/sensor1", 512);
  Firebase.setString(firebaseData, nodo + "/sensor2", "On");

  //Para push para crear una variable con nombre aleatorio
  Firebase.pushInt(firebaseData, nodo + "/lecturas", 256);

  //Cerrar la conexion esto es cuando no lo volvamos a utilizar
  //Firebase.end(firebaseData);
  delay(3000);
}
```
