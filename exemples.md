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