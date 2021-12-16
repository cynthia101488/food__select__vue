<template>
  <div class="card__content">
    <div class="card__head">
      <h3 class="card__tag">{{ item.City }}</h3>
    </div>
    <div class="img__inner">
      <img class="image" :src="item.PicURL" :alt="item.Name" loading="lazy">
    </div>
    <div class="card__body">
      <div class="card__info">
        <h3 class="card__tit">{{ item.Town }}</h3>
        <h2 class="card__name">{{ item.Name }}</h2>
      </div>
      <div class="card__footer">
        <p class="card__desc">{{ item.HostWords }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardItem',
  props: {
    item: Object,
  },
};
</script>

<style scoped>
.card__content {
  position: relative;
  overflow: hidden;
}

.card__head, .card__body {
  z-index: 2;
  position: absolute;
}

.card__tag {
  margin: 0;
  padding: 4px;
  font-size: 12px;
  font-weight: 400;
  color: #fff;
  background-color: #e79500;
}

.img__inner {
  position: relative;
  height: 200px;
  overflow: hidden;
}

.img__inner::before {
  content: "";
  position: absolute;
  z-index: 1;
  display: block;
  width: 100%;
  height: 100%;
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0), rgba(0, 0, 0, .5));
}

.img__inner img {
  transition: transform 1s;
}

.card__content:hover img {
  transform: scale(1.05);
}

.card__body {
  bottom: 0;
  padding: 10px;
  transform: translateY(70px);
  transition: transform 1s;
}

.card__content:hover .card__body {
  transform: translateY(0);
}

.card__tit, .card__name {
  margin: 0;
  font-weight: 400;
  color: #fff;
}

.card__tit {
  font-size: 14px;
  font-style: italic;
}

.card__name {
  font-size: 16px;
}

.card__desc {
  height: 4.5em;
  margin: 0;
  font-size: 15px;
  line-height: 1.5em;
  color: #fff;
  overflow: hidden;
}

.card__desc::before {
  content: "";
  display: block;
  width: 50px;
  height: 3px;
  margin-top: 10px;
  margin-bottom: 10px;
  background-color: #fff;
}
</style>
