
# Pourquoi savoir lire une erreur est important ? 
Savoir reconnaître un problème est très important, sinon, comment corriger un crash de quelque chose qui est important ( par exemple un bot discord de protection ).

*Si dessous, beaucoup de types d'erreurs proviendront de NodeJS*

# Quels types d'erreurs existent ?
- Error : l'erreur classique, ça vient généralement d'un problème de syntaxe ou de quelque chose que l'interpréteur n'a pas accepté ( par exemple une variable manquante utilisée ).
- uncaughtException : une vraie bête noir celle là, cette erreur coupe instantanément le code, heureusement, le message est généralement clair dans ce cas !

Vous retrouverez ce type d'erreur, ou des erreurs customisés, mais bonne nouvelle, la structure reste la même !

# Observons une erreur classique :
Pour déclencher une erreur, vous pouvez écrire ça :
```js
throw new Error("Some Bad Error");
```

Ça me donneras cette erreur :
```js
/Users/akinsella/Workspace/Projects/gtfs-playground/build/app-test.js:30
    throw new Error("Some Bad Error");
          ^
Error: Some Bad Error
    at /Users/akinsella/Workspace/Projects/gtfs-playground/build/app-test.js:30:11
    at process._tickCallback (node.js:415:13)
    at Function.Module.runMain (module.js:499:11)
    at startup (node.js:119:16)
    at node.js:901:3
Process finished with exit code 8
```

Ça fait peur hein ? Pas d'inquiétude, quand on sais la lire, c'est facile !

En premier, ici, nous avons le chemin vers le fichier où l'erreur as eu lieu, je sais donc que c'est dans app-test.js, ensuite, ça m'indique :30:11, c'est la ligne et colonne, donc mon erreur est à la ligne 30 et au 11e caractère de cette ligne !
Puis vous avez le code en lui même qui a provoqué l'erreur, ça pourrait très bien être autre chose bien sûr.
Et là, la magie opère, vous avez le nom de l'erreur ! "Some Bad Error", mais ça pourrait aussi être "Invalid value" ou "cannot access value before initialization"
Oui vous devez apprendre l'anglais, fallait écouter la prof en cours ;)
Bon trêve de plaisanterie, après tout ça, vous avez pleins de trucs bizarres, mais ce charabia vous liste d'où provient l'erreur, par exemple, ça me met mon fichier, puis le code a exécuter le fichier, puis le fichier lancer au démarrage, puis Node tout simplement, c'est très utile car parfois, nous avons des erreurs dans un module mais qui sont provoqués par notre code, et nous pouvions ainsi retrouver ce qui nous intéresse en retraçant le trajet :De

Finalement, la surprise pour certains types d'erreurs et de couper le processus, donc un bon crash, et il vous indiqueras un code, mais ici, on cherche pas à lire les code d'erreurs !

*Passage sur stackoverflow, et me revoilà avec une liste d'erreur*
Voici une erreur type :
```js
[nodemon] app crashed - waiting for file changes before starting...
[nodemon] restarting due to changes...
[nodemon] starting `node server.js`
C:\Users\Sini\Documents\SurfApp\backend\passport.js:20
  new JwtStatregy(
  ^
TypeError: JwtStatregy is not a constructor
    at Object.<anonymous> (C:\Users\Sini\Documents\SurfApp\backend\passport.js:20:3)
    at Module._compile (node:internal/modules/cjs/loader:1101:14)
    at Object.Module._extensions..js (node:internal/modules/cjs/loader:1153:10)
    at Module.load (node:internal/modules/cjs/loader:981:32)
    at Function.Module._load (node:internal/modules/cjs/loader:822:12)
    at Module.require (node:internal/modules/cjs/loader:1005:19)
    at require (node:internal/modules/cjs/helpers:102:18)
    at Object.<anonymous> (C:\Users\Sini\Documents\SurfApp\backend\routes\User.js:5:24)
    at Module._compile (node:internal/modules/cjs/loader:1101:14)
    at Object.Module._extensions..js (node:internal/modules/cjs/loader:1153:10)
[nodemon] app crashed - waiting for file changes before starting...
```
Bon ici, nous avons une "TypeError", donc une valeur qui n'est pas du bon type, mais par soucis de clarté, voici la définition de MDN :
TypeError
Crée une instance représentant une erreur se produisant quand une variable ou un paramètre n'est pas d'un type valide.
Enfin bref, l'interpréteur nous dit "JwtStrategy is not a constructor", traduction ? JwtStrategy n'est pas un constructeur, donc la méthode "new" devant doit être retiré, ce qui donnerais :
```js
 JwtStrategy()
```
Second exemple !
```js
ReferenceError: Can't find variable: Intl
```
Là, quelqu'un a oublier de définir la valeur "Intl", très classique comme erreur, ça arrive même aux meilleurs !
Dernier exemple avec Discord.js :
```js
C:\Users\hugo\Documents\Loisir\Dev\Discord_Bots\Aura-discord\bot\node_modules\discord.js\src\client\Client.js:544
      throw new TypeError('CLIENT_MISSING_INTENTS');
      ^
TypeError [CLIENT_MISSING_INTENTS]: Valid intents must be provided for the Client.
    at Client._validateOptions (C:\Users\hugo\Documents\Loisir\Dev\Discord_Bots\Aura-discord\bot\node_modules\discord.js\src\client\Client.js:544:13)
    at new Client (C:\Users\hugo\Documents\Loisir\Dev\Discord_Bots\Aura-discord\bot\node_modules\discord.js\src\client\Client.js:73:10)
    at Object.<anonymous> (C:\Users\hugo\Documents\Loisir\Dev\Discord_Bots\Aura-discord\bot\src\index.js:5:16)
    at Module._compile (node:internal/modules/cjs/loader:1101:14)
    at Object.Module._extensions..js (node:internal/modules/cjs/loader:1153:10)
    at Module.load (node:internal/modules/cjs/loader:981:32)
    at Function.Module._load (node:internal/modules/cjs/loader:822:12)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:79:12)
    at node:internal/main/run_main_module:17:47 {
  [Symbol(code)]: 'CLIENT_MISSING_INTENTS'
}
```
"Valid intents must be provided for the Client", si vous avez cet erreur et ne connaissez pas les Intents de discord.js, il va falloir lire la documentation, et une fois que vous savez comment régler ça, il faudras aller dans index.js à la ligne 5 !
# Mot de fin :
Ce ne sont que des exemples, mais gardez à l'esprit que beaucoup d'erreurs existent, et que si vous avez un problème, la documentation est votre meilleur atout !
Personnellement, je recommence MDN pour la JavaScript, ça fait très bien le travail, ils expliquent très bien en plus :D
[Vous avez une liste plus complète des erreurs ici](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Error)
