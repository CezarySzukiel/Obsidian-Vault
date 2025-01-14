docker run: -> wysyła zapytanie przez restapi do docker daemona -> ten daemon wysyła zapytanie przez GRPC do containerD. -> ten z kolei odpala shimy (pośrednik) a te uruchamiają RUNC i one są odpowiedzialne za odpalanie kontenera.
shim wywołuje RUNC

docker daemon: image management

containerD: lifecycle managment

RUNC: low level runtime

przez te shemy może się zdarzyć tak że containerD padnie, daemon padnie, a kontenery nadal będa działać. można nawet podmienić system do zarządzania kontenerami, a same kontenery nie przestaną działać.

![[Zrzut ekranu z 2025-01-14 21-36-05.png]]


Docker inspect image - szczegóły imegea

docker push -> teraz robi kompresję (zmienia zawartość  i sumy kontrolne) -> wysyła na serwer
docker pull image -> pobiera image
docker manifest inspect image

docker inspect image -> dużo fajnych danych, jak port, konfiguracja, 

docker history image

docker history --no-trunc --format '{{json .}}' python | jq (trzeba zainstalopwać paczkę jq)

CMD vs Entrypoint: 
jeśli w manifeście jhest cmd, to jeśłi podasz jakieś parametry w komendzie uruchamiania kontenera, to parametry przysłonią CMD, a