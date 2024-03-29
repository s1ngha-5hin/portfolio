<template>
    <svg v-if="direction == 'up' || direction == 'down'" v-bind="$attrs" viewBox="0 0 12 20" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-svg icon-arrow" :class="[color ? color : '', size ? 'icon--size-' + size : '', direction ? 'icon--direction-' + direction : '']">
        <path d="M0.0667731 6.39046L0.772691 7.14227L5.48962 2.11869L5.48961 19.9507L6.5108 19.9507L6.51081 2.12343L11.2277 7.14227L11.9336 6.39046L6.00021 0.0712741L0.0667731 6.39046Z"/>
        <path fill-rule="evenodd" clip-rule="evenodd" d="M5.94909e-07 6.39008L6 3.044e-07L12 6.39008L11.2275 7.21276L6.55806 2.24441L6.55806 20L5.44194 20L5.44194 2.23975L0.772482 7.21278L5.94909e-07 6.39008ZM5.48941 2.11831L5.48941 19.9503L6.5106 19.9503L6.5106 2.12305L11.2275 7.14189L11.9334 6.39009L6 0.0708908L0.0665645 6.39008L0.772482 7.14189L5.48941 2.11831Z"/>
    </svg>
    <svg v-else v-bind="$attrs" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 12" class="icon-svg icon-arrow" :class="[color ? color : '', size ? 'icon--size-' + size : '', direction ? 'icon--direction-' + direction : '']">
        <path d="M13.6095 0.0668945L12.8577 0.772812L17.8813 5.48974H0.0493164V6.51093H17.8766L12.8577 11.2279L13.6095 11.9338L19.9287 6.00033L13.6095 0.0668945Z"/>
        <path fill-rule="evenodd" clip-rule="evenodd" d="M13.6099 0L20 6L13.6099 12L12.7872 11.2275L17.7556 6.55806H0V5.44194H17.7602L12.7872 0.772482L13.6099 0ZM17.8817 5.48941H0.0496985V6.5106H17.8769L12.8581 11.2275L13.6099 11.9334L19.9291 6L13.6099 0.0665639L12.8581 0.772482L17.8817 5.48941Z"/>
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
.icon--direction-left,
.icon--direction-down{
    transform: rotate(180deg);
}
.icon--direction-left.icon--size-default,
.icon--direction-right.icon--size-default{
    width: 18px;
}
.icon--direction-up.icon--size-default,
.icon--direction-down.icon--size-default{
    height: 18px;
}
@media (min-width:768px){
    .icon--direction-left.icon--size-default,
    .icon--direction-right.icon--size-default{
        width: 20px;
    }
    .icon--direction-up.icon--size-default,
    .icon--direction-down.icon--size-default{
        height: 20px;
    }
}
</style>
