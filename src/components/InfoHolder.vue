<template>
  <div class="info-container">
    <transition name="fade" mode="out-in">
      <span :key="person.id" class="evaluation-holder">
        {{ personEvaluation }}
      </span>
    </transition>

    <transition name="fade" mode="out-in">
      <div :key="person.id" class="stars-holder">
        <span v-for="star in personStars.full" :key="star">
          <fa-icon icon="fa-solid fa-star" />
        </span>
        <span v-for="star in personStars.half" :key="star">
          <fa-icon icon="fa-solid fa-star-half-stroke" />
        </span>
        <span v-for="star in personStars.empty" :key="star">
          <fa-icon icon="fa-regular fa-star" />
        </span>
      </div>
    </transition>

    <transition name="fade" mode="out-in">
      <h2 :key="person.name"> {{ person.name }} &nbsp; </h2>
    </transition>

    <transition name="fade" mode="out-in">
      <h3 :key="person.title"> {{ person.title }} &nbsp; </h3>
    </transition>

    <transition name="fade" mode="out-in">
      <div :key="person.id" class="text">
        <span v-html="person.text"></span>
      </div>
    </transition>

    <transition name="fade" mode="out-in">
      <div :key="person.id" class="social-holder mb-4">
        <a v-if="person.linkedin" target="_blank" :href="'https://www.linkedin.com/in/' + person.linkedin" class="me-3"><fa-icon icon="fa-brands fa-linkedin" size="2x" /></a>
        <a v-if="person.linkedin" target="_blank" :href="'https://github.com/' + person.github" class="me-3"><fa-icon icon="fa-brands fa-github" size="2x" /></a>
      </div>
    </transition>

    <a href="#" class="mt-4">
      <div class="primary-button shadow">
        <span> Book a session </span>
      </div>
    </a>
  </div>
</template>

<script>

export default {
  name: 'InfoHolder',
  props: {
    person: {
      type: Object,
      default: () => { return {} }
    }
  },

  data() {
    return {}
  },

  computed: {
    personStars() {
      const response = {full: 0, half: 0, empty: 0}
      response.full = this.person.evaluation ? Math.floor(this.person.evaluation) : 0
      response.half = this.person.evaluation ? Math.ceil(this.person.evaluation) - response.full : 0
      response.empty = 5 - (response.full + response.half)

      return response
    },

    personEvaluation() {
      return this.person.evaluation ? this.person.evaluation.toFixed(1) : 0
    }
  },
}

</script>

<style lang="css" scoped>

.info-container {
  display: flex;
  justify-content: flex-end;
  align-items: flex-start;
  flex-direction: column;
}

.evaluation-holder {
  font-size: 50px;
  font-style: normal;
  font-weight: 700;
  color: #4CAF50;
}

.stars-holder {
  width: 120px;
  display: flex;
  justify-content: space-between;
  color: #4CAF50;
}

.info-container h2 {
  font-weight: 900;
  margin: 20px 0px 0px 0px;
}

.info-container h3 {
  margin: 0px;
}

.text {
  text-align: justify;
  text-justify: inter-word;
  margin: 30px 0px;
  font-size: 17px;
}

.social-holder a {
  color: #609B6C !important;
  transition: 0.2s;
}

.social-holder a:hover {
  color: #4a8055 !important;
}

</style>