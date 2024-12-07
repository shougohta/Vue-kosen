<template>
  <div>
    <header>
      my Trello
    </header>
    <main>
      <p class="info-line">total: {{ totalCardInBoard }}</p>
      <draggable :list="lists" group="lists" class="list-index" @end="movingList">
        <task-list v-for="(item, index) in lists"
              :key="item.id"
              :title="item.title"
              :listIndex="index"
              :cards="item.cards"
              @end="movingCard"
        />
        <task-list-add />
      </draggable>
    </main>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import TaskListAdd from './TaskListAdd'
import TaskList from './TaskList'
import { mapState } from 'vuex'

export default {
  components: {
    TaskListAdd,
    TaskList,
    draggable,
  },
  computed: {
    ...mapState([
      'lists'
    ]),
    totalCardInBoard() {
      return this.$store.getters.totalCardCount
    }
  },
  methods: {
    movingCard: function() {
      this.$store.dispatch('updateList', { lists: this.lists })
    },
    movingList: function() {
      this.$store.dispatch('updateList', { lists: this.lists })
    }
  }
}
</script>
