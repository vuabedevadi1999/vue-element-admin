<template>
  <tbody>
    <template v-for="(itemChild, indexChild) in childrenRecursive">
      <tr :key="indexChild">
        <td v-if="indexChild === 0 || childrenRecursive[indexChild - 1].parent_id !== itemChild.parent_id" :rowspan="parentQuestionCounts[itemChild.parent_id]">{{ JSON.parse(itemChild.parent.content).vn }} </td>
        <td v-if="indexChild === 0 || childrenRecursive[indexChild - 1].parent_id !== itemChild.parent_id" :rowspan="parentQuestionCounts[itemChild.parent_id]">{{ itemChild.parent.proportionMain }}%</td>
        <td>{{ typeof itemChild.content == "string" ? JSON.parse(itemChild.content).en : itemChild.content.en }}</td>
        <td>{{ itemChild.max_level || 5 }}</td>
        <td>{{ itemChild.max_score_group }}</td>
        <td>{{ itemChild.max_score }}</td>
        <td>
          <span>{{ itemChild.caculate_point }}</span>
        </td>
        <td>
          <span>{{ itemChild.note }}</span>
        </td>
      </tr>
    </template>
  </tbody>
</template>

<script>

export default {
  name: 'TrRecursive',
  props: {
    childrenRecursive: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      yourAnswers: []
    }
  },
  computed: {
    parentQuestionCounts() {
      const counts = {}
      this.childrenRecursive.forEach(question => {
        const parentId = question.parent_id
        if (parentId in counts) {
          counts[parentId]++
        } else {
          counts[parentId] = 1
        }
      })
      return counts
    }
  },
  mounted() {
    this.childrenRecursive.forEach((child) => {
      this.yourAnswers.push({
        id: child.id,
        parent_id: child.parent_id,
        your_answer: null,
        category_id: child.categories[0].id || null,
        max_level: child.max_level || 5,
        max_score: child.max_score,
        caculate_point: 0,
        note: null
      })
    })
  }
}
</script>

<style scoped>

</style>
