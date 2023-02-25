# AWS CloudFormation Template

Questo template CloudFormation crea un'istanza EC2 con Nginx installato e un load balancer che distribuisce il traffico alle istanze EC2.

## Prerequisiti

- Un account AWS
- Accesso alla console AWS o un client AWS CLI installato e configurato

## Come usare

1. Accedi alla console AWS o apri il client AWS CLI.
2. Creare una coppia di chiavi EC2 nel menu Key Pairs della console o con il comando `aws ec2 create-key-pair` del CLI.
3. Scarica il file PEM contenente la tua chiave EC2 e conservalo in un luogo sicuro.
4. Aprire il file `template.yml` e sostituire i valori `KeyName`, `PublicSubnet1`, `PublicSubnet2`, `VPC` e `MySecurityGroup` con i valori appropriati.
5. Creare lo stack di CloudFormation usando il comando `aws cloudformation create-stack` o usando la console AWS.
6. Attendere il completamento della creazione dello stack.
7. Accedere all'indirizzo IP del bilanciatore di carico nella console EC2 o usando il comando `aws cloudformation describe-stacks` del CLI.

## Architettura

- 1 istanza EC2 con Nginx installato
- 1 gruppo di sicurezza EC2
- 1 bilanciatore di carico che distribuisce il traffico alle istanze EC2

### Architettura dettagliata

- EC2 instance:
  - Amazon Linux 2 AMI
  - t2.micro instance type
  - Nginx installed
  - Launch configuration with User data script to configure Nginx and serve a basic HTML page
- Security Group:
  - Allows SSH access from anywhere
  - Allows HTTP access from anywhere
- Elastic Load Balancer:
  - Application Load Balancer
  - Internet-facing
  - Listens on port 80
  - Routes traffic to the EC2 instances in the target group
- Target Group:
  - Health check enabled
  - Health check listens on port 80 and checks the root path
  - Targets are the EC2 instances created by the Auto Scaling group

## Template details

### Resources

- `EC2Instance`: Amazon EC2 instance running the specified Amazon Machine Image (AMI).
- `MySecurityGroup`: Gruppo di sicurezza che consente l'accesso SSH e HTTP.
- `MyTargetGroup`: Gruppo di destinazione per il bilanciatore di carico che controlla lo stato della salute dell'istanza EC2.
- `MyLoadBalancer`: Bilanciatore di carico di applicazioni che distribuisce il traffico alle istanze EC2.
- `MyLaunchConfiguration`: Configurazione di lancio per l'istanza EC2.

### Outputs

- `WebsiteURL`: L'URL del sito Web che utilizza il bilanciatore di carico.

### Codice

