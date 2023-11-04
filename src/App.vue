<template>
  <StepOne v-if="step===1" @formatList="formatList($event)"/>
  <StepTwo v-if="step===2" :formatted-list=formattedList :pickers=pickers @add="add($event)" @next="next"/>
  <StepThree v-if="step===3" :formatted-list=formattedList :pickers=pickers :picker=picker :teams=teams @add="add($event)" @sort="sort" @pick="pick"/>

</template>

<script>
import StepOne from "./components/StepOne.vue";
import StepTwo from "./components/StepTwo.vue";
import StepThree from "./components/StepThree.vue";

export default {
  name: 'App',
  components: {
    StepTwo,
    StepOne,
    StepThree
  },
  data() {
    return {
      step: 1,
      formattedList: [],
      pickers: [],
      picker: '',
      teams: [
        [],
        [],
        [],
        [],
        []
      ]
    }
  },
  methods: {
    formatList: function (list) {
      list = list.split('\n');
      list.forEach((name, index) => {
        if (index > 0 && this.formattedList.length < 20) {
          name = name.trim()
          name = name.replace(/^([0-9]*-( *))/, "")
          this.formattedList.push(name)
        }
      })
      this.step = 2;
    },
    add: function (item) {
      if (this.pickers.includes(item)) {
        this.pickers.splice(this.pickers.indexOf(item), 1)
      } else if (this.pickers.length < 5) {
        this.pickers.push(item)
      }
    },
    sort: function () {
      let lucky = Math.floor(Math.random() * this.pickers.length)
      this.pick(this.pickers[lucky])
      this.pickers.splice(lucky, 1)

    },
    next: function () {
      this.step += 1
    },
    pick: function(player){
      this.teams[this.nextTeam()].push(player);
      this.formattedList.splice(this.formattedList.indexOf(player), 1)
      this.picker = this.teams[this.nextTeam()][0];
    },
    nextTeam: function(){
      console.log(this.teams.length)
      for(let i = 1; i < this.teams.length; i++){
        if(this.teams[i].length < this.teams[i-1].length)
          return i;
      }
      return 0;
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.bn39 {
  background-image: linear-gradient(135deg, #008aff, #86d472);
  border-radius: 6px;
  box-sizing: border-box;
  color: #000000;
  display: block;
  height: 50px;
  font-size: 1.4em;
  font-weight: 600;
  padding: 4px;
  position: relative;
  text-decoration: none;
  width: 7em;
  z-index: 2;
}

.bn39:hover {
  color: #000000;
}

.bn39 .bn39span {
  align-items: center;
  background: #ffffff;
  border-radius: 6px;
  display: flex;
  justify-content: center;
  height: 100%;
  transition: background 0.5s ease;
  width: 100%;
}

.bn39:hover .bn39span {
  background: transparent;
}
</style>
