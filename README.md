# Workshop clang tools

*Ce workshop traite sur l'intégration des outils clang dans vscode. Il peut aussi vous aider à vous familiariser avec les outils qu'offrent la suite clang si vous utilisez des IDE's inférieurs.*

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

 Ainsi que l'extesion vscode [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd)
 à l'aide de la commande *(ctrl+p)*:
 
 ``ext install llvm-vs-code-extensions vscode-clangd``

### Installation CLANG-FORMAT
Clang-format devrait être installé depuis le paquet installé dans l'étape précédente, pour le vérifier, faites: ``clang-format --version``

### Installation CLANG-TIDY
Clang-format devait également être installé.
On vérifie ça grâce à: ``clang-tidy --version``

### Installation de bear
Nous allons également installer [bear](https://github.com/rizsotto/Bear) afin de générer une base de donnée de compiliation de nos projets. Bear créera un ``compile_commands.json`` qui permettera à clangd de mieux linter votre code.

## Mise en place de sa propre norme grâce à Clang-Format
### Configuration de notre norme
Dans cette étape, nous allons générer un fichier .clang-format qui vas être utilisé pour dire à ``clang-format`` quelle forme utiliser pour linter nos fichiers.

Pour ce faire on va utiliser un [générateur en ligne](https://zed0.co.uk/clang-format-configurator/)

Sauvegardez votre .clang-format dans le dossier de ce workshop.