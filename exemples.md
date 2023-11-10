***EXEMPLES

```bash

#!/bin/bash

echo "Sélectionnez une commande à exécuter :"

# Liste des commandes
commands=("date" "ls" "whoami" "df -h" "free -m" "uptime" "ps aux" "top -n 1" "echo Hello World" "ifconfig")

# Affichage des options
for i in "${!commands[@]}"; do
    echo "$((i+1))) ${commands[i]}"
done

# Lecture du choix de l'utilisateur
read -p "Entrez le numéro de votre choix (1-10): " choice

# Vérification de la validité du choix
if [[ $choice -ge 1 && $choice -le 10 ]]; then
    # Exécution de la commande sélectionnée
    eval "${commands[$choice-1]}"
else
    echo "Choix invalide. Veuillez entrer un numéro entre 1 et 10."
fi

```

```bash
#!/bin/bash

echo "Liste des processus connectés à Internet :"
echo "----------------------------------------"

# Utilisation de netstat pour obtenir les connexions actives
# -tupn affiche les connexions TCP/UDP, les processus, et n'effectue pas de résolution de noms
netstat -tupn | grep 'ESTABLISHED' | while read -r line ; do
    # Extraction du PID/Program name
    pid_prog=$(echo $line | awk '{print $7}')
    pid=$(echo $pid_prog | cut -d'/' -f1)
    prog=$(echo $pid_prog | cut -d'/' -f2)

    # Affichage des informations
    if [[ $pid_prog != "-" ]]; then
        echo "Processus: $prog (PID: $pid)"
    fi
done
```

```bash
#!/bin/bash

# Définir le répertoire de départ pour la recherche
# Par exemple, pour chercher dans le répertoire courant, utilisez '.'
# Pour chercher dans tout le système, utilisez '/'
DIRECTORY='.'

# Afficher les fichiers modifiés dans les dernières 24 heures
echo "Fichiers modifiés dans les dernières 24 heures dans $DIRECTORY :"
find "$DIRECTORY" -type f -mtime -1 -print
```

```bash
#!/bin/bash
# URL de l'API web
API_URL="https://api.exemple.com/data"

# En-têtes optionnels, par exemple : Authorization, Content-Type, etc.
# Décommentez et modifiez selon vos besoins
# HEADER="Authorization: Bearer VotreTokenIci"

# Envoi de la requête GET
# Ajoutez -H "$HEADER" après curl si vous utilisez des en-têtes
response=$(curl -s -X GET "$API_URL" /* -H "$HEADER" */)

# Affichage de la réponse
echo "Réponse de l'API :"
echo "$response"

# Traitement de la réponse JSON (si la réponse est au format JSON)
# Vous devez avoir 'jq' installé pour traiter le JSON
# Exemple : echo $response | jq .
```
