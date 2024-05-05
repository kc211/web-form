<template>
  <form @submit.prevent="handleSubmit">
    <label>email:</label>
    <input type="email" required v-model="email" />

    <label>password:</label>
    <input type="password" required v-model="password" />
    <div class="passwordErr">{{ passwordError }}</div>

    <label>roles:</label>
    <select name="" id="roles" v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>skills</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkills">

    <div v-for="skill in skills" :key="skill" class="pill" >
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms" />
      <label>Accept terms and conditions</label>
    </div>
    <div class="submit">
      <button>create account</button>
    </div>
    <!-- <div class="names">
      <input type="checkbox" v-model="names" value="charan">
      <label >charan</label>
    </div>
    <div class="names">
      <input type="checkbox" v-model="names" value="kranti">
      <label >kranti</label>
    </div>
    <div class="names">
      <input type="checkbox" v-model="names" value="sruthi">
      <label >sruthi</label>
    </div> -->
  </form>

  <p>email: {{ email }}</p>
  <p>password:{{ password }}</p>
  <p>role: {{ role }}</p>
  <p>terms accepted:{{ terms }}</p>
  <!-- <p>names:{{ names }}</p> -->
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "designer",
      terms: false,
      // names:[]
      tempSkill:'',
      skills:[],
      passwordError:''
    };
    
  },
  methods:{
      addSkills(e){
        if(e.key===',' && this.tempSkill)
        {
          if(!this.skills.includes(this.tempSkill))
          {
            this.skills.push(this.tempSkill);
          }
          this.tempSkill=''
        }
      },
      deleteSkill(skill){
        console.log(skill);
        
        this.skills=this.skills.filter((item)=>{
          return skill!==item
        })
      },
      handleSubmit(){
        //validation of password
        if(this.password.length<5)
        {
          this.passwordError='password must have atleast 6 characters';
        }else{
          this.passwordError='';
        }
      }
    }
};
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
input,
select {
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
.pill{
  display: inline-block;
  margin:20px 10px 0 0 ;
  padding: 6px 12px;
  background:#eee;
  border-radius:20px;
  font-size:12px;
  letter-spacing:1px;
  font-weight: bold;
  color:#777;
  cursor:pointer;
}
.submit{
  text-align: center;
}
button{
  background: #0b6dff;
  border:0;
  padding:10px 20px;
  margin-top:20px;
  color:white;
  border-radius:20px;
  cursor:pointer

}
.passwordErr{
color:#ff0062;
margin-top:10px;
font-size:0.8em;
font-weight:bold;
}
</style>