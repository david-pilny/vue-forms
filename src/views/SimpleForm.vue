<template>
  <div>
    <h1>Create an event</h1>
    <form @submit.prevent="sendForm">
      <BaseSelect
        v-model="event.categories"
        :options="categories"
        label="Select a category"
      />

      <fieldset>
        <legend>Name & describe your event</legend>

        <BaseInput v-model="event.title" label="Title" type="text" />

        <BaseInput
          v-model="event.description"
          label="Description"
          type="text"
          error="This input has an error!"
        />
      </fieldset>

      <fieldset>
        <legend>Where is your event?</legend>
        <BaseInput
          v-model="event.location"
          label="Location"
          type="text"
          error="This input has an error!"
        />
      </fieldset>

      <!-- <p>{{ event }}</p> -->
      <fieldset>
        <legend>Pets</legend>
        <p>Are pets allowed?</p>
        <div>
          <BaseRadioGroup
            v-model="event.pets"
            name="pets"
            :options="petOptions"
          />
        </div>
      </fieldset>

      <fieldset>
        <legend>Extras</legend>
        <div>
          <BaseCheckbox v-model="event.extras.catering" label="Catering" />
        </div>

        <div>
          <BaseCheckbox v-model="event.extras.music" label="Live music" />
        </div>
      </fieldset>

      <button class="button -fill-gradient" type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      categories: [
        'sustainability',
        'nature',
        'animal welfare',
        'housing',
        'education',
        'food',
        'community',
      ],
      event: {
        category: '',
        title: '',
        description: '',
        location: '',
        pets: 1,
        extras: {
          catering: false,
          music: false,
        },
      },
      petOptions: [
        { label: 'Yes', value: 1 },
        { label: 'No', value: 0 },
      ],
    }
  },
  methods: {
    sendForm() {
      axios
        .post(
          'https://my-json-server.typicode.com/Code-Pop/Vue-3-Forms/events',
          this.event
        )
        .then((response) => {
          console.log('Response', response)
        })
        .catch((err) => {
          console.log('Error', err)
        })
    },
  },
}
</script>

<style scoped>
fieldset {
  margin: 0;
  padding: 0;
  border: 0;
}
legend {
  font-size: 28px;
  font-weight: 700;
  margin-top: 20px;
}
</style>
