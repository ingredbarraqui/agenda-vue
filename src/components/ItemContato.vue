<template>
   <tr :class=defineDestaque(contato)>
      <td class="nome">
        <span class="icone" :style="{backgroundColor:corIcone(contato.nome[0])}">
            {{contato.nome[0]}}
        </span>{{contato.nome}}
      </td>
      <td>{{contato.email}}</td>
      <td>{{contato.tel}}</td>
      <td class="edit">
         <button type="button" data-toggle="modal" :data-target="'#ModalContato' + contato.id"><img src="../assets/ic-edit.svg" /></button>
         <button type="button" data-toggle="modal" :data-target="'#ModalExcluir' + contato.id"><img src="../assets/ic-delete.svg"/></button>
         <ModalExcluir :index=contato.id />
         <ModalForm titulo="Editar contato" :contato=contato />
      </td>
   </tr>
</template>

<script>
import ModalForm from './ModalForm.vue'
import ModalExcluir from './ModalExcluir.vue'

export default {
    props: [
        "contato"
    ],

    components: {
        ModalExcluir,
        ModalForm,
   },

    data(){
        return{
            nome: "null",
            email: "null",
            tel: "null",
        }
    },

    methods: {
        defineDestaque(contato) {
            if (Date.parse(contato.destaqueAte) >= new Date()) {
                return "destaque";
          }
            return "";
        },

        corIcone(letra){
            if(typeof letra !== "string"){
                return "#fff"
            }

            var hue = Math.floor((letra.toLowerCase().charCodeAt()-96)/26*360);
            return "hsl(" + hue + ", 100%, 70%)";
        }
    },
}
</script>

<style scoped>
.icone{
    content: "";
    display: inline-block;
    width: 25px;
    height: 25px;
    border-radius: 50%;
    text-align: center;
    vertical-align: middle;
    line-height: 25px;
    color: #fff;
    text-transform: uppercase;
    margin-right: 10px;
}

.contato{
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 100%;
    border-radius: 4px;
}

.contato tr{
    border: solid 1px #e1e1e1;
    background-color: #ffffff;
}

.contato th{
    background: #fff;
    color: #9198af;
    font-weight: normal;
    font-size: 0.813rem;
    padding: 1rem;
    text-align: initial;
    width: 30%;
}

.contato td{
    margin: 0.063rem 1rem 0;
    padding: 1rem;
    border: #e1e1e1;
    color: #2a2d3b;
}

.contatos{
    text-align: center;
}

tr:not(:first-child):hover {
    background-color: #fff3f2;
}

tr.destaque td {
    background-color: #fff3f2;
}

.edit button{
    background: none;
    border: none;
    cursor: pointer;
    display: -webkit-inline-box
}
</style>
