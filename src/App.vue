<template>
	<div class="container my-3">
		<div class="row">
			<div class="col-12 col-sm-12 col-md-6 offset-md-3 col-lg-6 offset-lg-3 mt-4 py-3 bg-light">
				<h2 class="text-uppercase text-center font-weight-bold">
					{{ titulo }}
				</h2>
				<hr />
				<p class="text-center font-weight-bold">{{ subtitulo }}</p>
				<div class="form-group">
					<label class="" for="titulo">Título</label>
					<input
						class="form-control"
						name="titulo"
						type="text"
						placeholder="Ej: Dar de comer al perro"
						v-model="nota.titulo"
					/>
				</div>
				<div class="form-group">
					<label class="" for="descripcion">Descripción</label>
					<textarea
						class="form-control"
						name="descripcion"
						type="text"
						placeholder="Ej: Aqui se describe con detalle la nota a crear"
						v-model="nota.descripcion"
					></textarea>
				</div>
				<button
					type="button"
					class="btn btn-success btn-block"
					@click="agregarTarea"
				>
					Guardar Nota
				</button>
			</div>
		</div>
    <div class="row mt-4">
      <div class="col-12">
        <h5 class="text-center">Notas agregadas</h5>
        <hr>
        <div class="card-columns">
          <div class="card" v-for="(nota, index) in notas" :key="index">
            <div class="card-header d-flex justify-content-between align-items-center">
              <span>{{ nota.titulo }}</span>
              <button type="button" class="btn btn-danger font-weight-bold" @click="quitarTarea(index)">&times;</button>
            </div>
            <div class="card-body">
              <blockquote class="blockquote mb-0">
                <p>{{ nota.descripcion }}</p>
                <footer class="blockquote-footer">
                  {{ nota.fecha }}
                </footer>
              </blockquote>
            </div>
          </div>
        </div>
      </div>
    </div>
	</div>
</template>

<script>
	export default {
		name: 'App',
		data() {
			return {
				titulo: 'Libreta de notas',
				subtitulo: 'Crea una nueva nota:',
				nota: {
					titulo: '',
					descripcion: '',
					fecha: '',
				},
				notas: [],
			}
		},
		methods: {
			agregarTarea: function() {
        this.nota.fecha = new Date(Date.now()).toLocaleString();
				this.notas.push(this.nota);
        this.limpiarForm();
			},
      quitarTarea: function(index) {
        this.notas.splice(index, 1);
      },
      limpiarForm: function() {
        this.nota = {};
      }
		},
		components: {},
	}
</script>

<style scoped>
	label::after {
		content: ':';
	}
	input::placeholder,
	textarea::placeholder {
		font-style: italic;
		color: #d2d2d2;
	}
</style>
