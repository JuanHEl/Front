<template>
    <div id="contenedor">
        <div id="tabla">
            <div class="form-group left col-sm-10">
                <b-input-group>
                    <b-input-group-prepend is-text @click.prevent="buscanombre">
                        <b-icon icon="search" style="color:black">
                        </b-icon>
                    </b-input-group-prepend>
                        <b-input
                            v-model="form.id"
                            id="input-1"
                            type="text"
                            placeholder="Buscar por id de administrador"
                            required
                        />
                </b-input-group>
            </div>
            <div class="form-group left">
                <label for="" class="control-label col-sm-2 text-white">Nombre</label>
                <div class="col-sm-10">
                    <input
                    type="text"
                    class="form-control"
                    name="nombre"
                    id="nombre"
                    v-model="form.nombre"
                    required
                    />
                </div>
            </div>
            <div class="form-group left">
                <label for="" class="control-label col-sm-2 text-white"
                    >Apellido Paterno</label
                >
                <div class="col-sm-10">
                    <input
                    type="text"
                    class="form-control"
                    name="nombre"
                    id="nombre"
                    v-model="form.apellidop"
                    required
                    />
                </div>
            </div>
            <div class="form-group left">
                <label for="" class="control-label col-sm-2 text-white"
                    >Apellido Materno</label
                >
                <div class="col-sm-10">
                    <input
                    type="text"
                    class="form-control"
                    name="nombre"
                    id="nombre"
                    v-model="form.apellidom"
                    required
                    />
                </div>
            </div>
            <div class="form-group left">
                <label for="" class="control-label col-sm-2 text-white"
                    >Nombre Usuario</label
                >
                <div class="col-sm-10">
                    <input
                    type="text"
                    class="form-control"
                    name="direccion"
                    id="direccion"
                    v-model="form.nombreusuario"
                    required
                    />
                </div>
            </div>
            <div>
                <div class="form-check-inline">
                    <b-form-group label="Status" class="text-white">
                        <b-form-select v-model="form.statusa" required>
                            <template #first>
                                <b-form-select-option :value="null" disabled>
                                    Selecciona un status
                                </b-form-select-option>
                                <b-form-select-option v-for="stat in statusadmin" :key="stat.index" :value="stat.Id_Status_Admin">{{stat.Nom_Tipo_Admin}}
                                </b-form-select-option>
                            </template>
                        </b-form-select>
                    </b-form-group>
                </div>
            <br /><br />
            </div>
        </div>
        <div id="botones">
            <div>
                <br>
                <b-button block class="buttons" pill variant="primary" to="/nuevoadmin" font-scale="3"> Agregar Nuevo Administrador</b-button>
                <b-button block class="buttons" pill variant="primary" to="/cambiastatus" font-scale="3"> Cambiar Status </b-button>
                <b-button block class="buttons" pill variant="primary" to="/editaradmin" font-scale="3"> Editar Administrador</b-button>
                <br>
                <b-button block class="buttons" pill variant="primary" to="/editarpermisos" font-scale="3"> Editar Permisos</b-button>
            </div>
        </div>
    </div>
</template>
<script>
import axios from "axios";
export default {
    name: "FormStatus",
    data: function () {
        return {
            statusadmin: null,
            Listaadmins: null,
            logs:[],
            form: {
                id: "",
                nombre: "",
                apellidop: "",
                apellidom: "",
                pass: "",
                nombreusuario: "",
                statusa: null,
                tipoa: null,
                servicios:null,
            }
        };
    },
    components: {
    },
    methods: {
        buscanombre(){
            this.logs=this.Listaadmins;
            let listapornombre = this.logs.filter(x => x.Id_Administradores == this.form.id);
            this.logs=listapornombre;
            // console.log(this.logs)
        }
    },
    watch: {
    },
    mounted: function () {
        let admin = "http://127.0.0.1:8000/api/muestra";
        axios.get(admin).then((data) => {
            console.log(data);
            this.Listaadmins = data.data;
            this.logs = this.Listaadmins;
        });
        let statusadmin = "http://127.0.0.1:8000/api/muestrastatusa";
        axios.get(statusadmin).then((data) => {
            console.log(data);
            this.statusadmin = data.data;
        });
    },
};
</script>
<style scoped>
#contenedor {
    display: flex;
}
.left {
    text-align: left;
}
#botones {
    width: 35%;
    margin: 2px;
    padding: 5px;
    border-radius: 10px;
    min-height: 400px;
    color: white;
}
#tabla {
    width: 100%;
    /* background-color: rgb(255, 255, 255); */
    /* margin: 2px;
    padding: 5px;
    border-radius: 10px;
    min-height: 400px; */
}
</style>