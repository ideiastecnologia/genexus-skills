# IdeiasHub KB Patterns

   Convenções e padrões observados em Knowledge Bases de clientes
   IdeiasHub durante o piloto e projetos anteriores.

   ## Convenções de nomenclatura

   - Transactions de negócio: nome singular no domínio (Cliente, Pedido)
   - Procedures de lógica: prefixo `p` seguido de verbo (pCalcularFrete)
   - Web Panels: prefixo `w` ou sufixo `Panel`
   - Attributes: PascalCase com prefixo da entity (ClienteNome, PedidoData)

   ## Padrões de integração

   - Tabelas TOTVS Protheus entram como External Tables (ver `totvs-protheus-tables.md`)
   - GAM (GeneXus Access Manager) usado para autenticação em ~70% dos clientes
   - SDT (Structured Data Types) usados como DTOs de integração

   ## Antipadrões conhecidos

   - Credenciais hardcoded em Procedures (Environment Properties) — ver piloto
   - Business logic em Events de Form (migração mapeia para service layer)
   - Cache local em Transaction sem invalidação (precisa revisão manual)

   ## TODO Sprint 4

   - Expandir com padrões específicos por vertical (logística, varejo, etc)
   - Documentar triggers de banco comuns em integrações Protheus
