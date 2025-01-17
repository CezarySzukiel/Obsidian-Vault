Portainer.io app do zarządzania wszystkim.

CLI - komunikuje się z serwerem, server to daemon. CLI łączy się z daemonen przez http

Applikacja + manifest -> docker build -> tworzy obraz -> docker push (wrzuca obraz na registry zdalne (dockerhub)) -> docker run (tworzy i uruchamia kontener)
image to klasa, kontener to obiekt

OCI image
OCI container
OCI- organizacja, która zdefiniowała standardy kontenerów i imageów. docker spełnia te standardy

container D - buduje obrazy, jest instalowany razem z dockerem


rodzaje manifestów:
- master config
-  FAT Manifest


Public registry (docker hub, cloudy)
local registry

domyśle kontenery są linuxowe (pierwsza warstwa)
na macos i win stawiane są vm, do kontenerów

kontenery windowsowe działają tylko na windowsie. 
unixowych nie ma

wsl to 1:1 linux bez jądra (windows subsystem for linux)

image kontenerów jest readonly, kontenerma dodatkową warstwę read write.
technika copywrite (ride on copy): jeśli chcemy zmienić plik z warstwy readonly to plik jest kopiowany do najwyższej warstwy.

warstwy: BasicOS + App + dependencies + config

kontenery są efemeryczne (stateless) oraz są niemutowalne

FAT Manifest: jak tworzymy image to on może chodzić na różnych architekturach systemu. na FAT Manifest można zdefiniować na jakich architekturach może działać. ale pobierasz tylko jedną architekturę

każda architektura ma swój manifest


instrukcje w dockerfile albo Tworzą warstwy, albo metadane

TTY - interaktywny terminal występuje w docker exec - it (literka t)

ctrl + p + q wyjście z kontenera tak by go nie zabić

restart kontenera nie powoduje skasowania warstwy readwrite. to jeśli go zatrzymam, co innego gdy go zabiję ctrl c

update kontenera: zabijamy stary i tworzymy nowy.


system overlay 2 spłaszcza wszystkie warstwy do jednej

### container lifecycle:
Create
update/ stop/ start/ restart/ (tutaj zachowany jest stan)
Delete

### volumy
- najczęściej są anonimowe
- można je stworzyć z cli, albo w docker-compose
- tworzą się też automatycznie przy tworzeniu kontenera
- na macu docker desktop jest na vm, i volumy tworzą się też na tej VM-ce


dlaczego niue trzyma się logów na tym samym serwerze co app;
- inne zasoby są potrzebne do logów, więc używamy serwerów storageowych
- bezpieczeństwo (jak zostanie zhakowana appka, to logi, bazy danych itp też)

json path- wyszukiwanie w jsonie

zmienne środowiskowe- nie są bezpieczne
są secrets do takich rzeczy jak hasła do DB ale secrets są suppportowane przez docker compose (w D C są nieszyfrowane), więc lepiej docker swarm. tam są różne rodzaje secretów, w tym szyfrowane. ale tego się nie używa tylko k8s.

