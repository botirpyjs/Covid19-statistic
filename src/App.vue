<template>
  <div class="title">
    Ushbu saytda davlatlarning Covid-19 ning hozirgi holatini ko'rishingiz
    mumkin.
  </div>
  <div class="container">
    <select name="" id="" v-model="country" @change="getData">
      <option value="">Select</option>
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

<style lang="sass">
body
  background-image: url("./assets/img.jpg")
  background-position: center
  background-size: cover
  background-attachment: fixed
  font-family: monospace
  #app
    display: flex
    overflow: hidden
    flex-direction: column
    align-items: center
    justify-content: center
    text-align: center
    width: 100%
    .title
      display: flex
      align-items: center
      justify-content: center
      background-color: #ffffffdd
      border-radius: 10px
      font-size: 25px
      font-family: monospace
      font-weight: 600
      color: #BF0000
      padding: 30px
      margin: 40px
      width: 60%
      height: 60px
      box-shadow: 0px 0px 5px 10px #ffffffdd
    .container
      border-radius: 10px
      margin: 40px
      padding: 30px
      padding-bottom: 0
      background-color: #ffffffdd
      width: 60%
      height: auto
      border: none
      box-shadow: 1px 1px 5px 10px #ffffffdd
      select
        outline: none
        padding: 15px 20px
        font-size: 20px
        font-weight: 500
        font-family: monospace
        letter-spacing: 2px
        width: auto
        border: none
        box-shadow: 0px 0px 15px 10px #ff0000ac
        background: #BF0000
        color: #fff
        border-radius: 10px
        option
          font-family: monospace
          background-color: #FF00
          border-radius: 10px
          transition: .5s ease all
      .panel
        width: 100%
        padding: 10px
        height: 180px
        display: flex
        align-items: end
        justify-content: space-around
      .asos
        padding: 10px
        font-size: 22px
        .asos1
          margin: 10px 0
          font-size: 25px
          color: green
        .asos2
          margin: 10px 0
          font-size: 25px
          color: red
        .asos3
          margin: 10px 0
          font-size: 25px
          color: blue
@media only screen and (max-width: 1024px ) 
  body
    overflow: hidden
    #app
      .title
        font-size: 23px
        height: 50px
        margin-bottom: 20px
      .container
        padding-bottom: 0
        select
          outline: none
          font-size: 18px
        .panel
          .asos
            font-size: 18px
            .asos1,
            .asos2,
            .asos3
              font-size: 20px
@media only screen and (max-width: 768px ) 
  body
    overflow: hidden
    #app
      .title
        font-size: 20px
        height: 30px
        margin-bottom: 10px
      .container
        width: 70%
        padding-bottom: 0
        select
          outline: none
          font-size: 15px
        .panel
          justify-content: space-between
          width: 100%
          .asos
            font-weight: 700
            font-size: 15px
            .asos1,
            .asos2,
            .asos3
              font-size: 18px
@media only screen and (max-width: 425px ) 
  body
    background-position: top
    background-image: url("./assets/img_mobile.jpg")
    overflow: hidden
    #app
      .title
        width: 60%
        font-size: 16px
        height: 50px
        margin-bottom: 5px
      .container
        padding-bottom: 50px
        select
          outline: none
          font-size: 14px
        .panel
          height: 350px
          align-items: center
          flex-direction: column
          margin-bottom: 10px
          .asos
            border-bottom: 1px solid rgb(0 0 0 / 29%)
            width: 100%
            height: 50px
            margin: 0 100px
            padding: 40px 0
            font-size: 16px
            .asos1,
            .asos2,
            .asos3
              height: 60px
              font-size: 25px

@media only screen and (max-width: 375px )
  body
    overflow: scroll
    #app
      .container
        height: 500px
        padding-left: 10px
        padding-top: 8px
        padding-bottom: 0
@media only screen and (max-width: 360px )
  body
    overflow: hidden
    #app
      .container
        width: 80%
        height: 500px
        padding-top: 8px
        padding-bottom: 0
        select
          margin: 0 12px
@media only screen and (max-width: 320px ) 
  body
    background-position: top
    background-image: url("./assets/img_mobile.jpg")
    overflow: hidden
    #app
      .title
        width: 70%
        font-size: 16px
        height: 50px
        margin-bottom: 5px

      .container
        margin: 30px
        padding-left: 20px
        padding-bottom: 50px
        select
          outline: none
          font-size: 10px
          box-shadow: 0px 0px 8px 5px #ff0000ac

        .panel
          height: 350px
          align-items: center
          flex-direction: column
          margin-bottom: 10px
          .asos
            border-bottom: 1px solid rgb(0 0 0 / 29%)
            width: 100%
            height: 50px
            margin: 0 80px
            margin-left: 70px
            padding: 40px 0
            font-size: 16px
            .asos1,
            .asos2,
            .asos3
              height: 60px
              font-size: 25px
</style>
