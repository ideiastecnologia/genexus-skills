# TOTVS Protheus — Knowledge Base Pointer

**Status:** Este arquivo é um ponteiro para a Knowledge Base TOTVS
administrada pela rotina SuperAdmin do CloudPilot.

## Fonte autoritativa

A base de conhecimento TOTVS vive no **banco de dados do CloudPilot**
(tabela gerenciada por `DsKnowledgeBase` entity em `cloudpilot-devstudio`)
e é administrada pela rotina **Admin → Base de Conhecimento** do SuperAdmin.

Atualizações (novas tabelas, novos módulos, correções) devem ser feitas
**exclusivamente via UI do SuperAdmin** — não editar este arquivo nem os
.md files legados em `cloudpilot-devstudio/src/main/resources/knowledge-base/totvs/`.

## Como os agentes devem consumir

Qualquer agente que precise de conhecimento TOTVS (@dev-totvs,
@migration-architect, futuros) deve consumir via API REST:

- `GET /api/v1/dev-studio/knowledge-base?platform=TOTVS` — listagem
- `GET /api/v1/dev-studio/knowledge-base/{id}` — conteúdo específico

O `@migration-architect` no Sprint 4 deve:

1. Detectar tabelas Protheus no Semantic Inventory (padrão `[A-Z]{2}[0-9]{4}`)
2. Consultar a Knowledge Base via API para obter o módulo correspondente
   (ex: tabela SC5010 → consulta entry `sigafat`)
3. Aplicar regras de negócio extraídas dos entries retornados
4. Se tabela não estiver coberta, emitir warning no Semantic Inventory
   sugerindo que o arquiteto TOTVS adicione a cobertura via rotina
   SuperAdmin antes de prosseguir

## Seed inicial (.md files)

Os arquivos em `cloudpilot-devstudio/src/main/resources/knowledge-base/totvs/`
são o **seed inicial** carregado pelo `DsKnowledgeBaseDataLoader` na primeira
inicialização. Após o seed, o source of truth passa a ser o banco.

Editar os .md files diretamente **não tem efeito** em runtime — apenas em
novos deployments que resetem o banco.

## Estratégia de migração (Protheus)

**DbStrategy.SAME** (default para Protheus):
- App migrado continua lendo/escrevendo via endpoints Protheus existentes
- Nenhum schema novo
- Preserva integrações downstream (BI, ETL, conciliação)

**DbStrategy.NEW**: não recomendado — quebra integrações externas.

**DbStrategy.HYBRID**: apenas para sistemas críticos com cutover longo (12+ meses).

## Detecção de tabelas Protheus

Uma tabela é identificada como Protheus quando:
- Nome segue padrão `[A-Z]{2}[0-9]{4}` (ex: SA1010, SB1010, CT2010)
- Colunas têm prefixo igual às 2 primeiras letras do nome (A1_*, B1_*)
- Coluna `*_FILIAL` sempre presente como parte da chave composta

## Cobertura atual (32 entries ativos)

- **9 entries em Core** (AdvPL/TLPP standards, REST API Protheus, SX Dictionary, etc)
- **14 entries em Módulos** (SIGAFIS, SIGAFAT, SIGAFIN, SIGACOM, SIGAEST, SIGAGPE, etc)
- **Entries em Integrações** (CNAB 240, SPED Fiscal, NF-e, etc)
- **Entries em Fluig** (workflows, datasets)

Números exatos por categoria são consultáveis na rotina SuperAdmin.

## Fluxo de atualização

Quando `@migration-architect` encontrar tabela Protheus não coberta:

1. Emitir warning no Semantic Inventory com nome da tabela e contexto
2. Arquiteto TOTVS humano analisa o warning
3. Acessa Admin → Base de Conhecimento na UI SuperAdmin
4. Clica em "Novo Arquivo" ou edita entry existente
5. Salva — mudança imediata, sem redeploy
6. Nova execução do `@migration-architect` já tem a cobertura

**Zero edição de código para ampliar a base.** A rotina SuperAdmin já
tem CRUD completo, versionamento e auditoria.
