<script setup>
    import { onBeforeRouteUpdate, RouterLink, RouterView } from 'vue-router'
    import HomePage from './views/HomePage.vue'
    import SideBar from './components/SideBar.vue'
    import { onMounted } from 'vue'
    import router from './router'
    import NoAccess from './views/NoAccess.vue'

    import { toRefs } from 'vue';
    
    let isAuthenticated  = isAuth();
    onMounted(() => {
        let currentUrl = window.location.href;
        const token = currentUrl.split(/[\&=/]/);
        setLocalVariables(token);
        checktoken();
    })

    function checktoken(){
        let currentUrl = window.location.href;
        const token = currentUrl.split(/[\&=/]/);
        if(isTokenValid(token) ==  true){
            if(isAuth(token) == true){
                console.log('valid token')
                setLocalVariables(token);
                return true
            }
        }
        else{
            console.log('invalid token')
           // localStorage.clear();
            router.push('noaccess') 
        }        
    }

    function isTokenValid(token){
        if (token[6] == null || token[6] == undefined || token[6] == ''){
            return false;
        }
        else{
            return true;
        }

    }

    function isAuth(token){
        if (localStorage.accesstoken) {
            const jwtPayload = parsesJwt(localStorage.accesstoken);
            //console.log(localStorage.accesstoken);
            if (jwtPayload.exp < Date.now()/1000) {
                // token expired
                //deleteTokenFromLocalStorage();
                return false;
            }
            console.log('true');
            return true;
        } else {
            console.log('false');
            return false;
        }
    }
    function parsesJwt(token) { //if jwt token is valid do this
        try{
            var base64Url = token.split('.')[1];
        var base64 = base64Url.replace(/-/g, '+').replace(/_/g, '/');
        var jsonPayload = decodeURIComponent(window.atob(base64).split('').map(function(c) {
            return '%' + ('00' + c.charCodeAt(0).toString(16)).slice(-2);
        }).join(''));
    return JSON.parse(jsonPayload);
        } catch{
            return false;
        }
        
        }
    

    function setLocalVariables(token) {
        if(isTokenValid(token)){
            localStorage.setItem("accesstoken", token[6]);
            var json = parsesJwt(token[6])
            localStorage.setItem("username", json.username);
            localStorage.setItem("userId", json.sub);
            localStorage.setItem("role", json["cognito:groups"])
        }
        else{
            console.log('invalid token')
        }


    }
</script>

<template>
            <SideBar v-if="isAuthenticated"></SideBar> <!-- Hier is de error in-->
            <div class="test">
                <Suspense>
                <HomePage v-if="isAuthenticated" />
                <NoAccess v-else />
            </Suspense>

            </div>

</template>

<style scoped>
    .test {
        width: 100px;
        height: 100px;
        position: absolute;
        top: 0;
        bottom: 0px;
        left: 0;
        right: 0;
        margin: auto;
    }
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
