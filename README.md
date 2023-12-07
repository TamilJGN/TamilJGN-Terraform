# Terraform - JEGATHASAN Tamilselvan


## Hello_Terraform

Je suis passé directement par le cloudshell AWS, parce que j'avais un compte AWS. (J'ai mis une carte temporaire !)

1. J'ai créé un repertoire Terraform avec ces commandes

- mkdir mon_projet_terraform
- cd mon_projet_terraform


2. Dans ce repertoire, j'ai créé un fichier dans laquelle j'ai mis ce code

-  nano main.tf

```
// TODO Publier une petite instance AWS EC2
provider "aws" {
 region = "eu-west-3"
}

resource "aws_instance" "debian12" {
ami           = "ami-087da76081e7685da"
instance_type = "t2.micro"
}`
```

3. Pour lancer l'EC2, il m'a suffit de taper ces trois commandes, et l'instance est lancée

-  terraform init

-  terraform plan

-  terraform apply


## Hello_VPC

1. Dans la meme logique que dans le precedent exercice, j'ai créer un dossier avec la commande ci-dessous, et je me dirige vers celui-ci avec la deuxième commande

- mkdir mon_projet_vpc
- cd mon_projet_vpc

2. Je créer le fichier main.tf et j'y ajoute le code ci-dessous

-  nano main.tf

```
provider "aws" {
  region = "us-west-2" # Remplacez par votre région AWS
}

resource "aws_vpc" "my_vpc" {
  cidr_block = "10.0.0.0/16" # Plage d'adresses IP pour le VPC
  enable_dns_support = true
  enable_dns_hostnames = true
}

resource "aws_subnet" "my_subnet" {
  vpc_id                  = aws_vpc.my_vpc.id
  cidr_block             = "10.0.1.0/24" # Plage d'adresses IP pour le subnet
  availability_zone       = "us-west-2a" # Remplacez par votre zone de disponibilité préférée
}
```
3. Pour lancer tous ça, il m'a suffit de taper encore une fois ces trois commandes, et le VPC et le subnet ont été créés

-  terraform init

-  terraform plan

-  terraform apply

## 06_hello_github

1.  J'ai lancé les commande suivante comme vous demandé pour telecharger le terraform

```
Invoke-WebRequest -Uri "https://releases.hashicorp.com/terraform/1.0.0/terraform_1.0.0_windows_amd64.zip" -OutFile "terraform.zip"
Expand-Archive -Path "terraform.zip" -DestinationPath "C:\Terraform"
[System.Environment]::SetEnvironmentVariable("Path", "$env:Path;C:\Terraform", [System.EnvironmentVariableTarget]::User)
```

2.  Voici le contenu de mon main.tf j'ai seulement le nom du repo

```
provider "github" {
  token = "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"
}

resource "github_repository" "mon_repo" {
  name        = var.nom_du_repo
  description = "Cree avec Terraform"
  private     = true
}

variable "nom_du_repo" {
 description = "Nom du dépôt GitHub"
 type        = string
 default     = "test"
}
```

3.  Voici le contenu de mon variable.tf je n'ai rien changé dans ce fichier
   
``` 
variable "nom_du_repo" {
  description = "Nom du dépôt GitHub"
  type        = string
}
```

4. Voici le contenu de du script je n'ai rien changé non plus dans ce fichier

```
import subprocess
import sys

nom_du_repo = sys.argv[1]

subprocess.run(["terraform", "apply", "-auto-approve", f"-var=nom_du_repo={nom_du_repo}"], check=True)
```
Résultat final : Voici le resultat que j'ai eu à la fin, et j'ai bine un repo qui a été créé

```
Plan: 1 to add, 0 to change, 0 to destroy.
github_repository.mon_repo: Creating...
github_repository.mon_repo: Creation complete after 5s [id=ex6]
╷
│ Warning: "private": [DEPRECATED] use visibility instead
│
│   with github_repository.mon_repo,
│   on main.tf line 5, in resource "github_repository" "mon_repo":
│    5: resource "github_repository" "mon_repo" {
│
│ (and 2 more similar warnings elsewhere)
╵

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

## 07_hello_Vultr

Voici mon main.tf
```
terraform {
  required_providers {
    vultr = {
      source = "vultr/vultr"
    }
  }
}

provider "vultr" {
  api_key = "SILLVA2A6J3F6S4SKKSNXAPFNZFMWNFF2MRA"
}

resource "vultr_instance" "tamil" {
  region = "fra"
  plan = "vc2-1c-1gb"
  image_id = "docker"

  user_data = <<-EOF
            #!/bin/bash
            sudo apt-get update
            sudo apt-get install -y docker.io
            sudo systemctl start docker
            sudo systemctl enable docker
            EOF
}
```

## SQL : Katas

Voici la requete pour afficher tous les livres empruntés en 2022

```
SELECT Livres.*
FROM Livres
JOIN Emprunts ON Livres.id = Emprunts.id_livre
WHERE EXTRACT(YEAR FROM date_emprunt) = 2022;
```
![2023-12-07_10h33_35](https://github.com/TamilJGN/TamilJGN-Terraform/assets/93328111/459a4d96-9eb2-47b1-868c-3bc560eb4e0d)

Voici la requête pour afficher le nombre total de livres empruntés.

```
SELECT COUNT(*) AS total_emprunts
FROM Emprunts;
```
![2023-12-07_10h33_24](https://github.com/TamilJGN/TamilJGN-Terraform/assets/93328111/73b39f57-981c-45c8-9e9b-01edb9d628b1)


Voici la requête pour afficher combien de fois chaque genre de livre a été emprunté.
```
SELECT Livres.genre, COUNT(*) AS total_emprunts_par_genre
FROM Livres
JOIN Emprunts ON Livres.id = Emprunts.id_livre
GROUP BY Livres.genre;
```
![2023-12-07_10h33_10](https://github.com/TamilJGN/TamilJGN-Terraform/assets/93328111/b57b6832-ef33-4c99-9cc1-e06949c47564)


