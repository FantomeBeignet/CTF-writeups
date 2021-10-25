# Basic

On voit dans l'énoncé du chall et dans le nom des fichiers que ça parle de ti84, alors on commence par télécharger un émulateur (pour moi tilem2).

Avec ça on peut ouvrir le fichier `.rom`, puis avec `Clic droit > Send file` on envoie le fichier `.8xp` sur la calculatrice émulée.

On se retrouve avec un programme appelé `BASIC` (je sais, très surprenant).

Allons donc voir le contenu de ce programme :
```BASIC
:ClrHome
:ClrList L4
:"F4X67ENQPK0{MTJRHL}O3G59UB-ZAWV8S2YI1CD"->Str2
:{26, 25, 38, 10, 6, 35, 6, 12, 13, 2, 14, 17, 27, 38, 18, 29, 23, 23, 27, 30, 2, 33, 27, 26, 11, 16, 37, 7, 22, 19}->L4
:Input "GUESS :", Str7
:If length(Str7)=/=30:Then
:Disp "WRONG"
:Stop
:End
:For(I,1,30,1)
:If sub(Str7,I,1)=/=sub(Str2, L4(I), 1)
:Then
:Disp "WRONG"
:End
:End
:Disp "CORRECT"
```

La commande `sub(S, I, L)` renvoie la sous-chaîne de `S` de longueur `L` commençant à l'indice `I`.

On peut donc voir qu'on nous demande de rentrer un mot de pass (le flag), qui devra faire 30 caractères et qui semble correspondre à une permutation des lettres de `Str2` dictée par `L4`.

Notre but est de retrouver la permutation en question
Écrivons donc un peu de python:
```python
s = "F4X67ENQPK0{MTJRHL}O3G59UB-ZAWV8S2YI1CD"
l = [26, 25, 38, 10, 6, 35, 6, 12, 13, 2, 14, 17, 27, 38, 18, 29, 23, 23, 27, 30, 2, 33, 27, 26, 11, 16, 37, 7, 22, 19]
res = ""
for i in l:
    res += s[i-1]
print(res)
```

Utiliser l'indice `i-1` est important car en TI-BASIC, tout est indexé à 1 et non à 0 comme en Python.

Le gars qui a fait ce challenge devait vraiment se faire chier en cours de maths...