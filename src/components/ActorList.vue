<template>
    <main>
        <div class="dark-side">
            <h1>Welcome To The Star Wars DataBase</h1>
            <p>This project is about the Star Wars API. The project is based on API practice and Front-End work in Vue.js.</p>
            <h2>You have chosen for</h2>
        <div class="cards">
          <ul>
            <li v-for="detail in moreactordetails" :key="detail"><h3>Name: {{detail.name}}</h3><h3>Gender: {{detail.gender}}</h3><h3>Height: {{detail.height}}</h3><h3>Birth Year: {{detail.birth}}</h3><h3>Hair Color: {{detail.hair}}</h3></li>
            <li v-for="film in filmdetails" :key="film"><h3>Movie:</h3><p>{{film.title}}</p><h3>Release date:</h3><p>{{film.release}}</p><h3>Info:</h3><p>{{film.intro}}</p></li>
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
        name: "actorList",
        components: {
        },
        data() {
            return {
                moreactordetails: [],
                id: this.$route.params.id, /*https://router.vuejs.org/guide/essentials/dynamic-matching.html#reacting-to-params-changes*/
                filmdetails: []
            }
        },
        methods: { //Get actor details
            async getStarWarsActorDetails() {
                    let response = await fetch(`https://swapi.dev/api/people/` + this.id);
                    let data = await response.json();
                    let listActorDetails = {
                    name: data.name,
                    gender: data.gender,
                    height: data.height,
                    birth: data.birth_year,
                    hair: data.hair_color,
                    films: data.films
                    }
                    this.moreactordetails.push(listActorDetails);
            },
            async getStarWarsFilmsDetails() { //Get film details of actor
              await this.moreactordetails.map(async detail => {
                detail.films.map(async url => {
                  let response = await fetch(url);
                  let data = await response.json();
                  let filmlist = {
                    title: data.title,
                    intro: data.opening_crawl,
                    release: data.release_date,
                  }
                  this.filmdetails.push(filmlist);
                })
              })
            }
        },
        async created() {
          await this.getStarWarsActorDetails(); //call get actors details function
          await this.getStarWarsFilmsDetails(); // call get film details of chosen actor function
        },
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