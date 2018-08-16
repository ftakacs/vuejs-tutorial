<template>
  <div class="skills">
    <div class="img-center"><img alt="Vue logo" src="../../assets/logo.png"></div>
    <form @submit.prevent="addSkill">
      <input type="text" placeholder="Enter a skill you have.." v-model="skill" v-validate="'min:5'" name="skill">
      <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
        <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
      </transition>
      
    </form>

    <h1 v-once>{{name}}</h1>
    <div class="holder">
      <ul>
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
          <li v-for="(data, index) in skills" :key='index'>{{data.skill}}
            <i class="fa fa-minus-circle" v-on:click="remove(index)"></i>
          </li>
        </transition-group>
      </ul>
      <p v-if="skills.length > 0">Essas são as suas Skills</p>
      <p v-else>Você não possui Skills cadastradas</p>

      <div v-bind:class="{ alert: showAlert}"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data() {
    return {
      name: 'Lista de Skills',
      btnState: true,
      skill: '',
      skills: [
          
      ],
      showAlert: true
    }
  },
  methods : {
      addSkill(){
          this.$validator.validateAll().then((result) => {
          if (result) {
            this.skills.push({skill: this.skill});
            this.skill = '';
          } else {
            console.log('Not valid');
          }
        })
      },
      remove(id) {
        this.skills.splice(id, 1);
      }
  }
}
</script>

<style src="./Skills.css" scoped></style>
<!-- Add "scoped" attribute to limit CSS to this component only -->

