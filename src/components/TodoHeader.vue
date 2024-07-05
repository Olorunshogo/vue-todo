
<script setup>
import { RouterLink } from 'vue-router';


</script>




<template>
    <div>
        <header>
            <nav class="container">
                <div class="branding">
                    <img src="../assets/logo.svg" alt="Vue Logo">
                    <h1>Vue Todos</h1>
                </div>
                <ul class="nav-routes">
                    <RouterLink class="routerLink" to="/">Todos</RouterLink>
                    <RouterLink class="routerLink" to="/about">About</RouterLink>
                </ul>
            </nav>
        </header>
    </div>
</template>

<style lang="scss" scoped>
    header {
        background-color: #f1f1f1;
        nav {
            display: flex;
            flex-direction: row;
            justify-content: space-between;
            align-items: center;
            padding: 25px 16px;
            flex: 0 0 100%;
            max-width: 100%;
            .branding {
                display: flex;
                flex-direction: row;
                align-items: center;
                flex: 0 0 50%;
                max-width: 50%;
                gap: 8px;
                img {
                    max-width: 50px;
                    height: auto;
                }
                h1 {
                    font-size: 24px;
                }
            }
            .nav-routes {
                display: flex;
                flex-direction: row;
                flex: 0 0 50%;
                max-width: 50%;
                flex: 1;
                justify-content: flex-end;
                gap: 12px;
                list-style-type: none;
                a {
                    text-decoration: none;
                    color: inherit;
                }
            }
        }
    }

    .routerLink {
        transition: all 0.1s ease-in-out;
        &:hover {
            text-decoration: underline;
            font-weight: bold;
        }
    }
</style>
    

    