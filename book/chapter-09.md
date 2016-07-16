\newpage

# Macros et Metaprogramming

On aime Ruby pour son côté dynamique et la métaprogrammation!
A la différence de Ruby, Crystal est un langage compilé.
C'est pour cela que l'on trouve certaines différences:

- Il n'y a pas d'`eval`.
- Il n'y a pas de `send`.

Dans Crystal on utilise des `Macro`s pour obtenir le même comportement et la métaprogrammation.
Vous pouvez voir les `Macro`s comme 'du Code qui écrit/modifie du code'.

P.S: Les `Macro`s sont étendues en code à la compilation.

Testez cela.

```ruby
macro define_method(name, content)
  def {{name}}
    {{content}}
  end
end

define_method foo, 1
# Qui génère:
#
#     def foo
#       1
#     end

foo # => 1
```

Dans cet exemple nous avons créé une macro nommée `define_method`
et nous avons fait un appel à cette macro comme n'importe quelle méthode.
Cette macro s'étend en:

```ruby
  def foo
    1
  end
```

Plutôt sympathique! On a un comportement
équivalent à `eval` à la compilation.

Les macros sont vraiment puissantes mais il y a une règle que vous ne pouvez enfreindre.

***Une macro doit s'étendre en un programme Crystal valide***
