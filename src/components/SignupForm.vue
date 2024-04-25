<script>
import UserDetails from './UserDetails.vue';
export default {
    data() {
        return {
            selectedRole: "",
            userData: { email: "", password: "", role: "", skills: [], termsAccepted: false, ischecked: false },
            newSkill: '',
            validateDetails: false,
            termsAccepted: false,
            showPassword: false,
            emailErrorMessage: null,
            passwordErrorMessage: null,
            roleErrorMessage: null,
            skillErrorMessage: null,
            termErrorMessage: null,
            ischecked: false,
            errorcheck: false,
            showUserData: false,
            editIndex:null
        }
    },
    methods: {
        addSkill() {
            if(this.editIndex){
                this.userData.skills.splice(index, 1, this.newSkill.trim());
                this.newSkill = '';
                 this.validateSkill();
                 this.editIndex=null;
            }else if (this.newSkill.trim() !== '') {
                    this.userData.skills.push(this.newSkill.trim());
                    this.newSkill = '';
                    this.validateSkill();
            }
        },
        removeSkill(index) {
            this.userData.skills.splice(index, 1);
            this.validateSkill();
        },
        editSkill(index) {
            this.newSkill=this.userData.skills[index];
            this.editIndex=index;
        },
        checkComma(event) {
            if (event.keyCode === 188 || event.key === "Enter") {
                console.log("cvbn");
                event.preventDefault();
                this.addSkill();
            }
        },
        validateForm() {
            console.log("xcvbnm")
            // e.preventDefault();
            this.errorCheck = true;
            this.validateEmail();
            this.validatePassword();
            this.validateRole();
            this.validateSkill();
            this.validateTerms();
            if (
                this.emailErrorMessage === null &&
                this.passwordErrorMessage === null &&
                this.roleErrorMessage === null &&
                this.skillErrorMessage === null &&
                this.termErrorMessage === null
            ) {
                this.validateDetails = true;
                this.errorCheck = false;
            }

        },
        validateEmail() {
            if (this.userData.email === "")
                this.emailErrorMessage = "Email is required"
            else if (!this.validateEmailRegex(this.userData.email))
                this.emailErrorMessage = "Please enter a valid email"
            else
                this.emailErrorMessage = null;
        },
        validatePassword() {
            if (this.userData.password === "")
                this.passwordErrorMessage = "Password is Required"
            else if (!this.validatePasswordRegex(this.userData.password)) {
                this.passwordErrorMessage = "min 8 letters, at least a special Character, upper and lower case letters and a number"
            } else
                this.passwordErrorMessage = null;
        },
        validateRole() {
            if (this.userData.role === "")
                this.roleErrorMessage = "Please select a role"
            else
                this.roleErrorMessage = null;
        },
        validateSkill() {
            if (this.userData.skills.length === 0) {
                this.skillErrorMessage = "Please add minimum one skill";
            } else {
                this.skillErrorMessage = null;
            }
        },
        validateTerms() {
            if (!this.userData.ischecked)
                this.termErrorMessage = "Please accept Terms and Conditions";
            else
                this.termErrorMessage = null
        },
        validateEmailRegex(email) {
            return String(email)
                .toLowerCase()
                .match(
                    /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|.(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
                );
        },
        validatePasswordRegex(password) {
            const regex = /^(?=.*\d)(?=.*[!@#$%^&])(?=.*[a-z])(?=.*[A-Z]).{8,}$/;
            return regex.test(password);
        },
        validateOnChange(event) {
            if (this.errorCheck) {
                this.validateForm(event);
            }
        },
        userValidatedetails() {
            // e.preventDefault();
            console.log("fg");
            if (this.validateDetails)
                this.showUserData = true;
        }
    },
    components: {
        UserDetails
    }
    , updated() {

    }
}
</script>
<template>
    <form class="input-feilds" @input="validateOnChange()">
        <label for="email">EMAIL:</label>
        <input type="text" name="" id="email" v-model="userData.email">
        <div v-if="emailErrorMessage" class="error">
            {{ emailErrorMessage }}
        </div>
        <label for="password">PASSWORD:</label>
        <input :type="showPassword ? 'text' : 'password'" id="password" v-model="userData.password">
        <div v-if="passwordErrorMessage" class="error">{{ passwordErrorMessage }}</div>
        <div><input type="checkbox" id="checkbox" @click="showPassword = !showPassword">Show Password</div>
        <label for="role">SELECT ROLE:</label>
        <select id="role" v-model="userData.role" @change="validateOnChange">
            <option value="web-developer">Web Developer</option>
            <option value="web-designer">Web Designer</option>
        </select>
        <div v-if="roleErrorMessage" class="error">{{ roleErrorMessage }}</div>
        <label for="skills">SKILLS:</label>
        <input type="text" id="skills" v-model="newSkill" @keydown="checkComma">
        <ul>
            <li v-for="(skill, index) in userData.skills" :key="index" @click="editSkill(index)">
                {{ skill }} <span @click="removeSkill(index)" class="delete">x</span>
            </li>
        </ul>
        <div v-if="skillErrorMessage" class="error">{{ skillErrorMessage }}</div>

        <label for="terms">
            <input type="checkbox" id="terms" v-model="termsAccepted" @click="userData.ischecked = !userData.ischecked">
            I ACCEPT TERMS AND CONDITIONS
        </label>
        <div v-if="termErrorMessage" class="error">{{ termErrorMessage }}</div>
        <button @click="(e) => { e.preventDefault(); validateForm(); userValidatedetails(); }">Create an
            Account</button>

    </form>
    <UserDetails v-if="showUserData" :userData="userData" />
</template>
<style scoped>
.input-feilds {
    display: flex;
    flex-direction: column;
    gap: 15px;
    width: 50%;
    margin: auto;
    border: 10px solid rgb(226, 218, 218);
    padding: 20px;
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

ul li .delete {
    color: red;
    size: 10px;
    font-weight: bold;
    font-family: sans-serif;
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

.error {
    color: red;
}
</style>