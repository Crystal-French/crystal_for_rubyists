\newpage

# Ecrire votre premier programme Crystal

Okay! Passons à l'action: pour pouvoir vous auto-proclamer
"Programmeur X", vous devez écrire votre "Hello, world" en X.
Alors, allons-y. Ouvrez un éditeur de fichiers: j'utiliserez `vim`
parce-que je suis ce genre de personne, vous être libre d'utiliser
ce que bon vous semble. Les programmes Crystal finissent en `.cr`:

    $ vim hello.cr

Ajoutez-y ceci::

```ruby
puts "Hello World!"
```

Et exécutez-le avec la commande `crystal`:

    $ crystal hello.cr
    Hello World!

Il devrait s'exécuter et afficher la sortie sans erreur.
Si vous en avez une, vérifiez que vous avez bien utilisé les guillemets doubles.
Cette erreur devrait ressembler à:

    $ crystal hello.cr
    Syntax error in ./hello.cr:1: unterminated char literal, use double quotes for strings

    puts 'Hello World!'

Au passage la commande `crystal` est très bien pour rapidement exécuter du code mais elle est lente.
A chaque fois elle compile et exécute le programme.
Voyons quel temps ça prend d'exécuter ce programme.

    $ time crystal hello.cr
    crystal hello.cr  0.30s user 0.20s system 154% cpu 0.326 total

0.326 seconde pour un `Hello World`? C'est lent.

Au lieu de compiler et exécuter une nouvelle fois vous pouvez compiler le programme en un binaire
avec la commande `build`.

    $ crystal build hello.cr

Puis pour exécuter votre programme, suivez la Classique Méthode Unix:

    $ time ./hello
    ./hello  0.00s user 0.00s system 87% cpu 0.006 total

Vous devriez voir "Hello, world." affiché à l'écran 50 fois plus rapidement :) félicitations!
