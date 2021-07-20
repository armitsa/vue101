<template>
  <div>
    Add New Pokemon

    <div>
        <div>
            <label for="name"> Name (EN)</label>
            <input type="text" v-model="form.name.english"> 
        </div>
        
        <div>
            <label for="name"> Name (JP)</label>
            <input type="text" v-model="form.name.japanese">
        </div>

        <div>
            <label for="type"> Type </label>
            <input type="text" v-model="form.type">
        </div>

        <div>
            <button @click="addPokemon">Add</button>
        </div>
    </div>
  </div>
</template>

<script>

import PokemonStore from '@/store/Pokemon'
export default {
    data() {
        return {
            form: {
                name: {
                    english: '',
                    japanese: '',
                },
                type: ''
            }
        }
    },
    methods: {
        clearForm() {
            this.form = {
                name: {
                    english: '',
                    japanese: ''
                },
                type: ''
            }
        },
        addPokemon() {
            let payload = {
                name: this.form.name,
                type: this.form.type.split(",").map(
                    (item) => item.trim()
                )
            }
            //todo : เรียก action ใน PokemonStore เพื่อเพิ่มข้อมูล
            console.log(payload)
            PokemonStore.dispatch("addPokemon", payload)

            this.clearForm()
        }
    }
}
</script>

<style>

</style>