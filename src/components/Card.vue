<template>
  <div class="card row">
    <div class="card__sec" v-for="(item, index) in data" :key="index">
      <a :href="item.Url" target="_blank" v-if="item.Url">
        <CardItem :item="item" />
      </a>
      <CardItem :item="item" v-else />
    </div>
  </div>
</template>

<script>
import CardItem from '@/components/CardItem.vue';

export default {
  name: 'Card',
  props: {
    data: Array,
  },
  components: {
    CardItem,
  },
};
</script>

<style scoped>
.row {
  margin-left: -15px;
  margin-right: -15px;
}

.card {
  display: flex;
  flex-wrap: wrap;
}

.card__sec {
  box-sizing: border-box;
  width: 33.33333%;
  padding: 15px;
}

@media screen and (max-width: 414px) {
  .row {
    margin-left: 0;
    margin-right: 0;
  }

  .card__sec {
    width: 100%;
    margin-bottom: 15px;
    padding: 0;
  }
}
</style>
