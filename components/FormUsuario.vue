<template>
    <div>
        <div class="container">
        <form @submit.stop.prevent="sig" class="form-horizontal">
            <div v-if="step==0">
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
                <div class="form-group left row">
                <div class="col">
                    <label for="" class="control-label col-sm-3 text-white"
                    >Contraseña</label
                    >
                    <div class="col-sm-7">
                        <b-input-group>
                            <b-input-group-prepend is-text @click.prevent="mostrarContrasena">
                                <b-icon :icon="icon" style="color:black">
                                </b-icon>
                            </b-input-group-prepend>
                                <b-input
                                    :type="showpass"
                                    class="form-control"
                                    name="correo"
                                    id="correo"
                                    v-model="form.pass"
                                    required
                                />
                        </b-input-group>
                    </div>
                </div>
                <div class="col">
                    <button type="button" id="password" class="btn btn-primary" v-on:click="generarcontra()">
                    Generar Contraseña
                    </button>
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
                        <div class="col-md-6">
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
                        <div class="col-md-6">
                            <b-form-group label="Tipo" class="text-white">
                                <b-form-select v-model="form.tipoa" required>
                                    <template #first>
                                        <b-form-select-option :value="null" disabled>
                                            Selecciona un tipo
                                        </b-form-select-option>
                                        <b-form-select-option v-for="tipo in tipoadmins" :key="tipo.index" :value="tipo.Id_Tipo_Admin">{{tipo.Nom_Tipo_Admin}}
                                        </b-form-select-option>
                                    </template>
                                </b-form-select>
                            </b-form-group>
                        </div>
                    </div>
                <br /><br />
                </div>
            </div>

            <div v-if="step==1">
                <div class="container">
                    <b-form-group>
                        <template #label>
                            <label for="" class="control-label col-sm-3 text-white">Selecciona los servicios:</label>
                            <!-- <b class="control-label col-sm-2 text-white">Selecciona los servicios:</b> --><br>
                            <b-form-checkbox
                            size="lg"
                            v-model="allSelected"
                            :indeterminate="indeterminate"
                            @change="toggleAll"
                            class="control-label text-white"
                            stacked
                            >
                            {{ allSelected ? 'Quitar todos' : 'Selecciona todos' }}
                            </b-form-checkbox>
                        </template>

                        <template v-slot="{ ariaDescribedby }">
                            <b-form-checkbox-group
                            size="lg"
                            v-model="selected"
                            :options="listservicios"
                            :aria-describedby="ariaDescribedby"
                            class="ml-4 control-label text-white"
                            value-field="item"
                            text-field="name"
                            stacked
                            ></b-form-checkbox-group>
                        </template>
                    </b-form-group>
                    <!-- 
                    <div>
                    Selected: <strong>{{ selected }}</strong><br>
                    All Selected: <strong>{{ allSelected }}</strong><br>
                    Indeterminate: <strong>{{ indeterminate }}</strong>
                    </div> -->
                </div>
            </div>

            <div class="form-group">
                <button v-if="step==0" type="button" class="btn btn-primary" v-on:click="salir()">
                    Salir
                </button>
                <button v-if="step==1" type="button" class="btn btn-primary" v-on:click="ant">
                    Anterior
                </button>
                <button v-if="step==0" type="button submit" class="btn btn-primary" >
                    Continuar
                </button>
                <button v-if="step==1" type="button" class="btn btn-primary" v-on:click="setinfo">
                    Finalizar
                </button>
            </div>
        </form>
        <p>{{form}} y además del form {{ selected }}</p>
        </div>
    </div>
