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