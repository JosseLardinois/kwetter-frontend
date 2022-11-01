<script setup>
    import { RouterLink, RouterView } from 'vue-router'
    import HelloWorld from './components/HelloWorld.vue'
    import '@aws-amplify/ui-vue/styles.css';
    import { Amplify } from 'aws-amplify';
    import {
        Authenticator,
        AuthenticatorSignUpFormFields,
        // Vue Composable to get access to validation errors
        useAuthenticator,
        // Amplify UI Primitives to simplify the custom fields
        AmplifyCheckBox,
    } from '@aws-amplify/ui-vue';
    import '@aws-amplify/ui-vue/styles.css';

    import awsExports from './aws-exports';
    import { toRefs } from 'vue';
    Amplify.configure(awsExports);

    const { validationErrors } = toRefs(useAuthenticator());

    const services = {
        async validateCustomSignUp(formData) {
            if (!formData.acknowledgement) {
                return {
                    acknowledgement: 'You must agree to the Terms & Conditions',
                };
            }
        },
    };
</script>

<template>
    <header>
        <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

        <div class="wrapper">

            <nav>
                <RouterLink to="/">Home</RouterLink>
                <RouterLink to="/about">About</RouterLink>
            </nav>
        </div>
    </header>
    <authenticator initial-state="signUp" :services="services">
        <template v-slot:sign-up-fields>
            <authenticator-sign-up-form-fields />
            <amplify-check-box :errorMessage="validationErrors.acknowledgement" />
        </template>
        <template v-slot="{ user, signOut }">
            <h1>Hello {{ user.username }}!</h1>
            <button @click="signOut">Sign Out</button>
        </template>
    </authenticator>


</template>

<style scoped>
    header {
        line-height: 1.5;
        max-height: 100vh;
    }

    .logo {
        display: block;
        margin: 0 auto 2rem;
    }

    nav {
        width: 100%;
        font-size: 12px;
        text-align: center;
        margin-top: 2rem;
    }

        nav a.router-link-exact-active {
            color: var(--color-text);
        }

            nav a.router-link-exact-active:hover {
                background-color: transparent;
            }

        nav a {
            display: inline-block;
            padding: 0 1rem;
            border-left: 1px solid var(--color-border);
        }

            nav a:first-of-type {
                border: 0;
            }

    @media (min-width: 1024px) {
        header {
            display: flex;
            place-items: center;
            padding-right: calc(var(--section-gap) / 2);
        }

        .logo {
            margin: 0 2rem 0 0;
        }

        header .wrapper {
            display: flex;
            place-items: flex-start;
            flex-wrap: wrap;
        }

        nav {
            text-align: left;
            margin-left: -1rem;
            font-size: 1rem;
            padding: 1rem 0;
            margin-top: 1rem;
        }
    }
</style>
