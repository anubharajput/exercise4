<script>
import SignupForm from './components/SignupForm.vue';
export default {
    components: {
        SignupForm
    }
}
</script>

<template>
    <div class="container">
        <SignupForm />
    </div>
</template>

<style scoped>
.container {
    width: 50%;
    margin: auto;
    border: 10px solid rgb(226, 218, 218);
    padding: 20px;
    }
</style>
