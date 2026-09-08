# Salao Da Lu

Plataforma para saloes e negocios de beleza, com backend, web e aplicativo Flutter.

## Objetivo

Evoluir esta base para um **produto comercial reutilizavel para saloes, barbearias e negocios de beleza**, com qualidade de producao e sem depender de telas demonstrativas.

## Stack

- Backend Node.js + Prisma
- MySQL
- Web
- Flutter mobile

## Setup local

1. Inicie o MySQL no XAMPP.
2. Crie o banco `salao_dev`.
3. No backend:

```powershell
cd backend
npx prisma db push
npm run prisma:seed
npm run start:dev
```

4. No web:

```powershell
cd web
npm run dev
```

5. No mobile Flutter:

```powershell
cd mobile
flutter run -d windows
```

Endpoints locais:

- backend: `http://localhost:3100/api`
- web: `http://localhost:3001`

---

# Roadmap de producao real

> **Regra:** funcionalidade planejada deve ser marcada como roadmap. So apresentar como existente aquilo que estiver implementado, testado e validado.

## 1. Agenda e operacao

- [ ] Agenda por profissional
- [ ] Horarios e disponibilidade
- [ ] Bloqueios, feriados e intervalos
- [ ] Agendamento pelo cliente
- [ ] Confirmacao/cancelamento/remarcacao
- [ ] Controle de no-show
- [ ] Lista de espera
- [ ] Servicos com duracao e preco
- [ ] Comissoes por profissional
- [ ] Pacotes e recorrencia quando fizer sentido

## 2. Clientes

- [ ] Cadastro completo
- [ ] Historico de atendimentos
- [ ] Preferencias
- [ ] Anotacoes internas
- [ ] Consentimento de comunicacao
- [ ] Exportacao/exclusao de dados
- [ ] Segmentacao para campanhas

## 3. Financeiro e vendas

- [ ] Caixa
- [ ] Pagamentos
- [ ] Comissoes
- [ ] Relatorios de faturamento
- [ ] Cancelamento/estorno
- [ ] Conciliacao
- [ ] Pacotes/creditos
- [ ] Integracao de pagamento real quando houver cliente pagante

## 4. Notificacoes

- [ ] Confirmacao de agendamento
- [ ] Lembretes
- [ ] Cancelamento/remarcacao
- [ ] Comunicacao por canal configuravel
- [ ] Controle de opt-in/opt-out
- [ ] Fila/retry para mensagens

## 5. Multi-tenant e seguranca

- [ ] Definir isolamento entre negocios
- [ ] Testar acesso cruzado
- [ ] RBAC por funcao
- [ ] Revisar IDOR/BOLA
- [ ] Validacao de entradas
- [ ] Rate limiting
- [ ] Protecao de sessoes/tokens
- [ ] Segredos fora do repositorio
- [ ] Logs sem PII desnecessaria

## 6. Robustez

- [ ] Transacoes nos fluxos financeiros
- [ ] Idempotencia onde houver risco de duplicidade
- [ ] Tratamento consistente de erros
- [ ] Timeouts
- [ ] Retry seguro de jobs
- [ ] Recuperacao apos falhas

## 7. Performance

- [ ] Baseline de API
- [ ] Revisar consultas Prisma/MySQL
- [ ] Indices
- [ ] Paginação em listas grandes
- [ ] Cache quando comprovadamente necessario
- [ ] Teste de carga

## 8. Testes

- [ ] Testes unitarios
- [ ] Testes de API
- [ ] Testes de autorizacao
- [ ] Testes de agenda/conflitos
- [ ] Testes de pagamento
- [ ] Testes E2E dos fluxos principais
- [ ] Testes de regressao
- [ ] Testes de carga

## 9. Observabilidade

- [ ] Logs estruturados
- [ ] Health check
- [ ] Monitoramento de erros
- [ ] Monitoramento de jobs/notificacoes
- [ ] Alertas
- [ ] Metricas de agenda, clientes e faturamento

## 10. Backup e recuperacao

- [ ] Backup automatico
- [ ] Testar restauracao
- [ ] Politica de retencao
- [ ] Rollback de deploy
- [ ] Plano de contingencia

## 11. UX

- [ ] Estados de loading/erro/vazio/sucesso
- [ ] Fluxo de agendamento simples
- [ ] Fluxo de profissional simples
- [ ] Responsividade
- [ ] Experiencia mobile consistente
- [ ] Acessibilidade basica
- [ ] Teste com profissional real

## 12. Produto comercial

- [ ] Onboarding de novo salao/barbearia
- [ ] Configuracao por negocio sem alterar codigo
- [ ] Identidade visual por cliente
- [ ] Planos e limites
- [ ] Treinamento
- [ ] Manual de suporte
- [ ] Checklist de go-live
- [ ] Processo de atualizacao sem interromper clientes

## Criterio de pronto

O produto deve conseguir atender um negocio real de ponta a ponta: agendamento -> atendimento -> pagamento -> comissao/caixa -> historico -> relatorios, com seguranca, testes e tratamento de falhas adequado.

## Deploy

Consulte `PRODUCTION_DEPLOYMENT.md` para o procedimento de producao.
