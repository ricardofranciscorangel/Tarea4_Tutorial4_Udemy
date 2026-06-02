<script>
import axios from "axios";
import{ref} from "vue"

export default {
    setup(){
        const libros = ref([]);
        const listarLibros = async()=>{
            try {
                const response = await axios.get("http://localhost:3000/libros");
                libros.value = response.data;
                console.log(libros.value);
            } catch (error) {
                console.log("Error al leer los libros desde el endpoint",error)
            }
            
        }
    }
}
</script>

<template>
    <main>
        <table>
            <thead>
                <tr>
                    <th>id</th>
                    <th>Titulo</th>
                    <th>ISBN</th>
                    <th>Genero</th>
                    <th>Precio</th>
                    <th>Disponibilidad</th>
                    <th>Accciones</th>
                </tr>
            </thead>
            <tbody>

            </tbody>
        </table>
    </main>
</template>

<style></style>