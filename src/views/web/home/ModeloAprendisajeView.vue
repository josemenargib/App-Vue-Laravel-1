<template>
	<section id="modelo" class="padding-medium background">
		<div class="container text-white">
			<div class="text-center">
				<h2 class="display-6 monserrat-bold-titulo titulo">
					MODELOS DE APRENDIZAJE
				</h2>
			</div>
			<div class="row d-flex justify-content-center mt-5">
				<div class="col-12 col-md-6 mt-3" v-for="modelo in modelos" :key="modelo.id">
					<div class="card text-center rounded-4 shadow mt-5 border border-secondary-subtle cardm">
						<div class="">
							<img class="position-absolute start-50 translate-middle rounded-circle p-1 text-light bg-dark"
								:src="urlBaseAsset+'img/img-modelos/'+modelo.icono || 'https://img.freepik.com/vector-premium/servidor-no-encontrado-simbolo-icono-error-nube-ilustracion-vectorial-eps-10-imagen-archivo_756957-2264.jpg'"
								alt="50%" width="120px" />

						</div>
						<div class="card-body mt-5">
							<h5 class="card-title monserrat-regular-subtitulo">
								{{ modelo.nombre }}
							</h5>
							<p class="card-text text-muted monserrat-regular">
								{{ modelo.descripcion }}
							</p>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>
</template>
<script setup>
import { datosModeloAprendisaje } from "@/services/ModelosServices";
import { onMounted, ref } from "vue";
import { urlBaseAsset } from "@/services/Http";
const modelos = ref([
	{
		id: 1,
		nombre: "vacio",
		descripcion: "vacio",
		icono: "/public/jubilee/images/uno.png",
	},
	{
		id: 2,
		nombre: "vacio",
		descripcion: "vacio",
		icono: "/public/jubilee/images/uno.png",
	},
	{
		id: 3,
		nombre: "vacio",
		descripcion: "vacio",
		icono: "/public/jubilee/images/uno.png",
	},
]);
async function obtenerModeloAprendizaje() {
	try {
		const { data } = await datosModeloAprendisaje();
		if (data.datos.length >= 1) {
			modelos.value = data.datos;
			
		}
	} catch (error) {
		console.log("Error fatal: " + error);
	}
}
onMounted(() => {
	obtenerModeloAprendizaje();
});
</script>
<style>
@import 'https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap';
.monserrat-bold-titulo{
  font-family: "Montserrat", sans-serif;
  font-weight: 700;
  font-style: normal;
  font-size: 40px;
  text-transform: none; 
}
.monserrat-regular-subtitulo {
 font-family: "Montserrat", sans-serif;
  font-weight: 700;
  font-style: normal;
  font-size: 20px;
  text-transform: none; 
}
.monserrat-regular {
font-family: "Montserrat", sans-serif;
  font-weight: 400;
  font-style: normal;
  font-size: 18px;
  text-transform: none; 
}
.monserrat-regular-italic {
  font-family: "Montserrat", sans-serif;
  font-weight: 400;
  font-style: italic;
  font-size: 18px;
  text-transform: none; 
}
.monserrat-bold-italic {
  font-family: "Montserrat", sans-serif;
  font-weight: 700;
  font-style: italic;
  font-size: 18px;
  text-transform: none; 
}
.background {
    background-color: white;
}
.titulo{
	text-color: #303644;
}
.cardm:hover{
	background-color: #ffcc01;
}

</style>
