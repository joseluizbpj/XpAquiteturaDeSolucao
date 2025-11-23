# Arquitetura de Solução

Arquitetura de uma solução de alta disponibilidade para um web app de vendas online, projetada para estar disponível 24/7, resistente a falhas e capaz de lidar com variações de demanda. 
O diagrama foi desenvolvido utilizando a ferramenta draw.io e exportado diretamente em HTML para este repositório.
## Componentes
### Entrada e Distribuição de Tráfego

- Azure Front Door: CDN global com WAF (firewall de aplicação) para proteção e cache.
- Azure Load Balancer: distribui o tráfego entre as VMs nas diferentes zonas.

### Camada de Aplicação

- Virtual Machine Scale set: com auto scaling configurado entre 3 e 6 instâncias Linux, distribuídas em 3 zonas de disponibilidade para garantir que uma falha de zona não derrube o serviço.

### Camada de Dados (PaaS)

- Azure SQL Database (Business Critical): banco gerenciado com réplicas síncronas automáticas em múltiplas zonas, garantindo alta disponibilidade e failover automático.
- Azure Blob Storage: para imagens e assets, com GRS (Geo-Redundant Storage).

### Segurança e IAM

- Managed Identity: identidade gerenciada atribuída às VMs com permissões de leitura/escrita no banco de dados e no Blob Storage, sem necessidade de credenciais no código.
- Azure Key Vault: armazenamento seguro de secrets e certificados.

### Disaster Recovery

- Azure Backup: backups automatizados do banco.
- Geo-Replication: réplica assíncrona em região secundária para recuperação de desastres.

### Monitoramento

- Azure Monitor + Application Insights: observabilidade completa da aplicação e infraestrutura.

## Diagrama
![diagrama estático](https://github.com/joseluizbpj/XpAquiteturaDeSolucao/blob/main/diagrama.png?raw=true)
[Página do diagrama](https://joseluizbpj.github.io/XpAquiteturaDeSolucao/)
