<script>
export default {
  name: 'StepOne',
  props: {
    formattedList: Array,
  },
  methods: {
    formatList: function (list) {
      this.$emit('formatList', list)
      this.persist()
    },
    persist: function () {
      this.$emit('persist')
    }
  },
  data() {
    return {
      list: ""
    }
  },
}
</script>

<template>
  <div class="mb-3">
    <label for="exampleFormControlTextarea1" class="form-label">Lista:</label>
    <textarea class="form-control" id="exampleFormControlTextarea1" rows="10" v-model="list" placeholder="Cole aqui a lista"></textarea>
    <div class="col-12 mt-3">
      <a class="offset-4 col-4 bn39" @click="formatList(list)"><span class="bn39span">Começar</span></a>
    </div>
  </div>

</template>

<style>

</style>
