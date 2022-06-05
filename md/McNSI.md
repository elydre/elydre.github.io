# 1 • Get started

## 1.1 • Telechargement du client

Telechargez et installez [java](https://download.oracle.com/java/18/latest/jdk-18_windows-x64_bin.exe), puis telechargez et extrayez le [zip](https://pf4.ddns.net/dl/mc.zip)
Une fois le zip extrait, executez **TLauncher-MC.exe** (*ou le lanceur de Minecraft officiel si vous avez un compte ^^*).<br>
Cliquez `Créer au moins un compte` puis `+` et `Gratuit`, entrez le pseudo de votre choix et `Add account`.<br>
Retournez sur l'accueil du lançeur et sélectionnez `Forge 1.18.2` dans la liste des versions. (*si forge n'est pas dans la liste, vous pouvez l'ajouter en cliquant sur préférences puis en cochant Modifiée*)<br>
<br>![launcher](https://elydre.github.io/img/launcher.png)<br>
Enfin, cliquez sur l'icône du dossier creez un dossier `mods` et copiez le contenu du dossier `mods` du zip dans ce dossier (*dossier*).<br>
Maintenant, vous pouvez lançer le jeu.<br>

## 1.2 • Configuration

Une fois le jeu lancé, vous pouvez accéder au option et choisir le `Français (Canada)` comme langue. Dans Paramètres graphiques, vous pouvez bais*s*er la qualité, la distance de rendu, etc de pour de meilleures performances.<br>
Sur l'accueil de minecraft, cliquez `Partie multijoueur` puis `Connexion directe` et rentrez l'ip du serveur.<br>

## 1.3 • Construction d'un ordinateur

Placez au sol un `Infinite Energy Cube` puis un `computer`.
Ovrez l'ordinateur et cliquez sur `Open Inventory`. Vous pouvez ajouter des composants comme de la ram, des disques, des cartes d'extension, etc.<br>
Pour la suite, nous aurons besoin d'un disque dur avec Sedna Linux, 24Mo de ram, une carte internet ainsi qu'une carte redstone.<br>
<br>![inventory](https://elydre.github.io/img/inventory.png)<br>
Une fois les composants ajoutés, cliquez sur le bouton power, vous aurrez accès à la console.<br>
Entrez `root` comme nom d'utilisateur. BIENVENUE SUR LINUX!<br>
<br>![shell](https://elydre.github.io/img/shell.png)<br>

# 2 • MicroPython

## 2.1 • Test de python

Dans la console, taper `micropython` pour lancer la console Python.<br>
Testez le classique `print("Hello World")`!<br>

## 2.2 • setup de la lampe

A l'arrière de l'ordinateur, un `Bus Interface` suivi de quelques `Bus Cable` puis a nouveau un `Bus Interface`.<br>
Ajoutez un `Redstone Interface` à l'extrémité de l'interface bus.<br>

<br>![shell](https://elydre.github.io/img/redstone.png)<br>

## 2.3 • Interaction avec la lampe

Redemarrez l'ordinateur et accédez à la console python.<br>
Ecrivez le code suivant:<br>

```py
import devices                  # importe la librairie de devices
bus = devices.bus()             # crée un bus
r = bus.find("redstone")        # cherche un bus redstone
r.setRedstoneOutput("up", 15)   # met un courant de 15 vers le haut
```

Vous pouvez voir la lampe s'allumer.<br>

## 2.4 • Activité

**Faites clignoter la lampe toutes les 2 secondes**.<br>

Indice1: *un courant de 0 fait éteindre la lampe.*<br>
Indice2: *utilisez la fonction* `time.sleep(2)` *pour attendre 2 secondes.*<br>