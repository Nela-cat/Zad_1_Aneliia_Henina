

Programowanie aplikacji w chmurze obliczeniowej 
SPRAWOZDANIE Zadanie 1
Grupa: IO 6.4  
 		 	 
Temat zajęć: 	Zadanie 1.1 - Aplikacje w chmurze 
	 
 	data zajęć: 06.05.25 
Imię  i nazwisko 	Aneliia Henina		Prowadzący: 
dr inż. Sławomir Przyłucki 
 
 
 
Opis projektu
Aplikacja WeatherApp umożliwia sprawdzenie aktualnej pogody w wybranym mieście na podstawie API OpenWeatherMap.

Środowisko
- Python 3.10
- FastAPI
- Uvicorn
- Jinja2
- Requests
- python-dotenv
- python-multipart
## Rozmiar obrazu
- Nazwa obrazu: `weather-app-zadanie1.1`
- Rozmiar: ~200MB
- Liczba warstw: 16

Polecenia Docker
- a. Budowa obrazu:
docker build -t weather-app-zadanie1.1 .

  Wyjście komendy:
  # [+] Building 23.1s (14/14) FINISHED docker:desktop-linux
  # => [internal] load build definition from Dockerfile 0.0s
  # => => transferring dockerfile: 996B 0.0s
  # => [internal] load metadata for docker.io/library/python:3.10-slim 0.7s
  # => [internal] load .dockerignore 0.0s
  # => => transferring context: 109B 0.0s
  # => [builder 1/5] FROM docker.io/library/python:3.10-slim@sha256:57038683f4a259e17f 0.0s
  # => [internal] load build context 0.0s
  # => => transferring context: 1.62kB 0.0s
  # => CACHED [builder 2/5] WORKDIR /app 0.0s
  # => [stage-1 3/6] RUN apt-get update && apt-get install -y curl && rm -rf /var/lib 21.0s
  # => CACHED [builder 3/5] COPY requirements.txt . 0.0s
  # => CACHED [builder 4/5] RUN pip install --no-cache-dir -r requirements.txt 0.0s
  # => CACHED [builder 5/5] RUN rm requirements.txt 0.0s
  # => [stage-1 4/6] COPY --from=builder /usr/local/lib/python3.10/site-packages/ /usr 0.9s
  # => [stage-1 5/6] COPY --from=builder /usr/local/bin/ /usr/local/bin/ 0.0s
  # => [stage-1 6/6] COPY . /app 0.0s
  # => exporting to image 0.3s
  # => => exporting layers 0.3s
  # => => writing image sha256:a9b5cf6ac3c7d1796a3ab04bdf339a256ba435f719914e9471d9ad6 0.0s
  # => => naming to docker.io/library/weather-app-zadanie1.1 0.0s
  # Komentarz: Komenda buduje obraz na podstawie zoptymalizowanego Dockerfile.

- b. Uruchomienie kontenera:
  docker run -d -p 8000:8000 --name weather-app-container --env-file .env weather-app-zadanie1.1


Wyjście komendy:
  # 96513a086311d5825bf0250170b96fc1732e2c535861c474f2cfe863c562b55f
  # Komentarz: Uruchamia kontener, przekazując klucz API przez plik .env.

- c. Sposób uzyskania informacji z logów:
docker logs weather-app-container


  Wyjście komendy:
  # INFO:     Started server process [1]
  # INFO:     Waiting for application startup.
  # INFO:src.main:Uruchomienie aplikacji (Zadanie 1.1): 2025-05-06 12:46:54
  # INFO:src.main:Autor: Aneliia Henina
  # INFO:src.main:Port TCP: 8000
  # INFO:     Application startup complete.
  # INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
  # Komentarz: Wyświetla logi aplikacji, w tym datę, autora i port.

- d. Sprawdzenie liczby warstw oraz rozmiaru obrazu:
docker history weather-app-zadanie1.1




Wyjście komendy: 
IMAGE          CREATED          CREATED BY                                      SIZE      COMMENT
706093b2ff9b   25 minutes ago   CMD ["uvicorn" "src.main:app" "--host" "0.0.…   0B        buildkit.dockerfile.v0
<missing>      25 minutes ago   HEALTHCHECK &{["CMD-SHELL" "curl -f http://l…   0B        buildkit.dockerfile.v0
<missing>      25 minutes ago   COPY . /app # buildkit                          15.7kB    buildkit.dockerfile.v0
<missing>      4 hours ago      COPY /usr/local/bin/ /usr/local/bin/ # build…   19.4kB    buildkit.dockerfile.v0
<missing>      4 hours ago      COPY /usr/local/lib/python3.10/site-packages…   30.9MB    buildkit.dockerfile.v0
<missing>      4 hours ago      RUN /bin/sh -c apt-get update && apt-get ins…   5.12MB    buildkit.dockerfile.v0
<missing>      4 hours ago      WORKDIR /app                                    0B        buildkit.dockerfile.v0
<missing>      3 weeks ago      CMD ["python3"]                                 0B        buildkit.dockerfile.v0
<missing>      3 weeks ago      RUN /bin/sh -c set -eux;  for src in idle3 p…   36B       buildkit.dockerfile.v0
<missing>      3 weeks ago      RUN /bin/sh -c set -eux;   savedAptMark="$(a…   43.2MB    buildkit.dockerfile.v0
<missing>      3 weeks ago      ENV PYTHON_SHA256=4c68050f049d1b4ac5aadd0df5…   0B        buildkit.dockerfile.v0
<missing>      3 weeks ago      ENV PYTHON_VERSION=3.10.17                      0B        buildkit.dockerfile.v0
<missing>      3 weeks ago      ENV GPG_KEY=A035C8C19219BA821ECEA86B64E628F8…   0B        buildkit.dockerfile.v0
<missing>      3 weeks ago      RUN /bin/sh -c set -eux;  apt-get update;  a…   9.23MB    buildkit.dockerfile.v0
<missing>      3 weeks ago      ENV LANG=C.UTF-8                                0B        buildkit.dockerfile.v0
<missing>      3 weeks ago      ENV PATH=/usr/local/bin:/usr/local/sbin:/usr…   0B        buildkit.dockerfile.v0
<missing>      3 weeks ago      # debian.sh --arch 'amd64' out/ 'bookworm' '…   74.8MB    debuerreotype 0.15
  # Komentarz: Wyświetla liczbę i szczegóły warstw.
  # Komentarz: Wyświetla rozmiar obrazu.



Linki
- GitHub: https://github.com/Nela-cat/Zad_1_Aneliia_Henina/tree/main/zad1/weather-app-zadanie1.1
- DockerHub:  https://hub.docker.com/repository/docker/nelacot/zad_1/tags


