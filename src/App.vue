<template>
  <div id="app">
    <header class="header container mx-auto">
      <h1 class="header__tit">農村地方美食小吃特色料理</h1>
    </header>
    <nav class="nav container mx-auto">
      <NavSelect :list="computedCity" list-caption="請選擇行政區域..."
        @changeOption="currentCity = $event" />
      <NavSelect :list="computedTown" list-caption="請選擇鄉鎮區..."
        @changeOption="currentTown = $event" />
    </nav>
    <main class="main container mx-auto">
      <Card :data="computedData" />
    </main>
    <Footer />
    <Loading :isLoad="isLoad" />
  </div>
</template>

<script>
import NavSelect from '@/components/NavSelect.vue';
import Card from '@/components/Card.vue';
import Footer from '@/components/Footer.vue';
import Loading from '@/components/Loading.vue';

export default {
  name: 'App',
  components: {
    NavSelect,
    Card,
    Footer,
    Loading,
  },
  data() {
    return {
      data: [],
      currentCity: '',
      currentTown: '',
      isLoad: false,
    };
  },
  computed: {
    computedCity() {
      const allPlace = this.data.map((item) => item.City);
      return allPlace.filter((item, index) => allPlace.indexOf(item) === index);
    },
    computedTown() {
      const arr = [];
      this.data.forEach((item) => {
        if (item.City === this.currentCity) {
          arr.push(item);
        }
      });
      const allPlace = arr.map((item) => item.Town);
      return allPlace.filter((item, index) => allPlace.indexOf(item) === index);
    },
    computedData() {
      const cityArr = [];
      const townArr = [];

      if (this.currentCity) {
        this.data.forEach((item) => {
          if (item.City === this.currentCity) {
            cityArr.push(item);
          }
        });
        if (this.currentTown) {
          cityArr.forEach((item) => {
            if (item.Town === this.currentTown) {
              townArr.push(item);
            }
          });
          return townArr;
        }
        return cityArr;
      }
      return this.data;
    },
  },
  watch: {
    currentCity() {
      this.currentTown = '';
    },
  },
  created() {
    const api = 'https://data.coa.gov.tw/Service/OpenData/ODwsv/ODwsvTravelFood.aspx';
    this.$http.get(api).then((res) => {
      this.data = res.data;
    })
      .finally(() => {
        this.isLoad = true;
      });
  },
};
</script>

<style>
body {
  margin: 0;
  font-family: Arial, Helvetica, "微軟正黑體", sans-serif;
  background-color: #eee;
}

img {
  max-width: 100%;
  width: 100%;
  height: 100%;
  object-fit: cover;
  vertical-align: bottom;
}

.container {
  width: 1170px;
}

.mx-auto {
  margin-left: auto;
  margin-right: auto;
}

.header__tit {
  margin-top: 20px;
  margin-bottom: 20px;
  font-size: 30px;
  color: #666;
  text-align: center;
}

.nav {
  display: flex;
  justify-content: center;
  box-sizing: border-box;
  margin-bottom: 15px;
  border-radius: 5px;
  background-color: #fff;
}

@media screen and (max-width: 414px) {
  .container {
    width: 384px;
  }

  .header__tit {
    margin-top: 30px;
    margin-bottom: 30px;
  }

  .nav {
    flex-direction: column;
    margin-bottom: 0;
    background-color: transparent;
  }

}

@media screen and (max-width: 375px) {
  .container {
    width: 345px;
  }

  .header__tit {
    font-size: 28px;
  }
}

@media screen and (max-width: 360px) {
  .container {
    width: 330px;
  }

  .header__tit {
    font-size: 27px;
  }
}

@media screen and (max-width: 320px) {
  .container {
    width: 290px;
  }

  .header__tit {
    font-size: 24px;
  }
}
</style>
