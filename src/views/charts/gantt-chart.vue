<template>
  <div class="app-container">
    <GanttChart />
  </div>
</template>

<script>
import GanttChart from '@/components/Charts/GanttChart'

export default {
  name: 'DHtmlxGanttChart',
  components: { GanttChart },
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

