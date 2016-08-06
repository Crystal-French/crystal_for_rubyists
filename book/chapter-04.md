\newpage

# Créer un nouveau projet

Jusqu'à présent nous avons utilisé la commande `crystal` uniquement pour exécuter notre code.

En fait la commande `crystal` est très utile et ne se résume pas qu'à ça (exécutez `crystal --help` pour en savoir plus).

Par exemple nous pouvons l'utiliser pour créer un nouveau projet Crystal.

    $ crystal init app sample
      create  sample/.gitignore
      create  sample/LICENSE
      create  sample/README.md
      create  sample/.travis.yml
      create  sample/shard.yml
      create  sample/src/sample.cr
      create  sample/src/sample/version.cr
      create  sample/spec/spec_helper.cr
      create  sample/spec/sample_spec.cr
    Initialized empty Git repository in /Users/serdar/crystal_for_rubyists/code/04/sample/.git/

Fantastique. `crystal` nous a permis de créer un nouveau projet.
Voyons voir ce qu'il a fait pour nous:

  - Création d'un nouveau dossier nommé `sample`,
  - Création d'un fichier de licence LICENSE,
  - Création d'un `.travis.yml` pour intégrer facilement Travis pour l'intégration continue,
  - Création d'un `shard.yml` pour la gestion des dépendances,
  - Initialisation d'un dépôt Git vide,
  - Création d'un README pour notre projet,
  - Création des dossiers `src` et `spec` pour contenir notre code et nos tests(chut..nous en discuterons bientôt).

Exécutons tout ça:

    $ cd sample
    $ crystal src/sample.cr

Rien ne se passe! Super :)

Maintenant que nous avons créé notre premier projet, utilisons des librairies externes.

## Utiliser des Shards pour la gestion des dépendances

Pour gérer les dépendances d'un projet nous utilisons des `shards`. `shards` est l'équivalent de `bundler`
et `shard.yml` l'équivalent de `Gemfile`.

Ouvrons notre `shard.yml`.

```yaml
name: sample
version: 0.1.0

authors:
  - sdogruyol <dogruyolserdar@gmail.com>

license: MIT
```

C'est le fichier `shard.yml` par défaut et contient les informations minimales nécessaires sur notre projet. Elles sont:

- `name` spécifie le nom du projet,
- `version` spécifie la version du project. Crystal utilise lui-même [semver](http://semver.org/)
  pour la gestion des versions c'est donc une bonne convention à suivre dans vos propres projets,
- `authors` section qui spécifie les auteurs du projet. Récupéré par défaut depuis votre configuration `git` globale,
- `license` spécifie le type de la licence de votre projet. `MIT` par défaut.

Okay. Mais que peut-on faire avec ce `shard.yml`?
Et bien on peut utiliser ce fichier pour ajouter des librairies externes( que nous appelons dépendances)
et pour les gérer sans même avoir à nous soucier de dossiers, chemins, etc... Sympathique non?

Maintenant que nous connaissons toute la puissance des `shards`, ajoutons [Kemal](https://github.com/sdogruyol/kemal)
à notre `shard.yml` et développons une application web toute simple :)

Ouvrez `shard.yml`. Tout d'abord nous avons besoin d'ajouter `Kemal` comme dépendance de notre projet.
Pour cela on y inclut:

```yaml
dependencies:
  kemal:
    github: sdogruyol/kemal
    version: 0.14.1
```

C'est très bien! Nous avons ajouté `Kemal` à notre projet. D'abors, nous devons l'installer.

    $ shards install
    Updating https://github.com/sdogruyol/kemal.git
    Updating https://github.com/luislavena/radix.git
    Updating https://github.com/jeromegn/kilt.git
    Installing kemal (0.14.1)
    Installing radix (0.3.0)
    Installing kilt (0.3.3)

Okay maintenant nous sommes prêts à utiliser `Kemal` dans notre projet. Ouvrez `src/sample.cr`:

```ruby
require "./sample/*"
require "kemal"

module Sample

  get "/" do
    "Hello World!"
  end

end

Kemal.run
```

Remarquez comme nous avons utilisé `require` pour rendre disponible `Kemal` dans notre programme.

Exécutons tout ça.

    $ crystal src/sample.cr
    [development] Kemal is ready to lead at http://0.0.0.0:3000

Ouvrez `localhost:3000` et voyez votre programme en action!

Maintenant vous savez comment ajouter des dépendances et utiliser d'autres `shard`s :)
