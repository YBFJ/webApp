<template>
<div>
   <detail-banner
   :sightName="sightName"
   :bannerImg="bannerImg"
   :bannerImgs="gallaryImgs"></detail-banner>
   <detail-header></detail-header>
   <div class="content">
     <detail-list :list="list"></detail-list>
   </div>
</div>

</template>


<script>
import DetailBanner from './components/banner';
import DetailHeader from './components/header';
import DetailList from './components/list';
import axios from 'axios';
export default {
  name: 'Detail',
  components: {
    DetailBanner,
    DetailHeader,
    DetailList
  },
  data() {
    return {
      sightName: '',
      bannerImg: '',
      gallaryImgs: [],
      list: []
    };
  },
  methods: {
    getDetaiInfo() {
      axios
        .get('/api/detail.json', {
          params: {
            id: this.$route.params.id
          }
        })
        .then(this.handleGetDataSucc);
    },
    handleGetDataSucc(res) {
      res = res.data;
      if (res.ret && res.data) {
        const data = res.data;
        console.log(data);
        this.sightName = data.sightName;
        this.bannerImg = data.bannerImg;
        this.gallaryImgs = data.gallaryImgs;
        this.list = data.categoryList;
      }
    }
  },
  mounted() {
    this.getDetaiInfo();
  }
};
</script>

<style lang="stylus" scoped>
.content
  height 50rem
</style>
