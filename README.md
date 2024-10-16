# 🐾 TP : Crée ton Zoo virtuel en PHP orienté objet ! 🐾

## Objectif : Réviser les concepts de la POO tout en construisant un petit programme qui simule un zoo avec différents animaux et actions.

### Partie 1 : Les classes et objets 🦁

**📚 Rappel :**
Une **classe** est comme un plan (blueprint) pour créer des objets. Un **objet** est une instance de cette classe (dans la ligne `$animal = new Animal()` Animal est une classe, tandis que $animal est un objet car c'est un nouveau (new) Animal).

**Exercice :**

1. Dans un dossier `Classes`, créer une classe Animal (dans un fichier `Animal.php`, attention la majuscule est importante) avec les propriétés nom et espece. Il faudra un construct pour le nom et l'espèce.
2. Ajoute une méthode sePresenter() qui affichera : "Je suis un {nom}, un {espece}".
3. Dans un fichier `index.php` à la racine de ce projet, instancie deux objets de cette classe, par exemple un lion et un éléphant et tester votre méthode `sePrésenter()` pour chacun des objets.

```php
class Animal {
    public $nom;
    public $espece;

    public function __construct($nom, $espece) {
        $this->nom = $nom;
        $this->espece = $espece;
    }

    public function sePresenter() {
        echo "Je suis {$this->nom}, un {$this->espece}" . PHP_EOL;
        return $this;
    }
}


$lion = new Animal("simba", "lion");

$lion->sePresenter();
```

✅ **But** : Comprendre comment créer une classe et instancier des objets.

### 🛠 Partie 1.5 : Le chaînage (->) 🐍
**📚 Rappel :**
Le **chaînage** en PHP se fait avec l'opérateur `->`, qui permet d'accéder aux propriétés ou méthodes d'un objet. C'est comme une flèche qui pointe vers une action ou une caractéristique de cet objet.

1. Reprenons l'objet `$lion` que tu as créé dans la partie 1.
2. Pour appeler une méthode de cet objet, on utilise `->`. Par exemple : `$lion->sePresenter()`.

**🔎 Explication :**

* `$lion` est un **objet**.
* `->` nous permet d'**accéder** à ses **propriétés** ou **méthodes**.
* `sePresenter()` est la **méthode** de l'objet `$lion`.

**👉 Exemple concret :**

* Si tu veux que le **lion** se présente, il faut utiliser la méthode `sePresenter()` du lion et non pas celle de l'éléphant.
* Il faudra d'abord accéder au lion, puis à sa méthode `sePresenter()` grâce au chaînage :

```php
$lion = new Animal("Simba", "Lion");
$lion->sePresenter();  // "Je suis un Simba, un Lion."
```

Grâce au chaînage on peut faire enchainer des actions à notre objet. Par exemple admettons le lion ait la méthode `crier()` tel que :

```php
public function crier() {
    echo "GROAAAAAR";
    return $this;
}
```

Dans cette méthode, on peut constater le `return $this` qui retourne l'objet qui a executé la méthode. 

A quoi ça sert ? Si l'on veut que notre lion se présente et crie directement après, on pourrait le faire en une seule ligne : 

```php
$lion->crier()->sePresenter();
// crier retourne l'objet qui a executé cette méthode, donc ici le lion. 
//Puisqu'à la fin de la méthode crier on a toujours un lion,
// on peut enchainer avec une autre méthode d'un lion, et ainsi de suite !
```

✅ **But** : Apprendre à utiliser `->` pour accéder aux fonctionnalités de nos objets.

### Partie 2 : L’héritage 🐻‍❄️
**📚 Rappel :**
L'**héritage** permet de créer une nouvelle classe en se basant sur une classe existante. Cela évite de réécrire tout le code.

**Exercice :**

1. Crée une classe `Mammifere` qui hérite de `Animal` grâce au mot-clé `extends` et ajoute une nouvelle méthode `allaite()` qui dit : "*Je suis un mammifère et je peux allaiter.*"
2. Crée un objet `ours` qui utilise cette nouvelle classe.
3. Dans `index.php`, testez que votre Ours est bien capable d'utiliser la méthode du mammifere.

✅ **But** : Comprendre comment réutiliser du code avec l’héritage.<br>
👉 **À toi de jouer** : Ajoute un autre mammifère comme une girafe ou un koala. 🦒

### Partie 3 : L'encapsulation 🦊
**📚 Rappel :**
L'**encapsulation** permet de protéger les données. On peut rendre des propriétés privées et utiliser des **getters** et **setters** pour y accéder.<br>
**Attention**, on ne parle pas de sécurité dans le sens protection contre des hackers 👨🏻‍💻 mais plutôt dans le sens de s'assurer que les personnes qui utiliseront notre code l'utiliserons correctement (par exemple nos collègues de travail !).

**Exercice** :

1. Rends la propriété `$nom` privée dans la classe `Animal` si ce n'est pas déjà fait.
2. Ajoute une méthode `getNom()` pour accéder à cette propriété et une méthode `setNom()` pour la modifier.
3. Test dans `index.php` que :
    - Le getter retourne bien le nom de l'objet.
    - Le setter permet bien de changer le nom de l'objet après sa création.

✅ But : Maîtriser la protection des données avec les méthodes privées et publiques.<br>
👉 À toi de jouer : Passes les autres propriétés de tes animaux en privé et fais les ajouts et modifications adéquates. 🦁🦓

### Partie 4 : Le polymorphisme 🐼
**📚 Rappel :**
Le **polymorphisme** permet d’utiliser une même méthode pour des objets de classes différentes, avec un comportement spécifique selon la classe.

**Exercice :**

1. Crée une méthode `crier()` dans `Animal`, et redéfinis-la dans `Mammifere` et une nouvelle classe `Oiseau`.
    * Animal dit : "*Je fais un bruit générique*"
    * Mammifere dit : "*Je rugis ou grogne*"
    * Oiseau dit : "*Je chante ou siffle*"
2. Tester votre code dans `index.php` tel que :
```php
$canari->crier(); // "Je chante ou je siffle"
$lion->crier(); // "Je rugis ou je grogne"
$animal->crier(); // "je fais un bruit générique"
```

✅ But : Appliquer le polymorphisme pour avoir des comportements différents selon la classe.

### 🛠 Partie 5 : Les classes abstraites et finales 🦍

📚 **Rappel** :

* Une **classe abstraite** ne peut pas être instanciée directement. Elle sert de modèle pour d'autres classes qui vont la **hériter**.
* Une **classe finale** ne peut plus être héritée par d'autres classes. C'est une classe que l'on verrouille, parce qu'on ne veut plus de modifications dans son comportement.

**Pourquoi utiliser une classe abstraite ?**

Dans notre zoo, il est logique que tu ne puisses pas créer un "Animal" ou un "Mammifère" directement. Ce sont des catégories trop générales. Ce qui est concret, c’est le lion, le tigre, ou l’éléphant ! Les classes abstraites permettent d'imposer certaines règles sans être utilisées telles quelles.

</hr>

#### Les classes abstraites 👨‍🏫

**Exercice :**

1. Transforme la classe `Animal` en classe abstraite. Elle ne pourra plus être instanciée directement, mais ses enfants (comme `Mammifere` ou `Oiseau`) pourront l’hériter.
2. Rends la méthode `crier()` abstraite dans la classe `Animal`. Cela signifie que chaque classe enfant devra obligatoirement la définir à sa manière (c’est ce qu’on appelle **l’implémentation**).

```php
abstract class Animal {
    private $nom;
    private $espece;

    public function __construct($nom, $espece) {
        $this->nom = $nom;
        $this->espece = $espece;
    }

    abstract public function crier();  // Méthode abstraite à implémenter dans les classes enfants

    // [...]
}
```

Ensuite, dans chaque classe enfant (`Mammifere`, `Oiseau`), tu devras définir la méthode `crier()` selon l'animal :

```php
class Mammifere extends Animal {
    public function crier() {
        echo "Je rugis ou grogne.";
    }
}

class Oiseau extends Animal {
    public function crier() {
        echo "Je chante ou je siffle.";
    }
}
```

⚠️ Il faudra faire des modifications dans `index.php` car par exemple : `$animal = new Animal()` ne marchera plus puisque c'est devenu une classe abstraite. ⚠️

De plus n'oubliez pas de **tester** les modifications que vous avez faites pour **vérifier** que le code fonctionne toujours.

✅ **But** : Apprendre à utiliser des classes abstraites pour éviter d’instancier des catégories trop générales.<br>
👉 **À toi de jouer** : Oiseau et Mammifere sont des catégories encore trop générale, rends les abstraites et créer des classes d'animaux très spécifique qui en héritent (exemple : Lion, Colibri, Elephant etc....).

#### Les classes finales 🚫


**Exercice** :

1. Les classes qui sont très spécifique comme `Lion` ou `Elephant`, n'auront pas d'enfant, il font donc empêcher le fait qu'elles puissent être héritées. Pour cela, tu utilises le mot-clé `final`.
2. Ce type de classe pourrait être utilisé pour des cas particuliers dans ton zoo, où tu veux verrouiller le comportement d’un animal sans permettre d’autres extensions.

✅ **But** : Utiliser `final` devant `class` pour empêcher l’héritage dans certains cas spécifiques.


### Partie 6 : Interfaces et abstraction 🐨

📚 **Rappel** :

Les **interfaces** et les **classes abstraites** permettent de définir des méthodes que d'autres classes doivent implémenter. C'est un peu comme établir des règles que les classes doivent suivre.

**Exercice** :

Certains Mammifere comme le `Lion` sont carnivore. Mais celui-ci hérite déjà de `Mammifere` et ils ne sont pas tous carnivore. De plus une classe ne peut hériter que d'une seule autre classe. Dans ce cas de figure, il faut utiliser une interface !

1. Dans un dossier `interfaces` à la racine du projet, crée une interface `Carnivore` (dans un fichier `CarnivoreInterface.php`)
2. l'interface aura une méthode `mangerViande()`.
3. Implémente cette interface dans la classe `Lion` pour les animaux carnivores.

```php
interface Carnivore {
    public function mangerViande();
}

class Lion extends Mammifere implements Carnivore {

    public function mangerViande() {
        echo "Je mange de la viande !";
    }
}

$lion->mangerViande();
```

✅ **But** : Comprendre comment imposer des comportements avec les interfaces.<br>
👉 **À toi de jouer** : Ajoute un autre carnivore dans ton zoo, comme un tigre ou un loup ! 🐅

<hr>

🎉 **Félicitations !** 🎉

Tu as maintenant révisé les concepts clés de la POO en PHP à travers la création de ton propre zoo ! Continue d'améliorer ton zoo en ajoutant de nouvelles classes, méthodes et animaux. Pourquoi pas des enclots pour loger tes animaux ?