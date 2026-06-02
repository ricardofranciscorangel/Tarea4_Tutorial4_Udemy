<script>
import {ref} from "vue";
import axios from "axios";
export default {
    setup(){
        const nuevoLibro = ref ({
            titulo:"",
            autor:"",
            ISBN:"",
            genero:"",
            precio:"",
            disponibilidad:""
        });

        const CrearLibro = async()=>{
            try{
               const response = await axios.post("http://localhost:3000/libros", nuevoLibro.value);

               setTimeout(()=>{
                alert("libro creado con exito");
                
               },200);
        
                    nuevoLibro.value.titulo="",
                    nuevoLibro.value.autor="",
                    nuevoLibro.value.ISBN="",
                    nuevoLibro.value.genero="",
                    nuevoLibro.value.precio="",
                    nuevoLibro.value.disponibilidad=""
                    console.log("Libro crado con exito". response.data)
                
            }catch(error){
                console.log("No se pudo crear el libro", error);
            }

        };

        return{
            nuevoLibro,
            CrearLibro
        };
    }
}
</script>

<template>
    <main>
        <form @submit.prevent="CrearLibro">
            <div>
                <div>
                    <label for="titulo">Título</label>
                <input v-model="nuevoLibro.titulo" type="text" required placeholder="Titulo">
                </div>
                <div>
                    <label for="autor">Autor</label>
                <input v-model="nuevoLibro.autor" type="text" required placeholder="Autor">
                </div>
                <div>
                    <label for="ISBN">ISBN</label>
                <input v-model="nuevoLibro.ISBN" type="text" required placeholder="ISBN">
                </div>
                <div>
                    <label for="genero">Genero</label>
                <input v-model="nuevoLibro.genero" type="text" required placeholder="Genero">
                </div>
                <div>
                    <label for="precio">Precio</label>
                <input v-model="nuevoLibro.precio" type="text" required placeholder="Precio">
                </div>
                <div>
                    <label for="disponibilidad">Disponibilidad</label>
                <input v-model="nuevoLibro.disponibilidad" type="text" required placeholder="Disponibilidad">
                </div>
            </div>
            <button class="btn enviar" type="submit">Agregar Libro</button>
        </form>
    </main>
</template>

<style scoped>
form{
    width: 90%;
    margin: 25px auto;
    padding: 20px;
    border: solid 1px black;
    box-shadow: 0 0 20px rgba(0,0,0,0.1);
    
}

label {
    font-weight: bold;
 margin-bottom: 5px;
 display: block;
 font-size: 1rem;
}

input {
    width: 100%;
    padding: 5px;
    border: 1px solid black;
    margin-bottom: 15px;
    font-family: "Montserrat", sans-serif;
    font-size: 1rem;
}

input:focus {
    outline: none;
}
.btn {
    background-color: transparent;
    border: none;
    padding: 10px 15px;
    text-decoration: none;
    font-family: "Montserrat", sans-serif;
    color:black;
    font-size: 1rem;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out;
    width: 100%;
}

.enviar {
    background-color: rgba(13, 179, 121, 0.644);
    color: white;
    transition: background-color 0.3s ease-in-out;
}

.enviar:hover{
    background-color: rgb(4, 53, 43);
    transition: background-color 0.3s ease-in-out;
}

</style>