<template>          

  <div id="application">
    <div>   
      <h3>Оцените сервис магазина</h3> 
    </div>
    <div></div>
       <router-link to="/feed" class="btns"  v-on:click="sendEmoji('normal')"><img src="../assets/normal.png" alt="normal" height="50"></router-link>
       <router-link to="/feed" class="btns"  v-on:click="sendEmoji('good')"><img src="../assets/good.png" alt="good" height="50"></router-link>
       <router-link to="/feed" class="btns"  v-on:click="sendEmoji('bad')"><img src="../assets/bad.png" alt="bad" height="50"></router-link>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      modifiedData: {
          status: '',
          ip_address: '',
          shop_id: this.$route.params.id
        },
      error: null
    }
  },
  async mounted () {
    try {
      const response = await axios.get('https://immense-wave-26764.herokuapp.com/api/shops')
      this.feedbacks = response.data;
    } catch (error) {
      this.error = error;
    }
  },
  methods: {
    sendEmoji(status) {
      axios.post('https://immense-wave-26764.herokuapp.com/api/feedbacks', {
        data: {
            status: status, //modifiedData.status,
            ip_address: '126.12.29.29', //modifiedData.ip_address,
            shop_id: this.$route.params.id //modifiedData.shop_id
          }
        })
        .then(response => {
          console.log(response.data)
        })
        .catch(error => {
          console.error(error)
        })
    },
  }
}
</script>

<style>

#application{
position: relative;
top: 16rem;
}

.btns{
  margin: 15px;
  cursor: pointer;
}
</style>
