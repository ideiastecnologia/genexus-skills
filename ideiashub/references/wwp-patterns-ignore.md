# WWP (Work With Plus) Patterns — Ignore List

   Padrões de objetos GeneXus que devem ser classificados como
   `WWP_GENERATED` pelo `ObjectClassifier` e ignorados pelo
   `@migration-architect` (Dev Studio regenera equivalente).

   ## Prefixos de nome

   - `WW*` — Work With root (ex: WWCliente, WWPedido)
   - `Trn*` + sufixo `_BC` — Business Component gerado
   - `*_WorkWithBCLevel*` — level Work With
   - `Prompt*` — prompts gerados
   - `Selection*` — seleções geradas

   ## Sufixos

   - `_WC`, `_WP` — Web Component / Web Panel gerado
   - `_Entry`, `_List`, `_Grid`, `_Filter` — views auto-geradas

   ## Propriedades

   - Object com `Generator.Pattern = Work With Plus`
   - Object com `Generator.Version` presente e `Generator.Source = WWP`

   ## Categoria cruzada

   Se um objeto bate em WWP E em LIB (GAMWWUser, por exemplo), classificar
   como `LIB_IMPORTED` (LIB tem precedência).

   ## TODO Sprint 4

   - Calibrar com KB GLPPortal real (5.736 objetos)
   - Adicionar padrões específicos de Work With Plus v18+
