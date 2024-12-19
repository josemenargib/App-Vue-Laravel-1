<template >
       <div class="row gy-3">
        <div class="col-12">
      <div class="card border border-0 shadow-lg">
        <div class="card-body">
          <h5 class="card-title font-weight-bolder">
            <i class="fas fa-graduation-cap"></i>  Agregar horas trabajadas
          </h5>
        </div>
      </div>
    </div>
            <div class="col-12">
                <div class="card shadow-lg">
                    <div class="card-body">
                        <div class="row gy-3">
                            <div class="col-4 ">
                                <label class="form-label font-weight-bolder text-sm" for="nombre">Description <span
                                        class="text-danger fst-italic"> * </span></label>
                                <input type="text" class="form-control" v-model="formulario.description">
                                
                            </div>
                            <div class="col-4 ">
                                <label class="form-label font-weight-bolder text-sm" for="nombre">Date start <span
                                        class="text-danger fst-italic"> * </span></label>
                                <input type="datetime-local" class="form-control" v-model="formulario.date_start">
                                
                            </div>
                            <div class="col-4 ">
                                <label class="form-label font-weight-bolder text-sm" for="nombre">Date finish <span
                                        class="text-danger fst-italic"> * </span></label>
                                <input type="datetime-local" class="form-control" v-model="formulario.date_finish">
                                
                            </div>

                            <div class="col-12 text-center d-flex justify-content-center">

                                <div >
                                    <button type="button" class="btn btn-danger me-2" @click="cancelar()"><i
                                        class="fas fa-reply me-2"></i>Volver</button>
                                    <button type="button" class="btn btn-primary ms-2" @click="enviar()">Enviar<i
                                            class="fas fa-save ms-2"></i></button>
                                </div>
                                
                                
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        
    </div>
</template>
<script setup>
import { ref,onMounted } from 'vue';
import { useRouter } from 'vue-router';
import { HorasTrabajadasStore } from '@/services/PruebasService';
const router=useRouter();

const cancelar=()=>{
    router.push({path:`/horas-trabajadas`})
}
const formulario=ref({})
const enviar= async()=>{
    try {
        const {data}=await HorasTrabajadasStore(formulario.value)
        router.push({path:`/horas-trabajadas`})
        console.log(data);
        
    } catch (error) {
        
    }
}

</script>
<style >
    
</style>