<template>
  <section class="statistics">
    <container class="container">
      <st-title class="statistics__title" :theme="'notline'"
        >Статистика по онкозаболеваниям</st-title
      >
      <div class="statistics__container">
        <st-box
          v-for="statistic in statistics"
          :key="statistic.id"
          class="statistics__box"
        >
          <st-text class="statistics__text">{{
            statistic.description
          }}</st-text>
          <st-progress-bar
            v-if="statistic.oldValue === 0"
            :currentValue="statistic.currentValue"
            :maxValue="statistic.maxValue"
          />
          <st-double-progress-bar
            v-else-if="statistic.id === 3"
            :oldValue="60"
            :currentValue="76.8"
            :maxValue="100"
          />
          <st-double-progress-bar
            v-else
            :oldValue="76.8"
            :currentValue="60"
            :maxValue="100"
          />
          <st-counter class="statistics__counter">{{
            statistic.summary
          }}</st-counter>
          <st-data-source class="statistics__data-source">{{
            statistic.source
          }}</st-data-source>
        </st-box>
      </div>
    </container>
  </section>
</template>

<script>
import Title from '@/components/ui/Title';
import Box from '@/components/ui/Box';
import TextBox from '@/components/ui/TextBox';
import ProgressBar from '@/components/ui/ProgressBar';
import Counter from '@/components/ui/Counter';
import DataSource from '@/components/ui/DataSource';
import DoubleProgressBar from '@/components/ui/DoubleProgressBar';
import Container from './Container';

export default {
  components: {
    'st-title': Title,
    'st-box': Box,
    'st-text': TextBox,
    'st-progress-bar': ProgressBar,
    'st-counter': Counter,
    'st-data-source': DataSource,
    'st-double-progress-bar': DoubleProgressBar,
    container: Container,
  },
  props: {
    currentValue: Number,
    maxValue: Number,
    oldValue: Number,
  },
  computed: {
    statistics() {
      return this.$store.getters['statistics/getStatistics'];
    },
  },
};
</script>

<style scoped>
.statistics {
  padding: 100px 0;
}

.container {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
}

.statistics__container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 40px;
  /* overflow: auto; */
  margin-top: 70px;
}

.statistics__box {
  padding: 20px 20px;
}

.statistics__text {
  margin-bottom: 76px;
}

.statistics__counter {
  margin-top: 20px;
}

.statistics__data-source {
  margin-top: 20px;
}

@media screen and (max-width: 1280px) {
  .statistics {
    padding: 90px 0;
  }

  .statistics__container {
    margin-top: 60px;
  }

  .statistics__box {
    padding: 18px 18px;
  }

  .statistics__text {
    margin-bottom: 56px;
  }
}

@media screen and (max-width: 1024px) {
  .statistics {
    padding: 80px 0;
  }

  .statistics__container {
    margin-top: 46px;
    grid-gap: 30px;
  }

  .statistics__box {
    padding: 10px 10px;
  }

  .statistics__text {
    margin-bottom: 54px;
  }

  .statistics__counter {
    margin-top: 10px;
  }

  .statistics__data-source {
    margin-top: 10px;
  }
}

@media screen and (max-width: 768px) {
  .statistics__title {
    margin-left: auto;
    margin-right: auto;
    text-align: center;
  }

  .statistics__container {
    margin-top: 60px;
    grid-gap: 20px;
    overflow-x: auto;
    padding-left: 40px;
  }

  .statistics__text {
    margin-bottom: 62px;
  }

  .container {
    padding: 0;
  }
}

@media screen and (max-width: 320px) {
  .statistics {
    padding: 50px 0;
  }

  .statistics__title {
    text-align: left;
  }

  .statistics__container {
    margin-top: 30px;
    grid-gap: 10px;
    padding-left: 15px;
  }
}
</style>
