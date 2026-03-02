copie des zip de portages non termines, parce que utiliser discord comme cloud c'est surfait non ?

**note importante**: si il vous vient la mauvaise idée de vouloir continuer ses portages,
le chemins de profan dans les sources est a changer, c'est generalement
`/home/pf4/Documents/GitHub/profanOS` ou `../../GitHub/profanOS`, vous devrez les changer vers votre chemin local de profanOS :)

| Name                      | Status | Build in | Notes |
| ------------------------- | ------ | -------- | ----- |
| [bash](bash.zip)          | nope   | linux    | necessite des signaux et termios | 
| [libbearssl](bearssl.zip) | OK ?   | linux    | build mais infernal a utiliser   |
| [gcc](build_gcc.zip)      | OK ~   | linux    | fonctionne mais necessite des ajustements et un gros disque |
| [libX11](libX11.zip)      | nope   | linux    | demande `xcb` et probablement un serveur X11 pour build |
| [mksh](mksh.zip)          | OK ~   | profanOS | build mais vieux et peu utile |
| [toybox](toybox.zip)      | nope   | linux    | INFERNAL ALLEZ BRULER EN ENFER |

| [asqel/PDCurses](https://github.com/asqel/PDCurses)   | OK ? | linux | je crois qu'elle marche |
| [asqel/gameboy-c](https://github.com/asqel/gameboy-c) | OK ~ | linux | il y a 2 ans ça marchait :) |


bon courage
