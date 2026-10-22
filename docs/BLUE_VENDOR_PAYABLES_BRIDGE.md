# Integração Conexão Azul: contas a pagar recorrentes

**Upstream:** OCA/contract, branch 19.0. **Licença:** AGPL-3.0, preservar os arquivos e créditos originais.

A Conexão Azul utiliza este fork como **motor intacto** de contratos recorrentes de fornecedores. A camada de produto é mantida no repositório privado `conexaoazul/BlueApps19`:

- `blue_account_vendor_recurring`: painel OWL brasileiro para faturas de fornecedores.
- `blue_account_vendor_recurring_contract`: integração `contract.contract` (tipo `purchase`) com o painel.

Revisão em andamento: https://github.com/conexaoazul/BlueApps19/pull/1272

## Regra de integração

**Não renomear** o addon `contract`: modelos `contract.contract`, XML IDs, migrações e cron OCA dependem do identificador técnico. A marca Blue pertence à extensão. Não duplicar cron nem criar faturas a partir do painel; a OCA conserva a geração de `account.move`.

## Instalação em QA isolado

Adicionar os dois repositórios ao `addons_path` do Odoo 19 e instalar `contract`, `blue_account_vendor_recurring`, `blue_account_vendor_recurring_contract`. Realizar snapshot do banco/filestore e desativar processamento automático, pagamentos reais, emissão fiscal e e-mail externo até canário autorizado. Usar contratos e fornecedores fictícios.

**Risco do legado:** o antigo `ca_account_vendor_recurring` presente no BlueApps19 tem clonagem antecipada massiva e rotinas de parcelamento que exigem auditoria. Não combiná-lo com o motor OCA antes de um plano de migração.

## Homologação

Validar ACL multiempresa, periodicidade mensal/anual, criação de rascunho, idempotência da rotina agendada, cálculo da data de competência e vencimento, ausência de pagamento automático e eventual compatibilidade com `l10n_br_account_due_list`. Não instalar `contract_invoice_auto_validate` no piloto.

Não instalar na PHD ou divulgar como entregue antes da aprovação dos gates operacionais, financeiros e de testes.

## Proveniência

Este documento é específico do fork. Os arquivos upstream AGPL-3 e respectivos créditos não foram modificados para esta integração. Manter o fork atualizado a partir de OCA/contract e contribuir upstream quando uma correção geral for pertinente.
