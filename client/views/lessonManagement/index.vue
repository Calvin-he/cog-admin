<template>
<div>
    <div class="tabs is-boxed">
    <ul>
      <li :class="{'is-active': activeTab==null}" @click="activeTab=null"><a>Series Of Lesson</a></li>
      <li v-for="(tab,index) in tabs" :key="index" :class="{'is-active': activeTab===tab}">
        <a @click="viewSeries(tab.series._id)">{{tab.series.title}}</a>
      </li>
      <li><a title="Add new series">+</a></li>
    </ul>

    </div>
    <div :hidden='activeTab!=null'>
      <table class="table">
        <thead>
          <tr>
            <th>操作</th>
            <th>标题</th>
            <th>课程数</th>
            <th>更新时间</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="series in seriesList" :key="series._id">
            <td>
              <a class="btn btn-info" @click="viewSeries(series._id)">查看</a>
            </td>
            <td>{{series.title}}</td>
            <td>{{series.lessonList.length}}</td>
            <td>{{series.updated | date}}</td>
          </tr>
        </tbody>
    </table>
    </div>

    <div v-for="(tab,index) in tabs" :key="index" :hidden="activeTab!==tab">
        <series-editor :series='tab.series'></series-editor>
    </div>
</div>
</template>

<script>
import SeriesEditor from './SeriesEditor'

export default {
  data () {
    return {
      activeTab: null,
      tabs: [] // { series: **}
    }
  },
  computed: {
    seriesList () {
      return this.$store.state.lesson.seriesList
    }
  },
  mounted () {
    this.$store.dispatch('listSeries')
  },
  methods: {
    viewSeries (seriesId) {
      if (this.activeTab && this.activeTab.series._id === seriesId) {
        return
      }
      let tab = this.tabs.find(t => t.series._id === seriesId)
      if (tab != null) {
        this.activeTab = tab
      } else {
        let foundSeries = this.seriesList.find(t => t._id === seriesId)
        let ntab = { series: foundSeries }
        this.tabs.push(ntab)
        this.activeTab = ntab
      }
    }
  },
  components: {
    SeriesEditor
  }
}
</script>

<style>

</style>
