<script>
export default{
props:['userData']
}
</script>
<template>
<div class="account-details-container">
     <div class="email-details"><span>Email:</span>{{ userData.email }}</div>
     <div class="password-details"><span>Password:</span>{{ userData.password }}</div>
     <div class="role-details"><span>Role:</span>{{ userData.role }}</div>
     <div class="skills-details" v-if="userData.skills"><span>Skills:</span><div v-for="(skill, index) in userData.skills" class="skill">
              <span v-if="index!==0">,</span>  {{ skill }} 
     </div></div>
</div>
</template>
<style scoped>
.account-details-container{
    width: 50%;
    margin: auto;
    border: 10px solid rgb(226, 218, 218);
    padding: 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    gap:6px;
}
.account-details-container span{
    font-size: 17px;
    font-weight: 550;
}
.account-details-container .skills-details .skill{
    display: inline;
}
</style>