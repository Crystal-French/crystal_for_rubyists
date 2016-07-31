\newpage

# FizzBuzz

Assurément, la première chose qu'on vous demandera en entretien professionnel
pour ce nouveau boulot tranquille en Crystal sera de développer FizzBuzz. Allons-y!

Si vous ne le connaissez pas, FizzBuzz est un petit problème de programmation:

> "Ecrire un programme qui affiche les nombres de 1 à 100. Mais pour les multiples de
> trois afficher 'Fizz' à la place et pour les multiples de cinq afficher 'buzz'.
> Pour les nombres qui sont multiples de trois et cinq, afficher 'FizzBuzz'."

Cela nous donnera une bonne excuse pour voir les bases de Crystal: boucles,
tests, affichage sur la sortie standard, et tout plein d'autres petites choses.

D'abord, créons notre projet.

    $ crystal init app fizzbuzz

Ecrivons notre premier test en échec. Ouvrez `/spec/fizzbuz_spec.cr`

```ruby
require "./spec_helper"

describe Fizzbuzz do
  it "shouldn't divide 1 by 3" do
    div_by_three(1).should eq(false)
  end
end
```

Et exécutons-le:

    $ crystal spec
    Error in ./spec/fizzbuzz_spec.cr:7: undefined method 'div_by_three'

    div_by_three(1).should eq(false)


Cela est logique: nous n'avons encore défini aucune méthode.
Définissons-en une:

```ruby
require "./fizzbuzz/*"

def div_by_three(n)
  false
end
```

De la même manière que Ruby, la valeur de la dernière expression sert de valeur de retour.

En TDD il faut aller au plus simple! Notre méthode définie, compilons et exécutons nos tests:

    $  crystal spec
    .

    Finished in 0.82 milliseconds
    1 examples, 0 failures, 0 errors, 0 pending


Fantastique! Ça passe! Ecrivons un nouveau test, et voyons ce qui se passe:

```ruby
require "./spec_helper"

describe Fizzbuzz do
  it "shouldn't divide 1 by 3" do
    div_by_three(1).should eq(false)
  end

  it "should divide 3 by 3" do
    div_by_three(3).should eq(true)
  end
end
```

Exécutons-le!

    $ crystal spec

    .F

    Failures:

      1) Fizzbuzz should divide 3 by 3
         Failure/Error: div_by_three(3).should eq(true)

           expected: true
                got: false

         # ./spec/fizzbuzz_spec.cr:9

    Finished in 0.83 milliseconds
    2 examples, 1 failures, 0 errors, 0 pending

    Failed examples:

    crystal spec ./spec/fizzbuzz_spec.cr:8 # Fizzbuzz should divide 3 by 3

Nous avons une erreur. Faisons-la passer.

```ruby
require "./fizzbuzz/*"

def div_by_three(n)
  if n % 3 == 0
    true
  else
    false
  end
end
```

Exécutons-la.

    $ crystal spec

    ..

    Finished in 0.61 milliseconds
    2 examples, 0 failures, 0 errors, 0 pending

Fantastique! Cela démontre également le fonctionnement de `else`.
Sûrement ce à quoi vous vous attendiez. Continuez et essayez
de refactoriser ça en un uniligne.

C'est fait? Comment feriez-vous? Voici ma version:

```ruby
def div_by_three(n)
  n % 3 == 0
end
```

Rappelez-vous, la valeur de la dernière expression est retournée.

Okay, maintenant essayez d'appliquer le principe du TDD sur
les `div_by_five` et `div_by_fifteen`.
Elles devraient être similaires, mais cela vous fera faire un peu de pratique
de les écrire. Dès que vous obtenez le même résultat suivant, vous pouvez passer à la suite:

    $ crystal spec -v

    Fizzbuzz
      shouldn't divide 1 by 3
      should divide 3 by 3
      shouldn't divide 8 by 5
      should divide 5 by 5
      shouldn't divide 13 by 15
      should divide 15 by 15

    Finished in 0.61 milliseconds
    6 examples, 0 failures, 0 errors, 0 pending

Okay! Voyons maintenant le programme principal.
Nous avons les outils pour coder FizzBuzz, faisons-le marcher.
Nous devons commencer par afficher tous les nombres de 1 à 100. Facile!

```ruby
1...100.times do |num|
  puts num
end
```

Première étape: afficher **quelque chose** 100 fois. Si vous exécutez ça avec
`crystal build src/fizzbuzz.cr && ./fizzbuzz` vous devriez voir `num` affiché
100 fois. Notez que nos tests ne sont pas exécutés. Non seulement ils ne sont pas exécutés,
ils ne sont en plus pas dans le binaire.

Maintenant nous pouvons mettre les deux ensemble:

```ruby
1...100.times do |num|
  answer = ""

  if div_by_fifteen num
    answer = "FizzBuzz"
  elsif div_by_three(num)
    answer = "Fizz"
  elsif div_by_five num
    answer = "Buzz"
  else
    answer = num
  end

  puts answer
end
```

Parce-que le `if` renvoie une valeur, nous pourrions aussi faire quelque chose comme:

```ruby
1..100.times do |num|
  answer = if div_by_fifteen num
    "FizzBuzz"
  elsif div_by_three(num)
    "Fizz"
  elsif div_by_five num
    "Buzz"
  else
    num
  end

  puts answer
end
```

Essayez de l'exécuter.

Fantastique! Nous sommes venus à bout de FizzBuzz.
