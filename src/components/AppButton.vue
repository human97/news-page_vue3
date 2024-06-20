<script setup>
const emit = defineEmits(['click'])

const clickOnButton = () => {
    emit('click')
}
</script>

<template>
    <button
        @click="clickOnButton"
        class="button"
    >
        <slot />    
    </button>
</template>



<style lang="scss" scoped>
.button {
    padding: 16px 32px;
    background: transparent;
    border-radius: 8px;
    border: 1px solid #002DBF;
    color: #002DBF;
    font-weight: 600;
    font-size: 20px;
    cursor: pointer;

    &:hover {
        border-color: lighten(#002DBF, 30%);
        color: lighten(#002DBF, 30%);
    }
}
</style>