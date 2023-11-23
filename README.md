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
# Définition du provider AWS
provider "aws" {
  region = "us-west-2" # Remplacez par votre région AWS
}

# Définition du VPC
resource "aws_vpc" "my_vpc" {
  cidr_block = "10.0.0.0/16" # Plage d'adresses IP pour le VPC
  enable_dns_support = true
  enable_dns_hostnames = true
}

# Définition du subnet dans le VPC
resource "aws_subnet" "my_subnet" {
  vpc_id                  = aws_vpc.my_vpc.id
  cidr_block             = "10.0.1.0/24" # Plage d'adresses IP pour le subnet
  availability_zone       = "us-west-2a" # Remplacez par votre zone de disponibilité préférée

  # Vous pouvez ajouter d'autres configurations de subnet ici
}
```
3. Pour lancer tous ça, il m'a suffit de taper encore une fois ces trois commandes, et le VPC et le subnet ont été créés

-  terraform init

-  terraform plan

-  terraform apply
