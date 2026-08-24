# Binding in Distrobox/Sandbox Environments

## Perché serve il binding?

In ambienti containerizzati come **Distrobox**, **Toolbox**, o
applicazioni sandboxate (es. Flatpak), un server locale può non essere
accessibile dall'host se è bindato solo su `localhost`.

Il binding definisce **da quali interfacce IP** il server accetta
connessioni.

------------------------------------------------------------------------

## Situazione tipica

Lanci:

``` bash
python3 -m http.server 8000
```

Questo fa il bind su:

    127.0.0.1

Dentro un container questa interfaccia è *solo interna* al container.\
L'host non può raggiungerla.

------------------------------------------------------------------------

## Soluzione

### Bind aperto a tutte le interfacce

``` bash
python3 -m http.server --bind 0.0.0.0 8000
```

Così il container espone il server anche all'host.

Apri dal browser dell'host:

    http://localhost:8000

------------------------------------------------------------------------

## Bind più restrittivo (ma compatibile)

``` bash
python3 -m http.server --bind 127.0.0.1 8000
```

Utile se usi un browser *dentro lo stesso container*.\
Non funziona se devi raggiungerlo da fuori.

------------------------------------------------------------------------

## Nota su Flatpak e browser

Anche se i browser Flatpak sono sandboxati, **possono accedere a
`localhost`**, ma se il server è in un container devi comunque usare
`--bind 0.0.0.0`.

------------------------------------------------------------------------

## Riepilogo rapido

  ------------------------------------------------------------------------
  Scenario                Comando corretto
  ----------------------- ------------------------------------------------
  Server in host +        `python3 -m http.server 8000`
  browser host            

  Server in Distrobox +   `python3 -m http.server --bind 0.0.0.0 8000`
  browser host            

  Server in Distrobox +   `python3 -m http.server --bind 127.0.0.1 8000`
  browser *nel container* 
  ------------------------------------------------------------------------

------------------------------------------------------------------------

## Troubleshooting veloce

### Verifica che la porta sia aperta:

``` bash
ss -tulpn | grep 8000
```

### Se non risponde:

-   assicurati di essere nel container giusto
-   riprova con `--bind 0.0.0.0`
-   verifica che non ci sia un firewall che blocca

------------------------------------------------------------------------

## Fine

File pensato per riferimento rapido durante sviluppo in container, Fedora, Distrobox e ambienti sandboxati.
