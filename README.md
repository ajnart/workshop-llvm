# Workshop clang tools

*Ce workshop traite sur l'intégration des outils clang dans vscode. Il peut aussi vous aider à vous familiariser avec les outils qu'offrent la suite clang si vous utilisez des ides inférieurs.*

Déroulement du workshop:
 - Installation des outils nécessaires
 - Mise en place de sa propre norme à l'aide de clang-format
 - Mise en place du language server clangd avec vscode.
 - Utilisation du language server, lint et clang-tidy
 - Mise en place d'un CI pour vérifier que son code compile

 ## 1 : Installation des outils nécessaires
 ### Installation LLVM
 Tout d'abord nous allons installer clangd, à l'aide de la page [d'installation](https://clangd.llvm.org/installation.html)

*Vous pouvez vérifier l'installation à l'aide de ``clangd --version``*

 Ainsi que l'extesion vscode [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd)
 à l'aide de la commande:    ``ext install llvm-vs-code-extensions.vscode-clangd``

[![asciicast](https://asciinema.org/a/14.png)](https://asciinema.org/a/14)