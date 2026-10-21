# Estimativa de custos

Região São Paulo, sob demanda, em US$ por mês. O grande pico considerado é uma semana de Black Friday.

| Componente | Como calculamos | Normal | Pico |
|---|---|---|---|
| EC2 t3.medium (FrontEnd) | 2 instâncias × 730 h. Pico: +2 × 168 h | 2.117,68 | 2.605,04 |
| EC2 t3.medium (BackEnd) | 2 instâncias × 730 h. Pico: +2 × 168 h | 2.117,68 | 2.605,04 |
| RDS MySQL Multi-AZ | Configuração RDS × 730 h + armazenamento | 428,41 | 428,41 |
| CloudFront | Tráfego mensal. Pico: +100% por 168 h | 216,45 | 216,45 |
| S3 Standard (500 GB) | 500 GB × 0,0405/GB | 41,13 | 41,13 |
| **Total estimado** | | **≈ 4.921,35** | **≈ 5.896,07** |

## Comparação com e sem Auto Scaling

| Cenário | Custo (US$) |
|---|---|
| Pico no pior caso: 8 servidores por 1 semana (+20% no total) | 5.896,07 (total da arquitetura) |
| Sem Auto Scaling: 8 servidores EC2 ligados o mês todo | 8.470,72 |
| Economia nos servidores no mês de pico (≈ 40%) | 3.260,65 |

## Observações

- Ficaram fora desta conta, por variarem com o uso: **ALB, ElastiCache, CloudWatch e SNS**.
- Valores estimados na AWS Pricing Calculator.
- Os valores da coluna *Normal* vêm da cotação. Os valores de *Pico* são uma simulação condicional.
