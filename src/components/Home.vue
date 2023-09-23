<template>
  <img src="../assets/img/spesa2.jpg" alt="foto Spesa" class="fotoSpesa">
  <div class="full-container">
    <div id="sfondo" class="col-sm-12">
      <h1>Scrivi qua cosa devi comprare:</h1>
      <p id="errore"></p>
      <div id="input">
        <input
          type="text"
          v-model="item"
          @keyup.enter="addItem"
          placeholder="Inserisci un prodotto"
        />
        <button @click="addItem">INVIO</button>
      </div>
      <div class="col-sm-12">
        <article v-if="listaSpesa != 0">
          <div v-for="item in listaSpesa.length" id="list">
            <div id="item">
              <input type="checkbox" id="checkbox" />
              <h2 id="element">{{ listaSpesa[item - 1] }}</h2>
              <div id="icons">
                <div>
                  <img
                    src="../assets/icone/delete.png"
                    alt="deleteItem"
                    height="30"
                    @click="deleteItem(item)"
                  />
                </div>
              </div>
            </div>
          </div>
          <button @click="deleteAllItems" class="reset">Azzera lista</button>
        </article>
        <article v-else id="emptyList">
          <h2>La lista è vuota!</h2>
          <h3>Comincia aggiungendo qualche elemento!</h3>
        </article>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "Home",
  setup() {
    let item = ref();
    let listaSpesa = ref([]);
    let err = ref(false);

    function addItem() {
      console.log("cliccato")
      if (item.value == null || item.value.length == 0 || item.value.trim() == "") {
        console.log("vuoto")
        document.getElementById("errore").innerHTML = "Non è stato inserito niente! Inserisci un elemento!"
      }else if(this.listaSpesa.includes(item.value.toUpperCase())){
        console.log("Il prodotto c'è già")
        document.getElementById("errore").innerHTML = "L'elemento inserito è già presente nella lista, aggiungine un altro!"
        this.item = "";
      }else{
        document.getElementById("errore").innerHTML = ""
        this.listaSpesa.push(item.value.toUpperCase());
        console.log(item.value);
        console.log(this.listaSpesa.length);
        this.item = "";
        }
    }

    function deleteItem(item) {
      console.log("Delete " + item);
      this.listaSpesa.splice(item - 1, 1);
    }

    function approvedItem(item) {
      console.log("Approved " + item);
      this.approved = !this.approved;
      console.log(this.approved);
    }

    function deleteAllItems() {
      this.listaSpesa = [];
    }

    return {
      item,
      listaSpesa,
      addItem,
      deleteItem,
      approvedItem,
      deleteAllItems,
      err,
    };
  },
};
</script>

<style scopped>
@font-face {
  font-family: CheaseBurgher;
  src: url(../assets/fonts/CheeseBurger.otf);
}
body{background-color: #271911;}
.full-container{
  z-index: 1;
}
.fotoSpesa {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: -1;
  object-fit: cover;
  background-repeat: repeat;
}
#sfondo {
  width: 70%;
  margin: auto;
  margin-top: 20px;
  background-color: rgba(255, 255, 255, 0.91);
  padding-bottom: 50px;
}
h1 {
  font-size: 50px;
  margin-bottom: 50px;
  color: red;
  text-align: center;
  font-family: "CheaseBurgher";
  padding-top: 20px;
}
#checkbox {
  width: 30px;
  height: 30px;
}
#errore{
  color: red;
  font-style: italic;
  text-decoration: underline;
  text-align: center;
  margin: auto;
  margin-bottom: 15px;
}
#input {
  width: 25%;
  margin: auto;
  display: flex;
  justify-content: space-evenly;
  text-align: center;
  align-items: center;
  margin-bottom: 20px;
}
#input input {
  padding: 5px;
  height: 30px;
  width: 300px;
  font-size: 20px;
  border-radius: 10px;
  font-family: "CheaseBurgher";
}
button {
  border: 0;
  background-color: rgb(4, 134, 255);
  padding: 12px 20px;
  margin-left: 10px;
  border-radius: 15px;
  transition: all 0.5s ease;
  color: white;
  font-family: "CheaseBurgher";
  cursor: pointer;
}
button:hover {
  background-color: rgb(4, 71, 255);
}
#list {
  width: 40%;
  margin: auto;
  padding-top: 20px;
  padding-bottom: 50px;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  margin: auto;
  font-family: "CheaseBurgher";
  font-size: 30px;
}
#list #item {
  margin-bottom: -45px;
}
#emptyList {
  width: 60%;
  margin: auto;
  margin-top: 80px;
  text-align: center;
}
#emptyList h2 {
  font-size: 60px;
  font-family: "CheaseBurgher";
}
#emptyList h3 {
  font-size: 40px;
  font-family: "CheaseBurgher";
}
#list #item {
  width: 100%;
  display: flex;
  align-items: baseline;
  justify-content: space-between;
}
#icons {
  display: flex;
}
#icons div {
  padding-left: 20px;
}
.reset {
  font-size: 15px;
  margin-left: 50px;
  margin-top: 50px;
}

@media only screen and (max-width: 600px){
  h1{font-size: 30px}
  #errore{font-size: 12px;}
  #input input{width: 150px; height: 20px;font-size: 15px;}
  #input button{font-size: 12px;padding: 4px;border-radius: 5px;}
  #list{width: 90%;padding-bottom: 30px;font-size: 11px;}
  #item input{height: 20px; width: 20px;}
  #icons img{height: 20px;}
  button{font-size: 11px;padding: 4px;border-radius: 5px;}
  #emptyList{padding-top: 20px;}
  #emptyList h2{font-size: 25px; margin-bottom: 20px;}
  #emptyList h3{font-size: 20px;}
}
@media only screen and (max-width: 992px){
  #list{width: 70%;padding-bottom: 30px;font-size: 11px;}  
}
</style>
