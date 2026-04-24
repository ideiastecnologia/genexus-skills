# UI Strategy — Preserve Faithful

   Reproduz a hierarquia exata do Form/Layout Part do XPZ. Aplica apenas
   a "skin" `dark-devstudio` sobre a estrutura original.

   ## Regras de geração

   - **Abas:** mesmas abas do Form Part, mesmos nomes, mesma ordem
   - **Campos:** posição (row, col, span) preservada; ordem original
   - **Grids:** mesmas colunas, mesmo número de colunas visíveis,
     scroll horizontal quando necessário (sem truncar)
   - **Labels:** texto original, sem reformular ou traduzir
   - **Botões:** Confirmar / Cancelar / Eliminar mapeados para
     equivalentes modernos mantendo rótulos originais

   ## Componentes React

   - Tabs: shadcn `<Tabs>` com tokens `dark-devstudio`
   - Form layout: CSS Grid seguindo row/col do Form Part
   - Grid: TanStack Table com configuração densa (sem paginação por default)
   - Inputs: componentes padrão mantendo máscaras e validações originais

   ## Trade-offs

   - Cutover zero-friction (usuário final não percebe mudança estrutural)
   - Visual denso, menos "moderno" que as outras opções
   - Ideal para clientes conservadores ou cutover sem janela de treinamento

   ## Usado quando

   - `MigrationPlan.uiStrategy = PRESERVE_FAITHFUL`
   - Cliente declarou prioridade "zero retrabalho de treinamento"
