# GeneXus → Node.js NestJS + Next.js Mapping Rules

   **Status:** STUB — Sprint 4 v2

   Regras de mapeamento de objetos GeneXus para stack Node 22 + NestJS
   (backend) + Next.js (frontend). Não implementado na v1; o
   `StubStackMapping` retorna `TODO_STACK_RULES` para este target.

   ## Escopo quando ativado (v2)

   - Transactions → TypeORM entities + NestJS repositories
   - Procedures → NestJS services (`@Injectable`)
   - Web Panels → Next.js pages + React components
   - SDTs → TypeScript interfaces/classes com class-validator
   - GAM → NestJS Passport (JWT strategy)

   ## Dependências

   - Feature flag: ativado quando `cloudpilot.legacy.stacks.node.enabled=true`
   - Requer: implementação de `NodeNestStackMapping` substituindo stub
