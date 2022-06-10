<template>
  <div class="title">
    Ushbu saytda davlatlarning Covid-19 ning hozirgi holatini ko'rishingiz
    mumkin.
  </div>
  <div class="container">
    <select name="" id="" v-model="country" @change="getData">
      <option value="">Davlat tanlash</option>
      <option v-for="(list, index) in countryList" :key="index" :value="list">
        {{ list }}
      </option>
    </select>
    <div class="panel">
      <div class="asos">
        <h3>Hozirgi holat</h3>
        <h4 class="asos1">{{ cases }}</h4>
      </div>
      <div class="asos">
        <h3>Vafot etganlar</h3>
        <h4 class="asos2">{{ death }}</h4>
      </div>
      <div class="asos">
        <h3>Tuzalganlar</h3>
        <h4 class="asos3">{{ recovered }}</h4>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      country: "",
      countryList: [],
      cases: "",
      death: "",
      recovered: "",
    };
  },
  methods: {
    getCountry() {
      fetch("https://covid-193.p.rapidapi.com/countries", {
        method: "GET",
        headers: {
          "x-rapidapi-host": "covid-193.p.rapidapi.com",
          "x-rapidapi-key":
            "5ac872da61msh39ea6056a39a591p177fc4jsnc1a925e7882b",
        },
      })
        .then((response) => response.json())
        .then((data) => {
          this.countryList = data.response;
        });
    },
    getData() {
      fetch(
        "https://covid-193.p.rapidapi.com/statistics?country=" + this.country,
        {
          method: "GET",
          headers: {
            "x-rapidapi-host": "covid-193.p.rapidapi.com",
            "x-rapidapi-key":
              "5ac872da61msh39ea6056a39a591p177fc4jsnc1a925e7882b",
          },
        }
      )
        .then((response) => response.json())
        .then((data) => {
          data = data.response[0];
          this.cases = data.cases.total;
          this.death = data.deaths.total;
          this.recovered = data.cases.recovered;
        });
    },
  },
  mounted() {
    this.getCountry();
  },
};
</script>

<style lang="css">
body {
  margin: 0;
  padding: 0;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  background-image: url(http://www.wto.org/images/img_index/photos/covid19_lg.jpg);
  background-position: center;
  background-size: cover;
}
#app{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 50px;
}
.title {
  width: 50%;
  height: 76px;
  font-size: 30px;
  position: relative;
  padding: 10px;
  text-align: center;
  border: 1px solid #444444a9;
  background: rgb(255, 255, 255);
  border-radius: 20px;
  color: rgb(163, 16, 16);
}

.container {
  width: 50%;
  padding: 20px auto;
  height: 250px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-direction: column;
  box-shadow: 5px 5px 11px rgba(113, 113, 113, 15%);
  background: rgb(255, 255, 255);
  border-radius: 20px;
}
select {
  border-radius: 15px;
  margin-top: 40px;
  padding: 10px;
  border: #444444 2px solid !important;
  box-shadow: 5px 5px 11px rgba(113, 113, 113, 15%);
  width: 60%;
  height: 60px;
  font-size: 18px;
}
.panel {
  text-align: center;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}
.asos1 {
  color: orange;
}
.asos2 {
  color: red;
}
.asos3 {
  color: green;
}
@media (max-width: 400px) {
  body {
    background-image: url(https://s.w-x.co/util/image/v/1583270398102_WHAT_YOU_NEED_TO_KNOW_ABOUT_CORONAVIRUS.jpg?v=at&w=1080&h=1920);
  }

  select:focus{
    border-radius: 15px;
  }
  select {
    margin-top: 15px;
    background-color: rgba(209, 209, 255, 0.4);
    box-shadow: 5px 5px 11px rgba(34, 114, 167, 0.15);
  }
  .title {
    margin: 5px;
    margin-top: -20px;
    width: 91%;
    font-size: 25px;
    height: 90px;
  }
  .container {
    margin-top: 200px !important;
    margin: 2%;
    width: 96%;
    height: 400px;
  }
  .asos{
  border-bottom: #5e5d5d46 1px solid;
  }
  .panel {
    font-size: 15px;
    display: flex;
    flex-direction: column;
    margin-bottom: -1px;
  }
}
</style>
