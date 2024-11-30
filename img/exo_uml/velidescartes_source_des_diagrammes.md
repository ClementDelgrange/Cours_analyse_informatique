Classes
```
@startuml

class Client{
    -numero: integer
    -emprunter_velo(v Velo)
    -deposer_velo(v Velo)
}
class Abonnement{
    -date_debut: date
    -duree_mois: int
    -montant_euros: int
    -est_valide(): bool
}
class Station{
    -nom: string
    -position: Position
    -rayon: integer
    +liberer(v velo): boolean
    +garer(): boolean
    -est_dans_station(p Position): boolean
}
class Velo{
    -numero: integer
    -status: StatusVelo
    -position: Position
    +emprunter(): boolean
    +rendre(s Station, incident boolean): boolean
    +reparer()
    -mettre_a_jour_position()
}
class Location{
    -date_heure_debut: datetime
    +terminer()
}
class Position {
    -longitude: float
    -latitude: float
}
class Gestionnaire {
}

enum Statusvelo {
LIBRE
OCCUPE
EN_PANNE
}

Client "1" -- "*" Abonnement: s'acquite
Client "*" -- "*" Velo
Velo "*" -- "0..1" Station: stationne
(Client,Velo) .. Location
Velo "1" -- "1" Position: est situé à
Station "1" -- "1" Position: est situé à
Gestionnaire "*" -- "*" Velo: demande reparation

@enduml
```


Etats-transitions vélo
```
@startuml
[*] --> Libre
Libre --> Occupé: [est emprunté]
Occupé --> Endommagé: [est déposé avec un signalement]
Occupé --> Libre: [est déposé]
Endommagé --> Libre: [est réparé]
@enduml
```


Activité prendre abonnement
```
@startuml
(*) --> "Demander date début"

if "Abonnement déjà valide à cette date?" then
  -->[oui] "Impossible d'avoir
deux abonnements
valides en même temps"
  --> (*)
else
  -->[non] "Demander type abonnement"
  --> "Faire payer"
  --> "Créer abonnement"
  --> (*)
endif
@enduml
```


Séquence emprunter un vélo
```
@startuml
participant "c:Client" as client
participant ":Abonnement" as abonnement
participant ":Location" as location
participant "v:Velo" as velo
participant ":Station" as station


activate client
client -> abonnement: est_valide()
activate abonnement
abonnement --> client: oui
deactivate abonnement

client -> velo: emprunter()
activate velo
opt v.status == LIBRE
    velo -> station: liberer(v)
    activate station
    station -> station: est_dans_station(v.position)
    opt true
        station --> velo: true
        velo -> velo: status = OCCUPE
        velo --> client: true
        create location
        client -> location: Location(now(), c, v)
    else
        station --> velo: false
        deactivate station
        velo --> client: false
    end
else
    velo --> client: false
end
deactivate velo

deactivate client

@enduml
```


Séquence déposer un vélo
```
@startuml
participant "c:Client" as client
participant ":Location" as location
participant "v:Velo" as velo
participant "s:Station" as station


activate client
client -> velo: deposer(s, a_incident)
activate velo
velo -> station: deposer(v)
activate station
station -> station: est_dans_station(v.position)
opt true
    station --> velo: true
    opt a_incident == true
        velo -> velo: status = LIBRE
    else
        velo -> velo: status = LIBRE
    end
    velo --> client: true
    activate location
    client -> location: terminer()
    deactivate location
else
    station --> velo: false
    deactivate station
    velo --> client: false
end
deactivate velo

deactivate client

@enduml
```