# Notes de conception 

## Démarrer avec svelte 

Bon c'est vraiment pas dur : 

    npx degit sveltejs/template my-svelte-project
    cd my-svelte-project

    npm install
    npm run dev

Et ça se passe sur localhost:5000, by the way.

## Installer Sass 

    npm install svelte-preprocess
    npm install node-sass

Dans rollup.config.js, clé plugins, ajouter : 

    preprocess: autoPreprocess()

Bien joué, sass est maintenant utilisable : 

    <style type="text/scss">
        $color:rgb(201, 15, 15);
        h1 {
            color: $color;
        }
    </style>

Encore mieux, dans un fichier style.scss : 

    <style type="text/scss">
	    @import 'style.scss';
    </style>

# Intéractions : 

Dans la partie **script** :

    let points = 100;

    const addPoint = () => (points+=1);

Dans le **rendu** :

    <button class="btn" on:click{addPoint}>+1</button>

# Conditions : 

Simple **if** :

    {#if showControls}
        <button class="btn" on:click{addPoint}>+1</button>
    {/if}

**If else** de ouf :

    {#if showControls}
        <button class="btn" on:click{addPoint}>+1</button>
    {:else}
        <p>I have no control over things.</p>
    {/if}

# Boucles : 

    {if playlers.length===0}
        <p>No players</p>
    {:else}
        {#each players as player}
            <Player name={player.name} points={player.points}>
        {/each}
    {/if}

# Passer des props : 

Comme vous pouvez le voir ci-dessous nous avons déjà passé des props : 

    <Player name={player.name} points={player.points}>

Dans le composant *Player* il faudra toutefois faire un export de ces props : 

    export let name;
    export let points;

Ne pas oublier les **données** :

    let players = [
        {
            name:"John Wick" 
            points:100
        },
        {
            name:"Sherlock Holmes",
            points:100
        }
    ]

# Components 

Les fichiers doivent avoir l'extension **.svelte** :

    import Navbar from "./Navbar.svelte";

S'utilise ainsi : 

    <Navbar/>


# Composant d'ajout

Formulaire : 

    <form on:submit={onSubmit}>
        <input type="text" placeholder="name" bind:value={player.name}>
        <input type="text" placeholder="points" bind:value={player.points}>
    </form>

Partie **script** : 

    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

    let player = {
        name:"",
        points:0
    };

    const onSubmit = (e) => {
        e.preventDefault();
        dispatch("addplayer",player);
        //reset : 
        player = {
            name:"",
            points:0
        };
    }

Dans App :

    const addPlayer = (e) => {
        //Les données à ajouter se trouvent dans detail
        const newPlayer = e.detail;
        //Ajout aux données
        players = [...players, newPlayer];
    }

    <AddPlayer on:addplayer={addPlayer}/>


# Compiler : 

    npm run build 

C'est le dossier **public** qui est compilé