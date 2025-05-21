<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
  <div>
    <v-container fluid>
      <br>
      <div style="text-align: center">
        <h1>Vue Slide Swap Zoom</h1>
        <p>
          Vue-Slide-Swap-Zoom é um componente Vue.js leve e personalizável que permite criar transições de slides com efeitos dinâmicos de deslizar,
          troca e zoom, ideal para galerias de imagem, carrosséis ou exibições de conteúdo interativo.        </p>
        <br>
      </div>
      <v-row>
        <v-col cols="12" >
          <h2>Vertical</h2>
        </v-col>
        <v-col cols="6" >
         
          <h3>Com lente</h3>
          <VSlideSwapZoom :images="images" :is_magnify="true" :is_vertical="true"></VSlideSwapZoom>
        </v-col>
        <v-col cols="6" >
          <h3>Sem lente</h3>
          <VSlideSwapZoom :images="images" :is_magnify="false" :is_vertical="true"></VSlideSwapZoom>
        </v-col>
        <v-col cols="12" >
          <h2>Horizontal</h2>
        </v-col>
        
        <v-col cols="6" >
          <h3>Com lente</h3>
          <VSlideSwapZoom :images="images" :is_magnify="true" :is_vertical="false"></VSlideSwapZoom>
        </v-col>
      
        <v-col cols="6" >
          <h3>Sem lente</h3>
          <VSlideSwapZoom :images="images" :is_magnify="false" :is_vertical="false"></VSlideSwapZoom>
        </v-col>
        
        
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import VSlideSwapZoom from "../components/VSlideSwapZoom";

export default defineComponent({
  name: 'HomeView',
  components: {
    VSlideSwapZoom,
  },
  data:()=>({
    images: [],
  }),
  created() {
    this.images = Array.from({length: 10}, (_, index) => ({
      id: index + 1,
      url: `https://picsum.photos/400/200?random=${index + 1}`,
    }))
  },
});
</script>
