\newpage

# Tests

Les rubyistes adorent les tests, alors avant d'aller plus loin,
parlons tests. Crystal est livré avec son propre framework de tests,
`spec`. Il est très similaire à `RSpec`.

Revenons au projet que nous avons créé au Chapitre 04.

Si vous vous souvenez bien `crystal` a créé une structure
de projet pour nous.

    $ cd sample && tree
    -- LICENSE
    -- README.md
    -- shard.yml
    -- spec
      -- sample_spec.cr
      -- spec_helper.cr
    -- src
      -- sample
        -- version.cr
      -- sample.cr

Vous avez remarqué ce dossier `spec`? Oui, comme vous l'avez deviné Crystal a créé ce dossier
et la première spécification pour nous.
Avec Crystal un fichier est testé avec un fichier `_spec` correspondant.
Etant donné que nous avons nommé notre projet `sample`, un fichier nommé `sample.cr`
a été créé ainsi que la spécification correspondante `spec/sample_spec.cr`.

Au passage, dans ce contexte `spécification` et `test unitaire` signifient
la même chose et peuvent-être utilisés indifférement.

Sans plus attendre ouvrons `spec/sample_spec.cr`

```ruby
require "./spec_helper"

describe Sample do
  # TODO: Ecrire des tests

  it "works" do
    false.should eq(true)
  end
end
```

Ce fichier est très intéressant. On y trouve trois mots-clés importants, `describe`, `it` et `should`.

Ces mots-clés sont uniquement utilisés dans `spec` pour les besoins suivants:

- `describe` vous permet de grouper des tests,
- `it` est utilisé pour définir un test avec un titre donné entre guillemets doubles,
- `should` est utilisé pour décrire les suppositions du test.

Comme vous pouvez le voir notre fichier a un groupe décrit (`describe`) par le nom `Sample`
qui a un test avec le titre `work` (`it "works"`) qui fait la supposition que false devrait
(`should`) être égal à true.

Vous vous demandez peut-être 'Comment exécuter ces tests'? Et bien la commande `crystal`
vient à notre rescousse.

    $ crystal spec
    F

    Failures:

      1) Sample works
         Failure/Error: false.should eq(true)

           expected: true
                got: false

         # ./spec/sample_spec.cr:7

    Finished in 0.69 milliseconds
    1 examples, 1 failures, 0 errors, 0 pending

    Failed examples:

    crystal spec ./spec/sample_spec.cr:6 # Sample works

Super! Nous avons un test en échec(rouge). Par la lecture de la sortie nous pouvons
facilement savoir quel test a échoué. Ici c'est le test dans le groupe `Sample` nommé `works` a.k.a `Sample works`.
Faisons en sorte que ce test passe (vert)

```ruby
require "./spec_helper"

describe Sample do
  # TODO: Write tests

  it "works" do
    true.should eq(true)
  end
end
```

Re-exécutez les tests.

    $ crystal spec

    .

    Finished in 0.63 milliseconds
    1 examples, 0 failures, 0 errors, 0 pending

Vert! C'est tout ce dont vous avez besoin pour débuter. Dans la suite: FizzBuzz.
