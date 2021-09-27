<template>
    <q-img
        :title='message'
        :src='imgSrc'
        :alt='name'
        class='shadow-10'
        style="height: 400px; max-width: 400px; border-radius: 10px"
    />
    <div v-if:='name'>
      <h3 class='q-mb-sm' style='text-align: center;'>{{ name }}</h3>
      <h5 style='text-align: center'>{{ `${race} from ${origin}` }}</h5>
    </div>
</template>

<script>
export default {
  props: {
    imgSrc: String,
    name: String,
    origin: String,
    race: String

  },
  data () {
    return {
      message: 'wow!'
    }
  }
}
</script>
