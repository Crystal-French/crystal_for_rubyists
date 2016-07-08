\newpage

# Pourquoi Crystal?

Vous développez déjà en Ruby. Ça paye les factures. Vous aimez coder avec.
Pourquoi vous intéresseriez-vous à Crystal?

Réfléchissons une minute à Ruby: quels sont ses principaux défauts?
Pour moi, ils sont:

-   Concurrence
-   Rapidité
-   Documentation

Qu'est-ce qui est super dans Ruby?

-   Blocs
-   Aspects fonctionnels
-   Syntaxe simple
-   Centré sur l'expérience développeur
-   Prise en main rapide
-   Typage dynamique

Nous pouvons donc apprendre beaucoup d'un langage aussi simple que Ruby,
qui gère bien la concurrence, et est rapide. Nous ne voulons pas sacrifier
les fonctions anonymes, la syntaxe élégante, ou ne pas faire
`AbstractFactoryFactoryImpls` juste pour faire le job.

Je pense que ce langage est *Crystal*.

Maintenant: Crystal n'est pas parfait. Mais il s'améliore.
Et le but est d'*apprendre*. Et utiliser un langage
qui est très familier, tout en étant très différent, peut nous apprendre beaucoup.

Voici un "Hello World" en Crystal:

```ruby
puts "Hello, world!"
```

Voici une version concurrente de "Hello World" en Crystal:

```ruby
channel = Channel(String).new
10.times do
  spawn {
    channel.send "Hello?"
  }
  puts channel.receive
end
```

La même, portée grossièrement en Ruby:


```ruby
10.times.map do
  Thread.new do
    puts "Hello?"
  end
end.each(&:join)
```

Et voilà. Remarquez les choses *similaires* avec Ruby:

-   La même syntaxe élégante.
-   Les variables, tout en étant statiquement typées, supportent l'inférence,
nous n'avons donc pas besoin de déclarer les types.

Remarquez les choses qui sont *différentes*:

-   Étant compilé et statiquement typé, le compilateur va nous jeter
    si nous avons fait une erreur.

Ah, et:

    $ time ./hello
    ./hello  0.00s user 0.00s system 73% cpu 0.008 total

    $ time ruby hello.rb
    ruby hello.rb  0.03s user 0.01s system 94% cpu 0.038 total

Cinq fois plus rapide. Chouette, des micro tests de performance complétement inutiles!

Quoi qu'il en soit, j'espère que vous avez saisi l'essentiel: Crystal présente
assez de similarités syntaxiques avec Ruby pour que vous vous sentiez
en terrain connu. Et ses forces sont certaines des plus grandes faiblesses
de Ruby. C'est pourquoi je pense que vous en apprendrez beaucoup en testant
Crystal, même si vous le faites en dehors de votre cadre de travail.
