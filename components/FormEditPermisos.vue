<template>
    <div id="contenedor">
        <div id="tabla">
            <h1 class="text-white">Editar Permisos</h1> <br>
            <div class="form-group left col-sm-10">
                <b-input-group v-if="form.id.length > 0">
                    <b-input-group-prepend is-text @click.prevent="setinfo()">
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
                <b-input-group v-else>
                    <b-input-group-prepend is-text >
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
            <div class="container form-group col-sm-10">
                <b-form-group>
                    <template #label>
                        <label for="" class="control-label text-white">Selecciona los servicios:</label>
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
            </div>
            <div class="form-group">
                <button type="button" class="btn btn-primary" v-on:click="salir()">
                    Salir
                </button>
                <b-button type="button" style="color:white" class="btn btn-primary" variant="primary" v-on:click="setpermisos" to="/admins" :disabled="bloqueado">
                    Finalizar
                </b-button>
            </div>
        </div>
        <div id="botones">
            <div>
                <br>
                <b-button block class="buttons" pill variant="primary" to="/nuevoadmin" font-scale="3"> Agregar Nuevo Administrador</b-button>
                <b-button block class="buttons" pill variant="primary" to="cambiastatus" font-scale="3"> Cambiar Status </b-button>
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
            bloqueado:true,
            selected: [],
            allSelected: false,
            indeterminate: false,
            listservicios:[],
            // Listaadmins: null,
            // logs:[],
            form: {
                id: "",
            }
        };
    },
    components: {
    },
    methods: {
        // buscanombre(){
        //     this.logs=this.Listaadmins;
        //     let listapornombre = this.logs.filter(x => x.Id_Administradores == this.form.id);
        //     this.logs=listapornombre;
        //     this.form.id=this.logs[0].Id_Administradores;
        //     // this.form.nombre=this.logs[0].Nombre_Admin;
        //     // this.form.apellidop=this.logs[0].Apellido_P_Admin;
        //     // this.form.apellidom=this.logs[0].Apellido_M_Admin;
        //     // this.form.nombreusuario=this.logs[0].Nombre_Usuario;
        //     // this.form.tipoa=this.logs[0].Id_Tipo_Admin[0].Id_Tipo_Admin;
        //     this.bloqueado=false;
        //     console.log(this.logs);
        // },
        toggleAll(checked) {
            let listavariable = [];
            let variable;
            for (let index = 0; index < this.listservicios.length; index++) {
                variable = this.listservicios[index].item;
                listavariable.push(variable)
            }
            this.selected = checked ? listavariable : []
        },
        salir() {
            this.$router.push("/admins");
        },
        async setinfo(){
            let lista=[];
            let listaapintar=[];
            let resp = `http://127.0.0.1:8000/api/showcattareaa/${this.form.id}`;
            await axios.get(resp).then((data) => {
                // for (let index = 0; index < data.data.admins.length; index++) {
                //     listaapintar.push(data.data.admins[index].tareaenadmin);
                //     // console.log(data.data.admins[index].tareaenadmin);
                // }
                for (let index = 0; index < this.listservicios.length; index++) {
                    console.log(this.listservicios[index].item)
                    console.log(data.data.admins[index].tareaenadmin)

                    // if (this.listservicios[index].item == data.data.admins[index].tareaenadmin) {
                    //     listaapintar.push(data.data.admins[index].tareaenadmin);                        
                    // }else{
                    //     lista.push(data.data.admins[index].tareaenadmin);    
                    // }


                    // if (data.data.admins[index]) {
                    //     console.log(this.listservicios[index].item);
                    //     console.log(data.data.admins[index].tareaenadmin)
                    // if (!this.listservicios.includes(data.data.admins[index].tareaenadmin)) {
                    //     const element = this.listservicios[index];
                    //     lista.push(element);
                    // }else{
                    //     listaapintar.push(data.data.admins[index].tareaenadmin);    
                    // }
                    // }
                }
            this.selected=listaapintar;
            this.bloqueado=false;
            console.log("Aqui ta")
            console.log(listaapintar);
            console.log("Lista a borrar")
            console.log(lista)
        });
        },
        async setpermisos(){
        //     let resp = `http://127.0.0.1:8000/api/update?Id_Administradores=${this.form.id}&Id_Status_Admin=${this.logs[0].Id_Status_Admin[0].Id_Status_Admin}&Nombre_Admin=${this.form.nombre}&Apellido_P_Admin=${this.form.apellidop}&Apellido_M_Admin=${this.form.apellidom}&Nombre_Usuario=${this.form.nombreusuario}&Id_Tipo_Admin=${this.form.tipoa}&Password_Hash=${this.logs[0].Password_Hash}&Cant_dias_limit=${this.logs[0].Cant_dias_limit}`;
        //     await axios.put(resp).then((data) => {
        //     // console.log(resp);
        // });
        },
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
        // let admin = "http://127.0.0.1:8000/api/muestra";
        // axios.get(admin).then((data) => {
        //     // console.log(data);
        //     this.Listaadmins = data.data;
        //     this.logs = this.Listaadmins;
        // });
        let catservicios = "http://127.0.0.1:8000/api/muestracatservicio";
        axios.get(catservicios).then((data) => {
            // console.log(data);
            this.catservicios = data.data;
            for (let index = 0; index < this.catservicios.length; index++) {
                this.listservicios.push({name:this.catservicios[index].Nom_Cat_Servicios,item:this.catservicios[index].Id_Cat_Servicios});
            }
            console.log(this.listservicios);
        });
        // let cattareas = `http://127.0.0.1:8000/api/showcattareaa/${this.form.id}`;
        // axios.get(cattareas).then((data) => {
        //     console.log(data);
        //     // this.catservicios = data.data;
        //     // for (let index = 0; index < this.catservicios.length; index++) {
        //     //     this.listservicios.push({name:this.catservicios[index].Nom_Cat_Servicios,item:this.catservicios[index].Id_Cat_Servicios});
        //     // }
        //     // console.log(this.listservicios);
        // });
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