# Migração e arquitetura

## Por que migrar

| Problema atual | Como a nuvem resolve |
|---|---|
| Picos de acesso (Black Friday) podem travar o site | A capacidade cresce sob demanda |
| Componente centralizado: se falha, a loja inteira sai do ar | Duas zonas de disponibilidade: uma assume a outra |
| Fotos e vídeos em disco local dificultam crescer e entregar rápido | O espaço cresce e a entrega é rápida (S3 + CloudFront) |
| Backups mensais e manuais aumentam o risco de perda de dados | Backups automáticos |

## Estratégia de migração

1. **Aplicação da loja → Amazon EC2:** reimplantação do back end e do front end.
2. **Banco legado → Amazon RDS:** migrado com o AWS DMS.
3. **Mídias → Amazon S3:** imagens e vídeos enviados com o AWS DataSync.

## Arquitetura (região São Paulo)

- O cliente acessa pela internet. Fotos e vídeos vêm do **S3 pelo CloudFront**.
- O acesso à loja passa pelo gateway de internet e chega ao **ALB**, que reparte os clientes entre os servidores.
- Os servidores **EC2** ficam em duas zonas de disponibilidade, separados em front end e back end. O **Auto Scaling** mantém de 2 a 4 instâncias por camada (4 a 8 no total).
- O **RDS** fica em sub-rede privada com cópia na outra zona (**Multi-AZ**). O **ElastiCache** acelera as consultas.
- **IAM** e **Security Groups** controlam o acesso. **CloudWatch** monitora e **SNS** avisa a equipe.

Diagrama: [`../arquitetura/diagrama-arquitetura-aws.png`](../arquitetura/diagrama-arquitetura-aws.png)
