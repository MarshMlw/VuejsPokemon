<template>

<div>
<!--
  <h1 id='idh1'>Hello Pokémon</h1>
  <button v-on:click="clicked">click</button>
  <button v-on:click="hide">hide</button>
  <button v-on:click="show">show</button><br>
  -->


  <img id='img' src='https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/International_Pok%C3%A9mon_logo.svg/2560px-International_Pok%C3%A9mon_logo.svg.png'><br>
  <button v-on:click="hideimg">hide image</button>
  <button v-on:click="showimg">show image</button><br>


 <input v-model="pokemon" type="text" name="pokemon" id="pokemon" placeholder="Entrer le numéro de votre pokémon ici !"><br>
    <p><strong>Nom du pokémon : </strong>{{ this.name }}</p>
    <p><strong>Type(s) du pokémon : </strong>{{ this.types }}</p>
      <img class="frontdefault" :src="image">

</div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      info: null,
      name: null,
      types: null,
      image: null,
      pokemon:'',
    } 
  },

methods: {
  clicked: function () {
    console.log('click')
  },
  hide: function() {
    console.log('hide')
    document.getElementById('idh1').style.display ='none';
  },
  show: function () {
    console.log('show')
    document.getElementById('idh1').style.display ='block';
  },
    hideimg: function() {
    document.getElementById('img').style.display ='none';
  },
    showimg: function () {
    document.getElementById('img').style.display ='block';
  },
    create: function () {
    var txt = 'test'
    var h = document.createElement('p');
    var t = document.createTextNode(txt);
    h.appendChild(t);
    var currentDiv = document.getElementById('create');
    currentDiv.appendChild(h)
  },
  findPokemon: function () {
    console.log(this.value);
  },
},
watch:{
  pokemon: function (val){
    console.log(val);
    let pokemon=val;
    axios
      .get('https://pokeapi.co/api/v2/pokemon/'+val)
      .then(response => {
        this.name = response.data.name;
        this.types = response.data.types;
        this.image = response.data.sprites.front_default;
        console.log(this.image);
        var typesString=[];
        for (const key in this.types) {
          if (Object.hasOwnProperty.call(this.types, key)) {
            const element = this.types[key];
            console.log(element.type.name);
            typesString.push(element.type.name);
          }
        }
        console.log(typesString);
        let mypokemontypes=typesString.join(', ');
        this.types = typesString.join(', ');
      })
      .catch(response => (console.log ('erreur')))
  }
},
 mounted () {
   
  }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
button {
  margin : 10px;
  width: 10%;
  padding:10px;
  border-radius: 50px;
  background-color: #17285e;
  color:#FFF;
  border-width: none;
  border-style: none;
  font-weight: bold;
  text-transform: uppercase;
}
button:hover {
  background-color:#f9cc33;
}
img {
  margin: 0 auto;
  width : 30%;
}
.frontdefault {
  width : 20%;
}
#pokemon {
  border-radius: 20px;
  padding: 10px;
  width:20%;
  margin-top:10px;
}
</style>