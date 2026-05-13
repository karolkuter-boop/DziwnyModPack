# DziwnyModPack

Packwiz modpack dla **DziwnyMod** (NeoForge 1.21.1).

Wymusza na graczach pobranie najnowszej wersji `DziwnyMod` oraz zestawu zależnych modów. Każda zmiana w `pack.toml` (np. podbicie wersji DziwnyModa) propaguje się do klientów przy starcie launchera.

## Zawartość

| Mod                 | Źródło    |
|---------------------|-----------|
| DziwnyMod           | GitHub Releases (`karolkuter-boop/DziwnyMod`) |
| Essential Mod       | Modrinth  |
| GeckoLib 4          | Modrinth  |
| Iris Shaders        | Modrinth  |
| Simple Voice Chat   | Modrinth  |
| Sodium              | Modrinth  |
| WorldEdit           | Modrinth  |
| Xaero's Minimap     | Modrinth  |

> **Lithium** — pominięty. Nie istnieje port na NeoForge 1.21.1; NeoForge ma własne optymalizacje wbudowane.

## Wypuszczanie nowej wersji DziwnyMod

1. W repo `DziwnyMod`:
   - Podbij `mod_version` w `gradle.properties`.
   - `./gradlew build` → JAR ląduje w `build/libs/` (oraz w Prism Launcher instancji, patrz `memory/reference_build_output.md`).
   - Utwórz git tag `v<version>` i wypchnij.
   - Stwórz GitHub Release o tagu `v<version>`, dołącz JAR (`dziwnymod-<version>.jar`).
2. W tym repo (`DziwnyModPack`):
   - Pierwsze dodanie moda:
     ```sh
     packwiz url add dziwnymod "https://github.com/karolkuter-boop/DziwnyMod/releases/download/v1.0.15/dziwnymod-1.0.15.jar"
     ```
   - Aktualizacja do nowej wersji — edytuj `mods/dziwnymod.pw.toml`, zaktualizuj URL i hash, a następnie:
     ```sh
     packwiz refresh
     ```
     albo prościej: `packwiz remove dziwnymod && packwiz url add dziwnymod "<nowy URL>"`.
   - Podbij `version` w `pack.toml` żeby launcher zauważył update.
   - Commit + push.

## Instalacja po stronie gracza

Przez Prism / MultiMC / ATLauncher z packwiz-installer-bootstrap, np.:

```
java -jar packwiz-installer-bootstrap.jar https://raw.githubusercontent.com/<user>/DziwnyModPack/master/pack.toml
```

(URL wskazuje na `pack.toml` w tym repo. Po wypchnięciu na GitHub podstaw właściwą ścieżkę raw.)

## Komendy packwiz — ściąga

```sh
packwiz list                    # wszystkie mody w packu
packwiz modrinth add <slug>     # dodaj z Modrinth
packwiz url add <name> <url>    # dodaj z dowolnego URL (GitHub Releases, CDN itp.)
packwiz update --all            # auto-update wszystkich modów z Modrinth/CF do najnowszej wersji zgodnej z packiem
packwiz refresh                 # przelicz hashe i index po ręcznych zmianach
packwiz remove <name>           # usuń mod
```
