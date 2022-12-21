

<template>
  <div id="app">
    <h2 class="title">Start counting!</h2>

    <img class="img" src="./assets/crono.png">
   
    <a class="time">{{ number }}</a>

    <div class="areaBtn">
      <button class="btn" @click="Go">{{ btn }}</button>
      <button class="btn" @click="Clean">Clean</button>
    </div>

    <div class="list" v-show="historic.length > 0">
      <ul>
        <li v-for="item in historic" :key="item"> You took a break! {{ historic }}</li>

        <button class="btn" @click="historic = []">
          Clean history
        </button>
      </ul>
    </div>
   
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      number: 0,
      btn: 'Go',
      timer: null,
      ss: 0,
      mm: 0,
      hh: 0,
      historic: []
    }
  },
  methods: {
    Go() {
      if (this.timer !== null) {
        //Timer rodando 

        clearInterval(this.timer);
        this.timer = null;
        this.btn = 'Go';
          if(this.ss !== 0){
            this.historic.push(this.number);
          }
      } else {
        //Time parado

        this.timer = setInterval(() => {
          this.runTimer();
        }, 1000);
        this.btn = 'Pause';
      }

    },
    Clean() {
      if (this.timer !== null) {
        clearInterval(this.timer);
        this.timer = null;
      } else {
        this.ss = 0;
        this.mm = 0;
        this.hh = 0;
        this.number = 0;
        this.number = 'Go',
        this.historic = []
      }
    },
    runTimer() {
      this.ss++;
      if (this.ss == 59) {
        //chegou 59s
        this.ss = 0;
        this.mm++;

      }
      if (this.mm == 59) {
        this.mm = 0;
        this.hh++;
      }

      let format = (this.hh < 10 ? '0' + this.hh : this.hh) + ':'
        + (this.mm < 10 ? '0' + this.mm : this.mm) + ':'
        + (this.ss < 10 ? '0' + this.ss : this.ss);

      return this.number = format;
    }
  }
}
</script>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
  width: 100%;
  align-items: center;
  justify-items: center;
  margin: 65% 0px 0px 200%;
  
}

.img {
  width: 420px;
  height: 420px;
  background: rgb(236, 236, 236);
  border: 5px solid;
  border-color: rgb(127, 167, 159);
  border-radius: 100%;

}

.time {
  color: rgb(127, 167, 159);
  font-size: 60px;
  margin-top: -190px;
}

.areaBtn {
  margin-top: 130px
}

.btn {
  -webkit-user-select: none;
  -moz-user-select: none;
  background: rgb(127, 167, 159);
  color: rgb(49, 2, 129);
  width: 150px;
  font-size: 20px;
  border: 0;
  border-radius: 8px;
  text-align: center;
  margin-left: 15px;
  margin-right: 15px;
  padding: 6px;
  cursor: pointer;
}

.btn:hover {
  color: rgb(49, 2, 129);
  border: 1px solid;
  border-color: rgb(0, 78, 134);
  opacity: 0.5;
  transition: all 0.50s;
}

ul {
  text-align: center;
  padding: 0px;
}

ul li{
  margin-top: 4px; 
  padding: 15px;
  background-color: rgb(250, 246, 209);
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  border: 0.5px solid;
  color: rgb(49, 2, 129);
  font-size: 15px;
  border-radius: 6px;
  list-style: none;
}

.list button{
  margin-top: 10px;
}
</style>
