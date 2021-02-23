<template>
  <v-app>
    <v-main class="mt-2">
      <v-tabs v-model="tab" centered>
        <v-tabs-slider color="red"></v-tabs-slider>
        <v-tab @click="changeComponent">Pokedex</v-tab>
        <v-tab @click="changeComponent">Pokemon Search</v-tab>
      </v-tabs>
      <v-tabs-items v-model="tab">
        <v-tab-item :eager="true">
          <component :is="test" />
        </v-tab-item>
        <v-tab-item :eager="true">
          <keep-alive>
            <component :is="test" />
          </keep-alive>
        </v-tab-item>
      </v-tabs-items>
    </v-main>

    <v-footer padless>
      <v-col class="text-center" cols="12">
        {{ new Date().getFullYear() }} — <strong>Vuetify</strong>
      </v-col>
    </v-footer>
  </v-app>
</template>

<script>
import PokemonList from "./components/PokemonList";
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",

  components: {
    PokemonList,
    HelloWorld,
  },

  data: () => ({
    test: "HelloWorld",
    tab: null,
  }),
  methods: {
    changeComponent() {
      if (this.tab == 1) {
        this.test = "HelloWorld";
      } else {
        this.test = "PokemonList";
      }
    },
  },
};
</script>

<style>
</style>
