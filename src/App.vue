<template>
  <div id="app">
    <HeaderVue/>
    <ModalForm :contato=contato />
    <Contatos :listaContatos=listaContatos />
  </div>
</template>

<script>
import HeaderVue from './components/HeaderVue.vue'
import Contatos from './components/Contatos.vue'
import ModalForm from './components/ModalForm.vue'

export default {
  data(){
      return {
         contato :{
            nome: null,
            email: null,
            tel: null,
         },
         listaContatos: this.listarContatos()
      }
   },
  components: {
    HeaderVue,
    Contatos,
    ModalForm
  },
  methods:{
    listarContatos(){
      return useLocalStorage("listaContatos", "")
    }
  },
}

  const useLocalStorage = (key, initialValue) => {

    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.log(error);
      return initialValue;
    }
  };

  const setValue = (value) => {
    try {
      const valueToStore = value instanceof Function ? value(storedValue) : value;
      setStoredValue(valueToStore);
      if (typeof window !== "undefined") {
        window.localStorage.setItem(key, JSON.stringify(valueToStore));
      }
    } catch (error) {
      console.log(error);
    }
  };

</script>

<style>
body, ul, li, dt, dd, dl {
    margin: 16px !important;
    font-family: 'Roboto', sans-serif !important;
    background: #f8f9fd !important;
}
</style>

