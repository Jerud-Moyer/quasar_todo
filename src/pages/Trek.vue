<template>
    <q-page class='q-pa-lg page'>
        <h5 class='q-mt-none'>
            Your daily Trek character!
        </h5>
        <Character
            class='absolute-center'
            :img-src='character.imageUrl'
            :name="character.name"
            :race="character.race"
            :origin='character.origin'
        />
        <q-btn
          @click='getCharacter'
          color='primary'
          icon='warning'
          label='get another!'
        />
        <q-ajax-bar
          ref='bar'
          position='bottom'
          color='indigo'
          size='10px'
        />
    </q-page>
</template>

<script>
import Character from '../components/Character.vue'
import axios from 'axios'

export default {
  components: {
    Character
  },
  data() {
    return {
      character: {
        imageUrl: String,
        name: String,
        race: String,
        origin: String
      }
    }
  },
  methods: {
    getCharacter() {
      this.character = ''
      axios.get('https://trek-dex.herokuapp.com/api/v1/characters')
        .then(json => {
          this.character = json.data[Math.floor(Math.random() * (json.data.length - 1))]
          console.log(this.character)
        })
    }
  },
  mounted() {
    this.getCharacter()
  }
}
</script>

<style lang='scss'>
  .page {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      max-height: 80vh;
  }
</style>
