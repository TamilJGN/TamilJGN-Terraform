Terraform
01_hello_terraform
Installation de Terraform sur la CloudShell AWS :

git clone https://github.com/tfutils/tfenv.git ~/.tfenv

echo 'export PATH="$HOME/.tfenv/bin:$PATH"' >> ~/.bashrc

exec $SHELL

tfenv install latest

tfenv use 1.6.4

https://github.com/DocteurSEO/terraform.git

cd terraform/01_hello_terraform/

nano main.tf

// TODO Publier une petite instance AWS EC2
provider "aws" {
 region = "eu-west-3"
}

resource "aws_instance" "debian12" {
ami           = "ami-087da76081e7685da"
instance_type = "t2.micro"
}
terraform init
terraform plan
terraform apply
