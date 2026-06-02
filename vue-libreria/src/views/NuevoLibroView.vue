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
                <input v-model="nuevoLibro.titulo" type="text" required paceholder="Titulo">
                </div>
                <div>
                    <label for="autor">Autor</label>
                <input v-model="nuevoLibro.autor" type="text" required paceholder="Autor">
                </div>
                <div>
                    <label for="ISBN">ISBN</label>
                <input v-model="nuevoLibro.ISBN" type="text" required paceholder="ISBN">
                </div>
                <div>
                    <label for="genero">Genero</label>
                <input v-model="nuevoLibro.genero" type="text" required paceholder="Genero">
                </div>
                <div>
                    <label for="precio">Precio</label>
                <input v-model="nuevoLibro.precio" type="text" required paceholder="Precio">
                </div>
                <div>
                    <label for="disponibilidad">Disponibilidad</label>
                <input v-model="nuevoLibro.disponibilidad" type="text" required paceholder="Disponibilidad">
                </div>
            </div>
            <button type="submit">Agregar Libro</button>
        </form>
    </main>
</template>

<style scoped>
form{
    width: 50%;
    border-collapse: collapse;
    margin: 25px auto;
    box-shadow: 0 0 20px rgba(0,0,0,0.2);
}
</style>