<template>
  <div>
    <img src="https://img.icons8.com/doodle/48/000000/building--v1.png" class="cluster-img"/>
    <p class="cluster-text">{{ getNumber() }}</p>
  </div>
</template>

<script>
export default {
  props: {
    clusterUsers: {
      type: Array,
      required: true
    },
  },
  methods: {
    getNumber () {
      return this.$props.clusterUsers.length
    },
  }
}
</script>

<style>
  .cluster-img {
    float: left;
    width: 60px;
    height: 60px;
  }
  .cluster-text {
    margin:12px;
    width:40px;
    height:40px;
    border-radius:100%;
    background-color: #FEBF34;
    color:#fff;
    text-align:center;
    font-size:14px;
    overflow:hidden;
    line-height:40px;
  }
</style>
