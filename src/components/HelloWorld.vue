<template>
  <div class="container">
    <h1 class="title">
      Base points: {{ bp }}
    </h1>
    <h1 class="title">
      Your points: {{ points }}
    </h1>
    <h1 class="title">
      Result: {{ status }}
    </h1>
    <div class="columns">
      <div class="column mr-5">
        <h1 class="title">
          SCORE CARD 
        </h1>
        <b-table :data="data" :columns="columns"></b-table>
      </div>
      <div class="column ml-5">
        <h1 class="title">
          FILL IN THE FORM
        </h1>
        <b-field label="Total Annual Income">
            <b-input v-model="annIncome"></b-input>
        </b-field>

        <b-field label="Apartment Average Score">
            <b-input v-model="aptScore"></b-input>
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

        <b-field label="Hour Approximately Process Start">
          <b-numberinput v-model="hourStart" placeholder="15" :min="0" :max="100"></b-numberinput>
        </b-field>

        <b-field label="Education Type">
        </b-field>
        <div class="block">
          <b-radio v-model="education"
              name="name"
              native-value="Higher education">
              Higher education
          </b-radio>
          <b-radio v-model="education"
              name="name"
              native-value="Incomplete higher">
              Incomplete higher
          </b-radio>
          <b-radio v-model="education"
              name="name"
              native-value="Lower secondary">
              Lower secondary
          </b-radio>
          <b-radio v-model="education"
              name="name"
              native-value="Secondary / secondary special">
              Secondary / secondary special
          </b-radio>
          <b-radio v-model="education"
              name="name"
              native-value="Academic degree">
              Academic degree
          </b-radio>
      </div>

      <b-field label="Region Rating Client with City">
          <b-slider v-model="rating" size="is-large" :min="1" :max="3" ticks></b-slider>
      </b-field>

      </div>      
    </div>
    <b-button type="is-primary m-5" @click="calculate">Submit</b-button>
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
      console.log(this.annIncome, this.aptScore, this.idPublish, this.lastPhoneChange, this.extScore1, this.extScore2, this.extScore3, this.flagDoc3, this.hourStart, this.education, this.rating)
    }
  },  
  data() {
      return {
          bp: 513,
          points: 0,
          status: "DEFAULTER",
          annIncome: 0,
          aptScore: 0,
          idPublish: 0,
          lastPhoneChange: 0,
          extScore1: 0,
          extScore2: 0,
          extScore3: 0,
          flagDoc3: "Yes",
          hourStart: 0,
          education: "Academic degree",
          rating:2, 
          data: [
              { 'characteristic': 'AMT_INCOME_TOTAL', 'attribute': '<180000', 'scaledWBP': '-1' },
              { '-': '-', 'attribute': '180000-220000', 'scaledWBP': '2' },
              { '-': '-', 'attribute': '>220000', 'scaledWBP': '6' },

              { 'characteristic': 'APARTMENTS_AVG', 'attribute': '<0.015','scaledWBP': '-2' },
              { '-': 'APARTMENTS_AVG', 'attribute': '0.015-0.075', 'scaledWBP': '0' },
              { '-': 'APARTMENTS_AVG', 'attribute': '>0.075', 'scaledWBP': '4' },

              { 'characteristic': 'DAYS_ID_PUBLISH', 'attribute': '<800','scaledWBP': '-3' },
              { '-': 'DAYS_ID_PUBLISH', 'attribute': '800-1500', 'scaledWBP': '-1' },
              { '-': 'DAYS_ID_PUBLISH', 'attribute': '>1500', 'scaledWBP': '3' },

              { 'characteristic': 'DAYS_LAST_PHONE_CHANGE', 'attribute': '<800','scaledWBP': '-3' },
              { '-': 'DAYS_LAST_PHONE_CHANGE', 'attribute': '800-1500', 'scaledWBP': '0' },
              { '-': 'DAYS_LAST_PHONE_CHANGE', 'attribute': '>1500', 'scaledWBP': '4' },  

              { 'characteristic': 'EXT_SOURCE_1', 'attribute': '<0.14','scaledWBP': '-13' },
              { '-': 'EXT_SOURCE_1', 'attribute': '0.14-0.29', 'scaledWBP': '-1' },
              { '-': 'EXT_SOURCE_1', 'attribute': '>0.29', 'scaledWBP': '12' },      
              
              { 'characteristic': 'EXT_SOURCE_2', 'attribute': '<0.18','scaledWBP': '-16' },
              { '-': 'EXT_SOURCE_2', 'attribute': '0.18-0.38', 'scaledWBP': '-4' },
              { '-': 'EXT_SOURCE_2', 'attribute': '0.38-0.6', 'scaledWBP': '3' },
              { '-': 'EXT_SOURCE_2', 'attribute': '>0.6', 'scaledWBP': '15' },       

              { 'characteristic': 'EXT_SOURCE_3', 'attribute': '<0.14','scaledWBP': '-29' },
              { '-': 'EXT_SOURCE_3', 'attribute': '0.14-0.24', 'scaledWBP': '-16' },
              { '-': 'EXT_SOURCE_3', 'attribute': '0.24-0.48', 'scaledWBP': '3' },
              { '-': 'EXT_SOURCE_3', 'attribute': '>0.48', 'scaledWBP': '21' }, 
              
              { 'characteristic': 'FLAG_DOCUMENT_3', 'attribute': '0','scaledWBP': '6' },
              { '-': 'FLAG_DOCUMENT_3', 'attribute': '1', 'scaledWBP': '-3' },

              { 'characteristic': 'HOUR_APPR_PROCESS_START', 'attribute': '<9','scaledWBP': '-6' },
              { '-': 'HOUR_APPR_PROCESS_START', 'attribute': '9-13', 'scaledWBP': '-2' },
              { '-': 'HOUR_APPR_PROCESS_START', 'attribute': '>13', 'scaledWBP': '3' },

              { 'characteristic': 'NAME_EDUCATION_TYPE', 'attribute': '<2','scaledWBP': '-12' },
              { '-': 'NAME_EDUCATION_TYPE', 'attribute': '2-3', 'scaledWBP': '-5' },
              { '-': 'NAME_EDUCATION_TYPE', 'attribute': '>3', 'scaledWBP': '10' },

              { 'characteristic': 'REGION_RATING_CLIENT_W_CITY', 'attribute': '<2','scaledWBP': '2' },
              { '-': 'REGION_RATING_CLIENT_W_CITY', 'attribute': '2-3', 'scaledWBP': '0' },
              { '-': 'REGION_RATING_CLIENT_W_CITY', 'attribute': '>3', 'scaledWBP': '-2' },
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
