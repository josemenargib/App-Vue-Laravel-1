<template>

<div class="row gy-3">
        <div class="col-12">
            <div class="card border border-0 shadow-lg">
                <div class="card-body">
                    <h5 class="card-title font-weight-bolder"><i class="fas fa-calendar me-2"></i>Horas trabajadas</h5>
                </div>
            </div>
        </div>
        <div class="col-12">
            <div class="card shadow-lg">
                <div class="card-body ">
                    <div class="row gy-2">
                        <div class="col-12 d-flex ">
                            <div class="col-12 col-md-8 d-flex align-items-center ">

                                <input type="search" class="form-control" placeholder="Buscar..." >
                            </div>
                            <div class="col-12 col-md-4 text-center">
                                <button  type="button" class="btn btn-primary" @click="agregar()" ><i
                                        class="fas fa-plus-circle me-2"></i> Agregar</button>
                            </div>


                        </div>

                        <div class="table-responsive p-0">
                            <table class="table align-items-center justify-content-center text-sm">
                                <thead class="table-gray-personalizado">
                                    <tr class="text-white">
                                        <th class="text-uppercase font-weight-bolder text-center">
                                            Item</th>
                                        
                                        <th class="text-uppercase font-weight-bolder text-center">
                                            Descripcion</th>
                                        <th class="text-uppercase font-weight-bolder text-center">
                                            Date Start</th>
                                        <th class="text-uppercase font-weight-bolder text-center" >
                                            Date Finish </th>
                                            <th class="text-uppercase font-weight-bolder text-center" >
                                                Duración  </th>
                                                <th class="text-uppercase font-weight-bolder text-center" >
                                                    Opciones  </th>
                                    </tr>
                                </thead>
                                <tbody class="text-center">
                                    <tr >
                        
                      </tr>
                                    <tr v-for="(item,i) in datos" :key="i" >
                                        <td>
                                            <p class="text-center text-sm font-weight-bold ms-3">{{ i=i+1 }}</p>
                                        </td>
                                        <td>
                                            <p class="text-center text-sm font-weight-bold ms-3">{{ item.description }}</p>
                                        </td>
                                        
                                        <td>
                                            <p class="text-center text-sm font-weight-bold mb-0">{{ item.date_start }}</p>
                                        </td>
                                        <td>
                                            <p class="text-center text-sm font-weight-bold mb-0">{{ item.date_finish }}</p>
                                        </td>
                                        <td>
                                            <p class="text-center text-sm font-weight-bold mb-0"><td><p class="text-center text-sm font-weight-bold mb-0">{{ duracion(item.date_start, item.date_finish) }} horas</p></td></p>
                                        </td>

                                        <td class="text-center">
                                            <div class="btn-group btn-group-sm">
                                               
                                                    <i class="fas fa-eye mx-1 text-info fa-lg fs-5 btn-action cursor-pointe"></i>
                                                
                                                
                                               
                                                    <i class="fas fa-trash mx-1 text-danger fa-lg fs-5 btn-action cursor-pointe " ></i>
                                               
                                            </div>
                                        </td>
                                    </tr>

                                </tbody>
                            </table>
                            <div class="col-12">
                                <nav aria-label="Page navigation example">
                                    <ul class="pagination justify-content-center">
                                        <li class="page-item">
                                            <button @click="paginaBefore()" type="button" class="page-link" aria-label="Previous"><span
                                                    aria-hidden="true">&laquo;</span>
                                            </button>
                                        </li>
                                        <li class="page-item">
                                            <button  type="button" class="page-link"></button>
                                        </li>
                                        <li class="page-item">
                                            <button   @click="paginaNext()" type="button" class="page-link" aria-label="Next"><span
                                                    aria-hidden="true">&raquo;</span>
                                            </button>
                                        </li>
                                    </ul>
                                </nav>
                            </div>
                        </div>
                    </div>


                </div>
            </div>

        </div>



    </div>


</template>
<script setup>
import { useRouter } from 'vue-router';
import { ref,onMounted } from 'vue';
import { HorasTrabajadasIndex,HorasTrabajadasIndexTodos } from '@/services/PruebasService';
const router=useRouter()
const agregar=()=>{
    router.push({path:`/horas-trabajadas-form`})
}

onMounted(()=>{
    listarHoras()
})

const datos =ref([])
const start=ref(null)
const end=ref(null)
const listarHoras=async()=>{
    try {
        const {data}=await HorasTrabajadasIndexTodos()
        datos.value=data.datos
        start.value=data.date_start
        console.log(typeof(start.value));
        
        end.value=data.date_finish
        console.log(data);
        
    } catch (error) {
        
    }
}
const duracion=(start,end)=>{
    const startDate = new Date(start);
    const endDate = new Date(end);
    const diffMs = endDate - startDate; // Diferencia en milisegundos
    const diffHrs = diffMs / (1000 * 60 * 60); // Convertir a horas
    return diffHrs.toFixed(2); // Limitar a 2 decimales
}

</script>
<style></style>