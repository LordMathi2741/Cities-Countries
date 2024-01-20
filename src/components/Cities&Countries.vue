<template>
  <div>
    <h1>Cities & Countries</h1>
    <h2>Welcome {{ user }}</h2>
    <input type="text" placeholder="Type city" v-model="city">
    <h1> {{ country }}</h1>
    <p>Dont forget to use Capital Letters!!</p>
    <footer> LordMathi2741 copyright all reserved</footer>

  </div>
</template>

<script>
export default {
  data() {
    return {
      user: null,
      country: null,
      city: null,
      citiesData:[]

    };
  },
  methods: {
    async generateUser() {
      const { first_name }= await fetch('https://random-data-api.com/api/v2/users').then(r => r.json());
      this.user = first_name
    },
    async generateCity(){
      const {data} = await fetch('https://countriesnow.space/api/v0.1/countries/population/cities').then(r => r.json());
      this.citiesData = data
      console.log(data)
    }
  },
  watch:{
      city(value, oldvalue){
        const cityInfo = this.citiesData.find(cityData => cityData.city === value);
      if (cityInfo) {
        this.country = cityInfo.country;
      } else {
        this.country = "País no encontrado";
      }
      }
  },
  //metodo del ciclo de vida de vue 
  created() {
    this.generateUser()
    this.generateCity()
  }
};
</script>

<style>

*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

h1, h2, p, footer{
  color:#fff;
}

footer{
  margin-block-start: 15%;
}
body{
    padding: 0px;
    margin: 0px;
    border:none;
    width: 100%;
    overflow: hidden;
}


input {
    border-radius: 5px;
    margin: 10px 0;
    background: #fff;
    border: 1px solid #ccc;
    color: #777;
    max-width: 100%;
    min-width: 30%;
    outline: none;
    padding: 7px 8px;
    font-size: 20px;
    text-align: center;

  }
</style>