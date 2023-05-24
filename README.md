<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
    <link href="css/styles.css" rel="stylesheet">
</head>
<body>
    <header class="site-header">
        <div class="contenedor">
        <div class="barra">
        
        <h1> Proyecto <span> SIDESS</span></h1>
        </a>
        </div>
    
        <div class="texto-header">
            <h2 class="no-margin">SIDESS</h2>
            <p class="no-margin">Sistema de seguridad basado en sensores de movimiento</p>
        </div>
    </div>
    
    </header>

    <!--Carousel-->
    <div id="wrapper">
        <div id="carousel">
          <div id="content">
            
          </div>
        </div>
        <button id="prev">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
          >
            <path fill="none" d="M0 0h24v24H0V0z" />
            <path d="M15.61 7.41L14.2 6l-6 6 6 6 1.41-1.41L11.03 12l4.58-4.59z" />
          </svg>
        </button>
        <button id="next">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
          >
            <path fill="none" d="M0 0h24v24H0V0z" />
            <path d="M10.02 6L8.61 7.41 13.19 12l-4.58 4.59L10.02 18l6-6-6-6z" />
          </svg>
        </button>
      </div>
    
    
<div class="listado">
    

    <h1>Gestor de tareas</h1>
    
    <div>
        <input type="text" name="clave_texto" autocomplete="off" placeholder="Clave de la tarea" id="Cl_Tarea">
    </div>
    <div>
        <input type="text" name="tarea_texto" autocomplete="off" placeholder="Nombre de la tarea" id="Nombre_T">
    </div>
    <div>
        <h4>Estado de la tarea</h4>
        <select id="Estado">
            <option>Completado</option>
            <option>Pendiente</option>
        </select>

    </div>
    <div class="btn_accion">
        
        <button id="crea" class="btn_crear">Crear</button>
        <button id="borra" class="btn_borrar">Borrar</button>
        <button id="actua" class="btn_actualizar">Actualizar</button>
    </div>
  
    <hr>
    <div class="contenedor" id="contenedor">

    </div>
</div>
<script>
       

</script>

    <script type="module">
        // Import the functions you need from the SDKs you need
        import { initializeApp } from "https://www.gstatic.com/firebasejs/9.18.0/firebase-app.js";
        // TODO: Add SDKs for Firebase products that you want to use
        // https://firebase.google.com/docs/web/setup#available-libraries
      
        // Your web app's Firebase configuration
        const firebaseConfig = {
  apiKey: "AIzaSyAj7cdG9iGRlyrCdz04QaKtp0fXberB41g",
  authDomain: "holamundo-b14a9.firebaseapp.com",
  databaseURL: "https://holamundo-b14a9-default-rtdb.firebaseio.com",
  projectId: "holamundo-b14a9",
  storageBucket: "holamundo-b14a9.appspot.com",
  messagingSenderId: "265875831725",
  appId: "1:265875831725:web:d40b1630065551b9787f24"
};
      
        // Initialize Firebase
        const app = initializeApp(firebaseConfig); 

        import {getDatabase, ref,set,child,update, remove}
        from "https://www.gstatic.com/firebasejs/9.18.0/firebase-database.js";

        const db=getDatabase();

/*alojar el valor de los campos en las siguientes variables */
        /*const preObject = document.getElementById(contenedor);*/
        var Cl_Tarea= document.getElementById("Cl_Tarea");
        var nombre= document.getElementById("Nombre_T");
        var estado= document.getElementById("Estado");
/*Botón*/
        var accBtn= document.getElementById("crea");
        var del=document.getElementById("borra");
        var act= document.getElementById("actua");

     /*Funciones del programa: insert*/
     function Insert(){
        set(ref(db,"Tareas/"+ Cl_Tarea.value),{
            Cl_Tarea: Cl_Tarea.value,
            Nombre_Tarea: nombre.value,
            Estado: estado.value
        })
        .then (()=>{
            alert("Los datos se han guardado");
        })
        .catch ((error)=>{
            alert("Los datos no se han podido guardar, error"+error);
        }); 
     }
     
