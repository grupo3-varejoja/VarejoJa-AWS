# Datas sazonais e evolução da arquitetura

## Calendário 2026

| Data | Evento |
|---|---|
| 10/05 | Dia das Mães |
| 12/06 | Dia dos Namorados |
| 09/08 | Dia dos Pais |
| 12/10 | Dia das Crianças |
| 27/11 | Black Friday |
| 25/12 | Natal |

## O problema e a solução

Cenário ilustrativo: 1 instância ≈ 1.000 acessos simultâneos.

- **Dia comum:** cerca de 2.000 acessos simultâneos (2 servidores).
- **Black Friday e Natal:** 10 a 12 mil acessos simultâneos (5 a 6 vezes mais). Com só 2 a 4 servidores fixos, o site travaria.

**Solução pensada:**

- Auto Scaling de 4 instâncias (2 front + 2 back) até 8 EC2 no pico.
- CloudFront e ElastiCache reduzem a carga e deixam o site mais rápido.
- Passado o pico, volta ao mínimo, o custo cai e evita gasto desnecessário.

> O limite de 8 EC2 é a capacidade proposta, não uma garantia de suportar 12 mil acessos.

## O que vem depois

| Próximo passo | O que envolve |
|---|---|
| Recuperação de desastres | Definir RTO e RPO, testar restauração de backups e planejar recuperação em outra região |
| Infraestrutura como código | CloudFormation / Terraform para recriar a infraestrutura de forma padronizada e versionada |
| Entrega contínua | Pipelines CI/CD para automatizar testes e implantações |
| Gestão de custos | FinOps e AWS Budgets: acompanhar gastos, criar alertas e ajustar recursos |
