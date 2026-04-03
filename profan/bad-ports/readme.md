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
| [mimalloc](mimalloc.zip)  | nope   | profanOS | `/src/prim/profanOS` à implementer pour gerer les pages memoire |
| [mksh](mksh.zip)          | OK ~   | profanOS | build mais vieux et peu utile |
| [toybox](toybox.zip)      | nope   | linux    | INFERNAL ALLEZ BRULER EN ENFER |
| [asqel/PDCurses](https://github.com/asqel/PDCurses)   | OK   | linux | fonctionnel |
| [asqel/gameboy-c](https://github.com/asqel/gameboy-c) | nope | profanOS | ajustements requis pour les nouvelles versions de profan |

| Drivers                   | Issues |
| ------------------------- | ------ |
| [rtl8139](https://github.com/elydre/elydre/blob/main/projet/profan/drivers/rtl8139.c) | fonctionne mal, crash et problemes aleatoires |
| [rtl8168](https://github.com/elydre/elydre/blob/main/projet/profan/drivers/rtl8169.c) | necessite le msi pour fonctionner sur le pc region |

bon courage
