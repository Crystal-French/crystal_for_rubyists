\newpage

# Liaisons avec C

Il y a de nombreuses librairies C utiles. Il est important de les ré-utiliser
au lieu de réécrire chacune d'entre elles.

Dans Crystal, c'est très simple d'utiliser des librairies C existantes
à l'aide de liaisons(bindings). Crystal lui-même utilise des librairies C.

Par exemple Crystal utilise `libpcre` pour son implémentation de `Regex`.

Comme je l'ai déjà dit c'est très simple d'écrire des liaisons avec C.
Crystal utilise lui-même `libpcre` comme cela

```ruby
@[Link("pcre")]
lib LibPCRE
...
end
```

Avec seulement 3 lignes de code vous êtes lié à `libpcre` :)
Nous utilisons le mot-clé `lib` pour grouper les fonctions et types
qui appartiennent à une librairie. Et c'est une bonne convention de
débuter vos déclarations de librairie C par `Lib`.

Ensuite nous nous lions aux fonctions C avec le mot-clé `fun`.

```ruby
@[Link("pcre")]
lib LibPCRE
  type Pcre = Void*
  fun compile = pcre_compile(pattern : UInt8*, options : Int, errptr : UInt8**, erroffset : Int*, tableptr : Void*) : Pcre
end
```

Ici nous avons fait une liaison sur la function compile de `libpcre` avec les types correspondants.
Désormais nous pouvons facilement utiliser cette fonction dans notre code Crystal.

```crystal
LibPCRE.compile(..)
```