/*Seleccionar */
     function selectData(){
        const dbref= ref(db);
        get(child(dbref,"Tareas/"+Cl_Tarea.value)).then((snapshot)=>{
            if(snapshot.exist()){
             Cl_Tarea.value= snapshot.val().Cl_Tarea;
            Nombre_Tarea.value= snapshot.val().Nombre_Tarea;
            Estado.value= snapshot.val().Estado;

            }
            else{
                 alert("No se han encontrado los datos");
            }
        })
        .catch ((error)=>{
            alert("No se ha podido realizar su peticion, error"+error);
        });

     }

/*Actualizar*/
     function Update(){
        update(ref(db,"Tareas/"+ Cl_Tarea.value),{
            Nombre_Tarea: nombre.value,
            Estado: estado.value
        })
        .then (()=>{
            alert("Los datos se han actualizado");
        })
        .catch ((error)=>{
            alert("Los datos no se han podido actualizar, error"+error);
        }); 
     }


     /*Eliminar*/
     function Delete(){
        remove(ref(db,"Tareas/"+ Cl_Tarea.value))
        .then (()=>{
            alert("Se ha eliminado");
        })
        .catch ((error)=>{
            alert("Los datos no se han podido eliminarr, error"+error);
        }); 
     }

     /*----------------------------------------------------*/
            accBtn.addEventListener('click',Insert);
            act.addEventListener('click',Update);
            del.addEventListener('click',Delete);

    

            /*----lista--*/
            var userDataRef = firebase.database().ref("task"); 
            userDataRef.on("value", function(snapshot) {
                html = ''; 
                snapshot.forEach(function(childSnapshot) { 
                    var childData = childSnapshot.val();
                    var l_Tarea = name.value;
                    var Nombre_Tarea = description.value;
                    var Estado = estado.value;
                    html += "<li><b>"+l_Tarea+": </b>"+Nombre_Tarea+"</li>";
                }); 
                contenedor.innerHTML = html;
        });       
     
        var splide = new Splide( '.splide', {
            perPage: 3,
            rewind : true,
          } );
          
          splide.mount();

      </script>
     

   <!-- <form action="">
        <div>
            <label for="nombre">Nombre</label>
            <input type="text" id="nombre">
        </div>
        <div>
            <label for="mensaje">Mensaje</label>
            <input type="text" id="mensaje">
        </div>
        <button type="button" id="btnEnviar">Enviar</button>
    </form>

    <ul id="chatUl">
    </ul>


    <script src="https://www.gstatic.com/firebasejs/3.6.1/firebase.js"></script>
  <script>
    // Initialize Firebase
    const config = {
    apiKey: "AIzaSyDY2ApGp65KICwf_yUPN5SQqa2gzx81UE0",
    authDomain: "chat-25155.firebaseapp.com",
    databaseURL: "https://chat-25155-default-rtdb.firebaseio.com",
    storageBucket: "chat-25155.appspot.com",
    messagingSenderId: "742265522795"
    };
    firebase.initializeApp(config);

    var txtNombre = document.getElementById("nombre");
    var txtMensaje = document.getElementById("mensaje");
    var btnEnviar = document.getElementById("btnEnviar");
    var chatUl = document.getElementById("chatUl");

   btnEnviar.addEventListener("click", function() {
        var nombre = txtNombre.value;
        var mensaje = txtMensaje.value;
        

        firebase.database().ref('chat').push({
            name: nombre,
            message: mensaje
        });

    });
    
    firebase.database().ref('chat')
            .on('value', function(snapshot){
                var html ='';
        snapshot.forEach(function(e){
          var element = e.val();
          var nombre = element.name;
          var mensaje = element.message;
          html += "<li><b>"+nombre+": </b>"+mensaje+"</li>";
        });
        chatUl.innerHTML = html;
    });

  </script>-->
  <footer class="site-footer">
                
    <div class="contenedor">
    <div class="barra">
    <a href="index.html">
    <h3 size="50px"> Proyecto<span>SIDESS</span></h3>
    </a>
<nav class="nav-bg">
    <a href="Nosotros.html">Nosotros</a>
    <a href="Cursos.html">Cursos</a>
    <a href="Contacto.html">Contacto</a>
     </nav>
</div>
<h6>Derechos reservados</h6>
</footer>
</body>
</html> 
