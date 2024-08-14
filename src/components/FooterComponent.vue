<template>
    <footer class="mt-10 w-full rounded-xl py-4 text-center children:(mx-3)">
        <a aria-label="telegram" href="https://t.me/madseller" target="_blank">
            <i class="i-fa6-brands:telegram" />
            <span class="ml-2" />
        </a>
    </footer>
</template>

<script>
// export default {
//     data() {
//         return {
//             donationHref: null,
//             statusPageHref: null,
//             privacyPolicyHref: null,
//         };
//     },
//     mounted() {
//         this.fetchConfig();
//     },
//     methods: {
//         async fetchConfig() {
//             this.fetchJson(this.apiUrl() + "/config").then(config => {
//                 this.donationHref = config?.donationUrl;
//                 this.statusPageHref = config?.statusPageUrl;
//                 this.privacyPolicyHref = config?.privacyPolicyUrl;
//             });
//         },
//     },
// };
</script>

<style>
footer {
    @apply bg-light-900;
}
.dark footer {
    @apply bg-dark-800;
}
</style>
