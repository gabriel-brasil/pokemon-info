<template>
  <div class="home">
    <div class="wrapper">
      <h1>Pokemon Info</h1>
      <Input
        newId="inputPesquisa"
        type="text"
        labelText="Pesquise por um pokemon"
        placegolderText="bulbasaur..."
      />
      <Button @click="pesquisar">Pesquisar Pokemon</Button>
      <br />
      <br />

      <Transition>
        <div class="pokemonWrapper" v-if="pokemon">
          <div>
            <img :src="pokemon?.sprites.front_default" />
          </div>

          <div>
            <p>Nome: {{ pokemon?.name }}</p>
            <p>Tipo: {{ pokemon?.types[0].type.name }}</p>
            <p v-for="el in pokemon?.stats" :key="el.stat.name">
              {{ pokemonStats[el.stat.name.replace("-", "")] }} :
              {{ el.base_stat }}
            </p>
          </div>
        </div>
      </Transition>
    </div>
  </div>
</template>

<script>
import Input from "@/components/Input.vue";
import Button from "@/components/Button.vue";

export default {
  name: "HomeView",
  components: { Input, Button },
  data: function () {
    return {
      pokemon: null,
      pokemonStats: {
        hp: "Vida",
        attack: "Ataque",
        defense: "Defesa",
        specialattack: "Ataque especial",
        specialdefense: "Defesa especial",
        speed: "Velocidade",
      },
    };
  },
  methods: {
    pesquisar() {
      const inputPesquisa = document
        .querySelector("#inputPesquisa")
        .value.toLowerCase();
      if (inputPesquisa != "") {
        fetch(`https://pokeapi.co/api/v2/pokemon/${inputPesquisa}`)
          .then((response) => response.json())
          .then((json) => {
            this.pokemon = json;
            console.log(json);
          });
      }
    },
  },
};
</script>


<style scoped>
h1 {
  margin: 30px 0;
  font-size: 40px;
  color: #eee;
}

.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;

  width: 600px;
  height: 75vh;

  margin: 0 auto;
  padding: 0 50px;

  border-radius: 8px;
  background-color: #333;
  color: #eee;
}

.pokemonWrapper {
  display: flex;
  align-items: center;
}

p {
  text-align: left;
  font-size: 14px;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>