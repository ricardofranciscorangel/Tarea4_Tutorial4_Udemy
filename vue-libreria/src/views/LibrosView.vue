<script>
import axios from "axios";
import{ref,onMounted} from "vue"

export default {
    setup(){

        onMounted(()=>{
            listarLibros();
        });

        const libros = ref([]);

        const listarLibros = async()=>{
            try {
                const response = await axios.get("http://localhost:3000/libros");
                libros.value = response.data;
                console.log(libros.value);
            } catch (error) {
                console.log("Error al leer los libros desde el endpoint",error)
            }
            
        };

        const eliminarLibro = async(id, titulo)=>{
            const confirmDelete = window.confirm(
                `Estas seguro de eliminar el libro? ${titulo}`
            );
            if(confirmDelete){
                try {
                    await axios.delete(`http://localhost:3000/libros/${id}`);
                    listarLibros();
                } catch (error) {
                    console.log("Error al eliminar el libro", error);
                }
            }
            
        }

         onMounted(()=>{
            listarLibros();
        });

        return{
            libros,
            listarLibros,
            eliminarLibro
        };
    }
};
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
                <tr v-for="libro in libros" key="libro.id">
                    <td class="alinear">{{ libro.id }}</td>
                    <td>{{ libro.titulo }}</td>
                    <td>{{ libro.ISBN }}</td>
                    <td>{{ libro.genero }}</td>
                    <td class="alinear">{{ libro.precio }}</td>
                    <td>{{ libro.disponibilidad }}</td>
                    <div class ="botones">
                        <button class="btn eliminar" @click="eliminarLibro(libro.id,libro.titulo)">
                            Eliminar
                        </button>
                        <RouterLink class="btn editar" :to="{path:'editarLibro/'+libro.id}">Editar</RouterLink>
                    </div>
                    
                </tr>
            </tbody>
        </table>
    </main>
</template>

<style scoped>
table {
    width: 90%;
    border-collapse: collapse;
    margin: 25px auto;
    box-shadow: 0 0 20px rgba(0,0,0,0.2);
}
th, td{
    border: 1px solid black;
    padding: 10px;
}
th {
    background-color: #e2e2e2;
}
.alinear {
    text-align: center;
}
.botones {
    display: flex;
    justify-content: space-around;
    border: solid 1px rgb(103, 103, 103);
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
    margin: 5px;
}

.eliminar {
    background-color: red;
    color: white;
    transition: background-color 0.3s ease-in-out;
}

.eliminar:hover{
    background-color: rgb(83, 2, 2);
    transition: background-color 0.3s ease-in-out;
}

.editar{
    background-color: orange;
    color: white;
    transition: background-color 0.3s ease-in-out;
}

.editar:hover{
    background-color: rgb(143, 94, 3);
    transition: background-color 0.3s ease-in-out;
}
</style>