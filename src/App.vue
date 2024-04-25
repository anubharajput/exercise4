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
    display: flex;
    flex-direction: column;
    gap:20px;
    }
</style>
