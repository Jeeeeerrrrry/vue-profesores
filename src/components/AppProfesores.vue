<template>

    <h1>App Profesores</h1>

    <div><label>Nombre del maestro: </label> <input type="text" v-model="profesor.nombreProfesor"></div> <br> <br>

    <div><label>Apellidos: </label> <input type="text" v-model="profesor.apellidos"></div> <br> <br>

    <div><label>DNI: </label> <input type="text" v-model="profesor.dni"></div> <br> <br>

    <div><label>MATERIA: </label> <input type="text" v-model="materia"> <button @click="agregarMateria()">Agregar materia</button> </div>  
    
    <div>
        <h4>Materias agregadas</h4>
        <ul class="materias-agregadas">
            <li v-for="(m,index) in profesor.materias" :key="index">{{ m }}</li>
        </ul>
    </div>

    <br> 

    <div>Documentos entregados 
        <input type="checkbox" v-model="profesor.docsentregados"> 
    </div>  <br>

    <div><button @click="agregarProfesor()">Agregar profesor</button></div>

    <br>
    <br>

    <div class="profesores-ingresados">
        <h3>Profesores ingresados</h3>
        <table border="1px black">
            <tr>
                <th>Nombre</th>
                <th>Apellido</th>
                <th>DNI</th>
                <th>MATERIAS</th>
                <th>DOCUMENTOS ENTREGADOS</th>
            </tr>
            <tr v-for="(p,index) in profesores" :key="index">
                <th>{{ p.nombreProfesor }}</th>
                <th>{{ p.apellidos }}</th>
                <th>{{ p.dni }}</th>
                <th> 
                    <ul> 
                        <li v-for="(materia,index) in p.materias" :key="index"> {{ materia }} </li> 
                    </ul> 
                </th>
                <th v-if="p.docsentregados === true">Entregados</th>
                <th v-else>No entregados</th>
            </tr>
        </table>
    </div>
    
</template>

<script setup>
    import { ref } from 'vue'

    const profesor = ref({
        nombreProfesor: '',
        apellidos: '',
        dni: '',
        materias: [],
        docsentregados: false
    })

    const profesores = ref([])

    const materia = ref('')

    const agregarMateria = () => {
        profesor.value.materias.push(materia.value)
        materia.value = ''
    }

    const agregarProfesor = () => {
        profesores.value.push({
            nombreProfesor: profesor.value.nombreProfesor,
            apellidos: profesor.value.apellidos,
            dni: profesor.value.dni,
            materias: profesor.value.materias, 
            docsentregados: profesor.value.docsentregados
        })

        profesor.value.nombreProfesor = ''
        profesor.value.apellidos = ''
        profesor.value.dni = ''
        profesor.value.materias = []
        profesor.value.docsentregados = false
    }   



</script>

    
<style scoped>

.materias-agregadas {
    list-style: none;
}

.profesores-ingresados{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

</style>