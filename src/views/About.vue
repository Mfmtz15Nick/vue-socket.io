<template>
  <div class="diego">
    <div>
      <div>
        <table id="matrix">
          <tr>
            <td>
              <button id="b1">
                <span>{{matriz.boton1}} </span>
              </button>
            </td>
            <td>
              <button id="b2">{{matriz.boton2}}</button>
            </td>
            <td>
              <button id="b3">{{matriz.boton3}}</button>
            </td>
          </tr>

          <tr>
            <td>
              <button id="b4">{{matriz.boton4}}</button>
            </td>
            <td>
              <button id="b5">{{matriz.boton5}}</button>
            </td>
            <td>
              <button id="b6">{{matriz.boton6}}</button>
            </td>
          </tr>

          <tr>
            <td>
              <button id="b7">{{matriz.boton7}}</button>
            </td>
            <td>
              <button id="b8">{{matriz.boton8}}</button>
            </td>
            <td>
              <button id="b9">{{matriz.boton9}}</button>
            </td>
          </tr>
        </table>
      </div>
      <br />
      <br />
      <div>
        <input placeholder="Numero de boton" autofocus  v-model="texto" class="form-control" />
        <br />
        <input placeholder="Texto" autofocus v-on:keyup.13="putElement" v-model="letras" class="form-control" />
        <br />

        <button
          @click="putElement()"
          class="btn text-light btn-block bg-success font-weight-bold"
        >Send</button>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
let lista = document.getElementById("lista");

export default {
  name: "Home",
  components: {
    HelloWorld
  },
  data: function() {
    return {
      matriz:{
        boton1:"" ,
        boton2:"" ,
        boton3:"" ,
        boton4:"" ,
        boton5:"" ,
        boton6:"" ,
        boton7:"" ,
        boton8:"" ,
        boton9:"" ,
      },
      texto: '',
      letras: ''
    };
  },
  methods: {
    putElement() {
        let boton = "boton" + this.texto
        this.matriz[boton] = this.letras;
        this.texto = ''
        this.letras = ''
    }
  }
};
</script>

<style scoped>
.diego {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#matrix {
  margin: 0 auto;
  padding: 5px;
}

#matrix tr,
td {
  padding: 5px;
}

#matrix button {
  height: 80px;
  width: 150px;
  border: none;
  font-family: helvetica;
  font-weight: bold;
}
/* 
#b1,
#b3 {
  background-color: rgba(255, 153, 51, 0.5);
}

#b1:hover,
#b3:hover {
  background-color: rgb(255, 153, 51);
}

#b2 {
  background-color: rgba(15, 138, 15, 0.5);
}

#b2:hover {
  background-color: rgb(15, 138, 15);
}

#b4 {
  background-color: rgba(189, 15, 15, 0.6);
}

#b4:hover {
  background-color: rgb(189, 15, 15);
} */
</style>
