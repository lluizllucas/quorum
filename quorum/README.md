# Quorum

Um sistema de análise multidisciplinar baseado em Claude. Você apresenta uma ideia e um comitê de especialistas a avalia em profundidade — de diferentes ângulos, em sequência lógica, sem otimismo fácil.

## O que é

O comitê é composto por membros fixos com papéis bem definidos: Desenvolvedor, Infra, Comercial, RH, Arquiteto, DevOps, Auditor e Maestro. Cada um analisa a ideia sob sua perspectiva específica, e o Maestro consolida tudo em um veredicto final de viabilidade.

O RH tem um papel especial: ele identifica o domínio não-técnico mais crítico da ideia (contabilidade, medicina, direito, logística, etc.) e cria dinamicamente um novo especialista para o comitê — um arquivo `.md` com o system prompt desse expert. Esse especialista é acionado na mesma sessão e suas análises entram no relatório final.

O Auditor fala por último entre os especialistas — depois de ler tudo — e tem permissão explícita para ser duro, cético e apontar o que ninguém quis dizer.

## Arquivos do repositório

```
README.md
ORQUESTRADOR.md        # instruções completas para o Claude orquestrar o comitê
squad/
├── MAESTRO.md
├── DESENVOLVEDOR.md
├── INFRA.md
├── ARQUITETO.md
├── DEVOPS.md
├── COMERCIAL.md
├── RH.md
└── AUDITOR.md
```

## Como montar no Claude.ai

### 1. Crie um Projeto

No [Claude.ai](https://claude.ai), clique em **Projects** no menu lateral e crie um novo projeto. Sugestão de nome: `Quorum`.

### 2. Anexe os arquivos

Dentro do projeto, vá em **Project content** e anexe todos os arquivos `.md` deste repositório:

- `ORQUESTRADOR.md`
- `squad/MAESTRO.md`
- `squad/DESENVOLVEDOR.md`
- `squad/INFRA.md`
- `squad/ARQUITETO.md`
- `squad/DEVOPS.md`
- `squad/COMERCIAL.md`
- `squad/RH.md`
- `squad/AUDITOR.md`

### 3. Configure a instrução do projeto

Em **Project instructions**, escreva apenas:

> Leia o arquivo ORQUESTRADOR.md e siga as instruções.

### 4. Pronto

Abra uma nova conversa dentro do projeto e apresente sua ideia diretamente no chat. Todas as respostas do comitê aparecem aqui mesmo, na conversa.

## Como usar

**Análise completa:** apresente sua ideia em linguagem natural.

```
Quero criar uma plataforma de gestão financeira para MEIs com
emissão automática de notas fiscais e apuração de impostos.
```

O comitê executa todas as fases e entrega o relatório final diretamente no chat.

**Consulta direta:** após o relatório, faça perguntas a membros específicos.

```
DEVOPS, quanto custaria escalar para 50 mil usuários?
```

```
AUDITOR, o que você acha do modelo de monetização proposto?
```

Apenas o membro convocado responde, com base no contexto da análise anterior.

## Experts dinâmicos

Quando o RH cria um novo especialista (ex: `CONTADOR.md`), o conteúdo desse arquivo aparece na resposta do RH durante a análise. Copie esse conteúdo, salve como `.md` e anexe ao projeto. Nas próximas sessões, o RH identificará que o expert já existe e o reutilizará sem recriar.
