<template>
  <div>
    <section v-if="destination" class="destination">
      <h1>{{ destination.name }}</h1>
      <GoBackButton />
      <div class="destination-details">
        <img :src="`/images/${destination.image}`" :alt="destination.name">
        <p>{{destination.description}}</p>
      </div>
    </section>
    <section class="experiences">
      <h2>Top experiences in {{ destination.name }}</h2>
      <div class="cards">
        <router-link
          v-for="experience in destination.experiences"
          :key="experience.slug"
          :to="{name: 'experience.show', params: {experienceSlug: experience.slug}}"
        >
          <ExperienceCard
            :experience="experience"
          />
        </router-link>
      </div>
      <router-view />
    </section>
  </div>
</template>

<script>
import sourceData from '../data.json'
import ExperienceCard from '../components/ExperienceCard.vue'
import GoBackButton from '../components/GoBackButton.vue'

export default {
  components: {ExperienceCard, GoBackButton},
  props: {
    id: {
      type: Number, required: true
    }
  },
  computed: {
    destination() {
      return sourceData.destinations.find(
        (destination) => destination.id === this.id
      )
    }
  },
}
</script>
