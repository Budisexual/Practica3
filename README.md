# Práctica 03 — Desarrollo de experiencias de realidad virtual

Proyecto desarrollado en Unreal Engine para la Práctica 03 de Desarrollo de experiencias de realidad virtual. Incluye una sala con varios minijuegos para utilizar en realidad virtual mediante Meta XR.

## 1\. Software y versiones

|Elemento|Versión|
|-|-|
|Unreal Engine|**5.8**|
|Meta XR Plugin|**El otorgado inicialmente**|
|Meta XR Simulator|`81.0.0.865.254`|
|Sistema operativo probado|**Windows 11**|

## 2\. Contenido y minijuegos

La experiencia reúne los siguientes minijuegos.

### 2.1. Bolos

**Cómo se juega:** agarrar la bola, situarse frente a la formación triangular de bolos y lanzarla para derribarlos. La bola y los bolos utilizan simulación física.

**Blueprints y elementos principales:**

* `BP\\\\\\\_GrabComponent`: componente compartido del proyecto utilizado para agarrar objetos.
* Blueprint de la bola: **Bola**

### 2.2. Rompeobjetos — Wreck-It Ralph

**Cómo se juega:** agarrar el martillo y golpear la piñata fracturada para provocar su rotura en fragmentos mediante Chaos Geometry Collection.

**Blueprints y elementos principales:**

* GC\_pinata2: estructura que se rompe (se ha utilizado esta porque las estatuas importadas no funcionaban.)
* `BP\\\\\\\_GrabComponent`: componente utilizado para agarrar el martillo.
* Blueprint del martillo: **Martillo**

### 2.3. Mr. Potato

**Cómo se juega:** colocar las distintas piezas del personaje sobre el cuerpo central. Cuando una pieza entra en contacto con el cuerpo y el usuario la suelta, debe quedar acoplada a él.

**Blueprints y elementos principales:**

* Blueprint del cuerpo central: **Cuerpo**
* Blueprint de las piezas: Piezas
* Componente de agarre utilizado: **BP\_GrabComponent**

### 2.4. Dardos

Importante: a veces un dardo a la primera no funciona, pero a la segunda siempre.

**Cómo se juega:** agarrar un dardo y lanzarlo hacia la diana. Al impactar, el dardo deja de simular física y queda unido a la diana. La puntuación depende de la distancia entre el punto de impacto y el centro: cuanto más cerca del centro, más puntos se obtienen.

**Zonas de puntuación implementadas:**

|Zona|Distancia respecto al radio exterior calculado|Puntos|
|-|-:|-:|
|Centro|Hasta el 10 %|50|
|Intermedia|Más del 10 % y hasta el 50 %|30|
|Exterior|Más del 50 % y hasta el 100 %|10|
|Fuera de la zona puntuable|Más del 100 %|0|



**Blueprints y elementos principales:**

* `Dardo`: actor del dardo; incorpora `BP\\\\\\\_GrabComponent` y la variable `bHasScored` para evitar que un mismo dardo puntúe más de una vez.
* `Diana`: detecta los impactos, detiene la simulación física del dardo, lo acopla a la diana y calcula la puntuación.
* `WDM\\\\\\\_MarcadorDardos`: widget que muestra la puntuación acumulada.
* `BP\\\\\\\_GrabComponent`: componente de agarre.
* Funciones relevantes de `Dardo`: `GetHasScored` y `MarkAsScored`.
* Función relevante de `Diana`: `CalcularPuntuacion`.
* Función relevante del widget: `ActualizarPuntuacion`.

## 4\. Estructura del proyecto

* `Practica3.uproject`: archivo principal del proyecto.
* `Config/`: configuración del proyecto y de los plugins.
* `Content/`: niveles, Blueprints, widgets, materiales y recursos importados.
* `Plugins/`: plugins incluidos en el proyecto, entre ellos Meta XR.
* `LanzarConSimulador.bat`: archivo de lanzamiento utilizado para iniciar el proyecto con el simulador.
* `.gitignore`: excluye carpetas generadas y archivos que no se versionan, como `Binaries/`, `Intermediate/`, `Saved/` y `DerivedDataCache/`.

## 5\. Controles

|Acción|Control|
|-|-|
|Agarrar / soltar objetos|**Doble click a la rueda del raton**|
|Desplazamiento|**WASD**|
|Teletransporte|**Click a la rueda del raton**|



