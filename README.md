# Terraform - TP 23.11 - JEGATHASAN Tamilselvan


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
  name        = "ex6"
  description = "Cree avec Terraform"
  private     = true
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
subprocess.run(["terraform", "apply", "-auto-approve"])
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
