# GeneXus → Python FastAPI + React Mapping Rules

   **Status:** STUB — Sprint 4 v2

   Regras de mapeamento de objetos GeneXus para stack Python 3.13 +
   FastAPI (backend) + React (frontend). Não implementado na v1; o
   `StubStackMapping` retorna `TODO_STACK_RULES` para este target.

   ## Escopo quando ativado (v2)

   - Transactions → SQLAlchemy models + Pydantic schemas
   - Procedures → FastAPI route handlers + service functions
   - Web Panels → React components (mesmo stack do JAVA_SPRING)
   - SDTs → Pydantic models
   - GAM → FastAPI Security com OAuth2 / JWT

   ## Dependências

   - Feature flag: ativado quando `cloudpilot.legacy.stacks.python.enabled=true`
   - Requer: implementação de `PythonFastApiStackMapping` substituindo stub
