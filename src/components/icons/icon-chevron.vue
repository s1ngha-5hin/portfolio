<template>
    <svg v-if="direction == 'up' || direction == 'down'" v-bind="$attrs" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-svg icon-chevron" :class="[color ? color : '', size ? 'icon--size-' + size : '', direction ? 'icon--direction-' + direction : '']">
        <path fill-rule="evenodd" clip-rule="evenodd" d="M1.49982 16.2871L3.42651 18.2138L11.9998 9.64157L20.5731 18.2138L22.4998 16.2871L11.9998 5.78711L1.49982 16.2871Z" />
    </svg>
    <svg v-else v-bind="$attrs" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="icon-svg icon-chevron" :class="[color ? color : '', size ? 'icon--size-' + size : '', direction ? 'icon--direction-' + direction : '']">
        <path fill-rule="evenodd" clip-rule="evenodd" d="M16.287 22.5L18.2137 20.5733L9.64145 12L18.2137 3.42669L16.287 1.5L5.78699 12L16.287 22.5Z" />
    </svg>
</template>

<script>
export default {
    props: {
        color: { type: String, default: "" },
        size: { type: String, default: "default" },
        direction: { type: String, default: "right" },
    },
    components: {},
    data() {
        return {};
    },
    mounted() {},
    methods: {},
};
</script>

<style scoped>
.icon--direction-right,
.icon--direction-down{
    transform: rotate(180deg);
}
.icon--size-default{ 
    width: 20px;
}
@media (min-width:768px){
    .icon--size-default{
        width: 24px;
    }
}
</style>
