<template>
    <main>
        <div class="dark-side">
            <h1>Welcome To The Star Wars DataBase</h1>
            <p>This project is about the Star Wars API. The project is based on API practice and Front-End work in Vue.js.</p>
            <h2>See here all the Star Wars actors</h2>
        <div class="cards">
          <ul>
            <li v-for="actor in actorname" :key="actor"><h3>{{actor.name}}</h3><button><router-link v-bind:to="/actors/ + actor.url">See Details</router-link></button></li>
          </ul>
        </div>
        </div>
        <div class="right-side">
            <!--<img src="https://www.wupply.nl/wp-content/uploads/2022/03/StarWars.png" class="banner" alt="Star Wars"/>-->
        </div>
    </main>
    
</template>

<script>
    export default {
        name: "MainArea",
        data() {
            return {
            actorname: [],
            characterid: [],
            moreactordetails: [],
            }
        },
        methods: {
          async  getStarWarsActor() {
            for(this.id = 1; this.id < 10; this.id++) { //begin loop
              let response = await fetch(`https://swapi.dev/api/people/${this.id}`);
              let data = await response.json();
              //console.log(data);
              let listDetails = {
                name: data.name,
                url: data.url.split("/").at(-2)
              }
              this.actorname.push(listDetails);
            } //end loop
          },
        },
        async created() {
          await this.getStarWarsActor(); //call get actors details function
        },
    }
</script>

<style>
.dark-side h1 {
  -webkit-text-stroke: 1px #FFE81F;
}

ul {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}

main {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  margin: 0px;
  padding: 0px;
  height: 100vh;
}
main > * {
  flex: 1;
}
.dark-side {
  background-color: #000000;
  padding: 5px 20px;
}
.dark-side li {
  color: white;
}
.dark-side p {
  color: white;
}
.right-side {
    background-image: url("/src/assets/star-wars-landscape.jpeg");
    background-size: cover;
    background-repeat: no-repeat;
    background-position: top center;
}
.right-side:hover {
    box-shadow: inset 0 0 10px #FFFFFF;
}
.banner {
  min-width: 100%;
  min-height: 100%;
}
.cards {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  gap: 40px;
  margin: 50px 0px;
  
}
.cards > * {
  flex: 1;
}
.card-item {
  border-radius: 10px;
  box-shadow: 0 4px 8px 0 rgba(255, 255, 255, 0.199);
  padding: 40px 80px;
}

button {
  background-color: white;
  border: none;
  border-radius: 5px;
  padding: 4px 6px;
  text-align: center;
  font-size: 16px;
  font-weight: 400;
  cursor: pointer;
}

@media only screen and (max-width: 1180px) {
  main {
      flex-direction: column;
      width: auto;
  }
  .right-side {
    display: none;
  }
  .dark-side {
    padding: 60px;
  }
  .cards {
    flex-direction: column;
    width: auto;
  }
  .card-item {
    padding: 40px 20px;
  }
}
</style>