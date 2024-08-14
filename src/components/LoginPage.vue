<template>
    <div class="flex justify-center">
        <h1 v-t="'titles.login'" class="my-4 text-center font-bold" />
        <i class="i-fa6-solid:circle-info ml-2 mt-6 cursor-pointer" :title="$t('info.login_note')" />
    </div>
    <hr />
    <div class="w-full flex items-center justify-center text-center" data-login="">
        <form class="w-min children:pb-3">
            <div>
                <input
                    v-model="username"
                    class="input"
                    type="text"
                    autocomplete="username"
                    :placeholder="$t('login.username')"
                    :aria-label="$t('login.username')"
                    @keyup.enter="login"
                />
            </div>
            <div>
                <input
                    v-model="password"
                    class="input"
                    type="password"
                    autocomplete="password"
                    :placeholder="$t('login.password')"
                    :aria-label="$t('login.password')"
                    @keyup.enter="login"
                />
            </div>
            <div>
                <a v-t="'titles.login'" class="btn w-auto" @click="login" />
                <a v-t="'titles.register'" class="btn w-auto" href="/register" />
            </div>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            username: null,
            password: null,
        };
    },
    mounted() {
        //TODO: Add Server Side check
        if (this.getAuthToken()) {
            this.$router.push(import.meta.env.BASE_URL);
        }
    },
    activated() {
        document.title = this.$t("titles.login") + " - Fruyt";
    },
    methods: {
        login() {
            if (!this.username || !this.password) return;
            this.fetchJson(this.authApiUrl() + "/login", null, {
                method: "POST",
                body: JSON.stringify({
                    username: this.username,
                    password: this.password,
                }),
            }).then(resp => {
                if (resp.token) {
                    this.setPreference("authToken" + this.hashCode(this.authApiUrl()), resp.token);
                    window.location = import.meta.env.BASE_URL; // done to bypass cache
                } else alert(resp.error);
            });
        },
    },
};
</script>

<style>
    div[data-login] input {
        padding: 25px 20px;
        min-width: 350px;
        margin-bottom: 15px;
    }
    div[data-login] .btn {
        display: block;
        text-align: center;
        margin-bottom: 50px;
        margin-top: 10px;
        padding: 10px;
        color: #fff;
        font-weight: bold;
    }
</style>