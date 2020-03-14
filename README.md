## Handling Events

**Autor : David Rodriguez Rodriguez**

**Event handlers**

Los controladores de eventos se tratan de aquellas funciones que nos permite hacer una función cuando pulsamos en esta.

Con el codigo siguiente lo que haremos sera leer cuando el usuario hace click en cualquier lado de la ventana del navegador ya que el enlace "window" permite resgistrar los click en toda la pagina.

```HTML
<p>Click this document to activate the handler.</p>
<script>
  window.addEventListener("click", () => {
    console.log("You knocked?");
  });
</script>
```

**Events and DOM nodes**

Los controladores de eventos se registra en un determinado contexto, se pueden usar objetos contenidos en DOM. Estos objetos son invocados cuando ocurre el evento, en el ejemplo siguiente funciona cuando pulsamos el botón.

El método **addListener** permite añadir cualquier tipo de controlodores, en cambio el metodo **removeEventListener** elimina el controlador del elemento que tiene asignado,en el siguiente codigo se puede ver como una vez que se pulse el botón este dejara de funcionar.


```HTML
<button>Act-once button</button>
<script>
  let button = document.querySelector("button");
  function once() {
    console.log("Done.");
    button.removeEventListener("click", once);
  }
  button.addEventListener("click", once);
</script>
```

**Event objects**

El Event Object se pasa a la funcion controladora como un argumento, conteniendo información sobre el evento que puede tener unas propiedades determinadas, en el siguiente codigo se ve como obtenemos que tipo de click estamos haciendo con el raton sobre el botón.

```HTML

  <button>Click me any way you want</button>
    <script>
      let button = document.querySelector("button");
      button.addEventListener("mousedown", event => {
        if (event.button == 0) {
          console.log("Left button");
        } else if (event.button == 1) {
          console.log("Middle button");
        } else if (event.button == 2) {
          console.log("Right button");
        }
      });
    </script>
```
**Propagation**

El método **stopPropagation** usado para evitar que los controladores reciban el evento.

**Target** se trata de unapropiedad para lanzar una red amplia para un tipo específico de evento, se puede usar esta propiedad para asegurarnos que no está manejando accidentalmente algo que se propagó desde un nodo que no desea manejar.


```HTML
<p>A paragraph with a <button>button</button>.</p>
<script>
  let para = document.querySelector("p");
  let button = document.querySelector("button");
  para.addEventListener("mousedown", () => {
    console.log("Handler for paragraph.");
  });
  button.addEventListener("mousedown", event => {
    console.log("Handler for button.");
    if (event.button == 2) event.stopPropagation();
  });
</script>
```

**Default actions**

El metodo **preventDefault** permite al usuario a configurar el comportamiento de la pagina evitando que funcione de manera normal, por lo con este método podremos crear atajos en nuestra pagina mediante teclado o menú, aunque existen algunas limitaciones dependiendo del navegador en el que nos encontremos.


```HTML
<a href="https://developer.mozilla.org/">MDN</a>
<script>
  let link = document.querySelector("a");
  link.addEventListener("click", event => {
    console.log("Nope.");
    event.preventDefault();
  });
</script>
```

**Key events**

Los eventos por clave se trata de leer las teclas del teclado una vez se pulsa o mantiente se siguen enviado repetidamente hasta que dejamos de pulsar la tecla, por lo que habrá que tener cuidado cuando se use un botón DOM ya que cuando se presiona una tecla y lo elimina nuevamente cuando se suelta la tecla, puede agregar accidentalmente cientos de botones.

El siguiente codigo de ejemplo, funciona cuando pulsamos la tecla **V** pondrá el fondo de la página en "violeta".

```HTML
<p>This page turns violet when you hold the V key.</p>
<script>
  window.addEventListener("keydown", event => {
    if (event.key == "v") {
      document.body.style.background = "violet";
    }
  });
  window.addEventListener("keyup", event => {
    if (event.key == "v") {
      document.body.style.background = "";
    }
  });
</script>
```

