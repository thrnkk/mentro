<template>
  <div class="w-container">
    <div class="left-container">
      <info-holder :person="selected" />
    </div>
    <div class="right-container">
      <photo-slider :team="team" :person="selected"/>
    </div>
  </div>
</template>

<script>

import infoHolder from './components/InfoHolder.vue';
import photoSlider from './components/PhotoSlider.vue';

export default {
  name: 'App',
  components: { infoHolder, photoSlider },
  data() {
    return {
      team: [
        { id: 1, name: 'Saurav Pal', title: 'SDE-2 @Amazon', text: this.generateText(), image: require('./assets/1.png'), evaluation: 3 },
        { id: 2, name: 'Prankur Gupta', title: 'SDE @Amazon', text: this.generateText(), image: require('./assets/2.png'), evaluation: 2.5 },
        { id: 3, name: 'Saumya Singh', title: 'Software Engineer @Red Hat', text: this.generateText(), image: require('./assets/3.png'), evaluation: 4.3 },
        { id: 4, name: 'Keshav Bathla', title: 'SDE-1 @Groww', text: this.generateText(), image: require('./assets/4.png'), evaluation: 5 },
        { id: 5, name: 'Ankita', title: 'ML Engineer @Firework', text: this.generateText(), image: require('./assets/5.png'), evaluation: 1.7 },
        { id: 6, name: 'Thomas R. Reinke', linkedin: 'thrnkk', github: 'thrnkk', title: 'Software Engineer @datafrete', text: this.generateAboutMe(), image: require('./assets/thomas.png'), evaluation: 5 },
      ],
      selected: {}
    }
  },

  mounted() {
    this.selectTeamPerson(1)
  },

  methods: {
    generateText() {
      return `Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin metus felis, bibendum sit amet malesuada non, 
        fermentum in neque. Nunc malesuada augue at consectetur fringilla. Quisque sagittis placerat sem suscipit hendrerit. 
        Nulla vitae ante sollicitudin, congue arcu a, fermentum magna. Sed tincidunt massa elit, eleifend sollicitudin arcu 
        feugiat at. Ut iaculis elementum urna, vitae volutpat libero pulvinar a. Ut quis diam placerat, condimentum ex sed, 
        tincidunt lorem. Praesent viverra ligula vitae mauris eleifend, eu gravida enim malesuada.`
    },

    generateAboutMe() {
      return `
      I am a passionate and dedicated Computer Science student at Universidade Regional de Blumenau (FURB), with a strong background in full-stack development using PHP, Python and Javascript (Typescript too). <br><br>
      I am always seeking new challenges and opportunities to learn, grow, and contribute to the tech community. Feel free to connect with me to discuss potential collaborations or to exchange ideas and insights.`
    },

    selectTeamPerson(id) {
      this.selected = this.team.find(person => {
        return person.id == id
      })
    }
  }
}

</script>

<style scoped>

.w-container {
  display: flex;
  height: 730px;
  width: 1500px;
  margin: auto;
}

.left-container {
  position: relative;
  display: flex;
  align-items: flex-end;
  width: 35%;
  padding: 50px;
}

.right-container {
  position: relative;
  width: 65%;
}

</style>
