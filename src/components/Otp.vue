<template>
  <div>
    <div class="date">{{ date }}</div>
    <!-- TITULO -->
    <div class="title">{{ title }}</div>
    <!-- SECRET -->
    <button class="generate-secret" v-on:click="generateSecret">GENERAR SECRET</button><br/>
    <div class="card">
      <div class="secret">{{ secret }}</div>
    </div>
    <div>
      <vue-qrcode :value="secret"></vue-qrcode><br/>
    </div>
    <div class="card">
      <!-- TIEMPO -->
      <div class="time-remaining">Tiempo restante: {{ timeRemaining }} segundos</div>
      <!-- OTP -->
      <div class="otp">{{ otp }}</div>
    </div>
  </div>
</template>

<script>
import { authenticator } from 'otplib';
import VueQrcode from 'vue-qrcode';
export default {
  name: 'Otp',
  components: {
    VueQrcode
  },
  data: () => ({
    title: 'OTP GENERATOR',
    date: new Date().toTimeString(),
    secret: null,
    timeRemaining: 0,
    otp: '000000',
    intervalOtp: null
  }),
  mounted () {
    this.generateSecret();
    this.setTimeRemaining();
  },
  methods: {
    generateSecret: function () {
      this.secret = authenticator.generateSecret();
      this.generateTotp(this.secret);
    },
    generateTotp: function (secret) {
      clearInterval(this.intervalOtp);
      this.otp = authenticator.generate(secret);
      this.intervalOtp = setInterval(() => {
        this.otp = authenticator.generate(secret);
      }, 1000);
    },
    setTimeRemaining: function () {
      setInterval(() => {
        this.timeRemaining = authenticator.timeRemaining();
        this.date = new Date().toTimeString();
      }, 1000);
    }
  }
}
</script>

<style> 
.date {
  font-size: 15px;
  color: rgb(12, 177, 12);
}
.title {
  font-size: 25px;
  padding: 15px;
  color: rgb(12, 177, 12);
}
.secret {
  font-size: 20px;
  color: rgb(109, 105, 105);
}
.card {
  margin: 10px;
  background: rgb(241, 239, 239);
  border-radius: 10px;
  display: inline-block;
  padding: 15px;
}
.otp {
  font-size: 50px;
  color: rgb(12, 177, 12);
}
.time-remaining {
  font-size: 12px;
}
.generate-secret {
  padding: 18px;
  color: white;
  background-color: rgb(12, 177, 12);
  font-weight: 700;
  font-size: 15px;
  text-align: center;
	border: none;
	border-radius: 20px;
  margin-top: 25px;
}
</style>
