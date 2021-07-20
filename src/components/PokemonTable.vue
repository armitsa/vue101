<template>
  <div>
      <table>
          <thead>
              <tr>
                  <th>#</th>
                  <th>Name (EN)</th>
                  <th>Name (JP)</th>
                  <th>Type</th>
                  <th>Action</th>
              </tr>
          </thead>
          <tbody>
              <tr v-for="(poke,index) in pokemons" :key="index">
              <td>{{ index + 1 }}</td>
              <td v-if="index !== editIndex">{{ poke.name.english }}</td>
              <td v-if="index === editIndex">
                  <input type="text" v-model="form.name.english">
              </td>

              <td v-if="index !== editIndex">{{ poke.name.japanese }}</td>
              <td v-if="index === editIndex">
                  <input type="text" v-model="form.name.japanese">
              </td>

              <td v-if="index !== editIndex">{{ poke.type }}</td>
              <td v-if="index === editIndex">
                  <input type="text" v-model="form.type">
              </td>

              <td v-if="index !== editIndex">
                  <button @click="openForm(index, poke)">Click to Edit</button>
              </td>
              <td v-if="index === editIndex">
                  <button @click="editPokemon">Update Pokemon</button>
                  <button @click="closeForm">Cancel</button>

              </td>
              </tr>
          </tbody>
      </table>

  </div>
</template>

<script>
// src/components/PokemonTabel.vue
import PokemonStore from '@/store/Pokemon'

export default {
    data() {
        return{
            pokemons: [], //list เอาไว้แสดง
            //สำหรับ form แก้ไข
            editIndex: -1,
            form :{
                name: {
                    english: '',
                    japanese: ''
                },
                type: ''
            }
        }
    },
    created(){
        this.fetchPokemon()
    },
    methods:{
        async fetchPokemon() {
            //เรียก action ใน store ใช้ disatch('ชื่อ action')
            await PokemonStore.dispatch('fetchPokemon')

            //เรียก getter ใน store
            this.pokemons = PokemonStore.getters.pokemons
        },
        openForm(index, pokemon){
            console.log('index', index)
            console.log('pokemon', pokemon)
            //ค่าใช้จ่ายสูงเพราะแปลงค่าไปมา
            let cloned = JSON.parse(JSON.stringify(pokemon))
            this.editIndex = index 
            this.form.name = cloned.name
            this.form.type = cloned.type.join(', ')

        },
        closeForm(){
            this.editIndex = -1
            this.form = {
                name: {
                    english: '',
                    japanese: ''
                },
                type: ''
            }
        },
        editPokemon(){
            let payload = {
                index: this.editIndex,
                name: this.form.name,
                type: this.form.type.split(',').map(
                    (item) => item.trim()
                ),
            }
            console.log(payload)
            PokemonStore.dispatch("editPokemon", payload)
            this.closeForm()
        },
    }

}
</script>

<style>

</style>