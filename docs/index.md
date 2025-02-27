# La programmation orientée objet

En programmation orientée objet (POO), un objet représente un concept, une idée ou toute entité du monde physique, comme une voiture, une personne ou encore une page d'un livre. Il possède une structure interne et sait interagir avec ses pairs.  

Il s'agit donc de représenter ces objets et leurs relations ; l'interaction entre les objets via leurs relations permet de concevoir et réaliser les fonctionnalités attendues et de mieux résoudre le ou les problèmes. 

## Créer des nouveaux objets

### Pour commencer

La création d'un nouvel objet passe en python, par l'implantation d'**une classe**.  

!!! question "Premier exemple"

    1. Dans un fichier python nommé **eleve.py**, coller le code suivant :
    ``` python title="Implantation d'une classe Eleve" linenums="1"
    class Eleve:
        pass
    ```
    2. Il est possible à présent de créer des nouveaux élèves.  
    Dans la **console**, tester les instructions suivantes :
    ``` python title="Nouveaux élèves" linenums="1"
    mathis = Eleve()
    elise  = Eleve()
    ```
    3. Ces deux élèves sont-ils en relation ? Tester l'instruction
    ``` python title="Nouveaux élèves" linenums="1"
    mathis == elise
    ```

        !!! important
            Cela signifie que l'objet ```mathis``` n'est pas le même objet que ```elise``` même s'ils sont tous les deux  du même type.  

            D'ailleurs les instructions ```type(mathis)``` et ```type(elise)``` le prouvent. 

Ces objets n'ont pour le moment aucune caractéristique. Rien ne permet de différencier l'élève Mathis de l'élève Élise.  

!!! question "Personnalisation"

    1.  1. Nous allons fournir à Mathis et Élise quelques propriétés.  
    Modifier le code de **eleve.py** avec le code suivant :
    ``` python title="Implantation d'une classe Eleve" linenums="1"
    class Eleve:
        pass

    mathis = Eleve()
    elise  = Eleve()

    mathis.nom = "Catteau"
    ```
        2. Dans la console, tester l'instruction ```mathis.nom``` puis l'instruction ```elise.nom```.
    
            !!! warning "Attention"
                Lorsqu'on définit une propriété à un objet en dehors de la classe, elle n'est pas partagée par les autres objets du même type.
    3.  1. Corriger le fichier **eleve.py** avec le code suivant :
    ``` python title="Implantation d'une classe Eleve'" linenums="1"
    class Eleve:
        nom = "Catteau"

    mathis = Eleve()
    elise  = Eleve()
    ```
        2. Tester dans la console chacune des instructions suivantes :
        ``` python title="Quelques contrôles" linenums="1"
        mathis.nom
        elise.nom
        Eleve.nom
        ```

            !!! warning "Attention"
                Quand on définit une propriété à l'intérieur d'une classe, elle est partagée entre tous les objets du type de la classe.
    4.  1. Ajouter une propriété ```age``` initialisée à 17 dans la classe ```Eleve```.
        2. Vérifier que les instructions ```mathis.age``` et ```elise.age``` renvoient bien ```17```.
        3. Tester l'instruction ```Eleve.age += 1``` et consulter l'âge des deux élèves.
        4. Tester l'instruction ```mathis.age += 1``` et consulter l'âge des deux élèves.
        5. Tester l'instruction ```Eleve.age += 1``` et consulter l'âge des deux élèves.

            !!! warning "Attention"
                Quand on modifie la propriété d'un objet **immutable** depuis l'objet lui-même, cela créé une nouvelle référence vers cette propriété et la propriété initiale est oubliée.  

                Ce comportement n'est plus vrai avec des objets **mutables** comme les listes.
    5.  1. Corriger le fichier **eleve.py** avec le code suivant :
    ``` python title="Implantation d'une classe Eleve'" linenums="1"
    class Eleve:
        nom = "Catteau"
        age = 17
        notes = [20, 13, 15]

    mathis = Eleve()
    elise  = Eleve()
    ```
        2. Tester l'instruction ```mathis.notes.append(5)``` et vérifier qu'Élise a aussi hérité d'un 5.

Les objets peuvent donc partager des propriétés mais ils peuvent aussi partager des actions.  
Pour cela, il suffit de définir des fonctions à l'intérieur de la classe.

