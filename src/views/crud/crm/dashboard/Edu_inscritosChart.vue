<template>
    <section class="card shadow-lg">
        <header class="card-header">
            <h5 class="card-title fs-3">Gráfico de Inscripciones</h5>
        </header>
        <div class="card-body p-0">
            <p class="alert alert-light m-3" role="alert">
                Tendencia de alumnos por Batch.
            </p>
            <div class="row">
                <div class="col-12 offset-lg-3 col-lg-6">
                    <label for="batch-select">Selecciona un batch:</label>
                    <select v-model="batchSelecionado" class="form-select" id="batch-select" name="batch-select">
                        <option value="todos">Todos</option>
                        <option v-for="batch in batches" :key="batch" :value="batch.id">
                            {{ batch.nombre }}
                        </option>
                    </select>
                    <!-- <p>Has seleccionado: {{ batchSelecionado }} - {{ batches[batchSelecionado - 1]?.nombre }}</p> -->
                </div>
            </div>
            <div class="inscritosDetalle">
                <Bar id="inscripcionDetalle" :data="datos" :options="opciones" />
            </div>
        </div>
        <footer class="card-footer">
            <div class="text-end">
                <button type="button" class="btn btn-sm my-0 mx-5 btn-secondary">Exportar datos</button>
            </div>
        </footer>
    </section>
</template>

<script setup>
    import { onMounted, ref } from 'vue';
    import { Bar } from 'vue-chartjs'
    import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
import { getEstudiantesXBatch } from '@/services/DashboardService';

    ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale);
    const batches = ref(
        [{ id: 1, nombre: 'Batch 1' },
        { id: 2, nombre: 'Batch 2' },
        { id: 3, nombre: 'Batch 3' },
        { id: 4, nombre: 'Batch 4' }]
    );
    const batchSelecionado = ref('todos');

    const baseColors = [
        'blue', 'pink', 'orange', 'green', 'purple', 
        'red', 'cyan', 'yellow', 'brown', 'gray', 
        'violet', 'lime', 'teal', 'magenta', 'indigo'
    ];
    const generateColors = (numData) => {
    const colors = [];
    for (let i = 0; i < numData; i++) {
        colors.push(baseColors[i % baseColors.length]);
    }
    return colors;
};

    const datos = ref({
        labels: [],
        datasets: [
            {
                // label: 'Estudiantes Activos',
                backgroundColor: [],
                data: [],
            }
        ]
    });
    const opciones = ref({
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
            legend: {
                // position: 'bottom',
                display: false
            },
        }
    });
    onMounted(()=>{
        obtenerEstudiantesXBatch();
    });
    async function obtenerEstudiantesXBatch() {
        let nombresBatchs = [];
        let datosBarraAux = [];//para capturar los datos del backend
        try {
            const { data } = await getEstudiantesXBatch();
            data.batch.forEach(element => {
                nombresBatchs.push(element.nombre);
                datosBarraAux.push(element.total_estudiantes);
            });
            
            datos.value = {
                labels: nombresBatchs,
                datasets: [
                    {
                        backgroundColor: generateColors(datosBarraAux.length),
                        data: datosBarraAux
                    }
                ]
            }
        } catch (error) {
            console.log(error);
        }
    }
</script>

<style>
    .inscritosDetalle {
        max-width: 100%;
        height: 350px;
        margin: 13px;
    }
</style>