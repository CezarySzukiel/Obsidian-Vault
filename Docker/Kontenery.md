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
