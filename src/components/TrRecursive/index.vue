<template>
  <tbody v-if="childrenRecursive.length">
    <template v-for="(itemChild, indexChild) in childrenRecursive">
      <tr :key="indexChild">
        <td v-if="indexChild === 0 || question.id !== itemChild.parent_id" :rowspan="childrenRecursive.length">{{ question.content.vn }} </td>
        <td v-if="indexChild === 0 || question.id !== itemChild.parent_id" :rowspan="childrenRecursive.length">{{ question.proportionMain }}%</td>
        <td v-if="indexChild === 0 || itemChild.id !== itemChild.parent_id" :rowspan="itemChild.children_recursive.length ? 1 : itemChild.children_recursive.length">{{ JSON.parse(itemChild.content).vn }}</td>
        <td v-if="indexChild === 0 || itemChild.id !== itemChild.parent_id" :rowspan="itemChild.children_recursive.length ? 1 : itemChild.children_recursive.length">{{ itemChild.max_score_group }}</td>
        <td>{{ itemChild.max_score }}</td>
        <td>
          <el-input v-model="itemChild.your_answer" />
        </td>
        <td>
          <el-input v-model="itemChild.your_answer" />
        </td>
        <td>
          <el-input v-model="itemChild.your_answer" />
        </td>
        <td>
          <el-input v-model="itemChild.your_answer" />
        </td>
        <td>
          <el-input v-model="itemChild.your_answer" />
        </td>
        <td>
          <el-input v-model="itemChild.your_answer" />
        </td>
        <td>
          <el-input v-model="itemChild.point" />
        </td>
      </tr>
      <TrRecursive :key="itemChild" :question="itemChild" :children-recursive="itemChild.children_recursive" />
    </template>
  </tbody>
</template>

<script>
import TrRecursive from '@/components/TrRecursive'

export default {
  name: 'TrRecursive',
  components: { TrRecursive },
  props: {
    question: {
      type: Object,
      required: true
    },
    childrenRecursive: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>

</style>
