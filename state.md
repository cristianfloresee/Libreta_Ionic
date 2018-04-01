Referencia: https://angular.io/api/animations/state

Paquete NPM: @angular/animations
Modulo: import { state } from '@angular/animations';
Fuente: animations/src/animation_metadata.ts

function state(
    name: string,
    styles: AnimationStyleMetadata,
    options?: {
        params: {
            [name: string]: any;
        }
    }  
): AnimationStateMetadata;

state('nombre_estado', style({
    opacity: 1
    opacity: 0
    height:
    transform: scale(1)
    overflow:
    backgroundColor: #fff
}))

Descripción

state es una función de animación diseñada para ser usada dentro del lenguaje de animaciones de Angular. 

state declara un estado de animación dentro del trigger. 
Cuando un estado está activo dentro de un componente, sus estilos asociados persistirán en el elemento al que está asociado el trigger. (incluso cuando finalice la animación)

El state void
El valor del state void es una palabra reservada que usa angular para determinar cuando el elemento no está separado de la aplicación?.
Por ejemplo: Cuando el ngIf se evalua como false, el state del elemento asociado es void.

El state *






transition: ease-in-out 0.5s; //DIFUMINAR
opacity: 0; //TOTALMENTE TRANSPARENTE
opacity: 1;
