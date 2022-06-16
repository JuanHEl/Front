<template>
    <div class="">
        <h1 v-if="permisos.length==0" class="text-white">No tienes permisos para configurar la RED</h1>
        <div v-for="permiso in permisos" :key="permiso">

            <div align="center" class="center" style="width: 50%" v-if="permiso==2">
                <h1 class="text-white">Router</h1>
                <b-form @submit.stop.prevent="configrouter" class="control-label text-white">
                    <b-form-group id="input-group-2" label="IP ROUTER" label-for="input-2">
                        <b-form-input v-model="router.ip" id="input-1" type="text" required placeholder="ip del router"></b-form-input>
                    </b-form-group>
                </b-form>
                <b-form-group
                class="ml-4 control-label text-white"
                label="Selecciona la configuración"
                v-slot="{ ariaDescribedby }"
                >
                <b-form-checkbox-group
                    class="control-label text-white"
                    v-model="selectedrouter"
                    :options="optionsrouter"
                    :aria-describedby="ariaDescribedby"
                    switches
                    stacked
                ></b-form-checkbox-group>
                </b-form-group>
                <b-button class="btn btn-primary" variant="primary" type="submit">Configurar Router</b-button>
            </div>

            <div align="center" class="center" style="width: 50%" v-if="permiso==3">
                <h1 class="text-white">Switch</h1>
                <b-form @submit.stop.prevent="configswitch" class="control-label text-white">
                    <b-form-group id="input-group-2" label="IP SWITCH" label-for="input-2">
                        <b-form-input v-model="switches.ip" id="input-1" type="text" required placeholder="ip del switch"></b-form-input>
                    </b-form-group>
                </b-form>
                <b-form-group
                class="ml-4 control-label text-white"
                label="Selecciona la configuración"
                v-slot="{ ariaDescribedby }"
                >
                <b-form-checkbox-group
                    class="control-label text-white"
                    v-model="selectedswitch"
                    :options="optionsswitch"
                    :aria-describedby="ariaDescribedby"
                    switches
                    stacked
                ></b-form-checkbox-group>
                </b-form-group>
                <b-button class="btn btn-primary" variant="primary" type="submit">Configurar Switch</b-button>
            </div>

            <div align="center" class="center" style="width: 50%" v-if="permiso==4">
                <h1 class="text-white">Servidor</h1>
                <b-form @submit.stop.prevent="configsserv" class="control-label text-white">
                    <b-form-group id="input-group-2" label="IP SERVIDOR" label-for="input-2">
                        <b-form-input v-model="servidor.ip" id="input-1" type="text" required placeholder="ip del servidor"></b-form-input>
                    </b-form-group>
                </b-form>
                <b-form-group
                class="ml-4 control-label text-white"
                label="Selecciona la configuración"
                v-slot="{ ariaDescribedby }"
                >
                <b-form-checkbox-group
                    class="control-label text-white"
                    v-model="selected"
                    :options="options"
                    :aria-describedby="ariaDescribedby"
                    switches
                    stacked
                ></b-form-checkbox-group>
                </b-form-group>
                <b-button class="btn btn-primary" variant="primary" type="submit">Configurar Servidor</b-button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
    name:'FormConfig',
    data(){
        return{
            servidor:{
                ip: "",
                servicios: "",
            },
            switches: {
                ip: "",
                servicios: "",
            },
            router: {
                ip: "",
                servicios: "",
            },
            selected: [],
            options: [
                {text: "Instalar FTP", value: "FTP"},
                {text: "Instalar Proxy", value: "Proxy"},
                {text: "Instalar Hwp", value: "Hwp"},
                {text: "Instalar Apache", value: "Apache"},
            ],
            selectedswitch: [],
            optionsswitch: [
                {text: "Instalar FTP", value: "FTP"},
                {text: "Instalar Proxy", value: "Proxy"},
                {text: "Instalar Hwp", value: "Hwp"},
                {text: "Instalar Apache", value: "Apache"},
            ],
            selectedrouter: [],
            optionsrouter: [
                {text: "Instalar FTP", value: "FTP"},
                {text: "Instalar Proxy", value: "Proxy"},
                {text: "Instalar Hwp", value: "Hwp"},
                {text: "Instalar Apache", value: "Apache"},
            ],
            permisos:[]
        }
    },
    computed:{},
    methods:{
        async configswitch(){

        },
        async configrouter(){

        },
        async configsserv(){
            
        }
    },
    mounted: function () {
        let permisos=this.$cookies.get("tareaa").admins;
        for (let index = 0; index < permisos.length; index++) {
            const element = permisos[index];
            this.permisos.push(element.tareaenadmin);
            // console.log(element.tareaenadmin)
        }
    }
}
</script>
<style scoped>
    .center {
    text-align: center;
    justify-content: center;
    }
</style>
