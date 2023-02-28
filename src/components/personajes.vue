<script>
import axios from "axios";
let API_URL = `https://rickandmortyapi.com/api/character`;
export default {
  data() {
    return {
      info: [],
      personajes: [],
      pagina: 1,
      siguiente: null,
      anterior: null,
      buscar: "",
      modal:false,
    };
  },
  mounted() {
    axios.get(API_URL).then((response) => {
      this.info = response.data.info;
      this.personajes = response.data.results;
    });
  },

  methods: {
    navpag(num) {
      API_URL =
        "https://rickandmortyapi.com/api/character/?page=" + this.pagina;
      console.log(API_URL);
      axios.get(API_URL).then((response) => {
        console.log(response.config);
        this.info = response.data.info;
        this.personajes = response.data.results;
      });
    },
    buscador(text) {
      API_URL =
        "https://rickandmortyapi.com/api/character/?name=" + text
      console.log(API_URL);
      axios.get(API_URL).then((response) => {
        console.log(response.config);
        this.info = response.data.info;
        this.personajes = response.data.results;
        this.pagina=1
      });
    },
  },
};
</script>

<template>
  <!----modal-->
  <Transition enter-active-class="ease-out duration-300"
      enter-class="opacity-0" enter-to-class="opacity-100"
      leave-active-class="ease-in duration-200"
      leave-class="opacity-100" leave-to-class="opacity-0">
  <div class="relative z-10" aria-labelledby="modal-title" role="dialog" aria-modal="true" v-show="modal">
  <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"></div>
  <div class="fixed inset-0 z-10 overflow-y-auto">
    <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">

      <Transition enter-active-class="ease-out duration-300"
      enter-class="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95" enter-to-class="opacity-100 translate-y-0 sm:scale-100"
      leave-active-class="ease-in duration-200" 
      leave-class="opacity-100 translate-y-0 sm:scale-100" leave-to-class="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">

      <div v-show="modal" class="relative transform overflow-hidden rounded-lg bg-white text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg">
        <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
          <div class="sm:flex sm:items-start">
            <div class="mx-auto flex h-12 w-12 flex-shrink-0 items-center justify-center rounded-full bg-red-100 sm:mx-0 sm:h-10 sm:w-10">
              <img
            class="rounded-full"
            v-bind:src="this.personajes.image"
            alt="Imagen_Personaje"
          />
            </div>
            <div class="mt-3 text-center sm:mt-0 sm:ml-4 sm:text-left">
              <h3 class="text-base font-semibold leading-6 text-gray-900" id="modal-title">Deactivate account</h3>
              <div class="mt-2">
                <p class="text-sm text-gray-500">Are you sure you want to deactivate your account? All of your data will be permanently removed. This action cannot be undone.</p>
              </div>
            </div>
        </div>
        <div class="bg-gray-50 px-4 py-3 sm:flex sm:flex-row-reverse sm:px-6">
          <button @click="modal=false" type="button" class="mt-3 inline-flex w-full justify-center rounded-md border border-gray-300 bg-white px-4 py-2 text-base font-medium text-gray-700 shadow-sm hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 sm:mt-0 sm:ml-3 sm:w-auto sm:text-sm">Cancel</button>
        </div>
      </div>
      </div>
      </Transition>
    </div>
  </div>
</div>
</Transition>

    <div>
      <div class="flex justify-center gap-6 p-5 pb-5">
        <input v-model="BUSCAR" placeholder="BUSCAR" class="text-black font-medium"/>
        <button class="button text-black font-medium" @click="buscador(BUSCAR)">BUSCAR</button>
      </div>
      <h2 class="text-center font-medium" >EXISTEN  {{ info.count }} PERSONAJES EN LA SERIE</h2>
      <div class="flex justify-center gap-6 p-5 pb-0">
        <button
          class="button text-black w-20 font-medium border-2 border-sky-500"
          v-if="pagina !== 1"
          @click="navpag(pagina--)"
        >
            ANTERIOR 
        </button>
        <a>{{ pagina }}</a>
        <button
          class="button w-20 font-medium border-2 border-sky-500"
          v-if="pagina !== this.info.pages"
          @click="navpag(pagina++)"
        >
          SIGUIENTE
        </button>
      </div>
    </div>

    <div>
      <ul class="grid grid-cols-4 text-center">
        <li @click="modal=true" type="button"
          class="card bg-green-900 outline outline-pink-500 rounded-3xl m-5 scale-75 cursor-pointer hover:rotate-2"
          v-for="p in personajes"
        >
          <img
            class="rounded-t-3xl"
            v-bind:src="p.image"
            alt="Imagen_Personaje"
          />
          <a>{{ p.name }}</a>
          
        </li>
      </ul>
    </div>
    <div class="flex justify-center gap-6 p-5 pb-0">
        <button
          class="button text-black w-20 font-medium border-2 border-sky-500"
          v-if="pagina !== 1"
          @click="navpag(pagina--)"
        >
          ANTERIOR
        </button>
        <a>{{ pagina }}</a>
        <button
          class="button w-20 font-medium border-2 border-sky-500"
          v-if="pagina !== this.info.pages"
          @click="navpag(pagina++)"
        >
            SIGUIENTE  
        </button>
    </div>
</template>