docker run: -> wysyła zapytanie przez restapi do docker daemona -> ten daemon wysyła zapytanie przez GRPC do containerD. -> ten z kolei odpala shimy (pośrednik) a te uruchamiają RUNC i one są odpowiedzialne za odpalanie kontenera.
shim wywołuje RUNC

docker daemon: image management

containerD: lifecycle managment

RUNC: low level runtime

przez te shemy może się zdarzyć tak że containerD padnie, daemon padnie, a kontenery nadal będa działać. można nawet podmienić system do zarządzania kontenerami, a same kontenery nie przestaną działać.

![[Zrzut ekranu z 2025-01-14 21-36-05.png]]

docker run 
Docker inspect image - szczegóły imegea

docker push -> teraz robi kompresję (zmienia zawartość  i sumy kontrolne) -> wysyła na serwer
docker pull image -> pobiera image
docker manifest inspect image

docker inspect image -> dużo fajnych danych, jak port, konfiguracja, 

docker history image

docker history --no-trunc --format '{{json .}}' python | jq (trzeba zainstalopwać paczkę jq)

docker stop + docker rm usuwa kontener

docker stop nie zabija kontenera, tylko go zamraża, nie kasuje danych z warstwy readwrite
docker restart używa docker stop i docker start

docker prune - usuwa dunglingi - czyli takie które nie są powiązane z niczym

docker rm -f $(ps -aq)
docker rmi -f $(docker images -aq)
 

## CMD vs Entrypoint: 
jeśli w manifeście jest cmd, to jeśłi podasz jakieś parametry w komendzie uruchamiania kontenera, to parametry przysłonią CMD, a
np docker run ...... i tu moge nadpisać CMD
ENTRYPOINT przed tymi kropkami wstawiłby swoje polecenia
w Docker-compose też można to cmd nadpisać

Expose - informacja na jakim porcie będzie usługa (to tylko metadane)

multi stage build: (używany w językach kompilowanych)
```
From python AS dependencies
WORKDIR /app  
  
COPY . .

RUN pip install -r requirements.txt

FROM python

COPY --from=dependencies /usr/local/bin/ /usr/local/bin/ 
# skopiowanie wyniku instalacji wszystkich paczek (np skopiował by gotowe skompilowane binarki, tylko trzeba znaleźć gdzie one są)

```
docker run -d --name web_c --mount source=web_volume,target=/app web.latest

mount stworzy volume anonimowy o source (jeśłi nie ma voluma podanego w source, to go stworzy(niebezpieczne, bo jak się literówke zrobi))

docker run -d --name web_c --mount type=bind source=./,target=/app web.latest
podpinanie voluma do folderu z kodem (web:latest to nazwa imagea)

jak tworzę bazę danych przez kontener na danym serwerze to gdzie powinien być volume do niej??
- gdzie indziej, na innym serwerze
- ale tak naprawdę to kupuje się gotowe zoptymalizowane usługi na cloudzie, tam nawet postgres będzie działał szybciej niż na zwykłym EC2, bo jest zoptymalizowany pod ich hardware.

żeby obsługiwać volumy, musi być sterownik do dockera
są różne rodzaje volumów i volumy są na innych poziomach
## dobre praktyki:
- kontenery powinny być ultra lekkie
- pushowanie 2 razy najnowszego imagea, pierwszy z nową wersją, a drugi z tagiem lattest, bo latest nie jest automatycznie ustawiany na najnowszym
- każdy image powinien mieć name i tag