<template>
  <div class="home">

    <div id="leftside">

      <h4>FilterBy:</h4>

      <div>
        <input type="checkbox" value="Non Alcoholic" v-model="checked" @click="analcolico" id="nonAlcholic" name="nonAlcholic">
        <label for="nonAlcholic">Non Alcholic</label>
      </div>

      <div>
        <input type="checkbox" @click="alcolici" v-model="checkedAl" id="Alcholic" name="Alcholic">
        <label for="Alcholic">Alcholic</label>
      </div>
    </div>

    <input id="find" type="text" v-model="drink" placeholder="search for a drink?"  name="" value="" @keyup.enter="filtra()">


    <button id="submit" type="button" name="button" @click="filtra()">submit</button>

    <div v-if="single == false" class="list">
      <div v-for="(item, ind) in texto" v-bind:key="item.id" class="cocktails card" @click="show(item.strDrink,ind)">
        <p>{{item.strDrink}}</p>
        <img class="smallphoto" :src="item.strDrinkThumb" alt="">
      </div>

    </div>

    <div class="mono" v-else>

      <div  class="card m-4 p-4 ">

        <img class="headimg" :src="info.strDrinkThumb" alt="Placeholder image">

        <div id="sizing" class="card-content">

          <p class="title is-2">{{info.strDrink}}</p>

          <div class="content">
            <h4>Ingredients:</h4>
            <ul v-for="ingr in {info}" v-bind:key="ingr.id">
              <li v-if="ingr.strIngredient1 != null">{{ingr.strIngredient1}}</li>
              <li v-if="ingr.strIngredient2 != null">{{ingr.strIngredient2}}</li>
              <li v-if="ingr.strIngredient3 != null">{{ingr.strIngredient3}}</li>
              <li v-if="ingr.strIngredient4 != null">{{ingr.strIngredient4}}</li>
              <li v-if="ingr.strIngredient5 != null">{{ingr.strIngredient5}}</li>
              <li v-if="ingr.strIngredient6 != null">{{ingr.strIngredient6}}</li>
              <li v-if="ingr.strIngredient7 != null">{{ingr.strIngredient7}}</li>
              <li v-if="ingr.strIngredient8 != null">{{ingr.strIngredient8}}</li>
              <li v-if="ingr.strIngredient9 != null">{{ingr.strIngredient9}}</li>
              <li v-if="ingr.strIngredient10 != null">{{ingr.strIngredient10}}</li>
              <li v-if="ingr.strIngredient11 != null">{{ingr.strIngredient11}}</li>
              <li v-if="ingr.strIngredient12 != null">{{ingr.strIngredient12}}</li>
              <li v-if="ingr.strIngredient13 != null">{{ingr.strIngredient13}}</li>
              <li v-if="ingr.strIngredient14 != null">{{ingr.strIngredient14}}</li>
              <li v-if="ingr.strIngredient15 != null">{{ingr.strIngredient15}}</li>

            </ul>

            <p id="instruction"><strong>Instruction</strong>: {{info.strInstructions}}</p>
          </div>
        </div>
      </div>

    </div>

    <!-- <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" /> -->
  </div>
</template>

<style media="screen">
  .home{
    color: white;
  }

  #leftside{
    display: flex;
    flex-direction: column;
    align-items: baseline;
    color: black;
    background: rgba(255,255,255, 0.85);
    float: left;
    top: 200px;
    position: fixed;
    padding: 20px 30px 40px 15px;
    margin-left: 15px;
    border-radius: 15px;
  }

  #leftside h4{
    align-self:center;
    margin-bottom:15px;
    font-size:20px;
    font-weight: bold;
  }

  #nonAlcholic,
  #Alcholic{
    margin-right:10px;;
  }

  .smallphoto{
    width: 150px;
    height: 150px;
    margin: 10px;
  }

  .list{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    max-width: 80%;
    margin-left: 15%;
  }

  .cocktails{
    border: 1px solid;
    margin: 15px;
  }

  .cocktails p{
    max-width: 170px;
  }

  .mono{
    width:100%;
    display: flex;
    justify-content: center;
  }

  ul{
    text-align:initial;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items:center;
  }

  li{
    width:150px;
  }

  .headimg{

    height: 300px;
  }

  .mono {
    /* transition: all 5s ease; */
    animation: fadeInFromNone 1.5s ease;
  }

  @keyframes fadeInFromNone {
    0% {
        transform: translateY(500px) scale(0);
        opacity: 0;
    }

    100% {
      transform: translateY(0px)  scale(1);
        opacity: 1;
    }
  }

  input{
    border:none;
  }

  #find{
    border-radius:50px;
    border:none;
    padding: 8px 25px;
    font-size: 15px;
    text-align: initial;
  }

  #submit{
    width: 80px;
    border-radius:50px;
    border:none;
    padding: 8px;
    margin: 15px;
  }

  #sizing{
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    width: 500px;
  }

