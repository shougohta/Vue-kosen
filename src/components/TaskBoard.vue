<template>
  <div>
    <header>
      my Trello
    </header>
    <main>
      <p class="info-line">All: 0 tasks</p>
      <!-- ★ここから追記 -->
      <div class="list-index">
        <TaskList v-for="(item, index) in lists"
              :key="item.id"
              :title="item.title"
              :listIndex="index"
              :cards="item.cards"
        />
        <TaskListAdd />
      </div>
    </main>
  </div>
</template>

<script>
import TaskListAdd from './TaskListAdd'
import TaskList from './TaskList'
import { mapState } from 'vuex'

export default {
  components: {
    TaskListAdd,
    TaskList,
  },
  computed: {
    ...mapState([
      'lists'
    ]),
  },
}
</script>
