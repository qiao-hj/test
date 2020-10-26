<template>
  <div class="model_box" :class="{'active': showActive}">
    <slot></slot>
  </div>
</template>
<script>
export default {
  props: ['showActive','userInfo'],
  data () {
    return {
    }
  },
}
</script>
<style scoped lang="scss">
.model_box {
  position: absolute;
  width: 100%;
  height: 50%;
  bottom: -50%;
  border-radius: 5px;
  transition: all 0.3s;
  background-color: #fff;
}
.active {
  width: 100%;
  bottom: 0;
}
</style>