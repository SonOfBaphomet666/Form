<template>
    <div class="child-component">
        <h3>Child Component:</h3>
        <p><strong>Submitted:</strong> {{ submitted }}</p>
        <p><strong>Is Valid:</strong> {{ isValid }}</p>
    </div>
</template>

<script>
export default {
    props: {
        submitted: Boolean,
        isValid: Boolean,
    },
};
</script>

<style scoped>
.child-component {
    border: 1px solid gray;
    padding: 20px;
    margin-bottom: 20px;
}
</style>