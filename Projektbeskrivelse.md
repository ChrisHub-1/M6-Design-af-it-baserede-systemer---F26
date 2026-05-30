Indholdsfortegnelse
Link til Repository - Github	1
Indholdsfortegnelse	1
Projektbeskrivelse:	2
Roller:	3
Projektplan:	4
Hypotetiske:	4
Realitet:	4
Pretotype:	5
Styringsværktøj:	6
Roadmap	6
UML:	6
Use case	7
Sekvensdiagram - Film Search	8
Sekvensdiagram - Login	9
Activity diagram	10
Retrospective	11



Navne og studienummer på gruppemedlemmer

Andreas Møller Hansen: 	20224191

Christian Brolykke Larsen: 	20250653

Christoffer Rask Holler: 	20224891


Gruppe 2, ITL-2, M6, F26


Projektbeskrivelse:
Dette projekt har til formål at udvikle en brugervenlig hjemmeside, der giver danske brugere et hurtigt og enkelt overblik over, hvilke streamingtjenester en bestemt film er tilgængelig på. Formålet er at skabe et samlet alternativ, hvor brugeren nemt kan søge efter film og finde relevante informationer ét sted.
Hjemmesiden skal blandt andet kunne:
Vise populære film og aktuelle trends.
Give mulighed for at søge efter film og se detaljer såsom resume, spillelængde og øvrige oplysninger.
Vise hvor en film kan streames, lejes eller købes.
Give brugeren mulighed for at gemme film på en personlig “Se senere”-liste.
Lade brugeren vælge specifikke streamingtjenester, der skal søges på.
Understøtte login, så brugerdata og præferencer kan gemmes.
Systemet udvikles som en webapplikation bestående af flere HTML-sider. Filmdata og søgefunktionalitet håndteres gennem en API-integration til TMDB (The Movie Database), mens login og brugeroplysninger lagres via Firebase Firestore-database.
Projektet er desuden udviklet med fokus på fremtidige udvidelsesmuligheder. Dette kan blandt andet inkludere understøttelse af TV-serier samt integration af annoncer.







Roller:
Database				Christoffer
Oprette database
Tilkoble database via API
Sikre fungerende oprettelse
Sikre fungerende login

API					Andreas
Oprette API forbindelse til TMDB
Oprette søgefunktion til kriterier
Sikre forbindelse til hjemmeside
Opretholdelse af API Connection og Token

CSS Frontend 			Christian
Sikre ensartet udseende på alle sider
Sikre alle sider connecter til CSS-fil
Sikre CSS-fil er opdateret

HTML Frontend 			Fælles
Frontpage			Christian
Searchpage			Christoffer
Searchpage prototype	Andreas
Profilepage			Andreas
User Settings		Christian
Login				Christoffer
Create User			Christoffer
Cookie Consent		Christian

IT-Arkitektur 			Fælles

Scrum-master 			Christian
Sikre overblik over opgaver
Sikre afholdelse af sprints
Sikre Product backlog / Task-oversigt

Developers 				Christoffer, Christian og Andreas

UML-Diagrams 			Fælles
Use Case Diagram		Christoffer
Sequence Diagram 1	Andreas
Sequence Diagram 2 	Andreas



Projektplan:
Hypotetiske:
Finde dage til at sætte af til projekt
Team kollab
UML
HTML og CSS
JSON
Database forståelse
Database connector
API connector
Test fase

Cyklus inkrementel - MVP - Videre
Agilt
Inspiration fra design thinking:





Realitet:


2 uger scrum sprints
Sprint review
Sprint planning
HTML og CSS
Initiel opsætning
JSON
Branching
Frontend og backend
API
Firebase
Merge fase
UML


Pretotype:



Styringsværktøj: Scrum
Scrum board - Trello
Kan tilgåes her: https://trello.com/b/BoCgYzye/m6-scrum-board



Roadmap



UML:
Use case diagram


Use Case diagrammet er lavet ud fra et “ønske”-scenarie, hvor Firestore lagrer gemte film, streamingtjenester og præferencer. Denne forbindelse til databasen nåede gruppen ikke at implementere, hvorfor det bør ses som videre arbejde.
Sekvensdiagram - Film Søgning

Sekvensdiagram - Login


Retrospective

I projektet blev der umiddelbart opnået de fleste af de funktionaliteter, som der var tiltænkt. Denne generelle projektstyring blev udlevet gennem Scrum, hvor medlemmer af gruppen blev tildelt roller, og hvor der blev arbejdet med sprints af forskellige længder. 

Hernede under bliver der udskrevet hvilke funktionaliteter, der ikke ikke blev nået at implementere:


Firestore til at lagre indstillinger for brugere:
Firestore (den NoSQL database projektet benytter) var tiltænkt at gemme oplysninger for registrerede brugere. Dette gælder de funktioner, som brugeren opnår ved at registrere sig, som består af 
“gemme film til “Min Side”” og “gemte film” - en funktion, hvor en registreret bruger kan gemme film, og tilgå dem senere for at se oplysninger om hvilke streamingtjenester der udbyder dem samt generel kort information omkring disse film
“Administrer streamingtjenester” - en funktion hvor en registreret bruger kunne gemme sine oplysninger omkring hvilke streamingtjenester denne havde adgang til. Hertil kunne der udarbejdes en notifikation, i tilfælde af at en registreret brugers “gemte film” nyligt matchede deres streaming adgang.
“ændre præferencer” - en funktion, hvor brugeren bl.a. kunne vælge mellem light/dark mode og gemme deres tilsagn til cookie præferencer.


E-mail authentication til opretningen af brugere
Som led i projektet brugeroprettelses-funktion udføres der i øjeblikket intet tjek om den indtastede email faktisk eksisterer. Dette kunne tackles ved at sende en request til e-mail-udbyderen, som kunne authenticate at den indtastede email adresse er registreret i deres database. Samtidig kunne der indarbejdes en funktion, hvor brugeren fik tilsendt en autogenereret engangskode, som kunne fungere som en ekstra authenticator, således at der indarbejdes et ekstra lag af sikkerhed, så en given e-mail adresse ikke ville kunne misbruges.
