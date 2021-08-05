<template>
    <div>
        <router-link to="/pokedex/create" v-if="isAuthen()">Add new Pokemon</router-link>
        <pokedex-table></pokedex-table>
    </div>
</template>

<script>
// src/views/pokedex/Index.vue

import PokedexTable from '@/components/PokedexTable'
//import AuthService from '@/services/AuthService'
import AuthUser from "@/store/AuthUser"

export default {
    components: {
        PokedexTable
    },
    methods:{
        isAuthen(){
            return AuthUser.getters.isAuthen
        }
    }
}
</script>

<style>
</style>