<script>
export default {
  name: 'StepTwo',
  props: {
    formattedList: Array,
    pickers: Array
  },
  methods: {
    add: function (pickers) {
      this.$emit('add', pickers)
    },
    next: function () {
      if(this.pickers.length === 5)
        this.$emit('next')
    },
    persist: function () {
      this.$emit('persist')
    }
  },
  data() {
    return {
    }
  },
}
</script>

<template>
  <h5 class="form-label">Quem vai escolher?</h5>
  <div class="offset-1 col-10 row">
    <div class="d-grid col-6" v-for="(item, index) in formattedList" :key="index">
      <a class="btn btn-outline-dark position-relative mt-1"
         @click="add(item)">
        {{ item }}
        <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-success"
              v-if="pickers.includes(item)">
        {{ pickers.indexOf(item) + 1 }}
      </span>
      </a>
    </div>
  </div>
  <div class="col-12 mt-3">
    <a class="offset-4 col-4 bn39" @click="next()"><span class="bn39span">Escolher</span></a>
  </div>

</template>

<style>

</style>