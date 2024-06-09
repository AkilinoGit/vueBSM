# <pre>             VEGGIE SUPPLY CHAIN<br>        VUE - FRONTEND
Frontend del proyecto
## 1. COMPONENTES  :
- [App.vue](https://github.com/AkilinoGit/vueBSM/blob/main/src/App.vue)<br>
  Lo primero que hace el servidor al arrancar es ejecutar el main.js que instala la applicación Vue a traves de este fichero y desde aquí se llama al resto de componentes
- [HelloWorld.vue](https://github.com/AkilinoGit/vueBSM/blob/main/src/components/HelloWorld.vue)
  Primera toma de contacto con el sistema de componentes de vue, solo pone el título
- [OrgSection.vue](https://github.com/AkilinoGit/vueBSM/blob/main/src/components/OrgSection.vue)
  Componente el cual contiene el formulario especifico de cada organización dependiendo de el valor que le envía App.vue, se podría haber desarrollado de cualquier otra manera    pero quería forzar algún uso dinamico de componentes
- [Formularios](https://github.com/AkilinoGit/vueBSM/tree/main/src/components/forms)
  Formulario destinado a cada organización
## 2. ESTILOS : 
- [main.css](https://github.com/AkilinoGit/vueBSM/blob/main/src/assets/main.css)
  A parte de los estilos iniciales, hay algun detalle y la clase de los spinners de carga
## 3. VARIABLE DE ENTORNO :
- [.env](https://github.com/AkilinoGit/vueBSM/blob/main/.env)
  Únicamente creo una varibale de entorno para agilizar el proceso de cambiar la ip de las llamadas ya que google cloud lo cambia cada vez que reinicias la máquina (si no lo configuras)
  
