## Situación de partida

Hemos desarrollado una app con Quasar + Vue (quasar.dev) que nos muestra todos los juegos gratuitos a los que podemos jugar.

Para obtener el listado, consumimos un API proporcionado por el portal **Free-To-Play** ([https://www.freetogame.com/api-doc](https://www.freetogame.com/api-doc)) que nos devuelve un listado de juegos.

Por defecto, nuestra aplicación permite filtrar por tipo de plataforma y nos muestra el listado de juegos disponibles con una maquetación mínima. Veamos las capturas de lo que hace hasta ahora la app:

***Selección de juegos:***
![Selección de la plataforma](https://i.im.ge/2022/07/08/ukn7PS.png)
***Listado de juegos sin maquetar:***
![Listado de juegos sin maquetar](https://i.im.ge/2022/07/08/uknDfz.png)

## Objetivos
El cliente nos pide que el listado de juegos se muestre adaptado a distintos tipos de dispositivos en función de sus dimensiones de pantalla:

 - xs = 1 columna
 - sm = 2 columnas
 - md = 3 columnas
 - &gt; md= 4 columnas

Además nos pide mejorar el aspecto de la caja que contiene cada juego y que le demos un aspecto más tipo ficha. Ahora mismo, se muestra una caja por cada juego sin un buen diseño gráfico. Nos sugiere un diseño tipo, por ejemplo, como aparecen los streamers en Twitch pero adaptado a la información con la que nosotros contamos para cada juego:
![Ejemplo de vista de streamer de Twitch](https://i.im.ge/2022/07/08/uknnzS.png)

**De todas formas, el cliente nos da libertad para proponer otra vista u otros cambios en la página.
Quiere que el resultado sea bonito y funcional y se pone en nuestras manos. Y nos indica que podemos usar diseños propios o componentes de Quasar para mejorar la vista.**


## ¿Qué necesitamos?
El responsable del proyecto, Antonio, ya ha creado la estructura básica con Quasar, ha sincronizado Quasar con el API de **Free-To-Play** y programado la caja de selección de plaatforma para que cargue dinámicamente los juegos. Ha subido también el código fuente a un repositorio.

Por tanto, para poder continuar con el proyecto, tenemos que:

 1. Descargarnos e instalar en nuestro equipo Node.js (https://nodejs.org/es/download/)
 2. Descargarnos el instalador de paquetes Yarn (https://yarnpkg.com/getting-started/install)
 3. Instalamos el cliente de líneas de comandos de Quasar con el comando: `yarn global add @quasar/cli` o `npm i -g @quasar/cli`
 (Más info en: https://quasar.dev/start/quasar-cli)
 4. Descargarnos el repositorio con el código fuente ya creado desde:
`https://gitlab.com/sistemassnackson/prueba-frontend`

 5. Desde nuestra terminal del sistema o la terminal integrada en nuestro editor(por ejemplo Visual Studio Code) accedemos al directorio del repositorio descargado y ejecutamos el comando para instalar las dependencias: `yarn` o `npm install`
 6. Una vez se hayan terminado de instalar las dependencias, ejecutamos el comando que nos abrirá un navegador: *`quasar dev`*
 7. Lá página donde se ubica el código actual y que se encarga de listar los juegos se encuentra en: "./pages/IndexPage.vue"

## ¿Cómo entregamos?

Una vez hayamos aplicado nuestros cambios, hay que subir el proyecto a un repositorio git y mandaremos un correo a Antonio indicándole el repositorio y le contaremos qué cambios hemos decidido aplicar o qué problemas hemos tenido en el desarrollo.


## Más info

#### Quasar tutoriales
Entender Quasar - Vídeos 1 y 2
1. https://www.youtube.com/watch?v=f6JXyPXUyNc&list=PLPl81lqbj-4LDCH5nPAHjoaQPDsivSem3
2. https://www.youtube.com/watch?v=3sbMmXalEpw&list=PLPl81lqbj-4LDCH5nPAHjoaQPDsivSem3&index=2

-- Quasar ha cambiado un poco desde los primeros vídeos, por lo que si hay dudas recomiendo ver este otro vídeo desde el mínuto 5 al 15 aprox que es la nueva versión actualziada del proceso de instalación:
https://www.youtube.com/watch?v=n4sdgDTrqEU&t=310s

