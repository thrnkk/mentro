<template>
  <div>
    <div class="circle-holder">
      <div class="circle">
        <div class="team-list">
          <ul id="list">
            <li v-for="person in team" :key="person.id">
              <img :src="person.image" :alt="person.name">
            </li>
          </ul>
        </div>
      </div>
      
      <div class="person-photo-holder">
        <div class="circular-button" @click="rotateSlider((person.id - 1) % team.length)">
          <fa-icon icon="fa-arrow-left" />
        </div>
        <transition name="fade" mode="out-in">
          <img :key="person.id" :src="person.image">
        </transition>
        <div class="circular-button" @click="rotateSlider((person.id + 1) % team.length)">
          <fa-icon icon="fa-arrow-right" />
        </div>
      </div>
      <transition name="fade" mode="out-in">
        <div :key="person.id" class="person-holder mt-5">
          <span> {{ person.name }} </span>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>

export default {
  name: 'PhotoSlider',
  props: {
    team: {
      type: Array,
      default: () => { return [] }
    },
    person: {
      type: Object,
      default: () => { return {} }
    }
  },

  data() {
    return {
      selectedIndex: this.person.id,

      allItems: null,
      allItemsAsArray: null,
      fixedPositions: {},
      transforms: {},
      auxPosition: 0,
    }
  },

  mounted() {
    this.allItems = document.getElementById('list').getElementsByTagName('li');
    this.allItemsAsArray = Array.from(this.allItems);

    this.allItemsAsArray.forEach((elem, index) => {
      this.transforms[this.auxPosition] = window.getComputedStyle(elem).transform;
      this.fixedPositions[index] = this.auxPosition++;
    });
  },

  methods: {    
    rotateSlider(id) {
      if (id == 0) {
        const [ lastPerson ] = this.team.slice(-1)
        id = lastPerson.id
      }

      let steps = this.team.length - this.fixedPositions[id - 1];
      this.allItemsAsArray.forEach((elem2, index2) => {
        this.copyTransformProp(this.transforms[this.fixedPositions[(index2 + steps) % this.team.length]], elem2);
      });

      this.$parent.selectTeamPerson(id)
    },

    copyTransformProp(sourceProperty, targetNode) {  
      targetNode.style.setProperty('transform', sourceProperty);
    },
  }
}

</script>

<style scoped>

.circle-holder {
  position: absolute;
  top: 0;
  right: 0;
  margin-top: -750px;
  margin-right: -150px;
}

.person-holder span {
  padding: 15px;
  background-color: #C5F8C7;
  font-size: 20px;
  font-weight: 700;
}

.person-photo-holder {
  margin-top: -150px;
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-items: center;
}

.person-photo-holder img {
  height: 250px;
  width: 250px;
  border-radius: 100%;
}

.circle {
  position: relative;

  background-color: #C5F8C7;
  width: 1250px;
  height: 1250px;
  border-radius: 100%;
  overflow: hidden;
}

.team-list {
  height: 700px;
  width: 700px;
  border-radius: 500px;
  background-image: url("data:image/svg+xml,%3csvg width='100%25' height='100%25' xmlns='http://www.w3.org/2000/svg'%3e%3crect width='100%25' height='100%25' fill='none' rx='500' ry='500' stroke='%230C3959FF' stroke-width='5' stroke-dasharray='4%2c 30' stroke-dashoffset='45' stroke-linecap='square'/%3e%3c/svg%3e");  position: absolute;
  bottom: 0;
  left: 0; 
  right: 0; 
  margin-left: auto; 
  margin-right: auto;

  margin-bottom: -300px;
}

.team-list > ul > li {
  display: block;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  transition: ease all 1s;
}

.team-list > ul > li img {
  border-radius: 100%;
  height: 150px;
  width: 150px;
}

.team-list > ul > :nth-of-type(1) {
  transform: translate(-50%, -50%) rotate(270deg) translate(340px) rotate(-270deg);
}

.team-list > ul > :nth-of-type(2) {
  transform: translate(-50%, -50%) rotate(330deg) translate(340px) rotate(-330deg);
}

.team-list > ul > :nth-of-type(3) {
  transform: translate(-50%, -50%) rotate(30deg) translate(340px) rotate(-30deg);
}

.team-list >ul > :nth-of-type(4) {
  transform: translate(-50%, -50%) rotate(90deg) translate(340px) rotate(-90deg);
}

.team-list > ul > :nth-of-type(5) {
  transform: translate(-50%, -50%) rotate(150deg) translate(340px) rotate(-150deg);
}

.team-list > ul > :nth-of-type(6) {
  transform: translate(-50%, -50%) rotate(210deg) translate(340px) rotate(-210deg);
}


</style>