# 💅 Studio Dani Nails - Sistema de Agendamento Inteligente

Sistema de agendamento *mobile-first* desenvolvido para profissionais autônomos do setor de beleza. O projeto permite que clientes agendem serviços online de forma visual e fluida, gerando links dinâmicos para que a profissional gerencie e confirme os atendimentos via WhatsApp com custo zero de infraestrutura e API.

## 📝 Descrição do Projeto
O projeto nasceu da necessidade real de automatizar o fluxo de marcação de horários de um salão de manicure local, eliminando o tempo gasto com atendimento manual e reduzindo o índice de ausências de clientes. 

O grande problema de micronegócios ao adotar ferramentas de automação é o alto custo de manutenção de servidores e taxas de envio de APIs oficiais de mensagens. Esta solução resolve esse problema combinando regras de negócio robustas no backend com uma estratégia inteligente de integração nativa e gratuita com o ecossistema do WhatsApp, onde a própria profissional realiza o disparo com um único toque no celular.

### 🧠 Desafios Técnicos Solucionados
Como desenvolvedor backend focado no ecossistema Java, este projeto foi arquitetado para ir além de operações CRUD básicas, cobrindo os seguintes conceitos de engenharia:

* **Controle de Concorrência e Overbooking:** Implementação de travas de isolamento na camada de persistência com o Spring Data JPA (como *Pessimistic Locking*) para garantir a consistência da agenda, impedindo que requisições simultâneas reservem o mesmo slot de horário.
* **Cálculo Dinâmico de Escopo de Tempo:** Lógica de serviço que analisa o horário de início desejado pelo cliente, consulta a duração cadastrada para o serviço no banco de dados e calcula automaticamente o horário de término para validação de disponibilidade.
* **Sanitização e Validação de Dados:** Uso do *Spring Validation* para garantir a integridade dos dados recebidos via REST, aplicando regras estritas para formatação internacional de números de telefone e strings.
* **Arquitetura Limpa e Desacoplada:** Divisão clara de responsabilidades utilizando o padrão MVC (Model-View-Controller) com DTOs (Data Transfer Objects) para proteção e controle da exposição das entidades do banco de dados.

## 🚀 Tecnologias Propostas
- **Backend:** Java 17 / Spring Boot 3 (Spring Web, Spring Data JPA, Spring Validation)
- **Banco de Dados:** MySQL
- **Front-end:** React / Next.js (Tailwind CSS)

## 📋 Funcionalidades
- [ ] Agendamento online pelo cliente (Sem necessidade de baixar app)
- [ ] Interface mobile-first elegante baseada em Design Tokens (Paleta suave/premium)
- [ ] Validação de concorrência de horários no banco de dados
- [ ] Painel Administrativo Responsivo para Celular da profissional
- [ ] Geração de lembretes formatados com redirecionamento dinâmico para o app do WhatsApp

## 🔄 Fluxo de Dados (Workflow)
```mermaid
graph TD
    A[Cliente acessa Link na Bio] --> B[Seleciona Serviço, Data e Hora]
    B --> C[Insere Nome e WhatsApp]
    C --> D[Front-end envia POST para a API]
    D --> E[API Spring Boot valida horário]
    E -->|Horário Livre| F[Salva no Banco MySQL]
    E -->|Horário Ocupado| G[Retorna Erro para o Front-end]
    F --> H[Manicure abre Painel no Celular]
    H --> I[Painel puxa agendamentos via GET]
    I --> J[Manicure clica em 'Gerar Lembrete']
    J --> K[Sistema abre App do WhatsApp com texto pronto]
