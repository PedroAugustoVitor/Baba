<template>
  <StepOne v-if="step===1" @formatList="formatList($event)" @persist="persist"/>
  <StepTwo v-if="step===2" :formatted-list=formattedList :pickers=pickers @add="add($event)" @persist="persist"
           @next="next"/>
  <StepThree v-if="step===3" :formatted-list=formattedList :pickers=pickers :picker=picker :teams=teams
             @add="add($event)" @sort="sort" @pick="pick" @persist="persist"/>
  <div class="dropup position-absolute top-0 end-0 rounded-circle m-5">
    <button type="button" class="btn btn-outline-danger" data-bs-toggle="modal" data-bs-target="#reset">
      <i class="bi bi-repeat"></i>
    </button>
  </div>
  <div class="modal fade" id="reset" tabindex="-1" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="resetLabel">Recomeçar escolhas</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          Caso clique em recomeçar, todas as escolhas serão zeradas.
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Fechar</button>
          <button type="button" class="btn btn-outline-danger" @click="reset" data-bs-dismiss="modal">Recomeçar</button>
        </div>
      </div>
    </div>
  </div>
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
  mounted() {
    if (localStorage.step) {
      this.step = parseInt(localStorage.step)
    }
    if (localStorage.picker) {
      this.picker = localStorage.picker
    }
    if (localStorage.teams) {
      this.teams = JSON.parse(localStorage.teams)

    }
    if (localStorage.formattedList) {
      this.formattedList = JSON.parse(localStorage.formattedList)
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
      this.persist()
    },
    add: function (item) {
      if (this.pickers.includes(item)) {
        this.pickers.splice(this.pickers.indexOf(item), 1)
      } else if (this.pickers.length < 5) {
        this.pickers.push(item)
      }
      this.persist()
    },
    sort: function () {
      let lucky = Math.floor(Math.random() * this.pickers.length)
      this.pick(this.pickers[lucky])
      this.pickers.splice(lucky, 1)

    },
    next: function () {
      this.step += 1
      this.persist()
    },
    pick: function (player) {
      this.teams[this.nextTeam()].push(player);
      this.formattedList.splice(this.formattedList.indexOf(player), 1)
      this.picker = this.teams[this.nextTeam()][0]
      this.persist()
    },
    nextTeam: function () {
      for (let i = 1; i < this.teams.length; i++) {
        if (this.teams[i].length < this.teams[i - 1].length)
          return i;
      }
      return 0;
    },
    persist: function () {
      localStorage.teams = JSON.stringify(this.teams)
      localStorage.formattedList = JSON.stringify(this.formattedList)
      localStorage.step = this.step
      localStorage.picker = this.picker
    },
    reset: function () {
      this.step = 1
      this.formattedList = []
      this.pickers = []
      this.picker = ''
      this.teams = [
        [],
        [],
        [],
        [],
        []
      ]
      this.persist()
    }
  }
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
