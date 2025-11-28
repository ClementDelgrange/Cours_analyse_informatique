Diagramme de cas d'utilisation :
```plantuml
@startuml
left to right direction
actor Joueur as j
package Démineur {
  usecase "Configurer une partie" as UC1
  usecase "Jouer une partie" as UC2
  usecase "Découvrir une case" as UC3
  usecase "Poser un drapeau" as UC4
}
j -- UC1
j -- UC2
UC2 ..> UC3: <<include>>
UC2 <.. UC4: <<extend>>
@enduml
```

Diagramme de classes:
```mermaid
%% Diagramme de Classes - Démineur
classDiagram
    direction LR

    class Partie {
        - tailleX: int
        - tailleY: int
        - nbMines: int
        -/ nbMinesRestantes: int
        - etat: EtatPartie
        + configurer(x: int, y: int, mines: int)
        + demarrer()
        + decouvrirCase(x: int, y: int)
        + marquerCase(x: int, y: int)
        - verifierEtat()
    }

    class Grille {
        - cases: Case[][]
        + trouverCase(x: int, y: int) Case
        + decouvrirCase(x: int, y: int)
        + marquerCase(x: int, y: int)
        - calculerVoisines(x, y)
        - propagerZero(x, y)
    }

    class Case {
        <<abstract>>
        - x: int
        - y: int
        - etat: EtatCase
        + decouvrir()
        + marquer()
        - changerEtat(e: EtatCase)
    }

    class CaseMinee {
    }

    class CaseNumerotee {
        - int valeur
    }

    class CaseVide {

    }

    %% Enumérations
    class EtatPartie {
        <<enumeration>>
        PREPARATION
        EN_COURS
        GAGNE
        PERDU
    }

    class EtatCase {
        <<enumeration>>
        MASQUEE
        DECOUVERTE
        MARQUEE
    }

    %% Relations
    Partie "1" -- "1" Grille : se joue sur
    Grille *-- "*" Case
    Case <|-- CaseMinee
    Case <|-- CaseNumerotee
    Case <|-- CaseVide
```

