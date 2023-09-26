<script setup>
import {ref} from 'vue'
import WelcomeItem from './WelcomeItem.vue'

const step = ref(1);


</script>

<script>
  export default {
    data: () => ({
      dataForm: {
        email:'',
        firstName:'',
        lastName:'',
        type:'test',
        password:'',
        cpassword:'',
        company:'',
        address:'',
        city:'',
        state:'',
        zip:'',
        country:'',
        userType:'Admin',
      },
      countryList: ''
    }),
    mounted() {
      this.getCountry();
    },
    computed: {
      samePassword() {
        return this.dataForm.password === this.dataForm.cpassword ? true : false
      }
    },
    methods: {
      submitData() {
        //console.log(this.dataForm)
        fetch('https://renting-api.onrender.com/users/register', {
          method: 'POST',
          body: JSON.stringify(this.dataForm),
          headers: {
            'Content-type': 'application/json; charset=UTF-8',
            'Authorization': 'Bearer 6nv9i5abfaipo2yks0vku611ut9y7x',
          }
        })
        .then(response => Promise.all([response, response.json()]))
        .then(([response, json]) => {
            //console.log('response', response);
            if (!response.ok || !response.status === 201) { 
                throw Error(`Respsonse status ${response.status} (${response.statusText}): ${json.message}`);
            }
            console.log(json);
            alert("Saved Successfully!");
        })
        .catch(exception => {
            console.log(new Map([
                [TypeError, "There was a problem fetching the response."],
                [SyntaxError, "There was a problem parsing the response."],
                [Error, exception.message]
            ]).get(exception.constructor()));
        });
      },
      async getCountry() {
        const a = await fetch(`https://restcountries.com/v3.1/all`);
        const d = await a.json();
        this.countryList = d.map((d) => { return d.name.common }).sort()
      }
    },
  }
</script>

<template>
  <div class="stepone" v-show="step==1">
    <WelcomeItem>
      <template #heading>Email</template>
      
      <input type="email" name="email" v-model="dataForm.email" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>First Name</template>
      
      <input type="text" name="firstname" v-model="dataForm.firstName" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>Last Name</template>
      
      <input type="text" name="lastname" v-model="dataForm.lastName" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>Password</template>
      
      <input type="password" name="password" v-model="dataForm.password" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>Confirm Password</template>
      
      <input type="password" name="cpassword" v-model="dataForm.cpassword" />
    </WelcomeItem>
  </div>


  <div class="steptwo" v-show="step==2">
    <WelcomeItem>
      <template #heading>Company</template>
      
      <input type="text" name="company" v-model="dataForm.company" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>Address</template>
      
      <input type="text" name="address" v-model="dataForm.address" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>City</template>
      
      <input type="text" name="city" v-model="dataForm.city" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>State</template>
      
      <input type="text" name="state" v-model="dataForm.state" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>Country</template>
      
      <select v-model="dataForm.country">
        <option disabled value="">Please select one</option>
        <option v-for="(item, i) in countryList" :value="item" :key="i">{{ item }}</option>
      </select>
    </WelcomeItem>

  </div>
  <WelcomeItem>

    <button @click="step--" v-if="step==2">Back</button>
    <button @click="step++" v-if="step==1">Next</button>
    <button @click="submitData" v-if="step==2" :disable="samePassword">Submit</button>
  </WelcomeItem>
</template>

<style scoped>

</style>
