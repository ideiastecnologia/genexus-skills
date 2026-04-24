# TOTVS Protheus — External Tables (Reference Pointer)

**Status:** Este arquivo é um ponteiro para a base de conhecimento
TOTVS completa do CloudPilot, não uma duplicação.

## Fonte autoritativa

Base de conhecimento TOTVS mantida no módulo `cloudpilot-devstudio`:
cloudpilot-devstudio/src/main/resources/knowledge-base/totvs/
├── core/
│   ├── advpl-coding-standards.md
│   ├── advpl-debugging-errors.md
│   ├── advpl-to-tlpp-migration.md
│   ├── embedded-sql-patterns.md
│   └── protheus-rest-api.md
├── modules/
│   ├── sigacom.md    (Compras)
│   ├── sigaest.md    (Estoque)
│   ├── sigafat.md    (Faturamento)
│   ├── sigafin.md    (Financeiro)
│   ├── sigafis.md    (Fiscal)
│   └── sigagpe.md    (Gestão de Pessoal)
├── integrations/
│   ├── cnab-240.md   (Arquivos bancários)
│   └── sped-fiscal.md
└── fluig/
├── fluig-datasets.md
└── fluig-workflows.md

## Como os agentes devem consumir

O `@migration-architect` deve consultar a base TOTVS diretamente
quando detectar tabelas Protheus no Semantic Inventory. A estratégia
de integração (DbStrategy.SAME por default) continua documentada
abaixo.

## Detecção de tabelas Protheus no Semantic Inventory

Uma tabela é identificada como Protheus quando:

- Nome segue padrão `[A-Z]{2}[0-9]{4}` (ex: SA1010, SB1010, CT2010)
- Colunas têm prefixo igual às 2 primeiras letras do nome (A1_*, B1_*)
- Coluna `*_FILIAL` sempre presente como parte da chave composta

## Estratégia de migração (default)

**DbStrategy.SAME** (recomendado para Protheus):
- App migrado continua lendo/escrevendo via endpoints Protheus existentes
- Nenhum schema novo no CloudPilot
- Preserva integrações com outros sistemas ERP (BI, ETL, conciliação)

**DbStrategy.NEW**: não recomendado para tabelas Protheus — alto risco
de quebrar integrações downstream.

**DbStrategy.HYBRID**: event sourcing para sincronizar — apenas para
sistemas críticos com cutover longo (12+ meses).

## Módulos cobertos pela base interna

Os 6 módulos SIGA* com cobertura direta:
- **SIGAFIN** — Financeiro (contas a pagar/receber, bancos, fluxo de caixa)
- **SIGAFAT** — Faturamento (pedidos de venda, notas fiscais de saída)
- **SIGACOM** — Compras (pedidos de compra, recebimento)
- **SIGAEST** — Estoque (saldos, movimentações, inventário)
- **SIGAFIS** — Fiscal (escrituração fiscal, SPED, apuração)
- **SIGAGPE** — Gestão de Pessoal (folha de pagamento)

## Módulos não cobertos ainda

Se um KB usar tabelas de módulos fora dos 6 acima, o `@migration-architect`
deve:
1. Marcar como "requer análise manual" no PRD de migração
2. Não assumir DbStrategy sem validação explícita do arquiteto humano
3. Registrar a lacuna para futura expansão da base

Módulos comuns ainda sem cobertura:
- SIGACTB (Contabilidade)
- SIGAATF (Ativo Fixo)
- SIGAPCP (Planejamento e Controle de Produção)
- SIGALOJA (Varejo)
- SIGATMS (Transporte)
- SIGAQIE (Qualidade)
- SIGAMNT (Manutenção de Ativos)
- SIGACRM (Relacionamento com Clientes)

## Integrações cobertas

- **CNAB 240** (`integrations/cnab-240.md`) — arquivos bancários
  padronizados FEBRABAN
- **SPED Fiscal** (`integrations/sped-fiscal.md`) — escrituração
  fiscal digital

## Fluig (workflow + datasets)

Para KBs que se integram com Fluig BPM:
- `fluig/fluig-workflows.md` — modelagem de processos
- `fluig/fluig-datasets.md` — criação de datasets para forms

## Notas de manutenção

Este arquivo é um ponteiro leve. A base real em
`cloudpilot-devstudio/src/main/resources/knowledge-base/totvs/` é
mantida pelo time TOTVS da IdeiasHub e deve ser a fonte de verdade
para todas as regras de negócio Protheus.

Se o `@legacy-analyzer` detectar tabelas Protheus que não batem com
nenhum módulo documentado, emitir um warning no Semantic Inventory
sugerindo expansão da base antes de prosseguir.
