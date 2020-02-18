# 1 - Variables d'environnements 
Pour afficher les dossiers ou l'ont peut trouver les commandes ils faut afficher la variable d'environnement $Path avec : `echo $PATH`

Pour revenir dans notre dossier personnel on utilise : `cd ~`

Quelques autes variables d'environnements :  
- LANG : Cette variable permet d'afficher l'encodage utilisé
- PWD : Permet d'afficher le dossier local (la ou on se trouve) ainsi que des infrmations sur celui-ci
- OLDPWD : Permet d'afficher le dossier local précédent (la ou on se trouvais) ainsi que des informations sur celui-ci
- SHELL : permet d'accéder au dossier de votre Bash

Pour créer une **variable de bash** on fait : `MY_VAR="zzezzezezez"`, on peut aussi faire `export VAR="azazazazaza"` pour céer **une variable d'envrionnement**. Attention : si on fait pas un `echo $VAR`, le bash va essayer d'executer ce qu'il y a a l'intérieur comme une commande.

La commande bash permet de créer une nouvelle session, ainsi lorsque l'on fait `bash`, nos variables d'environnements disparaissent. La commande `exit` ou `ctrl + D` permet de quitter la session et revenir a la précédente.

pour créer une variables d'envrionnement et l'afficher on va faire : 
```
export NOMS="Notin Penot"  
echo $NOMS  
    Notin Penot  
```
Il est aussi possible de créer et exécuter une commande via une variable d'envionnement (Attention respecter les guillemets): 
```
export NOMS='echo "Bonjour à vous deux, binôme1 binôme2!"'
$NOMS
    Bonjour à vous deux, binôme1 binôme2!
```

Si on donne une valeur vide la variable d'environnement existe toujours mais est vide, alors que la ocmmande unset ermet de la supprimer de la liste des variables de bash ou d'environnements

echo "$HOME =chemin (où chemin est votre dossier personnel d’après bash)"

# 2 - Contrôle de mot de passe

**Cette commande permet d'executer un fichier (donner les droits) :** ``chmod u+x testreel.sh``

Le script permettant de vérfier un mot de passe est : 
```
#!/bin/bash

pass="123456"
read -s -p "Rentre le mdp man ! " p
if [ $p = $pass ]; then
        echo "Bravo !"
else
        echo "Tu es mauvais"
fi
```

# 3 - Expressions rationnelles

```
#!/bin/bash


function is_number(){
        re='^[+-]?[0-9]+([.][0-9]+)?$'
        if ! [[ $1 =~ $re ]] ; then
                return 1
        else
                return 0
        fi
}

if is_number $1; then
        echo "c'est bien un reel"
else
        echo "erreur : ce n'es pas un reel"
fi

```

# 4 - Contrôle d’utilisateur

```
#!/bin/bash

if ! [[ $# = 1 ]]; then
        echo "Utilisation :nom_du_scriptnom_utilisateur"
        exit
fi
users=`cut -d : -f1 /etc/passwd | grep ^$1$ | wc -l`
echo "$users "
if [[ $users -eq 0 ]]; then
        echo "cet utilisateur n'existe pas"
else
        echo "Cet utilisateur existe bien"
dx
```

# 5 - Factorielle

```
#!/bin/bash


i=1;
resultat=1
for i in $(seq 1 $1); do
        resultat=$((resultat*i))
done
echo $resultat
```

# 6 - Juste Prix 

```
#!/bin/bash

nb=$((RANDOM%1000))
read -p "Entrez un nombre" unb
while [[ $unb -ne $nb ]]; do
if [ $unb -lt $nb ]; then
        read -p "Dommage essaie encore man ! C'est plus !" unb
else
        read -p "Dommage essaie encore man ! C'est moins !" unb
fi
done
echo "bigup, NOUS AVONS UN JUSTE PRIX !"
```

# 7 - Statistiques

### Question 1 & 2 : 

```
#!/bin/bash
max=$1
min=$1
nb=$#
moy=0
while (("$#")); do
echo $1
if [ $1 -lt $min ]; then
        min=$1
fi
if [ $1 -gt $max ]; then
        max=$1
fi

moy=$((moy+$1))
shift
done
moy=$((moy/nb))
echo "la moyenne est $moy, le max est $max et le min est $min"

```

### Question 3 :
```
#!/bin/bash
max=0
min=0
moy=0
i=0;
tab[]
while ((true)); do
read -p "Entrz une note" val
tab[i]=$val;
echo $val
if [ $val = "exit" ];then
    break
fi
if [ $val -lt $min ]; then
        min=$val
fi
if [ $val -gt $max ]; then
        max=$val
fi
moy=$((moy+val))
i=$((i+1))
shift
done
moy=$((moy/nb))
echo "la moyenne est $moy, le max est $max et le min est $min"

```
# Exercice 8

Pour les couleurs, on ouvre avec `\033[0` et on ferme avec `m`.

```
#!/bin/bash

echo "FG\\BG 40   41   42   43   44   45   46   47"
for ((i=30;i<=37;i++)); do
        echo -n "$1 "
        for ((j=40;j<=47;j++)); do
                echo -n -e "\033[0;"$i"m\033["$j"mBASH\033[0m"
        done
        echo ""
done
```
