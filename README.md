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
