# UI Strategy — Redesign from Scratch

   Ignora o Form/Layout Part do XPZ. Gera UI a partir do Semantic
   Inventory + skill `frontend-design` + tokens `dark-devstudio`.
   Nomes de abas, agrupamentos e ordem são **inferidos do modelo
   de dados**, não herdados do original.

   ## Regras de geração

   - **Abas:** inferidas por agrupamento semântico de attributes e
     sublevels (ex: "Identificação", "Endereços", "Financeiro")
   - **Campos:** ordenados por relevância e frequência de uso, não
     pela ordem do XPZ
   - **Grids:** DataTable com colunas selecionadas por score de
     importância (PK, FK, campos NOT NULL, campos mais referenciados)
   - **Componentes:** totalmente modernos, sem restrição de equivalência
   - **Hierarquia:** pode mesclar ou dividir abas originais
   - **Densidade:** espaçamento generoso, tipografia editorial

   ## Componentes React

   - Layout: master-detail com sidebar de navegação
   - Tabs/accordions decididos por heurística de quantidade de campos
   - Grid: TanStack Table com column visibility por default reduzida
   - Inputs: shadcn completo + validação com react-hook-form + zod

   ## Trade-offs

   - Melhor resultado estético (demo-ready)
   - Requer treinamento de usuário final (mudança estrutural)
   - Risco de esconder funcionalidade que o usuário dependia
   - Ideal para apresentação comercial, não para cutover direto

   ## Usado quando

   - `MigrationPlan.uiStrategy = REDESIGN`
   - Cliente priorizou modernização sobre continuidade operacional
   - Demo comercial ou projetos greenfield
