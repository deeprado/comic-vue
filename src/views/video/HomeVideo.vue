<template>
  <div class="mainContent">
    <scroll :top="0" :bottom="48" @onScroll="onScroll" ref="scroll">
      <div class="block">
        <video-item
          :item="item"
          v-for="(item, index) in videoImageList"
          :key="index"
        ></video-item>
      </div>
      <loading :show-loading="showLoading"></loading>
    </scroll>
  </div>
</template>

<script>
import VideoItem from '../../components/video/VideoItem'
import Scroll from '../../components/scroll/Scroll'
import Loading from '../../components/loading/Loading'

import HomeVideoImagesData from '../../mock/home_comic_image_list.json'

export default {
  data () {
    return {
      videoImageList: [],
      currentY: 0,
      showLoading: true
    }
  },
  components: {
    VideoItem,
    Scroll,
    Loading
  },
  created () {
    this.http
      .get('/get-home-video')
      .then(response => {
        this.videoImageList = response.videoImageList
        setTimeout(() => {
          this.showLoading = false
        }, 800)
      })
      .catch(error => {
        this.videoImageList = HomeVideoImagesData.data.comicPictureList
        console.log(error)
        setTimeout(() => {
          this.showLoading = false
        }, 800)
      })
  },
  methods: {
    onScroll (offsetY) {
      this.currentY = offsetY
    }
  },
  activated () {
    this.$refs.scroll.scrollTo(0, this.currentY)
  }
}
</script>

<style lang="scss" scoped>
@import "../../assets/css/mixin";

.mainContent {
  // padding-top: 3rem;
}

.block {
  padding-top: 10px;
  width: 100%;
  display: flex;
  flex-flow: row wrap;
  justify-content: space-around;
  background: #f8f8f8;
}
</style>
