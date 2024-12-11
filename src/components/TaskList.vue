<template>
  <div class="list">
    <div class="listheader">
      <p class="list-title">{{ title }}</p>
      <p class="list-counter">total: {{ totalCardInList }}</p>
      <div class="deletelist" @click="removeList">×</div>
    </div>
    <draggable group="cards" :list="cards" @end="movingCard">
      <task-card v-for="(item, index) in cards"
            :body="item.body"
            :key="item.id"
            :cardIndex="index"
            :listIndex="listIndex"
      />
    </draggable>
    <task-card-add :listIndex="listIndex" />
  </div>
</template>
<script>
import TaskCardAdd from './TaskCardAdd'
import TaskCard from './TaskCard'
import draggable from 'vuedraggable'

export default {
  components: {
    TaskCardAdd,
    TaskCard,
    draggable,
  },
  props: {
    title: {
      type: String,
      required: true
    },
    cards: {
      type: Array,
      required: true
    },
    listIndex: {
      type: Number,
      required: true
    }
  },
  computed: {
    totalCardInList() {
      return this.cards.length
    }
  },
  methods: {
    removeList: function() {
      if(confirm('本当にこのリストを削除しますか？')){
        this.$store.dispatch('removelist', { listIndex: this.listIndex })
      }
    },
    movingCard: function() {
      this.$store.dispatch('updateList', { lists: this.lists })
    }
  }
}
// ★ここまで追記
</script>

