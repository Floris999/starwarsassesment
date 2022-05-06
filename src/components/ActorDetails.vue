<template>
    <main>
        <div class="dark-side">
            <h1>Welcome To The Star Wars DataBase</h1>
            <p>This project is about the Star Wars API. The project is based on API practice and Front-End work in Vue.js.</p>
            <h2>See here all the Star Wars actors</h2>
        <div class="cards">
          <ul>
            <li v-for="detail in moreactordetails" :key="detail"><h3>{{detail.name}}</h3><h3>{{detail.gender}}</h3><h3>{{detail.birth}}</h3><h3>{{detail.haircolor}}</h3></li>
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
        name: "actorDetails",
        data() {
            return {
                moreactordetails: [],
                id: this.$route.params.id
            }
        },
        methods: {
            async getStarWarsActorDetails() {
                    let response = await fetch(`https://swapi.dev/api/people/this.id/`);
                    let data = await response.json();
                    //console.log(data);
                    let listActorDetails = {
                    name: data.name,
                    gender: data.gender,
                    birth: data.birth_year,
                    haircolor: hair_color
                    }
                    this.moreactordetails.push(listActorDetails);
            }
        },
        async created() {
          await this.getStarWarsActorDetails(); //call get actors details function
        }
    }
</script>

<style>
    .dark-side h1 {
  -webkit-text-stroke: 1px #FFE81F;
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
.card-item:hover {
    box-shadow: 0 4px 8px 0 #FFE81F;
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