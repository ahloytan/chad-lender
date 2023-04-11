<template>
  <div class="container">
    <h1 class="title">
      Cut-off points: {{ cutoffScore }}
    </h1>
    <h1 class="title">
      Your total points: {{ points }}
    </h1>
    <h1 class="title">
      <p>Result:</p> 
      <p id="status" style="font-size: 50px; margin-top: 20px;"> {{ status }} </p>
      &nbsp;
    </h1>
    <div class="columns">
      <div class="column mr-5">
        <h1 class="title">
          SCORE CARD 
        </h1>
        <b-table :bordered="isBordered" :data="data" :columns="columns"></b-table>
      </div>
      <div class="column ml-5">
        <h1 class="title">
          FILL IN THE FORM
        </h1>
        <b-field label="Total Annual Income">
            <b-input v-model="annIncome"></b-input>
        </b-field>

        <b-field label="Apartment Average Score">
            <b-numberinput 
              v-model="aptScore"
              :placeholder="0.015"
              :min="0" 
              :max="1"
              step="0.01"
              aria-minus-label="Decrement by 0.01"
              aria-plus-label="Increment by 0.01">
          </b-numberinput>
        </b-field>

        <b-field label="Days ID Publish">
          <b-numberinput v-model="idPublish"></b-numberinput>
        </b-field>

        <b-field label="Days Last Phone Change">
          <b-numberinput v-model="lastPhoneChange"></b-numberinput>
        </b-field>

        <b-field label="External Source 1 Score">
          <b-numberinput 
              v-model="extScore1"
              :placeholder="0.5"
              :min="0" 
              :max="1"
              step="0.01"
              aria-minus-label="Decrement by 0.01"
              aria-plus-label="Increment by 0.01">
          </b-numberinput>
        </b-field>

        <b-field label="External Source 2 Score">
          <b-numberinput 
              v-model="extScore2"
              :placeholder="0.5"
              :min="0" 
              :max="1"
              step="0.01"
              aria-minus-label="Decrement by 0.01"
              aria-plus-label="Increment by 0.01">
          </b-numberinput>
        </b-field>

        <b-field label="External Source 3 Score">
          <b-numberinput 
              v-model="extScore3"
              :placeholder="0.5"
              :max="1"
              :min="0" 
              step="0.01"
              aria-minus-label="Decrement by 0.01"
              aria-plus-label="Increment by 0.01">
          </b-numberinput>
        </b-field>

        <b-field label="Flag Document 3">
        </b-field>
        <b-field>
          <b-checkbox v-model="flagDoc3"
              true-value="Yes"
              false-value="No">
              {{ flagDoc3 }}
          </b-checkbox>
        </b-field>

        <b-field label="Education Type">
        </b-field>
        <div class="block">
          <b-radio v-model="education"
              name="name"
              native-value=1>
              Lower secondary
          </b-radio>
          <b-radio v-model="education"
              name="name"
              native-value=2>
              Secondary / secondary special
          </b-radio>
          <b-radio v-model="education"
              name="name"
              native-value=3>
              Incomplete higher
          </b-radio>
          <b-radio v-model="education"
              name="name"
              native-value=4>
              Higher education
          </b-radio>
          <b-radio v-model="education"
              name="name"
              native-value=5>
              Academic degree
          </b-radio>
      </div>

      <b-field label="Region Rating Client with City">
          <b-slider v-model="rating" size="is-large" :min="1" :max="3" ticks></b-slider>
      </b-field>
      <b-button type="is-primary m-5" size="is-large" @click="calculate">Submit</b-button>
      </div>      
    </div>
  </div>
  
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods:{
    calculate(){
      this.points = 487
      // console.log(this.annIncome, this.aptScore, this.idPublish, this.lastPhoneChange, this.extScore1, this.extScore2, this.extScore3, this.flagDoc3, this.hourStart, this.education, this.rating)

      if (this.annIncome < 180000){
        this.points += this.data[0]['scaledWBP'];
      } else if (this.annIncome >= 180000 && this.annIncome < 220000){
        this.points += this.data[1]['scaledWBP'];
      } else {
        this.points += this.data[2]['scaledWBP'];
      }

      if (this.aptScore < 0.015){
        this.points += this.data[3]['scaledWBP'];
      } else if (this.aptScore >= 0.015 && this.aptScore < 0.075){
        this.points += this.data[4]['scaledWBP'];
      } else {
        this.points += this.data[5]['scaledWBP'];
      }

      if (this.idPublish < 800){
        this.points += this.data[6]['scaledWBP'];
      } else if (this.idPublish >= 800 && this.idPublish < 1500){
        this.points += this.data[7]['scaledWBP'];
      } else {
        this.points += this.data[8]['scaledWBP'];
      }

      if (this.lastPhoneChange < 50){
        this.points += this.data[9]['scaledWBP'];
      } else if (this.lastPhoneChange >= 50 && this.lastPhoneChange < 1150){
        this.points += this.data[10]['scaledWBP'];
      } else {
        this.points += this.data[11]['scaledWBP'];
      }

      if (this.extScore1 < 0.14){
        this.points += this.data[12]['scaledWBP'];
      } else if (this.extScore1 >= 0.14 && this.extScore1 < 0.28){
        this.points += this.data[13]['scaledWBP'];
      } else {
        this.points += this.data[14]['scaledWBP'];
      }

      if (this.extScore2 < 0.18){
        this.points += this.data[15]['scaledWBP'];
      } else if (this.extScore2 >= 0.18 && this.extScore2 < 0.38){
        this.points += this.data[16]['scaledWBP'];
      } else if (this.extScore2 >= 0.38 && this.extScore2 < 0.6){
        this.points += this.data[17]['scaledWBP'];
      } else {
        this.points += this.data[18]['scaledWBP'];
      }

      if (this.extScore3 < 0.14){
        this.points += this.data[19]['scaledWBP'];
      } else if (this.extScore3 >= 0.14 && this.extScore3 < 0.24){
        this.points += this.data[20]['scaledWBP'];
      } else if (this.extScore3 >= 0.24 && this.extScore3 < 0.48) {
        this.points += this.data[21]['scaledWBP'];
      } else {
        this.points += this.data[22]['scaledWBP'];
      }

      if (this.flagDoc3 == "No"){
        this.points += this.data[23]['scaledWBP'];
      } else {
        this.points += this.data[24]['scaledWBP'];
      }

      if (this.education < 2){
        this.points += this.data[25]['scaledWBP'];
      } else if (this.education >= 2 && this.education < 3){
        this.points += this.data[26]['scaledWBP'];
      } else {
        this.points += this.data[27]['scaledWBP'];
      }

      if (this.rating < 2){
        this.points += this.data[30]['scaledWBP'];
      } else if (this.rating >= 2 && this.rating < 3){
        this.points += this.data[31]['scaledWBP'];
      } else {
        this.points += this.data[32]['scaledWBP'];
      }

      //final
      let statusClass = document.getElementById('status');
      statusClass.className = '';
      this.status = this.points >= this.cutoffScore ? "LIKELY NON-DEFAULTER" : "LIKELY DEFAULTER";
      this.points >= this.cutoffScore ? statusClass.classList.add('has-text-success') : statusClass.classList.add('has-text-danger');

      window.scrollTo(0, 0);
    }
  },  
  data() {
      return {
          cutoffScore: 520, 
          points: 487,
          status: "",
          annIncome: 1234560,
          aptScore: 0.015,
          idPublish: 0,
          lastPhoneChange: 0,
          extScore1: 0.5,
          extScore2: 0.5,
          extScore3: 0.5,
          flagDoc3: "Yes",
          education: 1,
          rating: 2, 
          isBordered: true,
          data: [
              { 'characteristic': 'AMT_INCOME_TOTAL', 'attribute': '<180000', 'scaledWBP': -2 },
              { '-': '-', 'attribute': '180000 - 220000', 'scaledWBP': 2 },
              { '-': '-', 'attribute': '>220000', 'scaledWBP': 6 },

              { 'characteristic': 'APARTMENTS_AVG', 'attribute': '<0.015','scaledWBP': -2 },
              { '-': 'APARTMENTS_AVG', 'attribute': '0.015 - 0.075', 'scaledWBP': 0 },
              { '-': 'APARTMENTS_AVG', 'attribute': '>0.075', 'scaledWBP': 4 },

              { 'characteristic': 'DAYS_ID_PUBLISH', 'attribute': '<800','scaledWBP': -4 },
              { '-': 'DAYS_ID_PUBLISH', 'attribute': '800 - 1500', 'scaledWBP': -1 },
              { '-': 'DAYS_ID_PUBLISH', 'attribute': '>1500', 'scaledWBP': 3 },

              { 'characteristic': 'DAYS_LAST_PHONE_CHANGE', 'attribute': '<50','scaledWBP': -3 },
              { '-': 'DAYS_LAST_PHONE_CHANGE', 'attribute': '50 - 1150', 'scaledWBP': 0 },
              { '-': 'DAYS_LAST_PHONE_CHANGE', 'attribute': '>1150', 'scaledWBP': 4 },  

              { 'characteristic': 'EXT_SOURCE_1', 'attribute': '<0.14','scaledWBP': -12 },
              { '-': 'EXT_SOURCE_1', 'attribute': '0.14-0.29', 'scaledWBP': -1 },
              { '-': 'EXT_SOURCE_1', 'attribute': '>0.29', 'scaledWBP': 10 },      
              
              { 'characteristic': 'EXT_SOURCE_2', 'attribute': '<0.18','scaledWBP': -17 },
              { '-': 'EXT_SOURCE_2', 'attribute': '0.18-0.38', 'scaledWBP': -4 },
              { '-': 'EXT_SOURCE_2', 'attribute': '0.38-0.6', 'scaledWBP': 4 },
              { '-': 'EXT_SOURCE_2', 'attribute': '>0.6', 'scaledWBP': 16 },       

              { 'characteristic': 'EXT_SOURCE_3', 'attribute': '<0.14','scaledWBP': -28 },
              { '-': 'EXT_SOURCE_3', 'attribute': '0.14-0.24', 'scaledWBP': -15 },
              { '-': 'EXT_SOURCE_3', 'attribute': '0.24-0.48', 'scaledWBP': 3 },
              { '-': 'EXT_SOURCE_3', 'attribute': '>0.48', 'scaledWBP': 21 }, 
              
              { 'characteristic': 'FLAG_DOCUMENT_3', 'attribute': 'Not Provided','scaledWBP': 5 },
              { '-': 'FLAG_DOCUMENT_3', 'attribute': 'Provided', 'scaledWBP': -3 },
            
              { 'characteristic': 'NAME_EDUCATION_TYPE', 'attribute': 'Lower secondary','scaledWBP': -15 },
              { '-': 'NAME_EDUCATION_TYPE', 'attribute': 'Secondary / secondary special', 'scaledWBP': -6 },
              { '-': 'NAME_EDUCATION_TYPE', 'attribute': 'Incomplete higher', 'scaledWBP': 12 },
              { '-': 'NAME_EDUCATION_TYPE', 'attribute': 'Higher education', 'scaledWBP': 12 },
              { '-': 'NAME_EDUCATION_TYPE', 'attribute': 'Academic degree', 'scaledWBP': 12 },             

              { 'characteristic': 'REGION_RATING_CLIENT_W_CITY', 'attribute': '1','scaledWBP': 4 },
              { '-': 'REGION_RATING_CLIENT_W_CITY', 'attribute': '2', 'scaledWBP': 0 },
              { '-': 'REGION_RATING_CLIENT_W_CITY', 'attribute': '3', 'scaledWBP': -4 },
          ],
          columns: [
              {
                  field: 'characteristic',
                  label: 'Characteristic',
                  centered: true
              },
              {
                  field: 'attribute',
                  label: 'Attribute',
                  centered: true
              },
              {
                  field: 'scaledWBP',
                  label: 'Scaled w/ BP',
                  centered: true
              }
          ]
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
</style>
