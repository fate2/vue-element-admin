<template>
  <Vue2OrgTree
    :data="data"
    :props="dataProps"
    :horizontal="horizontal"
    :collapsable="collapsable"
    :render-content="renderContent"
    @on-expand="onExpand"
    @on-node-click="onNodeClick"
  />
</template>

<script>
import Vue2OrgTree from 'vue2-org-tree'

export default {
  name: 'TreeChart',
  components: { Vue2OrgTree },
  data() {
    return {
      data: {
        id: 0,
        label: 'XXX科技有限公司',
        expand: true,
        collapsable: true,
        children: [{
          id: 2,
          label: '产品研发部',
          children: [{
            id: 5,
            label: '研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端研发-前端',
            children: [{
              id: 11,
              label: '微信小程序小程序微信小程序小程序微信小程序小程序微信小程序小程序'
            }]
          }, {
            id: 6,
            label: '研发-后端'
          }, {
            id: 9,
            label: 'UI设计'
          }, {
            id: 10,
            label: '产品经理'
          }]
        }, {
          id: 3,
          label: '销售部',
          children: [{
            id: 7,
            label: '销售一部'
          }, {
            id: 8,
            label: '销售二部'
          }]
        }, {
          id: 4,
          label: '财务部'
        }, {
          id: 9,
          label: 'HR人事'
        }]
      },
      horizontal: true,
      collapsable: true,
      expandAll: true,
      // labelClassName: 'bg-white',
      dataProps: {
        label: 'id',
        expand: 'expand',
        children: 'children'
      }
    }
  },
  mounted() {

  },
  methods: {
    labelClassName: function(data) {
      return 'clickable-node'
    },
    renderContent: function(h, data) {
      return data.label
    },
    onExpand: function(e, data) {
      if ('expand' in data) {
        data.expand = !data.expand

        if (!data.expand && data.children) {
          this.collapse(data.children)
        }
      } else {
        this.$set(data, 'expand', true)
      }
    },
    onNodeClick: function(e, data) {
      console.log('onNodeClick: %o', data)
      this.$set(data, 'selectedKey', !data.selectedKey)
    },
    collapse: function(list) {
      var _this = this
      list.forEach(function(child) {
        if (child.expand) {
          child.expand = false
        }

        child.children && _this.collapse(child.children)
      })
    },
    expandChange: function() {
      this.toggleExpand(this.data, this.expandAll)
    },
    toggleExpand: function(data, val) {
      var _this = this
      if (Array.isArray(data)) {
        data.forEach(function(item) {
          _this.$set(item, 'expand', val)
          if (item.children) {
            _this.toggleExpand(item.children, val)
          }
        })
      } else {
        this.$set(data, 'expand', val)
        if (data.children) {
          _this.toggleExpand(data.children, val)
        }
      }
    }
  }
}
</script>
<style scoped>
  @import '~vue2-org-tree/dist/style.css';
</style>
