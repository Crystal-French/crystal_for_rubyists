\newpage

# Concurrence et Channels

Vous vous souvenez du Chapitre 1? Nous avions écrit une version concurrente de Hello World!

Voici un petit rappel.

```ruby
channel = Channel(String).new
10.times do
  spawn {
    channel.send "Hello?"
  }
  puts channel.receive
end
```

Dans Crystal nous utilisons le mot-clé `spawn` pour faire exécuter quelque chose
en arrière-plan sans bloquer l'exécution principale.

Pour arriver à cela `spawn` crée un thread léger appelé `Fiber`.
Des `Fiber`s sont peu coûteux à créer et vous pouvez facilement créer
des dizaines de milliers de `Fiber`s sur un même coeur.

Okay, c'est cool! Nous pouvons utiliser `spawn` pour exécuter quelque chose en arrière-plan
mais comment récupérer quelque chose depuis un `Fiber`?

C'est ici que les `Channel`s entrent en jeu.

## Channel

Comme son nom l'indique un `Channel` est un canal entre un expéditeur et un destinataire.
Ainsi un `Channel` leur permet de communiquer l'un avec l'autre à l'aide des méthodes `send` et `receive`.

Examinons ligne par ligne notre exemple précédent.

```ruby
channel = Channel(String).new
```

Nous créons un `Channel` avec `Channel(String).new`.
Remarquez que nous un avons créé un `Channel` qui envoie (`send`) et reçoit (`receive`) des messages de type `String`.

```ruby
10.times do
  spawn {
    channel.send "Hello?"
  }
  puts channel.receive
end
```

Passons la boucle, nous envoyons ensuite un message dans notre canal avec `spawn`.
Vous vous demandez peut-être 'Pourquoi envoyons-nous un message en arrière-plan?'.
Parce-que `send` est une opération bloquante et si nous le faisons dans le programme principal,
nous allons le bloquer indéfiniment.

Considérez ceci:

```ruby
channel = Channel(String).new
channel.send "Hello?" # Ceci bloque l'exécution du programme
puts channel.receive
```

Quelle est la sortie de ce programme? En fait, ce programme ne terminera jamais son exécution
parce-qu'il sera bloqué par `channel.send "Hello?"`.
Maintenant que nous savons pourquoi nous utilisons `spawn` pour envoyer un message, continuons.

```ruby
spawn {
  channel.send "Hello?"
}
puts channel.receive
```

Nous envoyons juste un message dans notre canal en arrière-plan avec `spawn`.
Ensuite nous le réceptionnons avec `channel.receive`.
Dans cet exemple le message est `Hello?` donc ce programme affiche `Hello?` puis termine.
