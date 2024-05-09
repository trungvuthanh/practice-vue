<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addSkill">
        <validation-provider v-slot="{ errors }" rules="min:5">
          <input v-model="skill" type="text" placeholder="Enter a skill you have.." name="skill">
          <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
            <p v-if="errors.length" class="alert">
              {{ errors[0] }}
            </p>
          </transition>
        </validation-provider>
      </form>

      <ul>
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
          <li v-for="item in skills" :key="item.id">
            {{ item.skill }}
            <i class="fa fa-minus-circle" @click="remove(item.id)" />
          </li>
        </transition-group>
      </ul>

      <p>These are the skills that you possess.</p>
    </div>
  </div>
</template>

<script>
import { ValidationProvider, extend, validate } from 'vee-validate'

extend('min', {
  validate (value, args) {
    return value.length >= args.length
  },
  params: ['length'],
  message: 'The {_field_} field must be at least {length} characters.'
})

export default {
  name: 'SkillsPage',
  components: {
    ValidationProvider
  },
  data () {
    return {
      skill: '',
      skills: [
        {
          id: 0,
          skill: 'Vue.js'
        },
        {
          id: 1,
          skill: 'Frontend Developer'
        }
      ]
    }
  },
  methods: {
    addSkill () {
      validate(this.skill, 'min:5').then((value) => {
        if (value.valid) {
          this.skills.push({
            id: this.skills.length,
            skill: this.skill
          })
          this.skill = ''
        } else {
          console.log('"' + this.skill + '" is not valid')
        }
      })
    },
    remove (id) {
      this.skills.splice(id, 1)
    }
  }
}
</script>

<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";

.holder {
  background: #fff;
}

ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

ul li {
  padding: 20px;
  font-size: 1.3em;
  background-color: #E0EDF4;
  border-left: 5px solid #3EB3F6;
  margin-bottom: 2px;
  color: #3E5252;
}

p {
  text-align:center;
  padding: 30px 200px;
  color: gray;
}

input {
  width: calc(100% - 40px);
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  background-color: #323333;
  color: #687F7F;
}
.alert {
  background: #fdf2ce;
  font-weight: bold;
  display: inline-block;
  padding: 5px;
  margin-top: -20px;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}

i {
  float:right;
  cursor:pointer;
}

</style>
