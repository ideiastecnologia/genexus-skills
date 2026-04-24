# GeneXus → .NET Blazor Mapping Rules

   **Status:** STUB — Sprint 4 v2

   Regras de mapeamento de objetos GeneXus para stack .NET 8 + Blazor.
   Não implementado na v1 do Dev Studio; o `StubStackMapping` retorna
   `TODO_STACK_RULES` para este target.

   ## Escopo quando ativado (v2)

   - Transactions → Entity Framework Core entities + DbContext
   - Procedures → Services com dependency injection
   - Web Panels → Blazor Server / Blazor WebAssembly components
   - SDTs → DTOs com System.Text.Json
   - GAM → ASP.NET Core Identity

   ## Dependências

   - Feature flag: ativado quando `cloudpilot.legacy.stacks.dotnet.enabled=true`
   - Requer: implementação de `DotNetStackMapping` substituindo stub
