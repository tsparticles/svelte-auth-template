<script>
    import { onMount } from "svelte";
    import Login from "./Login.svelte";
    import Register from "./Register.svelte";

    export let name;

    let login = false;
    let register = false;

    async function hashchange() {
        // the poor man's router!
        const path = window.location.hash.slice(1);

        if (path.startsWith('/login')) {
            login = true;
            register = false;

            window.scrollTo(0, 0);
        } else if (path.startsWith('/register')) {
            login = false;
            register = true;
        } else {
            login = false;
            register = false;
        }
    }

    onMount(hashchange);
</script>

<svelte:window on:hashchange={hashchange}/>

<main>
    {#if !login && !register}
        <h1>Hello {name}!</h1>
        <p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
        <p><a href="#/login">Login</a>&nbsp;<a href="#/register">Register</a></p>
    {:else if login}
        <Login/>
    {:else if register}
        <Register/>
    {/if}
</main>

<style>
    main {
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
    }

    h1 {
        color: #ff3e00;
        text-transform: uppercase;
        font-size: 4em;
        font-weight: 100;
    }

    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }
</style>
