# UI Strategy — Preserve with Adjustments (RECOMENDADA)

   Mantém estrutura macro do Form Part (abas com nomes originais, ordem
   geral) mas moderniza implementação de componentes. É o **default**
   recomendado pelo wizard de importação.

   ## Regras de geração

   - **Abas:** mesmas abas, mesmos nomes, mesma ordem
   - **Campos dentro da aba:** reagrupados em seções semânticas quando
     denso (>15 campos em uma aba); sem mudar de aba
   - **Grids:** substituídos por DataTable com paginação server-side
     quando >100 linhas; mesmas colunas visíveis por default, com
     toggle de densidade
   - **Componentes legados:** substituídos por equivalentes modernos:
     - GeneXus checkbox → shadcn `<Switch>`
     - GeneXus select → shadcn `<Combobox>` tipado
     - GeneXus date picker → shadcn `<DatePicker>`
   - **Responsividade:** real (breakpoints mobile/tablet/desktop),
     não tabelas de largura fixa

   ## Componentes React

   - Tabs: shadcn `<Tabs>` com tokens `dark-devstudio`
   - Form layout: CSS Grid responsivo com seções (FieldGroup)
   - Grid: TanStack Table + paginação + column visibility toggle
   - Inputs: shadcn `<Input>`, `<Select>`, `<Combobox>`, etc

   ## Trade-offs

   - 80% familiar ao usuário GeneXus (abas, nomes, fluxo)
   - 100% moderno em componentes individuais
   - Permite iterar depois sem retrabalho estrutural

   ## Usado quando

   - `MigrationPlan.uiStrategy = PRESERVE_WITH_ADJUSTMENTS` (default)
   - Default do wizard em Sprint 3
