<template>
  <div>
    <van-nav-bar title="仿腾讯动漫">
      <template #left>
        <van-icon name="search" size="18" @click="search" />
      </template>
      <template #right>
        <van-icon name="location-o" size="18" @click="showMenu" />
      </template>
    </van-nav-bar>

    <van-action-sheet
      v-model="show"
      :actions="actions"
      cancel-text="取消"
      close-on-click-action
      @cancel="onCancel"
    />

    <keep-alive>
      <router-view />
    </keep-alive>
    <van-tabbar
      v-model="active"
      active-color="#ff9a6a"
      inactive-color="#999999"
      @change="changeTabBar(active)"
      class="active_tab"
    >
      <van-tabbar-item icon="home-o">首页</van-tabbar-item>
      <van-tabbar-item icon="music-o">短视频</van-tabbar-item>
      <van-tabbar-item icon="setting-o">我的</van-tabbar-item>
    </van-tabbar>
  </div>
</template>

<script>
export default {
  data () {
    return {
      active: 0,
      show: false,
      actions: [{ name: '选项一' }, { name: '选项二' }, { name: '选项三' }]
    }
  },
  created () {
    if (this.$route.path === '/home-comic') {
      this.active = 0
    } else if (this.$route.path === '/home-video') {
      this.active = 1
    } else if (this.$route.path === '/home-mine') {
      this.active = 2
    }
  },
  methods: {
    onCancel () {
      this.$toast('取消')
    },
    search () {
      this.$toast('进入搜索')
      // this.$router.replace({ path: "/search" });
    },
    showMenu () {
      this.show = true
    },
    changeTabBar (active) {
      switch (active) {
        case 0:
          this.$router.replace({ path: '/home-comic' })
          break
        case 1:
          this.$router.replace({ path: '/home-video' })
          break
        case 2:
          this.$router.replace({ path: '/home-mine' })
          break
      }
    }
  }
}
</script>

<style scoped>
.active_tab {
  z-index: 300;
}
</style>