**Pointer events**

Existen dos formas para señalar por pantalla, que se trata del ratón y las pantallas táctiles

##### Mouse clicks:
 Existen metodos parecidos a los de teclado pero en este caso son **"mousedown"** y **"mouseup"** , funcionan en los nodos DOM que en los que se encuentra el puntero del ratón.

Cuando queremos obtener la informacion del lugar del suceso, existe la propiedad **clientX** y **clientY**  que obtiene las coordenadas delevento en pixeles 

El siguiente ![codigo](/ejemplos/Mouse_clicks.html) su función es poner un punto de clolor justo debajo del puntero cunado hacemos click. 

##### Mouse motion: 

Siempre que se mueve el ratón un evento "mousemove", es util  para rastrear la posición del ratón.

En el código de ejemplo que se nos da podemos ver que su objetivos es alargar o estrecha de izquiera a derecha según necesitemos una barra, al tener "window" si nos salimos de la barra continuara moviendo la barra hasta que soltemos el click.

##### Touch Event :

Cuando se comienza a tocar la pantalla se obtiene un evento **touchstart**, cuando nos movemos mientras mantenemos seran los eventos **touchmove** y cuando dejemos de precionar será el evento **touchend**. 

##### Scroll events :

Cada vez que usamos el scroll de ratón este activara un evento. Los principales usos de este tipo de evento es ver que parte de la pagina está mirando el usuario asi como realizar acciones cada a la vez que baja con el scroll.

##### Focus Event: 

##### Load event

##### Events and the event loop

##### Timers

##### Debouncing

##### Summary






### Ejercicios:


##### Ejercicio 1:

Censored Keyboard: program a text field (an input tag) where the letters Q, W, and X cannot be typed into.

```JavaScript 
<input type="text">
<script>
  var field = document.querySelector("input");
  field.addEventListener("keydown", function(event) {
    if (event.keyCode == "Q".charCodeAt(0) ||
        event.keyCode == "W".charCodeAt(0) ||
        event.keyCode == "X".charCodeAt(0))
      event.preventDefault();
  });
</script>
```

##### Ejercicio 2: 

Mouse trail: a series of images that would follow the mouse pointer as you moved it across the page.

```HTML
<style>
    .trail {
        position: absolute;
        height: 5px; width: 5px;
        border-radius: 4px;
        background: black;
    }
    body {
        height: 300px;
    }
</style>
<body>
    <script>
    var dots = [];
    for (var i = 0; i <= 10; i++) {
      var node = document.createElement("div");
      node.className = "trail";
      document.body.appendChild(node);
      dots.push(node);
    }
    var currentDot = 0;
    
    addEventListener("mousemove", function(event) {
      var dot = dots[currentDot];
      dot.style.left = (event.pageX - 3) + "px";
      dot.style.top = (event.pageY - 3) + "px";
      currentDot = (currentDot + 1) % dots.length;
    });
  </script>


```

##### Tabs: A tabbed interface. It allows you to select an interface panel by choosing from a number of tabs sticking out above an element.

```HTML
<div id="panel">
        <div data-tabname="one">Tab one</div>
        <div data-tabname="two">Tab two</div>
        <div data-tabname="three">Tab three</div>
    </div>
      <script>
        function asTabs(node) {
          let tabs = Array.from(node.children).map(node => {
            let button = document.createElement("button");
            button.textContent = node.getAttribute("data-tabname");
            let tab = {node, button};
            button.addEventListener("click", () => selectTab(tab));
            return tab;
          });
      
          let tabList = document.createElement("div");
          for (let {button} of tabs) tabList.appendChild(button);
          node.insertBefore(tabList, node.firstChild);
      
          function selectTab(selectedTab) {
            for (let tab of tabs) {
              let selected = tab == selectedTab;
              tab.node.style.display = selected ? "" : "none";
              tab.button.style.color = selected ? "red" : "";
            }
          }
          selectTab(tabs[0]);
        }
      
        asTabs(document.querySelector("#panel"));
    </script>

```







