# Teste Técnico: API de Controle de Estoque e Vendas (Nível Sênior)

## Objetivo

Desenvolver uma API REST robusta e otimizada utilizando Laravel, para gerenciar um módulo simplificado de controle de estoque e vendas para um ERP. Este teste foca na capacidade do candidato de resolver problemas de desempenho, escalabilidade e concorrência, além da implementação das funcionalidades básicas.

## Requisitos Técnicos

- Laravel 10+
- PHP 8.1+
- Banco de dados à sua escolha (MySQL, PostgreSQL, SQLite)
- Testes unitários com PHPUnit
- **Conhecimento em filas (queues), cache, otimização de queries (N+1), concorrência e tarefas agendadas (cron jobs).**

## Funcionalidades

### 1. Gerenciamento de Estoque
- Registrar entrada de produtos no estoque com suas respectivas quantidades e preços de custo.
- Consultar o estoque atual com valores totais e lucro projetado.
    - A consulta de estoque (`GET /api/inventory`) deve ser otimizada.
- Implementar uma **tarefa agendada** para limpar registros de estoque antigos, ou seja, que não foram atualizados nos últimos 90 dias.

### 2. Processamento de Vendas
- Registrar uma venda com diversos itens, calculando automaticamente o valor total e a margem de lucro.
    - O processamento da venda e a subsequente atualização do estoque devem ser movidos para uma **fila assíncrona**. A resposta da API deve ser imediata.
- Consultar os detalhes de uma venda.
    - A consulta de uma venda (`GET /api/sales/{id}`) deve ser otimizada.

### 3. Relatórios
- Criar um endpoint para gerar um relatório de vendas, com filtros por período e por produto.

## Requisitos Obrigatórios

1.  Implementar um evento que seja disparado quando uma venda for finalizada, e que acione um **Job** para atualizar o estoque de forma **assíncrona**.
2.  Aplicar **testes unitários** para as principais funcionalidades.
3.  Utilize a estrutura de arquivos que melhor convenha, pensando no desenvolvimento em equipe e na **escalabilidade** da aplicação.
4.  Implemente um mecanismo de **concorrência** para garantir a integridade do estoque ao processar múltiplas vendas simultaneamente.
5.  A consulta de estoque (`GET /api/inventory`) deve ser **cacheada**.
7.  A implementação da limpeza de dados de estoque deve ser feita por meio de uma **tarefa agendada** que rode diariamente.
8.  O endpoint de relatório de vendas (`GET /api/reports/sales`) deve aceitar filtros de data (`start_date`, `end_date`) e SKU do produto (`product_sku`) via query parameters.

## Endpoints
- POST /api/inventory (Registrar entrada de produtos no estoque)
- GET /api/inventory (Obter situação atual do estoque)
- POST /api/sales (Registrar uma nova venda)
- GET /api/sales/{id} (Obter detalhes de uma venda específica)
- GET /api/reports/sales (Gerar relatório de vendas com filtros)

## Estrutura da Base de Dados

1.  **products**:
    - id, sku, name, description, cost_price, sale_price, created_at, updated_at
2.  **inventory**:
    - id, product_id, quantity, last_updated, created_at, updated_at
3.  **sales**:
    - id, total_amount, total_cost, total_profit, status, created_at, updated_at
4.  **sale_items**:
    - id, sale_id, product_id, quantity, unit_price, unit_cost, created_at, updated_at

## Dados para Teste

A aplicação deve incluir dados mocados para 5 produtos diferentes com seus respectivos preços de custo e venda.

## Entrega

1.  Repositório Git público (GitHub, GitLab, Bitbucket)
2.  README básico com instruções de instalação e execução, e detalhes sobre as estratégias de otimização implementadas.

## Prazo

72 horas a partir do recebimento do teste.

Enviar para o e-mail: henrique.souza@cplug.com.br o link do repositório público.