</style>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import axios from 'axios';
export default {
  name: "Home",
  components: {
    // HelloWorld,
  },
  data(){
    return{
      texto:'',
      drink : '',
      info : '',
      single: false,
      checked: false,
      checkedAl:false,
      filtered:[],
      checkboxitem: []
    }
  },
  methods:{
    filtra(){
      axios.get('https://www.thecocktaildb.com/api/json/v1/1/search.php?s=' + this.drink)
        .then(response => (this.texto = response.data.drinks));
        this.drink='';
        this.single = false;
        this.checkboxitem = this.texto;
        return this.texto
    },
    show(item){
      axios.get('https://www.thecocktaildb.com/api/json/v1/1/search.php?s=' + item)
        .then(response => {
          this.info = response.data.drinks[0];
          // console.log(response.data.drinks[0]);
        });
        this.single = true;

    },
    analcolico() {

      // console.log(this.checked,this.texto);
      if (this.checked == false) {
        for (var i = 0; i < this.texto.length; i++) {
          if (this.texto[i].strAlcoholic !== "Alcoholic") {
            this.filtered.push(this.texto[i]);

            // this.texto = this.texto[i];
          }
        }
        this.checked= true;
        this.texto = this.filtered;
        // console.log(this.filtered,this.checked);
      } else {
        this.checked= false;
        this.filtered = [];
        this.filtra();
        // console.log(this.filtered,this.checked,this.filtra());
      }
      /////////////////// METODO PER CHIAMATA AJAX CON TUTTI NON ALCOLICI ////////////////////
      // if (this.checked == true) {
      //   this.texto = null;
      //   this.checked = false;
      //   console.log(this.checked,this.texto)
      // } else{
      //   axios.get('https://www.thecocktaildb.com/api/json/v1/1/filter.php?a=Non_Alcoholic')
      //     .then(response => {
      //         this.texto = response.data.drinks;
      //         this.checked = true;
      //         console.log(this.checked,this.texto)
      //       });
      // }

  },

  alcolici() {
    if (this.checkedAl == false) {
      for (var i = 0; i < this.texto.length; i++) {
        if (this.texto[i].strAlcoholic == "Alcoholic") {
          this.filtered.push(this.texto[i]);
          // console.log(this.filtered);
          // this.texto = this.texto[i];
        }
      }
      this.checkedAl= true;
      return this.texto = this.filtered
    } else {
      this.checkedAl= false;
      this.filtered = [];
      this.filtra();
    }
    /////////////////// METODO PER CHIAMATA AJAX CON TUTTI ALCOLICI ////////////////////
    // if (this.checkedAl == true) {
    //   this.texto = null;
    //   this.checkedAl = false;
    // } else{
    //   axios.get('https://www.thecocktaildb.com/api/json/v1/1/filter.php?a=Alcoholic')
    //       .then(response => {
    //           this.texto = response.data.drinks;
    //           // console.log(response.data.drinks);
    //           this.checkedAl = true;
    //         });
    //
    // }

  },

}
  // computed: {
    // searchResults() {
    //     // If searchText property is empty, then return a empty string
    //     if (this.drink.length === 0) return '';
    //     // return only books with titles that match with
    //     // the searchText string
    //     return this.texto.filter(text => text.strDrink.toLowerCase().match(this.drink))
    //   }
  // },
  // mounted(){
  //   axios.get('https://www.thecocktaildb.com/api/json/v1/1/filter.php?a=Non_Alcoholic&a=Alcoholic')
  //     .then(response => {this.texto = response.data.drinks;
  //       console.log(response)
  //     });
  // }

};
</script>
