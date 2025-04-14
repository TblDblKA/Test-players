<template>
  <header class="tab__header">
    <button
      v-for="tab in tabs"
      :key="tab.id"
      :class="[
        'tab__button',
        { 'tab__button_active': currentTab === tab.id }
      ]"
      @click="currentTab = tab.id"
    >{{ tab.name }}</button>
  </header>
  <CreatePlayer v-if="currentTab === 'create'" @add-player="addPlayer" />
  <EditPlayers v-else v-model:players="playersList" />
</template>

<script>
import CreatePlayer from './components/CreatePlayer.vue'
import EditPlayers from './components/EditPlayers.vue'

export default {
  name: 'App',
  components: {
    CreatePlayer,
    EditPlayers
  },
  data() {
    return {
      playersList: [],
      tabs: [
        {
          id: 'create',
          name: 'Создание',
        },
        {
          id: 'edit',
          name: 'Редактирование',
        },
      ],
      currentTab: 'create',
    }
  },

  methods: {
    addPlayer(player) {
      this.playersList.push(player);
    }
  },
}
</script>

<style lang="scss" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  width: 600px;
}
.tab {
  &__header {
    text-align: left;
  }
  &__button {
    font-size: 14px;
    padding: 10px;
    cursor: pointer;
    border: 1px solid #ccc;
    border-radius: 3px;;

    &_active {
      background-color: #ccc;
    }
  }
}
</style>
