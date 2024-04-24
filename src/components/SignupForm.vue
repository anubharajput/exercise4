<script>
export default {
    data() {
        return {
            selectedRole: "",
            newSkill: '',
            skills: [],
            termsAccepted: false,
            password: "",
            showPassword: false,
            email:""
        }
    },
    methods: {
        addSkill() {
            if (this.newSkill.trim() !== '') {
                this.skills.push(this.newSkill.trim());
                this.newSkill = '';
            }
        },
        removeSkill(index) {
            this.skills.splice(index, 1);
        },
        checkComma(event) {
            if (event.keyCode === 188 || event.key == "Enter") {
                event.preventDefault();
                this.addSkill();
            }
        },
        validateForm() {
            this.validatePassword();
            this.validateEmail();
        },
        viewPassword() {
            this.showPassword = !this.showPassword;
        },
        validateEmail(){
         if(/\S+@\S+\.\S+/.test(this.email))
         console.log("Zxcvbnm,.")
        },
        validatePassword() {
            console.log(this.password)
            const regex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/;
            if (!regex.test(this.password)) {
                console.log("oh");
            } else {
                console.log('Password is valid');
            }
        }
    },
}
</script>
<template>
    <div class="input-feilds">
        <label for="email" >EMAIL:</label>
        <input type="text" name="" id="email" v-model="email">
        <label for="password">PASSWORD:</label>
        <input :type="showPassword ? 'text' : 'password'" id="password" v-model="password">
        <div><input type="checkbox" id="checkbox" @click="viewPassword">Show Password</div>
        <label for="role">SELECT ROLE:</label>
        <select id="role" v-model="selectedRole">
            <option value="web-developer">Web Developer</option>
            <option value="web-designer">Web Designer</option>
        </select>
        <p>You selected: {{ selectedRole }}</p>
        <label for="skills">SKILLS:</label>
        <input type="text" id="skills" v-model="newSkill" @keydown="checkComma">
        <ul>
            <li v-for="(skill, index) in skills" :key="index" @click="removeSkill(index)">
                {{ skill }}
            </li>
        </ul>

        <label for="terms">
            <input type="checkbox" id="terms" v-model="termsAccepted">
            I accept the terms
        </label>
        <button @click="validateForm">Create an Account</button>
    </div>
</template>
<style scoped>
.input-feilds {
    display: flex;
    flex-direction: column;
    gap: 15px;
}

#email,
#password,
#role,
#skills {
    border: none;
    border-bottom: 1px solid gray;
    outline: none;
    padding: 10px;
}

#role {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

ul {
    list-style: none;
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
}

ul li {
    padding: 9px 12px;
    background-color: rgb(232, 232, 232);
    border-radius: 15px;
    cursor: pointer;
}

button {
    background-color: rgb(7, 7, 228);
    color: white;
    margin: auto;
    padding: 10px;
    border-radius: 15px;
    border: none;
    font-size: 15px;
    font-family: bold;
    cursor: pointer;
}

button:hover {
    background-color: rgb(74, 74, 244);
}

label {
    font-family: sans-serif;
    font-size: 13px;
    font-weight: 600;
    color: rgb(76, 76, 76)
}
</style>