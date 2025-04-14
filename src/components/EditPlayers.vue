<template>
  <div class="edit-players">
    <h1>Редактирование игроков</h1>
    <div class="edit-form">
      <div
      v-for="(item, index) in playersList"
      :key="item.name"
      class="edit-form__row"
      >
        <label class="edit-form__label">
          Имя:
          <input id="name" class="edit-form__input" v-model="item.name">
        </label>
        <label class="edit-form__label">
          Количество жизней:
          <div class="edit-form__life-editor">
            <button class="edit-form__button" @click.prevent="changeLife(item, -1)">\/</button>
            <span>{{item.life}}</span>
            <button class="edit-form__button" @click.prevent="changeLife(item, 1)">/\</button>
          </div>
        </label>
        <button class="edit-form__delete-button" @click.prevent="delelePlayer(index)">Удалить игрока</button>
      </div>
      <!-- <button class="edit-form__save-button" @click.prevent="saveChanges()">Сохранить изменения</button> -->
    </div>
  </div>

  <div class="players-rating">
    <h2>Рейтинг</h2>
    <table>
      <tr
        v-for="(item, index) in rating"
        :key="index"
      >
        <td v-html="`${index + 1}`"></td>
        <td v-html="`У игрока <b>${item.name}</b> ${item.life} жизней`"></td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'EditPlayers',

  props: {
    players: {
      type: Array
    },
  },
  data () {
    return {
      playersList: []
    };
  },
  mounted() {
    this.copyPlayers(this.players)
  },
  computed: {
    rating () {
      let places = [...this.players];
      places.sort((a, b) => b.life - a.life);
      return places;
    }
  },
  methods: {
    changeLife (item, newValue) {
      item.life += newValue;
      this.$emit("update:players", this.playersList);
    },
    // saveChanges () {
    //   this.$emit("update:players", this.playersList);
    // },
    delelePlayer(playerIndex) {
      this.playersList.splice(playerIndex, 1)
      this.$emit("update:players", this.playersList);
    },
    copyPlayers(newValue) {
      this.playersList = newValue.map(el => ({ ...el }))
    },
  },
  watch: {
    players: {
      handler(newPlayers) {
        this.copyPlayers(newPlayers)
      },
      deep: true,
    },
  }
}
</script>

<style lang="scss" scoped>
.edit-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  justify-items: flex-start;
  &__row {
    display: flex;
    width: 100%;
    align-items: center;
    gap: 20px;
  }
  &__label {
    display: flex;
    flex-direction: column;
    gap: 5px;
  }
  &__input {
    height: 24px;
  }
  &__button {
    width: 24px;
    height: 24px;
  }
  &__life-editor {
    display: flex;
    gap: 5px;
    align-items: center;
  }
  &__delete-button {
    padding: 10px;
  }

  &__save-button {
    font-size: 16px;
    padding: 5px;
    align-self: flex-start;
  }
}

table {
  td {
    border: 1px solid #2c3e50;
    padding: 0 10px;
  }
}
</style>