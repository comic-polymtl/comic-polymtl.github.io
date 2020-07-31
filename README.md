# Site web du Comic

## Sommaire
Le site web du comité est affiché à l'adresse [comic.polymtl.ca](http://comic.polymtl.ca). Il est hébergé par le [STEP](https://infos.step.polymtl.ca/hosting). 

## Technologies

Le site est un statique HTML/CSS utilisant Bootstrap 4 de façon intensive. À l'heure actuelle, aucun JS ou PHP spécifique n'est utilisé.

## Branches

Le répo utilise deux branches:
* `dev` pour le développement et les tests.
* `master` pour la mise en prod. Cette branche n'est mise à jour que par `merge` en provenance de `dev`.

## Mise en ligne

Ajout des *remotes* du serveur d'hébergement (Nova):
* `test`: `git remote add test "ssh://comic@nova.step.polymtl.ca/home/comites/interne/comic/site/site-test.git/"`
* `prod`: `git remote add prod "ssh://comic@nova.step.polymtl.ca/home/comites/interne/comic/site/site.git/"`

Pour transférer le contenu du site d'une machine en local vers le serveur du STEP:
* `dev`: Avant de passer une modification locale en prod, celle-ci devrait être testée sur le serveur. Pour ce faire, lancer `git push test` pour déployer le site sous <http://comic.polymtl.ca/test/>, d'où il est accessible au développeur mais pas aux visiteurs.
* `master`: `git push prod`; mise en ligne directement sous <http://comic.polymtl.ca/>.

## Accès direct par le serveur Nova

Le Comic a un accès SSH/SFTP au serveur d'hébergement: `$ ssh comic@nova.step.polymtl.ca`. La racine du site y est placée sous `nova_html/`.

Le déploiement via `git push prod` est géré par un répo git *bare* situés sous `site/site.git/`. Quand la commande de déploiement est reçue, elle accroche le *post-receive hook* stocké sous `site.git/hooks/post-receive`. Ce script écrase le contenu actuel du site, et y copie le nouveau contenu.

Le déploiement des tests via `git push test` est pris en charge de la même manière par un *hook* stocké sous `site-test.git/hooks/post-receive`.

## Suggestion d'outils de dev

* Éditeur de texte: [Sublime text](https://www.sublimetext.com/) - plus adapté pour le web que les éditeurs en console ou les gros IDE.
* Plugin Sublime text: [Emmet](https://emmet.io/blog/sublime-text-3/)
