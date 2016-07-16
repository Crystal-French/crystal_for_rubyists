\newpage

# Types et surcharge de méthode

Crystal est comme Ruby, mais ce n'est pas Ruby!

A la différence de Ruby, Crystal est un langage compilé et statistiquement typé.
La plupart du temps vous n'avez pas à spécifier les types et le compilateur est assez
intelligent pour faire de l'`inférence de type`.

Alors avons-nous besoin de ces types? Commençons avec quelque chose de simple.

```ruby
def add(x, y)
  x + y
end

add 3, 5 # 8
```

C'est la même chose qu'en Ruby! Nous avons juste défini une méthode qui ajoute deux nombres.
Que se passe-t-il si nous essayons d'ajouter un nombre à une chaîne?

Commençons par le faire en Ruby.

```ruby
add 3, "Serdar"
TypeError: String can't be coerced into Fixnum
```

Comment??? Qu'est-ce que tu dis? Nous avons eu une erreur `TypeError`
mais nous n'avons pas à nous soucier des types en Ruby ( ou pas :)).
C'est aussi une erreur `runtime error` signifiant que votre programme a crashé
à l'exécution, ce qui n'indique rien de bon.

Maitenant faisons la même chose en Crystal.

    Error in ./types.cr:7: instantiating 'add(Int32, String)'

    add 3, "Serdar"
    ^~~

    in ./types.cr:2: no overload matches 'Int32#+' with types String
    Overloads are:
    - Int32#+(other : Int8)
    - Int32#+(other : Int16)
    - Int32#+(other : Int32)
    - Int32#+(other : Int64)
    - Int32#+(other : UInt8)
    - Int32#+(other : UInt16)
    - Int32#+(other : UInt32)
    - Int32#+(other : UInt64)
    - Int32#+(other : Float32)
    - Int32#+(other : Float64)
    - Int32#+()

    x + y

Okay, plutôt impressionnant comme sortie mais ça a du bon.
Notre code Crystal n'a pas compilé et nous a aussi indiqué qui n'y a pas
la surcharge attendue pour `Int32#+` et nous affiche les surcharges possibles.
C'est une `compile time error` qui signifie que notre code n'a pas compilé
et que l'erreur a été récupérée avant d'exécuter le programme. Ce qui est
fort agréable.

Maintenant ajoutons des types et une contrainte à cette méthode
pour qu'elle n'accepte que des `Number`s.

```ruby
def add(x : Number, y : Number)
  x + y
end

puts add 3, "Serdar"
```

Exécutez-la.

    Error in ./types.cr:7: no overload matches 'add' with types Int32, String
    Overloads are:
    - add(x : Number, y : Number)

    add 3, "Serdar"
    ^~~

Super! A nouveau, notre méthode n'a pas compilé. Et cette fois-ci avec une erreur plus succinte et précise.
Nous avons utilisé la `restriction de type` sur `x` et `y`.
Nous les avons restreints à des `Number`s et Crystal est assez intelligent
pour nous empêcher d'utiliser la méthode avec une `String`.

## Surcharge de Méthode

Nous venons juste de voir de nombreuses surchages.
Parlons de la `Surcharge de Méthode`.

La surcharge de méthode c'est avoir différentes méthodes avec le même nom mais avec
un nombre différent d'arguments.
Elles ont toutes le même nom mais en réalité ce sont des méthodes différentes.

Surchargeons notre méthode `add` et faisons-la fonctionner avec une String.

```ruby
def add(x : Number, y : Number)
  x + y
end

def add(x: Number, y: String)
  x.to_s + y
end

puts add 3, 5

puts add 3, "Serdar"
```

Exécutons-la.

    $ crystal types.cr
    8
    3Serdar

Ceci est la surcharge de méthode en action.
L'appel à la méthode avec un Number et une String a automatiquement déduit la méthode appropriée à exécuter.
Vous pouvez définir autant de méthodes surchargées que vous le voulez.
