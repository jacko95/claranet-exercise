# AWS CloudFormation Template

Questo script di CloudFormation distribuisce un'infrastruttura di base in AWS per l'hosting di applicazioni Web. L'architettura è costituita da un cloud privato virtuale (VPC) con quattro sottoreti: due sottoreti pubblici e due privati. Le sottoreti pubbliche vengono utilizzate per l'hosting di un bilanciamento del carico e le sottoreti private vengono utilizzate per l'hosting dei server Web. Lo script crea anche un gateway Internet e lo allega al VPC per l'accesso a Internet, nonché un gruppo di sicurezza per consentire il traffico ai server Web.

## Prerequisiti

- Un account AWS
- Accesso alla console AWS o un client AWS CLI installato e configurato

## Come usarlo

1. Apri la console AWS CloudFormation.
2. Scegli "Crea stack" e seleziona "con nuove risorse (standard)".
3. Carica questo script di CloudFormation e seleziona "Crea stack".
4. Nella pagina "Specifica i dettagli dello stack", fornire i parametri richiesti tra cui una chiave e un certificato ACM ARN.
5. Rivedi i parametri e seleziona "Crea stack".
6. Aspetta che lo stack completa la creazione. È possibile monitorare i progressi nella console CloudFormation AWS.

## Architettura

- VPC: definisce la Virtual Private Cloud per l'infrastruttura.
- InternetGateway: definisce l'Internet Gateway per la VPC.
- InternetGatewayAttachment: definisce l'associazione tra l'Internet Gateway e la VPC.
- PublicSubnet1, PublicSubnet2, PrivateSubnet1, PrivateSubnet2: definiscono le subnet per la VPC. Le subnet pubbliche sono associate a una tabella di routing pubblica, mentre le subnet private sono associate a una tabella di routing privata.
- PublicRouteTable: definisce la tabella di routing pubblica per la VPC.
- DefaultPublicRoute: definisce la route predefinita per la tabella di routing pubblica.
- PublicSubnet1RouteTableAssociation, PublicSubnet2RouteTableAssociation: definiscono l'associazione tra le subnet pubbliche e la tabella di routing pubblica.
- MySecurityGroup: definisce il security group per la VPC.
- MyTargetGroup: definisce il target group per il load balancer.
- MyLoadBalancer: definisce il load balancer per la VPC.
