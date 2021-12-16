<template>
  <div class="nav__select">
    <select class="nav__ls" @change="changeOption" v-model="selected">
    <!-- <select class="nav__ls" v-model="computedSelected">
      <option class="nav__item" value="" selected disabled>{{ listCaption }}</option> -->
      <option class="nav__item" value="all" :selected="selected" disabled>{{ listCaption }}</option>
      <option class="nav__item" :value="item"
        v-for="(item, index) in list" :key="index">{{ item }}</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'NavSelect',
  props: {
    list: Array,
    listCaption: String,
    // currentCity: String,
  },
  data() {
    return {
      selected: 'all',
    };
  },
  methods: {
    changeOption() {
      this.$emit('changeOption', this.selected);
    },
  },
  watch: {
    list() {
      this.selected = 'all';
    },
  },
  // computed: {
  //   computedSelected: {
  //     get() {
  //       console.log('getter');
  //       return this.currentCity;
  //     },
  //     set(val) {
  //       console.log('setter');
  //       this.$emit('changeOption', val);
  //     },
  //   },
  // },
};
</script>

<style scoped>
.nav__select {
  position: relative;
  margin: 20px 15px;
}

.nav__select::after {
  content: "";
  position: absolute;
  top: 15px;
  right: 5px;
  border: 4px solid transparent;
  border-top-color: #000;
}

.nav__ls {
  box-sizing: border-box;
  width: 300px;
  padding: 8px;
  font-size: 15px;
  border: none;
  border-radius: 5px;
  outline-color: #a3c5fc;
  background-color: #eee;
  appearance: none;
  cursor: pointer;
}

@media screen and (max-width: 414px) {
  .nav__select {
    margin: 0;
    margin-bottom: 15px;
  }

  .nav__ls {
    width: 100%;
    background-color: #ddd;
  }
}
</style>
