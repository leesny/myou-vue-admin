<template>
  <div class="logo-wrapper">
    <transition name="fade">
      <span v-if="isCollapse" key="0" :class="{'is-text':!type,'is-img':type}" class="logo-title is-bold">
        <template v-if="type">
          <img :src="website.logo" width="40" height="40">
        </template>
        <template v-else>{{ website.logo }}</template>
      </span>
    </transition>
    <transition-group name="fade">
      <template v-if="!isCollapse">
        <span key="1" class="logo-title is-bold">{{ website.title }}</span>
        <span key="2" class="logo-subtitle">{{ website.author }}</span>
      </template>
    </transition-group>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  name: 'Logo',
  props: {
    isCollapse: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {}
  },
  computed: {
    ...mapGetters(['website']),
    type: function(val) {
      return this.website.logo.indexOf('static') !== -1
    }
  },
  created() {},
  methods: {}
}
</script>

<style scoped="scoped" lang="scss">
.fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter-active {
  transition: opacity 2.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
.logo-wrapper {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50px;
  line-height: 50px;
  background: #17b3a3;
  color: #fdfdfd;
  text-align: center;
  font-size: 20px;
  font-weight: 600;
  overflow: hidden;
  box-sizing: border-box;
  position: sticky;
}
.logo-title {
  padding: 0 5px 0 0;
  color: #fff;
  font-size: 20px;
  &.is-bold {
    font-weight: 700;
  }
}
.is-text {
  position: absolute;
  top: 0;
  // left: 20px;
}
.is-img {
  position: absolute;
  top: 10px;
  left: 10px;
}
.logo-subtitle {
  font-size: 16px;
  padding-top: 5px;
}
</style>