!!! question "Partage d'actions"

    1.  1. Corriger le fichier **eleve.py** avec le code suivant :
    ``` python title="Implantation d'une classe Eleve'" linenums="1"
    class Eleve:
        nom = "Catteau"
        age = 17
        
        def vieillir():
            Eleve.age += 1

    mathis = Eleve()
    elise  = Eleve()
    ```
        2. Tester les instructions ```mathis.age```, ```Eleve.vieillir()``` puis vérifier que Mathis et Élise ont vieilli.
        3. Quelle erreur provoque l'instruction ```mathis.vieillir()``` ?

            !!! warning "Attention"

                Quand on appelle une action depuis un objet créé (comme dans l'instruction ```mathis.vieillir()```), python transforme l'instruction en ```Eleve.vieillir(mathis)``` ce qui explique l'erreur obtenue.  

                Pour pouvoir appliquer une action depuis un objet créé, il faut donc ajouter un paramètre à la fonction décrivant l'action. Ce paramètre fait implicitement référence à l'objet qui appelle l'action. Par convention, on le nomme **self**.
    2.  1. Corriger le fichier **eleve.py** avec le code suivant :
    ``` python title="Implantation d'une classe Eleve'" linenums="1"
    class Eleve:
        nom = "Catteau"
        age = 17
        
        def vieillir(self):
            self.age += 1

    mathis = Eleve()
    elise  = Eleve()
    ```

            !!! note "Remarque"
                Comme ```self``` fait référence à l'objet créé (par exemple ```mathis```), l'instruction ```self.age``` a du sens (ici : ```mathis.age```).

        2. Tester une à une dans la console, chacune des instructions suivantes :
        ``` python title="Quelques contrôles" linenums="1"
        mathis.age
        mathis.vieillir()
        mathis.age
        elise.age
        Eleve.vieillir(mathis)
        mathis.age
        elise.age
        ```
    3.  1. Corriger le fichier **eleve.py** avec le code suivant :
    ``` python title="Implantation d'une classe Eleve'" linenums="1"
    class Eleve:
        nom = "Catteau"
        age = 17
        notes = [20, 13, 15]
        
        def ajouter_note(self, note):
            self.notes.append(note)

    mathis = Eleve()
    elise  = Eleve()
    ``` 
        2. Tester une à une dans la console, chacune des instructions suivantes :
        ``` python title="Quelques contrôles" linenums="1"
        mathis.notes
        Eleve.ajouter_note(mathis, 17)
        mathis.notes
        elise.notes
        elise.ajouter_note(10)
        mathis.notes
        elise.notes
        ```

            !!! warning "Important"
                On n'oublie pas que ```self``` fait référence à l'objet qui appelle l'action.

On vient de voir que les propriétés mutables partagées posent des difficultés et empêchent la personnalisation.  
Mais si les actions peuvent être personnalisées, les propriétés (même les mutables) le peuvent également !

!!! question "Propriétés personnelles"

    1.  1. Corriger le fichier **eleve.py** avec le code suivant :
    ``` python title="Implantation d'une classe Eleve'" linenums="1"
    class Eleve:
        
        def nommer(self, nom):
            self.nom = nom
            
        def aimer(self, autre_eleve:"Eleve"):
            self.amour = autre_eleve.nom

    mathis = Eleve()
    elise  = Eleve()
    ```

            !!! note "Important"
                L'instruction ```self.amour = ...``` définit une propriété ```amour``` pour l'objet qui fait appel
                à l'action ```aimer``` (ici ```mathis```)

        2. Tester une à une dans la console, chacune des instructions suivantes :
        ``` python title="Quelques contrôles" linenums="1"
        mathis.nommer("Mathis")
        mathis.nom
        elise.nom
        elise.nommer("Élise")
        elise.nom
        mathis.aimer(elise)
        mathis.amour
        elise.amour
        ```
    2. 1. Corriger le fichier **eleve.py** avec le code suivant :
    ``` python title="Implantation d'une classe Eleve'" linenums="1"
    class Eleve:
    
        def initialiser(self, nom, age):
            self.nom   = nom
            self.age   = age
            self.notes = []
            
        def ajouter_note(self, val):
            self.notes.append(val)
            
    mathis = Eleve()
    elise  = Eleve()

    mathis.initialiser("Mathis", 18)
    elise.initialiser("Élise", 16)

    mathis.ajouter_note(15)
    elise.ajouter_note(17)
    ```

            !!! note "Important"
                L'étape d'initialisation est essentielle pour définir les propriétés personnelles des objets.

        2. Tester une à une dans la console, chacune des instructions suivantes :
        ``` python title="Quelques contrôles" linenums="1"
        mathis.notes
        elise.notes
        mathis.ajouter_note(12)
        mathis.notes
        elise.notes
        Eleve.notes
        ```

On se rend compte alors que les instructions ```mathis = Eleve()``` et ```mathis.initialiser("Mathis", 18)``` ne devraient faire qu'une. C'est le rôle de l'action spéciale ```__init__```.

!!! question "Les actions spéciales"

    1.  1. Corriger le fichier **eleve.py** avec le code suivant :
    ``` python title="Implantation d'une classe Eleve'" linenums="1"
    class Eleve:
    
        def __init__(self, nom, age):
            self.nom = nom
            self.age = age        
            
    mathis = Eleve("Mathis", 18)
    elise  = Eleve("Élise", 16)
    ```
        2. Tester une à une dans la console, chacune des instructions suivantes :
        ``` python title="Quelques contrôles" linenums="1"
        f"{mathis.nom} + {elise.nom} = {chr(0x2665)}"
        f"{mathis.nom} {chr(128139)} {elise.nom}"
        ```
    2. 1. Corriger le fichier **eleve.py** avec le code suivant :
    ``` python title="Implantation d'une classe Eleve'" linenums="1"
    class Eleve:
    
        def __init__(self, nom, age):
            self.nom = nom
            self.age = age

        def __repr__(self):
            return f"{self.nom} ({self.age} ans)"        
            
    mathis = Eleve("Mathis", 18)
    elise  = Eleve("Élise", 16)
    ```
        2. Tester une à une dans la console, chacune des instructions suivantes :
        ``` python title="Quelques contrôles" linenums="1"
        mathis
        elise
        Eleve("Zakaria", 17)
        ```

### À votre tour

!!! question "Travail personnel"

    1. Écrire une classe modélisant une date de Calendrier.
