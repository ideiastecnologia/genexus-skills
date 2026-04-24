# TOTVS Protheus — External Tables

   Tabelas Protheus que aparecem em KBs de clientes IdeiasHub e devem ser
   tratadas como **External Tables** na migração (não gerar schema novo;
   manter integração por endpoint existente).

   ## Tabelas principais

   | Tabela | Domínio | Observação |
   |---|---|---|
   | SA1010 | Clientes | chave A1_FILIAL + A1_COD + A1_LOJA |
   | SA2010 | Fornecedores | A2_FILIAL + A2_COD + A2_LOJA |
   | SA3010 | Vendedores | A3_FILIAL + A3_COD |
   | SB1010 | Produtos | B1_FILIAL + B1_COD |
   | SC5010 | Pedidos de venda (cabeçalho) | C5_FILIAL + C5_NUM |
   | SC6010 | Pedidos de venda (itens) | C6_FILIAL + C6_NUM + C6_ITEM |
   | SE1010 | Contas a receber | E1_FILIAL + E1_PREFIXO + E1_NUM |
   | SE2010 | Contas a pagar | E2_FILIAL + E2_PREFIXO + E2_NUM |
   | SF1010 | Notas fiscais entrada | F1_FILIAL + F1_DOC |
   | SF2010 | Notas fiscais saída | F2_FILIAL + F2_DOC |
   | CT2010 | Lançamentos contábeis | CT2_FILIAL + CT2_DATA |

   ## Padrão de detecção

   Tabela Protheus é identificada por:
   - Nome seguindo padrão `[A-Z]{2}[0-9]{4}` (ex: SA1010, SB1010)
   - Colunas com prefixo igual às 2 primeiras letras do nome (A1_*, B1_*)
   - Coluna `*_FILIAL` sempre presente como parte da chave

   ## Estratégia de migração

   - **DbStrategy.SAME** (default): app migrado continua lendo/escrevendo
     via endpoints Protheus existentes; nenhum schema novo
   - **DbStrategy.NEW**: não recomendado para tabelas Protheus — alto risco
     de quebrar integrações com outros sistemas ERP
   - **DbStrategy.HYBRID**: event sourcing para sincronizar — só para
     sistemas críticos com cutover longo

   ## TODO Sprint 4

   - Expandir lista com tabelas específicas de módulos (SIGAFAT, SIGAGPE, etc)
   - Documentar padrões de índices compostos

   ## Plataformas cobertas pela Knowledge Base

   A Knowledge Base do CloudPilot (`DsKnowledgeBase`) agora suporta múltiplas
   plataformas, administradas via rotina **Admin → Base de Conhecimento**
   (`/admin/knowledge-base`). Este arquivo documenta apenas o slice `TOTVS`.

   | Platform | Categorias | Status |
   |---|---|---|
   | `TOTVS` | CORE, MODULE, INTEGRATION, FLUIG, TEMPLATE | 32 entries ativas |
   | `SAP` | CORE, MODULE, INTEGRATION | em construção |
   | `RM` | CORE, MODULE, INTEGRATION | em construção |
   | `GENEXUS_MAPPING` | STACK_MAPPING, UI_STRATEGY, PATTERN | 3 placeholders (preenchidos via UI após piloto) |
   | `CUSTOM` | (livre) | entries específicos de cliente |

   Consumidores:
   - `buildTotvsContext()` — jobs do Dev Studio (platform=TOTVS hardcoded por enquanto)
   - `@migration-architect` — consulta `GENEXUS_MAPPING` durante Sprint 4 do
     `PRD-legacy-import-xpz-v1.1`
   - Admin UI — CRUD multi-plataforma por humanos
