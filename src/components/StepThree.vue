<script>
export default {
  name: 'StepTwo',
  props: {
    formattedList: Array,
    teams: Array,
    pickers: Array,
    picker: Text
  },
  methods: {
    add: function (pickers) {
      this.$emit('add', pickers)
    },
    next: function () {
      if (this.pickers.length === 4)
        this.$emit('next')
    },
    sort: function () {
      this.$emit('sort')
    },
    nextTeam: function () {
      this.$emit('nextTeam')
    },
    pick: function (player) {
      this.$emit('pick', player)
    },
    persist: function () {
      this.$emit('persist')
    }
  },
  data() {
    return {}
  },
}
</script>

<template>

  <div class="mt-1">
    <h5 v-if="pickers.length === 0 && formattedList.length > 0">É a vez de {{ picker }}!</h5>
    <h5 v-if="formattedList.length === 0">Acabou!!!</h5>
  </div>
  <div class="offset-1 col-10 row" v-if="pickers.length === 0">
    <div class="d-grid col-6" v-for="(item, index) in formattedList" :key="index">
      <a class="btn btn-outline-dark position-relative mt-1"
         @click="pick(item)">
        {{ item }}
        <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-success"
              v-if="pickers.includes(item)">
        {{ pickers.indexOf(item) + 1 }}
      </span>
      </a>
    </div>
  </div>
  <div class="col-12 mt-3" v-if="pickers.length > 0">
    <a class="offset-4 col-4 bn39" @click="sort()"><span class="bn39span">Sortear</span></a>
  </div>

  <div class="offset-1 card col-10 my-5" v-for="(items, i) in teams" :key="i">
    <div class="card-header">
      Time {{ i + 1 }}
    </div>
    <ul class="list-group list-group-flush">
      <li class="list-group-item" v-for="(item, j) in items" :key="j">{{ item }}</li>
    </ul>
  </div>
</template>

<style>

</style>