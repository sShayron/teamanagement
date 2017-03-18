<template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>Maratona Inovatech</h1>
    </div>
    <div class="row">

      <div class="col-xs-6">
        <div class="panel panel-success">
          <div class="panel-heading">
            <h3>Adicionar Integrante</h3>
          </div>
          <div class="panel-body">
            <form id="form" class="form-inline" @submit.prevent="addIntegrante">
              <div class="form-group">
                  <input type="text" id="integranteNome" placeholder="Nome: " value="" class="form-control" v-model="newIntegrante.nome">
              </div>
              <!--<div class="form-group">
                  <input type="text" id="integranteCurso" placeholder="Curso: " value="" class="form-control" v-model="newIntegrante.curso">
              </div>-->
              <div class="form-group">
                  <input type="text" id="integranteGrupo" placeholder="Grupo: " value="" class="form-control" v-model="newIntegrante.grupo">
              </div>
              <div class="form-group">
                  <input type="text" id="integrantePeriodo" placeholder="Periodo: " value="" class="form-control" v-model="newIntegrante.periodo">
              </div>
              <div class="form-group">
                  <input type="text" id="integranteEmail" placeholder="E-mail: " value="" class="form-control" v-model="newIntegrante.email">
              </div>
              <input type="submit" class="btn btn-success" value="Adicionar Integrante">
            </form>
          </div>
        </div>
      </div>

      <div class="col-xs-6">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>
                Nome
              </th>
              <!--<th>
                Curso
              </th>-->
              <th>
                Grupo
              </th>
              <th>
                Periodo
              </th>
              <th>
                E-mail
              </th>
              <th>
                Remover
              </th>
              <th>
                Alterar
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="integrante in integrantes">
              <td>
                {{ integrante.nome }}
              </td>
              <!--<td>
                {{ integrante.curso }}
              </td>-->
              <td>
                {{ integrante.grupo }}
              </td>
              <td>
                {{ integrante.periodo }}
              </td>
              <td>
                {{ integrante.email }}
              </td>
              <td>
                <span class="glyphicon glyphicon-trash remove" @click="removeIntegrante(integrante)"></span>
              </td>
              <td>
                <span class="glyphicon glyphicon-edit edit"></span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
  
    </div>
  </div>
</template>

<script>
import Firebase from 'firebase'
import toastr from 'toastr'

let config = {
  apiKey: "AIzaSyA82va9a2fR860rzjLlxTCtqYq7Zr7RQO0",
  authDomain: "vuejs-firebase-01-f8d34.firebaseapp.com",
  databaseURL: "https://vuejs-firebase-01-f8d34.firebaseio.com",
  storageBucket: "vuejs-firebase-01-f8d34.appspot.com",
  messagingSenderId: "104892687296"
}

let app = Firebase.initializeApp(config);
let db = app.database();

let integrantesRef = db.ref('integrantes');

export default {
  name: 'app',
  firebase: {
    integrantes: integrantesRef
  },
  data () {
    return {
      newIntegrante: {
        nome: '',
        curso: '',
        grupo: '',
        periodo: '',
        email: ''
      }
    }
  },
  methods: {
    addIntegrante: function(){
      integrantesRef.push(this.newIntegrante);
      this.newIntegrante.nome = '';
      this.newIntegrante.curso = '';
      this.newIntegrante.grupo = '';
      this.newIntegrante.periodo = '';
      this.newIntegrante.email = '';
    },
    removeIntegrante: function(integrante) {
      integrantesRef.child(integrante['.key']).remove();
      toastr.success('Integrante Removido');
    },
    editIntegrante: function(integrante) {
      // integrantesRef.child(integrante['.key']).update();
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.form-group {
  width: 100%;
}
input{
  margin: 5px 0;
  width: 80%!important;
}
.remove {
  cursor: pointer;
  color: red;
}
.edit {
  cursor: pointer;
  color: cadetblue;
}
</style>
