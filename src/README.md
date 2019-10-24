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