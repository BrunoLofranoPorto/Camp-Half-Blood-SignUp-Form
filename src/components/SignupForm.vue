<template>
  <form @submit.prevent="handleSubmit">
      <label>Name: </label>
      <input type="text" required v-model="name">

      <label>Godly Parent:</label>
      <input type="text" v-model="godlyParent" required>
      
      <label>E-mail:</label>
      <input type="email" required v-model="email">

      <label>Password:</label>
      <input type="password" required v-model="password">
      <div v-if="passwordError" class="error">{{ passwordError }}</div>

      <label>Role:</label>
      <select v-model="role">
          <option value="archery">Archery instructor</option>
          <option value="chariot">Chariot-Riding instructor</option>
          <option value="fencing">Fencing instructor</option>
          <option value="canoeing">Canoeing instructor</option>
          <option value="war-games">War games coordinator</option>
      </select> 

      <label>Skills:</label>
      <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
      <div v-for="skill in skills" :key="skill" class="pill" >
          <span @click="removeSkill(skill)">{{ skill }}</span>
      </div>
        <p class="obs">*Press the alt key and type a coma to register each skill</p>
        <p class="obs">*Click on a skill to remove it from the list</p>
      
      <div class="terms">
          <input type="checkbox" v-model="terms" required>
          <label>Accept terms and conditions</label>
      </div>


      <div class="submit">
          <button>Create an Account</button>
      </div>
     
      
    </form>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: '',
            terms: false,
            tempSkill: '',
            skills: [],
            godlyParent: '',
            name: '',
            passwordError: ''
        }
    },
    methods: {
        addSkill(e) {
            if (e.key === ',' && this.tempSkill) {
                if (!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill)
                } 
                this.tempSkill = ''
            }
        },
        removeSkill(skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit() {
            //validate password
            this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 characters long'

            if(!this.passwordError) {
                console.log('name: ', this.name)
                console.log('Godly parent: ', this.godlyParent)
                console.log('email: ', this.email)
                console.log('password: ', this.password)
                console.log('role: ', this.role)
                console.log('skills: ', this.skills)
                console.log('terms accepted: ', this.terms)
            }
        }
    }
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input, select {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"] {
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }
    .pill {
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background: #eee;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
    }
    button {
        background: #0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
        cursor: pointer;
    } 
    .submit {
        text-align: center;
    }
    .error {
        color: #ff0000;
        margin-top: 10px;
        font-size: 0.8em;
        font-weight: bold;
    }
    .obs {
        font-size: 0.8em;
        color: #aaa;
    }
</style>