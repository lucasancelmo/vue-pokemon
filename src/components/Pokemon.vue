<template>
  <v-flex xs12 sm4 md3 lg3 xl2>
    <v-hover open-delay="50" close-delay="75" v-slot="{ hover }">
      <v-card block class="ma-2" outlined :elevation="hover ? 3 : 1">
        <v-checkbox @change="addToList(pokemon.id)" class="mt-2 ml-2" hide-details> </v-checkbox>
        <v-list-item class="pa-1">
          <v-list-item-content>
            <div class="overline ml-1"># {{ pokedata.id }}</div>
            <v-list-item-title class="headline mb-2">
              {{ pokemon.name.toUpperCase() }}
            </v-list-item-title>
            <v-list-item-subtitle>
              <v-container v-if="pokedata.types.length >= 2">
                <v-chip :class="pokedata.types[0].type.name">
                  {{ pokedata.types[0].type.name }}
                </v-chip>
                <v-chip :class="pokedata.types[1].type.name">
                  {{ pokedata.types[1].type.name }}
                </v-chip>
              </v-container>

              <v-container v-else>
                <v-chip :class="pokedata.types[0].type.name">
                  {{ pokedata.types[0].type.name }}
                </v-chip>
              </v-container>
            </v-list-item-subtitle>
          </v-list-item-content>

          <v-list-item-avatar size="80" color="red darken-1">
            <v-img
              style="cursor:pointer;"
              class="elevation-6"
              :src="pokedata.front"
            >
            </v-img>
          </v-list-item-avatar>
        </v-list-item>
      </v-card>
    </v-hover>
  </v-flex>
</template>

<script>
import axios from "axios";
export default {
  props: {
    pokemon: Object,
    index: Number,
  },
  data() {
    return {
      pokedata: {
        types: [{ type: "" }],
        front: "",
        id: "",
      },
    };
  },
  mounted() {
    axios.get(this.pokemon.url).then((response) => {
      this.pokedata.types = response.data.types;
      this.pokedata.front = response.data.sprites.front_default;
      this.pokedata.id = response.data.id;
    });
  },
  methods:{
    addToList(id){
      return this.$emit('faveList', id);
    }
  }
};
</script>

<style scoped>
.normal {
  background-color: #aa9 !important;
}
.fire {
  background-color: #f42 !important;
}
.grass {
  background-color: #7c5 !important;
}
.bug {
  background-color: #ab2 !important;
}
.water {
  background-color: #39f !important;
}
.flying {
  background-color: #89f !important;
}
.poison {
  background-color: #a59 !important;
}
</style>
