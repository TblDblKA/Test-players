<template>
  <div class="create-player">
    <h1 class="create-player__title">Добавить нового игрока</h1>
    <CreatePlayerError
      :messages="errorsList"
    />
    <form
      class="create-player__form"
      @submit.prevent="createPlayer"
    >
      <label class="create-player__label">
        Имя:
        <input
          type="text"
          v-model="player.name"
          class="create-player__input"
          @input="errorsList = []"
        />
      </label>
      <label class="create-player__label">
        Количество жизней:
        <input
          type="number"
          v-model="player.life"
          class="create-player__input"
          @input="errorsList = []"
        />
      </label>
      <button
        type="submit"
        class="create-player__submit"
      >
        Создать
      </button>
    </form>
  </div>
</template>

<script>
import CreatePlayerError from './CreatePlayerError.vue'
export default {
  name: 'CreatePlayer',
  components: {
    CreatePlayerError,
  },
  data() {
    return {
      player: {
        name: '',
        life: '',
      },
      errorsList: []
    };
  },
  emits: ['add-player'],
  methods: {
    validatePlayer() {
      let isValid = true
      if (this.player.name === '' || this.player.name === undefined) {
        this.errorsList.push('Укажите имя');
        isValid = false;
      }

      if (this.player.life === '' || this.player.life === undefined) {
        this.errorsList.push('Укажите количество жизней');
        isValid = false;
      }
      else if (this.player.life <= 0) {
        this.errorsList.push('Значение не может быть меньше нуля');
        isValid = false;
      }
      return isValid;
    },
    createPlayer() {
      const isValid = this.validatePlayer();
      if (!isValid) return;
      const newPlayer = { ...this.player };
      this.$emit('add-player', newPlayer);
      this.player.name = '';
      this.player.life = '';
    },
  },
};
</script>

<style lang="scss">
.create-player {
  padding: 24px;
  max-width: 400px;
  margin: 0 auto;
  border-radius: 8px;

  &__form {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  &__label {
    display: flex;
    flex-direction: column;
    gap: 5px;
  }
  &__input {
    padding: 8px;
    border: 1px solid #ccc;
  }

  &__submit {
    background-color: #444;
    color: white;
    border: none;
    padding: 10px;
    font-size: 16px;
    cursor: pointer;
  }
  &__submit:hover {
    background-color: #333;
  }
}
</style>
