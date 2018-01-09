

# R on kalkulaator {#calc}

Liidame `2 + 2`. 

```r
2 + 2
#> [1] 4
```

Nüüd trükiti see vastus konsooli kujul `[1] 4`.
See tähendab, et `2 + 2 = 4`.

Kontrollime seda:

```r
## liidame 2 ja 2 ning vaatame kas vastus võrdub 4
answer <- (2 + 2) == 4
## Trükime vastuse välja
answer
#> [1] TRUE
```

Vastus on TRUE, (logical). 

Pane tähele, et aritmeetiline võrdusmärk on `==` (sest = tähendab hoopis väärtuse määramist objektile/argumendile).

Veel mõned näidisarvutused:

```r
## 3 astmes 2; Please read Note ?'**' 
3 ^ 2 # 3**2 also works
## Ruutjuur 3st
sqrt(3)
## Naturaallogaritm sajast
log(100)
```

Arvule $\pi$ on määratud oma objekt `pi`. 
Seega on soovitav enda poolt loodavatele objektidele mitte panna nimeks "pi".

```r
## Ümarda pi neljale komakohale
round(pi, 4)
#> [1] 3.14
```
Ümardamine on oluline tulemuste väljaprintimisel.

## Sama koodi saab kirjutada neljal viisil

Hargnevate teede aed: kui me muudame olemasolevat objekti on meil alati kaks valikut. 
Me kas jätame muudetud objektile vana objekti nime või me anname talle uue nime. 
Esimesel juhul läheb vana muutmata objekt workspacest kaduma aga nimesid ei tule juurde ja säilib teatud workflow sujuvus. 
Teisel juhul jäävad analüüsi vaheobjektid meile alles ja nende juurde saab alati tagasi tulla. 
Samas tekkib meile palju sarnaste nimedega objekte.

Kõigepealt laadime vajalikud raamatukogud. 

```r
## We need piping operator '%>%' from magrittr.
## We can import '%>%' via dplyr from tidyverse
library(dplyr)
```

Esimene võimalus:

```r
a <- c(2, 3)
a <- sum(a)
a <- sqrt(a)
a <- round(a, 2)
a
#> [1] 2.24
```

Teine võimalus:

```r
a <- c(2, 3)
a1 <- sum(a)
a2 <- sqrt(a1)
a3 <- round(a2, 2)
a3
#> [1] 2.24
```

Kolmas võimalus on lühem variant esimesest. 
Me nimelt ühendame etapid toru `%>%` kaudu.
Siin me võtame objekti "a" (nö. andmed), suuname selle funktsiooni `sum()`, võtame selle funktsiooni väljundi ja suuname selle omakorda funktsiooni `sqrt()`. 
Seejärel võtame selle funktsiooni outputi ja määrame selle nimele "result" (aga võime selle ka mõne teise nimega siduda). 
Kui mõni funktsioon võtab ainult ühe parameetri, mille me talle toru kaudu sisse sõõdame, siis pole selle funktsiooni taga isegi sulge vaja. 

> NB! R hea stiili juhised soovitavad siiski ka _pipe_-s kasutada funktsiooni koos sulgudega! 

See on hea lühike ja inimloetav viis koodi kirjutada, mis on masina jaoks identne esimese koodiga.

```r
a <- c(2, 3)
result <- a %>% sum() %>% sqrt() %>% round(2)
result
#> [1] 2.24
```

Neljas võimalus, klassikaline baas R lahendus:

```r
a <- c(2, 3)
a1 <- round(sqrt(sum(a)), 2)
a1
#> [1] 2.24
```
Sellist koodi loetakse keskelt väljappoole ja kirjutatakse alates viimasest operatsioonist, mida soovitakse, et kood teeks. 
Masina jaoks pole vahet. 
Inimese jaoks on küll: 4. variant nõuab hästi pestud ajusid.

Koodi lühidus 4 --> 3 --> 1 --> 2 (pikem)
Lollikindlus  1 --> 2 --> 3 --> 4 (vähem lollikindel)

See on teie otsustada, millist koodivormi te millal kasutate, aga te peaksite oskama lugeda neid kõiki.
