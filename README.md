# Esp32-Firebase

### Paso 1: Ir a la consola
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso1.png" width="1000" height="500" />

### Paso 2: Agregar proyecto
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso2.png" width="1000" height="500" />

### Paso 3: Crear el proyecto
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso3.png" width="1000" height="500" />

### Paso 4: Deshabilitar google analytics y confirmar para crear proyecto
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso4.png" width="1000" height="500" />

### Paso 5: Ir a Realtime Database
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso5.png" width="1000" height="500" />

### Paso 6: Crear una base de datos
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso6.png" width="1000" height="500" />

### Paso 7: Configurar base de datos
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso7.png" width="1000" height="500" />

### Paso 8: Seleccionar reglas de seguridad
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso8.png" width="1000" height="500" />

### Paso 9: Copiar la url del proyecto
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso9.png" width="1000" height="500" />

### Paso 10: Ir a configuracion del proyecto
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso10.png" width="1000" height="500" />

### Paso 11: Ir a cuentas de servicio
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso11.png" width="1000" height="500" />

### Paso 12: Ir a secretos de la base de datos
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso12.png" width="1000" height="500" />

### Paso 13: Copiar Secreto
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso13.png" width="1000" height="500" />

### Paso 14: Descargar la libreria de Firebase
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso14-Descargar-Libreria-de-Firebase.png" />

### Codigo
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

  //Para escribir datos, si existe sensor1 lo sobrescribe y sino existe lo crea
  Firebase.setInt(firebaseData, nodo + "/sensor1", 512);
  Firebase.setString(firebaseData, nodo + "/sensor2", "On");

  //Para push para crear una variable con nombre aleatorio
  Firebase.pushInt(firebaseData, nodo + "/lecturas", 256);

  //Cerrar la conexion esto es cuando no lo volvamos a utilizar
  //Firebase.end(firebaseData);
  delay(3000);
}
```
### En el puerto serial muestra los datos de Firebase
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso15-El-Esp32-Leyendo-Los-Datos.png" />

### Base de datos en Firebase muestra los datos enviados
<img src="https://github.com/IDiegoUlises/Esp32-Firebase/blob/main/Images/Paso16-En-Firebase-web-Muestra-Los-Datos.png" width="1000" height="500" />





