# IdeiasHub Extensions for genexus-skills

   Extensões proprietárias da IdeiasHub Tecnologia sobre o upstream
   `genexuslabs/genexus-skills`. Usadas pelos agentes `@legacy-analyzer`
   e `@migration-architect` do CloudPilot Dev Studio.

   ## Estrutura

   - `references/` — padrões, tabelas e regras observadas em KBs de clientes
   - `mapping-rules/` — regras de conversão GeneXus → stacks modernos

   ## Integração

   Este diretório é consumido via git submodule em
   `cloudpilot-api/src/main/resources/skills/genexus-skills/ideiashub/`
   e exposto aos agentes MCP do `cloudpilot-agent-runner` via `SKILL_PATH`.
