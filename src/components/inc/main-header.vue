<template>
    <header class="main-header">
        <div class="main-header__inner">
            <ul class="main-header__link">
                <li>
                    <a href="tel:01021008645" class="btn btn-icon white"><icon-tel /></a>
                </li>
                <li>
                    <a href="mailto:s1nghaaa.5hin@gmail.com" target="_blank" class="btn btn-icon white"><icon-mail /></a>
                </li>
                <li>
                    <a href="https://github.com/s1ngha-5hin" target="_blank" class="btn btn-icon white"><icon-github /></a>
                </li>
            </ul>
        </div>
    </header>
</template>

<script>
import IconTel from "@/components/icons/icon-tel.vue";
import IconMail from "@/components/icons/icon-mail.vue";
import IconGithub from "@/components/icons/icon-github.vue";

export default {
    props: {
    },
    components: {
        IconTel,
        IconMail,
        IconGithub,
    },
    data() {
        return {};
    },
    mounted() {},
    methods: {},
};
</script>

<style scoped>
</style>
