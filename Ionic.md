<h1 align="center">
    Apuntes de Ionic 3
</h1>

Librerías JS para Ionic
Música
https://howlerjs.com/

Para instalarlo, desde terminal:

npm install howler --save
Y donde lo quieras usar lo importas con sintaxis ES6:
import * as howler from 'howler';

NavController

Cualquier vista que se añade o quita a un NavController emite ciertos eventos que puedes aprovechar para inicializar la vista, refrescar contenido o guardar datos, por ejemplo.

Una Vista de Aplicación = Una Página = Un Componente

Todo componente de Angular tiene un ciclo de vida, lo mismo sucede con Ionic.
Angular y Ionic nos ofrecen eventos que podemos capturar en cada etapa del ciclo de vida (En Ionic también podemos usar estos eventos de Angular).
Estos eventos nos informan en qué etapa específica nos encontramos del ciclo de vida de un componente desde su creación hasta su destrucción para que de esta manera puedas ejecutar tareas de manera más eficientes en tu aplicación.

Ciclo de Vida de un Componente de Ionic
Entrando:
contructor() > ionViewCanEnter() > ionViewDidLoad() > ionViewWillEnter() > ionViewDidEnter() > Listo
Saliendo:
ionViewCanLeave() > ionViewDidLeave() > ionViewWillUnload() > Listo

https://lh3.googleusercontent.com/siNgCX3njHgGcZ6MW46bG9mVZNagFsLzao4Nxik7tRTRtLAWnyguWgzH-U53dr-kBRFfZlUGHA=s1200

constructor():
Característica de ES6.
Primer evento que se dispará cuando se crea la página.
No hay seguridad que todo dentro de su clase este listo para su uso.
Acá no se debe de realizar llamadas API REST (esto podría retrasar la creación de su clase y con ello hacer lenta la aplicación o causar comportamientos inesperados). 
Debe de mantenerse lo más simple posible y solo inicializar las variables de su clase. 
Este evento se dispara cuando se está creando la página y solo lo hace una vez.

@IonicPage()
@Component({
  selector: 'page-home',
  templateUrl: 'home.html',
})
export class HomePage {

  constructor(){
    //your code
  } 

  ...

}

ionViewCanEnter():
Útil si queremos chequear algo antes de entrar a la página.
Ideal para comprobar si cuentas con los permisos para poder ver el contenido de la página.
Debes de asegurarte que la lógica que utilices acá devuelva un booleano.
Retorna: boolean/Promise<void>

@IonicPage()
@Component({
  selector: 'page-home',
  templateUrl: 'home.html',
})
export class HomePage {
  ...

  ionViewCanEnter(){
    return //your check;
  }

}

ionViewDidLoad():
Se ejecuta cuando la página se ha cargado. 
Se llama únicamente cuando cargas una página en memoria (setRoot y push) y no se llama cuando se devuelve la página con un pop.
Puede estar seguro de que todas sus variables y dependencias inyectadas están disponibles para su uso. 
Esta es la función donde usted puede hacer todas sus llamadas HTTP iniciales para obtener sus datos y hacer el levantamiento pesado principal de su aplicación. 
Retorna: void



@IonicPage()
@Component({
  selector: 'page-home',
  templateUrl: 'home.html',
})
export class HomePage {
  ...

  ionViewDidLoad(){
    //your code;
  }

}

ionViewWillEnter()
Se ejecuta cuando la página está a punto de entrar y convertirse en la página activa. 
A pesar de que la página está completamente cargada desde el punto de vista del código, aùn hay cierta lògica que procesar (animaciòn de las transiciones, etc) para hacer que tu página sea totalmente activa y visible para el usuario. 
Este es un gran lugar para tareas que se deben de realizar siempre que entras en la vista, como activar listener de eventos, actualizar una tabla, ocultar y mostrar cosas en su página antes de que sea visible para el usuario etc.
Retorna: void

@IonicPage()
@Component({
  selector: 'page-home',
  templateUrl: 'home.html',
})
export class HomePage {
  ...

  ionViewWillEnter(){
    //your code;
  }

}

ionViewDidEnter()
Se ejecuta cuando la página ha entrado completamente y ahora es la página activa. 
Este evento se disparará, ya sea la primera carga o al cargar la página en caché. 
Es la función final que se activa al navegar en una página como parte del ciclo de vida de ella. Acá ya puedes poner toda la lógica que desees aunque se utiliza fundamentalmente para alguna característica que necesitas que el usuario vea muy pronto o la primera cosa que desees que el usuario interactúe cuando entre a la página.

Lo use para bloquear el slide del slider cuando hay solo un elemento. Con este evento me asegure que se halla renderizado el slider.
Retorna: void

@IonicPage()
@Component({
  selector: 'page-home',
  templateUrl: 'home.html',
})
export class HomePage {
  ...

  ionViewDidEnter(){
    //your code;
  }

}

ionViewCanLeave()
Corre antes de que la vista pueda salir. 
Esto puede usarse como una especie de “guardia” en las vistas autenticadas donde necesita comprobar los permisos antes de que la vista pueda salir. 
En esencia es lo mismo a ionViewCanEnter() pero en este caso te deja salir de la página si la lógica que utilizaste dentro de ella retorna true.
Retorna: boolean/Promise<void>	

@IonicPage()
@Component({
  selector: 'page-home',
  templateUrl: 'home.html',
})
export class HomePage {
  ...

  ionViewCanLeave(){
    return //your check;
  }

}

ionViewWillLeave()
Se ejecuta cuando la página está a punto de salir. 
En el punto en que se desencadena este evento, sigue siendo la página activa, pero se ha puesto en cola para que se elimine y ya no se puede evitar salir de la página. 
Acá puede ser un buen lugar para desactivar listeners, preparar los datos que podrías utilizar en la siguiente página o realizar una llamada asíncrona alguna API que se necesitará en la próxima vista.
Retorna: void

@IonicPage()
@Component({
  selector: 'page-home',
  templateUrl: 'home.html',
})
export class HomePage {
  ...

  ionViewWillLeave(){
    //your code;
  }

}

ionViewDidLeave()
Se ejecuta cuando la página ha terminado de salir y ya no es la página activa.
Esta función es un gran lugar para guardar datos o estados de la página que está dejando, así cómo activar algunas operaciones de fondo que no requieren que la vista sea visible.
Retorna: void

@IonicPage()
@Component({
  selector: 'page-home',
  templateUrl: 'home.html',
})
export class HomePage {
  ...

  ionViewDidLeave(){
    //your code;
  }

}

ionViewWillUnload()
Es el último evento que se dispara en el ciclo de vida de una página típica de Ionic. 
Se ejecuta cuando vas a destruir por completo una página (al hacer pop).
Este es el lugar donde se liberan los recursos que ya no son necesarios y todo tipo de limpieza para evitar posibles pérdidas de memoria. 
Acá haces el “unsubscribe” a los eventos y observables que te hayas suscrito. 
Esta función sólo se ejecuta una vez y es la última parada antes de que la página se destruya y se desvincula de la vista con todos sus elementos eliminados.
Retorna: void

@IonicPage()
@Component({
  selector: 'page-home',
  templateUrl: 'home.html',
})
export class HomePage {
  ...

  ionViewWillUnload(){
    //your code;
  }

}


REFERENCIAS:
https://blog.ng-classroom.com/blog/tips/lifecycle-ionic/
http://blog.enriqueoriol.com/2016/11/ionic2-lifecycle-events.html
