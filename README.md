# Workshop clang tools

*Ce workshop traite sur l'intégration des outils clang dans vscode. Il peut quand même vous aider à vous familiariser avec les outils qu'offrent la suite clang si vous utilisez un IDE différent.*

**N'hésitez pas à star ⭐ le repo si vous avez aimé ce workshop!**

![](https://img.shields.io/github/stars/ajnart/workshop-llvm?label=%E2%AD%90&style=for-the-badge?branch=master&kill_cache=1")

Déroulement du workshop:
 - Installation des outils nécessaires
 - Mise en place de sa propre norme à l'aide de clang-format
 - Mise en place du language server clangd avec vscode.
 - Utilisation du language server, lint et clang-tidy
 - Mise en place d'un CI pour vérifier que son code compile

## 0 : Mise en place du workshop en local

```sh
git clone git@github.com:ajnart/workshop-llvm.git workshop
cd workshop
```

 ## 1 : Installation des outils nécessaires
 ### Installation CLANGD
 Tout d'abord nous allons installer clangd, à l'aide de la page [d'installation](https://clangd.llvm.org/installation.html)

*Vous pouvez vérifier l'installation à l'aide de ``clangd --version``*

 Ainsi que l'extension vscode [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd) ou de [l'extension pour votre IDE](https://clangd.llvm.org/installation.html)
 à l'aide de la commande *(ctrl+p)*:
 
 ``ext install llvm-vs-code-extensions vscode-clangd``

### Installation CLANG-FORMAT
Clang-format devrait être installé depuis le paquet installé dans l'étape précédente, pour le vérifier, faites: ``clang-format --version``

### Installation CLANG-TIDY
Clang-format devait également être installé.
On vérifie ça grâce à: ``clang-tidy --version``

### Installation de Bear
Nous allons également installer [B-ear](https://github.com/rizsotto/Bear) afin de générer une base de donnée de compilation de nos projets. Bear créera un ``compile_commands.json`` qui permettra à clangd de mieux linter votre code.


### Recommandations
L'extension clangd recommande de désinstaller l'extension C/C++ pour ne pas avoir de duplications de recommandations

## Mise en place de sa propre norme grâce à Clang-Format
### Configuration de la norme
Dans cette étape, nous allons générer un fichier .clang-format qui va être utilisé pour dire à ``clang-format`` quelle norme utiliser pour linter vos fichiers.

Pour se faire, utilisez un [générateur en ligne](https://zed0.co.uk/clang-format-configurator/)

Sauvegardez votre .clang-format dans le dossier de ce workshop.

Clang-format va chercher le fichier .clang-format le plus proche du current working directory en remontant récursivement dans vos fichiers.

### Installation de la norme

Maintenant, faites en sorte que l'extension clangd soit le formateur de code par défaut dans vscode:

> *ctrl+p format document with...*

> ![formatter](/assets/formatter.gif)

ou alors en éditant son fichier *settings.json*:

```json
"[cpp]": {
        "editor.defaultFormatter": "llvm-vs-code-extensions.vscode-clangd"
    },
```
Vous devriez maintenant être en mesure de formater votre code à l'aide de votre config .clang-format

## Mise en place du language server Clangd

### Vérification du fonctionnement de clangd

⚠  **Il faut faire la commande `bear -- \build command\` pour créer la base de donnée de compilation pour clangd**.
Dans notre exemple : ``bear -- make`` générera un fichier ``compile_commands.json`` qui sera ensuite utilisé pour linter vos fichiers.

En mettant votre curseur sur la fonction divide, clangd devrait vous montrer le prototype de la fonction
> ![clang](assets/clang.png)

## Clang-tidy
### Mise en place de clang-tidy
Nous allons maintenant configurer clang-tidy pour avoir des recommandations sur notre code.

Créer un fichier ``.clang-tidy`` contenant:

```yaml
Checks: "
    *,
    -fuchsia*,
"
```

Cette configuration active tout les checks par défaut, il faut ensuite désactiver manuellement certains checks à la main en rajoutant une ligne sous la forme:  ``-\glob\,``

Pour voir tout les checks disponibles, rendez vous [ici](https://clang.llvm.org/extra/clang-tidy/checks/list.html)

## Utilisation du language server et de clang-tidy

Comme vous pouvez le voir sur le gif ci-dessous, grâce à clangd il est très facile de régler les erreurs basiques dans votre code :

> ![jitsu](assets/vscodejitsu.gif)

En fonction de votre configuration clang-tidyn vous aurez des recommendations affichées dans l'onglet *problems* en bas de la fenêtre vscode:

> ![code](assets/tidy-fix.png)


## Mise en place d'un CI pour vérifier que son code compile
Nous allons maintenant s'intéresser au dossier ``.github`` pour rajouter des workflows grâce aux [github actions](https://github.com/features/actions)

Tout d'abord, créer un fichier `CI.yml` pour créer une action il faut que cette action:

- S'active quand il y a des pushs sur master
- Contienne un job build qui:
    - Utilise le [docker epitech](https://github.com/Epitech/epitest-docker)
    - Contient une step qui:
        -  Réalise votre commande de build

Cette action va maintenant lancer un docker utilisant l'image docker epitech 

*L'indentation de cette liste correspond à l'indentation que vous aurez dans votre fichier yml* 😉

- - - 
J'espère que mon workshop vous a plu. Si vous voulez aller plus loin vous pouvez:
- Mettre en place une action pour vérifier que son code est conforme à sa propre norme
- Faire une action pour vérifier que les tests passent
- Utiliser --html sur gcovr pour créer un fichier .html indiquant le coverage 
- Uploader le .html généré par gcovr dans une [github pages](https://pages.github.com/)
 - Utiliser un [analyseur de code sémantique](https://www.deepcode.ai/) 
 - Transformer le résultat de ses [tests gtest en HTML](https://gitlab.uni-koblenz.de/agrt/gtest2html)



 *Made with ❤ by [Thomas "Ajnart" Camlong](https://github.com/ajnart)*
