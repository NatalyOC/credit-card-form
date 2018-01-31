# Credit Card Form

## Objetivo:
- Leer el codigo javascript e identificar las funciones globales, locales, funciones de callback, expresions, statement, clousure, scope, contextos de ejecucion, que funciones forman parte de la pila de ejecucion (stack execution) y que funciones forman parte de la cola de eventos (event queue) Conceptos revisados el día de hoy.

***

### Solucion:

De acuerdo al ambiente lexical
* Es una función global.
```js
$(document).ready(function() {
  ...
  });  
});
```
* Son variables locales (No es global por que se encuentra dentro de una funcion).
```js
 var $inputCard = $('#card-number');
  var $inputMonth = $('.input-month');
  var $inputYear = $('.input-year');
  var $buttonNext = $('#next');
  var regexOnlyNumbers = /^[0-9]+$/;
  var labelErrorOrSuccessMessages = $('label[for="card-number"]');
 ``` 
* En la linea númeradas (1-22-25-29)se declaran funciones callback.
```js
function isValidCreditCard(numberCard) {
1    var creditCardNumber = soloNumeros(longitud(numberCard));
    if (creditCardNumber !== undefined) {
      var arr = [];
      var sumaTotal = 0;
      for (var index = creditCardNumber.length - 1; index >= 0; index--) {
        arr.push(creditCardNumber[index]);
      }
      for (var index = 1; index < arr.length; index = index + 2) {
        arr[index] = arr[index] * 2;
        if (arr[index] >= 10) {
          arr[index] = arr[index] - 9;
        }    
      }
     
      for (var index = 0; index < arr.length; index++) {
        sumaTotal = sumaTotal + parseInt(arr[index]);
      }
     
      if (sumaTotal % 10 === 0) {
        console.log('Es una tarjeta valida');
22-        activeButton();
      } else {
        console.log('No es un numero valido');
25-        desactiveButton();
      }
    } else {
      console.log('Verifique el numero de su tarjeta'); 
29-      desactiveButton();  
    }
  }
});
```
* Todas las funciones son functions statements de Scope Local.

```js
 function activeButton() {
    $buttonNext.attr('disabled', false);
  } 
 function desactiveButton() {  
    $buttonNext.attr('disabled', true);
  } 
function longitud(input) {
    if (input.trim().length === 16) {
      return input;
    }
  }
function soloNumeros(input) {
    var regex = /^[0-9]+$/;
    if (regex.test(input)) {
      return input;
    }
  }
function isValidCreditCard(numberCard) {
...
});
```
* Clousure :
Recuerda el entorno padre.
isValidCreditCard($(this).val().trim());


* Funciones que forman parte de la cola de eventos(event queue):
```js
 $inputCard.on('input', function() {
    isValidCreditCard($(this).val().trim());
  });
```

* Funciones forman parte de la pila de ejecución (stack execution):
```js
activeButton();
desactiveButton()
longitud(input)
soloNumeros()
isValidCreditCard(numberCard);
$(document).ready(function() {
  ...
  });  
});
```
***
### Contextos de ejecucion

#### Fase de Creacion:
* Se crea el objeto Window y la variable this, la función global $(document).ready finalmente se crean las variables y funciones locales.

#### Fase de Ejecucion:
* Se ejecuta la función global, console.log y se asignan los valores a las variables locales.
* El evento input se coloca en la cola de eventos.
* Se ejecutan de arriba abajo hacia arriba de acuerdo a la pila de ejecución(ver stack execution)
* Finalmente se ejecuta el evento input.


 
