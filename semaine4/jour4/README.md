# Formation devOps
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 4

### Jour 4 : Azure devOps ###

---

**1 - Azure devOps**



[ ] <ins>### Initialisation ###</ins>

> Azure interface

> Connectez-vous à Azure DevOps, créez un compte puis une organisation 

> https://aex.dev.azure.com/me

> Créez un nouveau projet nommé : “My Flask App”.

> Accédez à l'onglet "Repos" et créez un nouveau repository Git vide.


👉 Clonez ce [repository](https://github.com/Microsoft/python-sample-vscode-flask-tutorial) sur votre ordinateur.

```
git clone https://github.com/Microsoft/python-sample-vscode-flask-tutorial
cd python-sample-vscode-flask-tutorial
```

👉 Changez origin pour l'url du repo fournie par azure

```
git remote rm origin
git remote add origin <url_repo_azure>
```

>  Azure Interface
>
> Créer les Git credentials ...
>
> user esteve.jm
> mdp zqsqyefvdufhleu5nnj2my3yg4243oe5dihcerb555jsctdz3tgq
>

👉 ... ou Mettez la connection SSH en place

```
ssh-keygen -t rsa-sha2-256 -b 2048
```

Laissez les options par défaut / **PAS DE PASSPHRASE**

```
cat ~/.ssh/id_rsa.pub
```

> Copier la clef et la rajouter sur le site de azureDevops


👉 Envoyez le projet python-sample-vscode-flask-tutorial sur Azure DevOps.

```
git add .
git commit -m "1er commit"
git push origin main
```

👉 Téléchargez l’agent Azure DevOps sur votre VM. Désarchivez le fichier .tar.gz et lancez la configuration de l’agent.

> Créer un pool d'agent
>
_Interface Organisation sur AzureDevOps :_
- Tout en bas à gauche Organisation Settings
- Menu Gauche Pipelines > Agent Pools : Créer un nouveau Pool
- Onglet Agent : Bouton New Agent
- Récupérer l'url de l'agent
>

👉 En local :

```
mkdir ~/azureAgent && cd ~/azureAgent
wget \<URL DE L'AGENT\>
tar zxvf <NOM AGENT>.tar.gz # ex sur Linux à ce jour : vsts-agent-linux-x64-3.241.0.tar.gz
rm -f <NOM AGENT>.tar.gz
```

Configurez l'agent 

```
./config.sh
```

! Attention il demande en Français mais il faut Répondre en anglais

```
Accepter contrat licence ? > Y
URL serveur ? > https://dev.azure.com/{your-organization}
Type authentification > PAT
```

> NB : pour créer un personnal roken : site azure > user setting (en haut à droite) > Personnal Access Token

```
Personnal Token > ************************************
Entrez pool d'agents (appuyez sur Entrée pour default) > <NOM POOL AGENT CREER CI-DESSUS>
Entrez nom de l’agent (appuyez sur Entrée pour <DEFAULT USER>) >  <VOTRE CHOIX>
Entrez dossierr de travail (default _work) > <LAISSER VIDE POUR DEFAUT>
```

👉 Installer l'agent en tant que service Système **systemd** (on pourra utiliser systemctl start agent)

```
sudo ./svc.sh install <LOCAL USER NAME>
```

Démarrer l'agent, check son status et l'arrêter 

```
sudo ./svc.sh start
sudo ./svc.sh status
sudo ./svc.sh stop
```
