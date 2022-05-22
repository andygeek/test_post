---
title: Hola mundo en Android
date: "2020-07-22T18:46:37.121Z"
template: "post"
draft: false
slug: "Hola-mundo-en-android"
category: "Fundamentos de Android"
tags:
  - "Android"
  - "Programming"
  - "Java"
  - "Desarrollo móvil"
description: "Este es el primer tutorial de la serie 'Fundamentos de Android con Java' En este tutorial vamos a explicar algunos conceptos importantes creando nuestro primer proyecto en Android."
socialImage: "/media/android.jpg"
---

En este tutorial explicaremos algunos conceptos importantes creando nuestro primer proyecto en Android. Nuestra aplicación mostrará un Snackbar que a su vez mostrará un mensaje de **Hello world**. Puede parecer simple pero a medida que desarrollemos el proyecto iremos explicando algunos conceptos muy importantes del desarrollo nativo en Android.

## Índice

1. [Nuestro primer activity](#1-nuestro-primer-activity)
2. [Ciclo de vida de un activity](#2-ciclo-de-vida-de-un-activity)
3. [El layout o diseño de un activity](#3-el-layout-o-diseño-de-un-activity)
4. [Un Layout con restricciones](#4-un-layout-con-restricciones)
5. [Más sobre los atributos XML](#5-más-sobre-los-atributos-xml)
6. [Creando nuestro primero botón](#6-creando-nuestro-primero-botón)
7. [Usando la consola para probar código](#7-usando-la-consola-para-probar-código)
8. [Material Design en nuestro proyecto](#8-material-design-en-nuestro-proyecto)
9. [Creación de SnackBar](#9-creación-de-snackbar)
10. [El código](#10-el-código)


## 1. Nuestro primer Activity

El primer concepto que debemos explicar en Android es el de Activity, ya que lo veremos desde la creación de cualquier proyecto en Android Studio. Los activitis son las vistas o interfaces gráficas de usuario de una aplicación Android. Es el lienzo donde agregaremos diferente elementos visuales para nuestra aplicación.

Cada activity en Android tiene asociado dos elementos importantes. El primero es la clase de Java o Kotlin que controla lo que sucederá con cada elemento que este en el interior del activity y el segundo es un archivo XML en el cual se diseña la interface del activity. Más adelante analizaremos cada archivo individualmente. Ahora crearemos nuestro primer Activity y proyecto en Android Studio.

Luego de ingresar a Android Studio en la pantalla de inicio hacemos click en el botón **Start a new Android Studio project** para crear nuestro primer proyecto Android.

![](https://imgur.com/FAAKPfO.png)

Luego escogeremos el Template o plantilla que queremos para nuestro proyecto. En este caso queremos comenzar con un activity vacío por eso seleccionamos **Empty Activity**.

![](https://imgur.com/aeHWTqN.png)

La nueva ventana nos pedirá información sobre nuestro proyecto y sobre nuestro primer activity. Aquí explicaremos cada espacio que debemos rellenar. 

![](https://imgur.com/Iw9Q2bW.png)

**- Name:** Es el nombre de nuestra aplicación puede tener letras, números, mayúsculas, minúsculas y espacios.

**- Package Name:** Es el identificador de nuestro proyecto. Este identificador debe ser único en la PlayStore, estar en minúsculas y además debe tener la siguiente forma ```com.<org>.<nombre>```. Nosotros usaremos ```com.andygeek.helloworld``` para este proyecto.

**- Save location:** Es la ubicación en nuestro disco duro para nuestro proyecto.

**- Language:** Es el lenguaje de programación que usaremos para nuestro proyecto. Podemos escoger entre Kotlin y Java. Este tutorial explica los fundamentos usando Java.

**- Minimun SDK:** Es la versión mínima de Android que soportará nuestra aplicación. Recuerda que mientras más alta sea la versión menos dispositivos podrán soportar nuestra aplicación. En este caso utilizaremos la versión 5 **Lollipop**. Si queremos saber que porcentaje de equipos son soportados por cada versión podemos hacer click donde dice **Help me choose**.

**- Use legacy android.support libraries:** A groso modo si seleccionamos este casillero nuestra aplicación podrá tener mayor compatibilidad hacia versiones de Android anteriores pero los detalles lo explicaremos en próximos tutoriales así que por ahora no marcaremos este casillero.

Para finalizar hacemos click en el botón **Finish** y Android Studio creará toda la estructura inicial para nuestro proyecto. Esta estructura consta de archivos y carpetas organizados en paquetes como se muestra a continuación.

![](https://imgur.com/ENJK6gw.png)

<div class="importante">
Si queremos cambiar la vista y ver los archivos y carpetas hacemos click en la parte superior donde dice <strong>Android</strong> y seleccionamos <strong>Project files</strong>.
</div>

La estructura que tenemos consta de dos elementos principales. El primero es ```app``` que es donde se encuentra los archivos propios de nuestra aplicación. El segundo elemento es ```Gradle Scripts``` que contiene los archivos importantes de Gradle, que es el administrador de paquetes y dependencias de Android.

Dentro de ```app``` tenemos el paquete ```manifests``` que contiene el manifiesto de nuestro proyecto, que es un archivo con metadatos importante sobre nuestro proyecto y sus activities. El segundo paquete es ```java``` y contiene los archivos de java o kotlin que controlan los activities de nuestro proyecto. El tercer paquete es ```res``` y contiene los recursos de nuestro proyecto, que van desde los layout o diseños de nuestras interfaces de usuario en XML hasta los iconos e imágenes que usaremos en el proyecto.

Entre todos los archivos que se generaron automáticamente en nuestro proyecto dos de ellos pertenecen al **empty activity** que creamos al inicio. Estos son el archivo ```activity_main.xml``` y el ```MainActivity.java```.

![](https://imgur.com/FeXIb4t.png)

Dentro del ```MainActivity.java``` encontraremos la clase que controla el activity. Mientras que en el archivo ```activity_main.xml``` es donde se define el diseño del activity usando el lenguaje XML.

Ahora analizaremos el código Java que trae nuestro primer activity por defecto.
```java
// Esta es una clase publica que hereda propiedades de la clase AppCompatActivity
public class MainActivity extends AppCompatActivity {

    // Sobreescribimos el método onCreate
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

- La clase ```AppCompatActivity``` proporciona compatibilidad de características actuales de Android, en nuestro activity.
- El método ```onCreate``` es un método sobreescrito que tenemos en un activity y es parte del ciclo de vida del activity. Todo lo que está dentro de este método se ejecutará al momento que se cree el Activity.
- El objeto ```R``` nos da una referencia a los recursos de nuestro proyecto. En este código referenciamos el layout de nuestro activity para entregárselo a la clase del actvity usando el método ```setContentView()```.

## 2. Ciclo de vida de un activity

Un activity pasa por diferentes estados desde el momento en el que es creado al ingresar al activity hasta cuando este es eliminado al cerrar o cambiar de activity. Cada uno de estos estados tienen un método asociado a él que se ejecuta justo cuando el activity entra en ese estado. Nosotros podemos sobrescribir estos método para tener control sobre los estados de un activity.

En el siguiente esquema podemos ver cuales son los estados por el que pasa un activity y los métodos asociados a ellos.

![](https://developer.android.com/guide/components/images/activity_lifecycle.png)

El ciclo de vida requiere una explicación más extensa por lo que se explicará en próximos tutoriales haciendo uso de ejemplos. Lo que deben saber ahora es que un activity tienen un ciclo de vida en cuyos estado podemos ejecutar código sobrescribiendo los métodos ```onCreate```, ```onStart```, etc.

## 3. El layout o diseño de un activity

En Android los diseños se reducen a código XML. El código es muy intuitivo y además Android Studio nos brinda una herramienta para poder generar este código de forma automática. Sin embargo, el uso de código es la forma más rápida de generar diseños.

Cada elemento visual dentro de un activity es conocido como **widget** y lo podemos definir usando código XML como en el siguiente ejemplo. Donde colocamos primero el nombre del widget y luego sus atributos en forma de cascada o lista.

```xml
<Nombre_widget
    atributo_del_widget="valor_del_atributo"
    atributo_del_widget="valor_del_atributo"
    atributo_del_widget="valor_del_atributo"/>
```

Los dos atributos que siempre estarán presentes en los widgets son el ```android:layout_width``` y ```android:layout_height``` que indican el ancho y alto del widget respectivamente. El valor de estos atributos puede ser numérico pero los más frecuentes son ```wrap_content``` y ```match_parent```. El primero se utiliza para que el valor se adapte al contenido del widget. Mientras que el segundo, se utiliza para que el valor se adapte automáticamente al elemento padre que lo contiene.

![](https://imgur.com/kHwHiT4.png)

Uno de los widgets más básico en Android el **TextView**, ya que únicamente muestra un texto en la pantalla. La forma de su código XML es e siguiente.

```xml
<TextView
     android:layout_width="match_parent"
     android:layout_height="wrap_content"
     android:text="Hello"
     android:textSize="23dp"/>
```

El atributo ```android:text``` indica el texto dentro del widget y ```android:textSize``` indica el tamaño de fuente del texto. 

Asi como estos tenemos atributos que son generales y la gran mayoría de widgets lo tienen como ```android:text```, ``` android:layout_width```,  ```android:layout_height```, etc. Estos atributos te serán fáciles de recordar ya que los estarás utilizando a cada momento. En caso de encontrarte con algún atributo que desconozcas o quieras saber si alguna característica de un widget se puede cambiar lo más recomendable es buscarlo en la [documentación oficial de Android](https://developer.android.com/) o investigar en foros de internet. **Recuerda que el desarrollo es 80% leer código y solo un 20% escribirlo.**

## 4. Un Layout con restricciones

Un **layout** en android es análogo a un **div** en el desarrollo web. Es el contenedor de widgets con el que podemos ordenar la interface de usuario que estamos desarrollando. Dentro de nuestro archivo ```activity_main.xml``` ya tenemos algo de código autogenerado. Entre todo este código generado tenemos al ```constraintlayout``` que es un tipo de **layout** que contiene al único **TextView** que contiene nuestra aplicación.

Pero, qué es el **ConstraintLayout**. Un ConstraintLayout es un layout en cuyo interior podemos definir la posición de los widgets haciendo uso de restricciones (**constraints**) respecto a otros widgets que estén cerca o a su widget padre. Como vemos en el siguiente ejemplo, gracias al ConstraintLayout podemos definir el sitio del botón usando restricciones en los cuatro lados del botón respecto al widget padre (ConstraintLayout).

![](https://imgur.com/MWq0YOG.gif)

El nombre ```androidx.constraintlayout.widget.ConstraintLayout``` nos indica que viene de la librería ```androix``` que es una librería reciente que agregó muchas funcionalidades a Android.

En la imagen anterior usamos el editor de diseños que trae Android Studio pero usando el código XML definimos las restricciones de la siguiente manera.

```xml
app:layout_constraintBottom_toBottomOf="parent"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toTopOf="parent"
```

Donde ```layout_constraintBottom_toBottomOf = "parent"``` es una restricción (**layout_constraint**) entre el fondo (**Bottom**) del widget hacia el fondo del (**to Bottom of**) widget padre (**parent**).

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click here"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:onClick="chick_here"/>

</androidx.constraintlayout.widget.ConstraintLayout>
```

Pero que hay detrás del código debajo del ConstraintLayout como ```xmlns:app``` o ```xmlns:tools``` para qué sirven, ahora pasaremos a explicarlo.

## 5. Más sobre los atributos XML

Los atributos en XML tienen la siguiente forma ```name_space:atributo="valor"``` donde el ```name_space``` proporcionan una forma de evitar conflictos en los atributos. Es una especie de categoría para los atributos. Entonces existen tres categorías para los atributos, estos son:

- ```xmlns``` : Esten no es un atributo en sí, es más bien el que definirá la dirección donde se encuentra la definición para cada uno de las otras categorías de atributos que existen. Por ejemplo, ```xmlns:android="http://..."``` : No es la dirección de una web es más bien un **URI** o **Identificador de recursos uniforme**. Mediante esta dirección el analizador de código XML encuentra el archivo donde se encuentra el esquema para las demás categorías de atributos. 

- ```android```: Estos son atributos propios del widget y son definidos por el API de Android que estamos usando para el desarrollo.

- ```app```: Estos atributos no pertenecen a una librería especifica más bien pertenecen a atributos propios de tu aplicación, quizá de bibliotecas que importes o incluso algún atributo que puedas crear. En próximos tutoriales hablaremos más al respecto.

- ```tools```: Estos son atributos que sirven de herramienta para el desarrollador no tiene que ver tanto con el widget en sí, si no más bien de cómo el widget se relaciona con los demás.

```xml
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
```

Entonces volviendo al código del ConstraintLayout. Los tres primeros atributos son necesarios ya que en esa dirección el analizador de XML encontrará el esquema necesario para definir los atributos ```android```, ```tools``` y ```app```. Las dos propiedades siguientes indican el alto y ancho del widget, ya lo explicamos anteriormente. Y el último atributo ```tools:context``` indica el archivo java donde está la clase que controlará a este layout.

## 6. Creando nuestro primero botón

El boton es uno de los widgets más usados dentro de cualquier aplicación. En Android tenemos el widget ```Button``` que nos permite crear un botón dentro de nuestra aplicación. Su código XML es el siguiente.

```xml
<Button
    android:id="@+id/btn_click"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="Hazme click"/>
```
Para poder capturar un evento del botón tenemos que utilizar el atributo ```id``` para poder identificarlo desde nuestra clase de java cuando queramos hacer uso de él. Un **id** en Android tiene la siguiente forma ```@+id/nombre```. Esto tiene que ser así porque el analizador de código XML de Android Studio identifica al ```@``` se prepara para recibir un id y al identificar al ```+id\``` el analizador sabe que tiene que agregar ese id a la lista de referencias de la clase R con el nombre que está después de ```\```. De esta manera podremos encontrar su referencia en el código Java usando la clase R.

Ahora que ya tenemos un botón creado en nuestro diseño, crearemos el método que será ejecutado al hacer click en el botón. 

En Android existen varias formas de vincular un botón a un método en este tutorial utilizaremos la forma más simple. vincularemos la función desde los atributos de Widget Button en el archivo ```main_activity.xml```. En un próximo tutorial hablaremos más a profundidad de los otros métodos.

Primero tenemos que crear la función en el archivo Java del activity donde se encuentra el botón. Yo lo llamaré ```click_here``` y dentro el código que se ejecutará cuando hagamos click en el botón. Pero para que el método sea reconocido por el código XML debe tener como parámetro a un objeto del tipo ```View```.

```java
public void click_here(View v){
    // Código a ejecutar
}
```

Luego en el archivo ```activity_main.xml``` debemos agregar el atributo onClick al widget Button y luego como valor colocar el nombre de la función que acabamos de crear en el archivo Java.

```xml
android:onClick="click_here"
```

## 7. Usando la consola para probar código

A veces es necesario usar la consola para probar algún widget que deseamos ejecutar o que no sabemos por qué no funciona correctamente, no sé si alguien lo dijo ya pero...

<div class="frase">La consola es el mejor aliado del desarrollador.
</div>

Para mostrar un mensaje en consola podemos hacerlo a la antigua usando el ```System.out.println()``` que nos proporciona Java o usar un el ```Log.i()``` que nos proporciona Android. Este último método es el más adecuado y para usarlo debemos enviarle dos parametros el primero es el nombre o identificador del mensaje y el segundo es el mensaje en si.

```java
Log.i("nombre_del_mensaje", "mensaje");
```

El mensaje solo saldrá cuando emulemos nuestra aplicación. Para encontrar el mensaje usaremos la pestaña **Logcat** y buscando ahí el mensaje con el nombre que le dimos a este. De la siguiente manera.

![](https://imgur.com/1RQyrFT.png)

<!--- Pero para poder emular nuestra aplicación necesitamos primero crear una máquina virtual de Android. Aquí tengo un articulo dedicado a este tema, te sugiero revisarlo antes de continuar. [Emular aplicaciones en Android Studio]() -->

## 8. Material Design en nuestro proyecto

Material Design es el lenguaje visual que junta los principios de diseño que Google desarrollo en el 2014. Gracias a Material Design tenemos una gran cantidad de componentes como SnackBars, Cards, etc que podemos usara en nuestra aplicación si agregamos las dependencias necesarias.

Para mostrar nuestro Hola mundo utilizaremos un componente de Material Desig llamado SnackBar necesitamos implementar la dependencias de Material Design a nuestro proyecto. Dentro de la [documentación de Material Design](https://material.io/develop/android/docs/getting-started/) tenemos información sobre cómo agregar esta dependencia en nuestro proyecto. 

Una de las formas de agregar Material Design al proyecto es usando la siguiente línea de código dentro del archivo ```build.gradle (Module:app)```, que controla las dependencias o librerías externas de nuestro proyecto.

![](https://imgur.com/hhmiJxp.png)

```js
implementation 'com.google.android.material:material:1.0.0'
```

Es importante que luego de alguna modificación en el Gradle el proyecto sincronice las nuevas dependencia. Para esto solo hacemos click en **Sync Now**.

![](https://imgur.com/q79iN5A.png)

Otra forma que nos brinda Android Studio para poder implementar dependencias dentro de nuestro proyecto es usando la herramienta **Project Structure** en el cual dentro de la sección **Dependencies** podemos buscar la dependencia que queramos agregar.

![](https://imgur.com/BJU6L0y.gif)


## 9. Creación de SnackBar

Un SnackBar no es más que una barra de que muestra un mensaje dentro de nuestra aplicación. Al ser parte de Material Design solo podremos utilizarlo después de haber agregado su dependencia dentro del proyecto.

![](https://lh3.googleusercontent.com/-osHhhWWYPzLb8UmhUU1pmmd2q-bUj1vU8raFKcPtAxDPMdRlGixw31rhd1EcOiW6guvgFZAflH7rFF1b-D45Pk-SFmPGiBg9BpazQ=w1064-v0)


<!--
<div class="importante">
A veces Android Studio no reconoce una clase de alguna implementación que hicimos en el gradle o layout de algún activity que agregamos. A veces solo reconoce después de reiniciado el programa.
</div>
-->

Para crear un SnackBar se necesita crear un objeto ```Snackbar``` dentro del código. En el siguiente ejemplo explicamos el código que debemos utilizar.

```java
public void chick_here(View v){
    
    // Creamos el objeto snackbar y utilizamos make para inicializarlo
	Snackbar message = Snackbar.make(v, "Hello world", Snackbar.LENGTH_LONG);
    
    // Mostramos el snackbar
    message.show
}
```
- El primer parámetro que recibe el ```Snackbar.make``` es el ```View``` donde se renderizará el SnackBar, de hecho el SnackBar buscará al último padre del View enviado para renderizarce.

- El segundo parámetro es el mensaje en string. Ahí escribimos el ```"Hello World"```.

- El tercer y ultimo parámetro es el tiempo de duración del mensaje. Para esto usamos las constantes que tiene la misma clase Snackbar en este caso usamos LENGTH_LONG para que el SnackBar aparezca un tiempo más prolongado.



<div align="center"><img src="https://imgur.com/lfGooZl.gif" width="280" height="510" align="middle"/></div>

**Terminamos!! y como vimos Android no es difícil pero esta lleno de conceptos. Así que en los siguientes tutoriales haremos nuevos y más complejos proyectos para Android.**

## 10. El código

El código fuente de la aplicación la podemos encontrar en el siguiente repositorio: [github.com/andygeek/HelloWorld](https://github.com/andygeek/HelloWorld)
