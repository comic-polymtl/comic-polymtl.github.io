# Site web du Comic

## Sommaire
Le site web du comité est affiché à l'adresse [comic.polymtl.ca](http://comic.polymtl.ca). <s>Il est hébergé par le [STEP](https://infos.step.polymtl.ca/hosting).</s> Le serveur du STEP a été mis hors-ligne suite à une attaque en Nov. 2020. Notre site est donc temporairement hébergé sur [Github Pages](https://guides.github.com/features/pages/) en attendant qu'ils remettent un serveur web en ligne. Quand ils l'auront fait nous pourrons y migrer le site.

## Technologies

Le site est un statique HTML/CSS utilisant Bootstrap 4 de façon intensive. À l'heure actuelle, aucun JS ou PHP spécifique n'est utilisé.

## Branches

Le répo utilise deux branches:
* `dev` pour le développement et les tests.
* `master` pour la mise en prod. Cette branche n'est mise à jour que par `merge` en provenance de `dev`.

## Mise en ligne

Clônage du répo (Gitlab):
* `git clone "https://git.step.polymtl.ca/comic/site-comic"`

Ajout du *remotes* du serveur d'hébergement (Github pages):
* `temp`: `git remote add temp "https://github.com/comic-polymtl/comic-polymtl.github.io"`
* S'ajouter comme collaborateur à partir du compte [comic-polymtl](https://github.com/comic-polymtl/) dans les [réglages du répo Github](https://github.com/comic-polymtl/comic-polymtl.github.io/settings/access?query=)

Pour transférer le contenu du site de la machine locale vers l'environnement de production:
* `git push`; mise-à-jour du répo Gitlab
* `master`: `git push temp`; mise en ligne directement sous <http://comic.polymtl.ca/>

NB: Le serveur peut prendre un moment avant de réfléter tout les changements après une mise en prod. Le versionnage se fait sur le répo Gitlab; tandis que le remote Github ne sert que d'environnement de production.
<s>

Ajout des *remotes* du serveur d'hébergement (Nova):
* `test`: `git remote add test "ssh://comic@nova.step.polymtl.ca/home/comites/interne/comic/site/site-test.git/"`
* `prod`: `git remote add prod "ssh://comic@nova.step.polymtl.ca/home/comites/interne/comic/site/site.git/"`

Pour transférer le contenu du site d'une machine en local vers le serveur du STEP:
* `dev`: Avant de passer une modification locale en prod, celle-ci devrait être testée sur le serveur. Pour ce faire, lancer `git push test` pour déployer le site sous <http://comic.polymtl.ca/test/>, d'où il est accessible au développeur mais pas aux visiteurs.
* `master`: `git push prod`; mise en ligne directement sous <http://comic.polymtl.ca/>.

NB: Le serveur peut prendre un moment avant de réfléter tout les changements après une mise en prod. Il a notamment tendance à refléter les changements au HTML sans prendre en compte les changements au CSS, ce qui peut faire croire à des problèmes dûs au code. Il corrige généralement ce défaut au bout d'un quart d'heure. Si le problème semble persister, vider la cache du navigateur.

## Accès direct par le serveur Nova

Le Comic a un accès SSH/SFTP au serveur d'hébergement: `$ ssh comic@nova.step.polymtl.ca`. La racine du site y est placée sous `nova_html/`.

Le déploiement via `git push prod` est géré par un répo git *bare* situés sous `site/site.git/`. Quand la commande de déploiement est reçue, elle accroche le *post-receive hook* stocké sous `site.git/hooks/post-receive`. Ce script écrase le contenu actuel du site, et y copie le nouveau contenu.

Le déploiement des tests via `git push test` est pris en charge de la même manière par un *hook* stocké sous `site-test.git/hooks/post-receive`.
</s>

## Suggestion d'outils de dev

* Éditeur de texte: [Sublime text](https://www.sublimetext.com/) - plus adapté pour le web que les éditeurs en console ou les gros IDE.
* Plugin Sublime text: [Emmet](https://emmet.io/blog/sublime-text-3/)
