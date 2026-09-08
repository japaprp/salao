# Auditoria de Producao — Setembro/2026

## Bloqueadores encontrados

### S1 — Corrida de concorrencia permite dois agendamentos no mesmo horario
- Arquivo: `backend/src/modules/appointments/appointments.service.ts`
- `create()` consulta disponibilidade e somente depois chama o repository para criar o agendamento.
- A verificacao nao esta protegida pela mesma transacao/lock da insercao.
- Duas requisicoes simultaneas podem ambas enxergar o horario livre e criar conflitos.
- Correcao: serializar a reserva por profissional/slot ou usar estrategia transacional/constraint adequada.

### S2 — Update pode aceitar entidades relacionadas sem revalidar pertencimento
- Arquivo: `appointments.service.ts`
- `update()` valida disponibilidade do novo profissional quando necessario, mas nao revalida explicitamente `clientId`/`serviceId` quando esses campos entram no payload de atualizacao.
- Como o schema possui `tenantId` separado das FKs, o banco deve impedir combinacoes entre tenants ou o service deve validar todas as relacoes.
- Correcao: validar cada FK contra o tenant e considerar FKs compostas/constraints.

### S3 — Drift entre SQL e Prisma
- Documento `database/RLS_IMPLEMENTATION_GUIDE.md` registra que `appointment_services` existe no SQL bruto mas nao esta modelada no Prisma atual.
- Esse drift cria risco de migrations, queries e runtime divergirem.
- Correcao: uma unica fonte de verdade para schema e migration verificadas em CI.

### S4 — Preco administrativo pode ser informado pelo payload
- Arquivo: `appointments.service.ts`
- `create()` usa `dto.price` quando presente em vez de obrigatoriamente derivar o preco do servico.
- Se o endpoint administrativo permitir entrada nao confiavel, isso pode gerar valores inconsistentes.
- Correcao: separar DTO administrativo de DTO publico e aplicar regras de desconto/alteracao explicitamente.

## Pontos positivos confirmados

- Multi-tenant aparece explicitamente no schema.
- Busca por entidade usa `findByIdAndTenant` nos fluxos principais.
- Fluxo de cliente autenticado confirma pertencimento do agendamento antes de reagendar/cancelar.
- Status possui maquina de transicao.
- Existem CI, mobile/web/backend e documentacao de producao.

## Prioridade

1. Corrigir concorrencia da agenda
2. Fechar integridade de FKs por tenant
3. Eliminar drift Prisma/SQL
4. Separar precificacao administrativa/publica
5. Testes E2E e concorrencia
