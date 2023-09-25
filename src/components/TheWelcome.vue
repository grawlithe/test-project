<script setup>
import {ref} from 'vue'
import WelcomeItem from './WelcomeItem.vue'

const step = ref(1);


</script>

<script>
  export default {
    data: () => ({
      email:'',
      firstName:'',
      lastName:'',
      type:'',
      password:'',
      company:'',
      address:'',
      city:'',
      state:'',
      zip:'',
      country:'',
      userType:''
    }),
    methods: {
      async alert() {
        const a = await fetch(`https://restcountries.com/v3.1/all`);
        const d = await a.json();
        console.log(d.map((m) => {  }))
      }
    }
  }
</script>

<template>
  <div class="stepone" v-show="step==1">
    <input type="email" name="email" v-model="email" />
    <WelcomeItem>
      <template #heading>Email</template>
      
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>First Name</template>
      
      <input type="text" name="firstname" v-model="firstname" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>Last Name</template>
      
      <input type="text" name="lastname" v-model="lastname" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>Password</template>
      
      <input type="password" name="password" v-model="password" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>Confirm Password</template>
      
      <input type="password" name="cpassword" v-model="cpassword" />
    </WelcomeItem>
  </div>


  <div class="steptwo" v-show="step==2">
    <WelcomeItem>
      <template #heading>Company</template>
      
      <input type="text" name="company" v-model="company" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>Address</template>
      
      <input type="text" name="address" v-model="address" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>City</template>
      
      <input type="text" name="city" v-model="city" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>State</template>
      
      <input type="text" name="state" v-model="state" />
    </WelcomeItem>
    
    <WelcomeItem>
      <template #heading>Country</template>
      
      <input type="text" name="country" v-model="country" />
    </WelcomeItem>
  </div>
  <div>
    <button @click="step--" v-if="step==2">Back</button>
    <button @click="step++" v-if="step==1">Next</button>
    <button @click="alert" v-if="step==2">Submit</button>
  </div>
</template>
<style scoped>

</style>
