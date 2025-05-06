# WeatherApp - Zadanie 1.1
## Autor: Aneliia Henina

Aplikacja webowa stworzona w ramach przedmiotu "Aplikacje w chmurze" (Zadanie 1.1). Umożliwia wybór kraju i miasta oraz wyświetlanie aktualnej pogody z API OpenWeatherMap. Aplikacja loguje informacje o uruchomieniu i jest zapakowana w Docker.

## Instrukcje uruchomienia
1. Sklonuj repozytorium: `git clone <link>`
2. Stwórz plik `.env` z kluczem API OpenWeatherMap.
3. Zbuduj obraz: `docker build -t weather-app-zadanie1.1 .`
4. Uruchom: `docker run --env-file .env -p 8000:8000 weather-app-zadanie1.1`
5. Otwórz: `http://localhost:8000`