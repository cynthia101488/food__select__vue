<template>
  <footer class="footer container mx-auto">
    <p class="footer__desc">政府資料開放平台</p>
    <a href="https://data.gov.tw/dataset/6037" target="_blank">https://data.gov.tw/dataset/6037</a>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
};
</script>

<style scoped>
.footer {
  margin-bottom: 15px;
  text-align: center;
}

.footer__desc {
  margin: 0;
  color: #999;
}

.footer a {
  font-size: 14px;
  color: #666;
}
</style>
