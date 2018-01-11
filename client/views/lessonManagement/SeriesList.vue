<template>
  <div>
    <table class="table">
    <thead>
        <tr>
        <th>序号</th>
        <th>标题</th>
        <th>课程数</th>
        <th>更新时间</th>
        <th>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</th>
        </tr>
    </thead>
    <tfoot>
    </tfoot>
    <tbody>
        <tr  v-for="(series, index) in seriesList" :key="series._id">
            <td>{{index+1}}</td>
            <td>{{series.title}}</td>
            <td>{{series.lessonList.length}}</td>
            <td>{{series.updated | date}}</td>
            <td>
            </td>
        </tr>
    </tbody>
    </table>
  </div>
</template>

<script>

export default {
  name: 'SeriesList',
  data () {
    return {
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
  },
  components: {
  }
}
</script>
