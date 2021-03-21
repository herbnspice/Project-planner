<template>
  <div class="filter-nav">
    <a href="#" class="filter" :class="{'active' : current === 'all' }" @click="updateFilter('all')">View All </a>
    <a href="#" class="filter" :class="{'active' : current === 'ongoing' }" @click="updateFilter('ongoing')">Ongoing </a>
    <a href="#" class="filter" :class="{'active' : current === 'completed' }" @click="updateFilter('completed')">Completed </a>
  </div>
</template>

<script>
export default {
  name: 'Filter Nav',
  props: {
    msg: String,
    current: String
  },
  methods:{
    updateFilter(by){
      this.$emit('updateFilter', by )
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.filter-nav{
  margin-top:10px;
}
.filter{
  margin: 10px 10px;
}
.filter.active{
  border-bottom: 2px solid #00ce89;
  padding-bottom:4px;
}
</style>