</template>
<script>
import Header from "@/components/Header.vue";
//import Footer from '@/components/Footer.vue'
import axios from "axios";
export default {
    name: "FormUsuario",
    data: function () {
        return {
            icon:'eye-slash',
            selected: [],
            allSelected: false,
            indeterminate: false,

            listservicios:[],
            tipoadmins: null,
            statusadmin: null,
            catservicios: null,
            step:0,
            showpass:'password',
        form: {
            nombre: "",
            apellidop: "",
            apellidom: "",
            pass: "",
            nombreusuario: "",
            statusa: null,
            tipoa: null,
            servicios:null,
        },
        };
    },
    components: {
        Header,
        //Footer
    },
    methods: {
    toggleAll(checked) {
        let listavariable = [];
        let variable;
        for (let index = 0; index < this.listservicios.length; index++) {
            variable = this.listservicios[index].item;
            listavariable.push(variable)
        }
        this.selected = checked ? listavariable : []
    },
        guardar() {
            this.form.token = localStorage.getItem("token");
            axios
            .post("http://127.0.0.1:8000/api/create", this.form)
            .then((data) => {
            console.log(data);
            this.makeToast("Hecho", "Paciente creado", "success");
            this.$router.push("/dashboard");
            })
            .catch((e) => {
            console.log(e);
            this.makeToast("Error", "Error al guardar", "error");
            });
        },
        salir() {
            this.$router.push("/admins");
        },
        makeToast(titulo, texto, tipo) {
            this.toastCount++;
            this.$bvToast.toast(texto, {
                title: titulo,
                variant: tipo,
                autoHideDelay: 5000,
                appendToast: true,
            });
        },
        sig(){
            if (this.step<1) {
                this.step++;
            }
        },
        ant(){
            if (this.step>0){
                this.step--;
            }
        },
        generarcontra(){
            let text = ""; 
            let possible = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789"; 
            for( let i=0; i < 8; i++ ){
                text += possible.charAt(Math.floor(Math.random() * possible.length)); 
            } 
            this.form.pass = text;
        },
        mostrarContrasena(){
            if (this.showpass=='password') {
                this.showpass = 'text'
                this.icon = 'eye'
            }else if(this.showpass=='text'){
                this.showpass = 'password'
                this.icon = 'eye-slash'
            }
        },
        async setinfo(){
            this.form.servicios=this.selected
            let resp = `http://127.0.0.1:8000/api/createadmintareas?Id_Status_Admin=${this.form.statusa}&Id_Tipo_Admin=${this.form.tipoa}&Nombre_Admin=${this.form.nombre}&Apellido_P_Admin=${this.form.apellidop}&Apellido_M_Admin=${this.form.apellidom}&Nombre_Usuario=${this.form.nombreusuario}&Password_Hash=${this.form.pass}&Cant_dias_limit=0&Id_Cat_Tareas=${this.form.servicios}`;
            await axios.post(resp).then((data) => {
            console.log(data);
        });
        }
    },
    watch: {
        selected(newValue, oldValue) {
            // Handle changes in individual flavour checkboxes
            if (newValue.length === 0) {
                this.indeterminate = false
                this.allSelected = false
            } else if (newValue.length === this.listservicios.length) {
                this.indeterminate = false
                this.allSelected = true
            } else {
                this.indeterminate = true
                this.allSelected = false
            }
        }
    },
    mounted: function () {
        let tipoadmin = "http://127.0.0.1:8000/api/muestratipoa";
        axios.get(tipoadmin).then((data) => {
            console.log(data);
            this.tipoadmins = data.data;
        });
        let statusadmin = "http://127.0.0.1:8000/api/muestrastatusa";
        axios.get(statusadmin).then((data) => {
            console.log(data);
            this.statusadmin = data.data;
        });
        let catservicios = "http://127.0.0.1:8000/api/muestracatservicio";
        axios.get(catservicios).then((data) => {
            console.log(data);
            this.catservicios = data.data;
            for (let index = 0; index < this.catservicios.length; index++) {
                this.listservicios.push({name:this.catservicios[index].Nom_Cat_Servicios,item:this.catservicios[index].Id_Cat_Servicios});
            }
            console.log(this.listservicios);
        });
    },
};
</script>
<style scoped>
.left {
    text-align: left;
}
</style>