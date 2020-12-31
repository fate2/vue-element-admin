<template>
  <div class="app-container">
    <TreeChart />
  </div>
</template>

<script>
import TreeChart from '@/components/Charts/TreeChart'

export default {
  name: 'OrgTreeChart',
  components: { TreeChart },
  mounted() {
  }
}
</script>

<style scoped>
.app-container{
  position: relative;
  width: 100%;
  height: calc(100vh - 84px);
}
</style>

