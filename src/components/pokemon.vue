<template>
  
  <div>
    
    <div class="mb-5" v-if="pokemonInfo">

      

      <div class="d-flex justify-content-center"><img  :src="pokemonInfo.image"></div>
      <span class="d-flex justify-content-center m-5"><input  @keyup.enter="pokemon" v-model="namePokemon" type="text"></span>
      <div class="d-flex justify-content-center" >
        <p> <span class="fw-bold "> name</span>: {{pokemonInfo.name}} </p>
        <p> <span class="fw-bold ps-5">HP</span>:  {{pokemonInfo.stats.HP}} </p>
        <p> <span class="fw-bold ps-5">attack</span>:  {{pokemonInfo.stats.attack}} </p>
      </div>
      
      <table class="w-100">
        <tbody>
          <tr class="d-flex flex-wrap">
            
            <td class="d-flex justify-content-center w-50">
              <div style="width: 50%;" class="d-flex flex-column">
                <span class="mb-3 d-flex justify-content-center"><p class="fs-5 m-0 fw-bold"> vulnerable à :</p></span>
                <ul class="list-unstyled d-flex flex-wrap pe-none justify-content-center">
                  <template v-for="resistance in pokemonInfo.apiResistances">
                    <p class="p-2 m-2 btn btn-danger" style="width: 80px;" :key="resistance.name" v-if="resistance.damage_multiplier == 2" >{{resistance.name}}  </p>
                  </template>
                </ul>
             </div>
            </td>
            
            <td class="d-flex justify-content-center w-50"> 
              <div style="width: 50%;" class="d-flex flex-column">
                <span class="mb-3 d-flex justify-content-center"><p class="fs-5 m-0 fw-bold"> resistant à:</p></span>
                <ul class="list-unstyled d-flex flex-wrap pe-none justify-content-center">
                  <template v-for="resistance in pokemonInfo.apiResistances">
                    <li class="p-2 m-2 btn btn-success" style="width: 80px;" :key="resistance.name" v-if="resistance.damage_multiplier == 0.5" >{{resistance.name}}</li>
                  </template>
                </ul> 
              </div>           
            </td>
              
            <td class="d-flex justify-content-center w-100">     
              <div style="width: 30%;" class="d-flex flex-column" >
                <span class="mb-3 d-flex justify-content-center"><p class="fs-5 m-0 fw-bold "> neutre à :</p></span>
                <ul class="list-unstyled d-flex flex-wrap pe-none justify-content-center">
                  <template v-for="resistance in pokemonInfo.apiResistances">
                    <li class="p-2 m-2 btn btn-secondary" style="width: 80px;" :key="resistance.name" v-if="resistance.damage_multiplier == 1" >{{resistance.name}}</li>
                  </template> 
              </ul> 
              </div>   
            </td>     

          </tr>
        </tbody>
      </table>


      
 
    </div>
    <p v-else > aucun pokemon trouver a ce nom </p>
    
  </div>
  
</template>
  
<script>

export default {
  data() {
    return {
      namePokemon: "pikachu",
      pokemonInfo: null,
    }
  },
  
  methods: {  
    pokemon(){
      fetch(`https://pokebuildapi.fr/api/v1/pokemon/`+this.namePokemon)
      .then(
        res => {
          
          if (!res.ok) {
            return Promise.reject(console.log('prout'))
          }
          return res.json()
        }
      )
      .catch(err => null)
      .then(data => this.pokemonInfo = data)    
    },
  },
  mounted() {
    this.pokemon()  
  }
}


</script>


  
  