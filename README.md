# idea-committee

Um agente de análise de ideias com um comitê de especialistas virtuais. Passe uma ideia e o sistema aciona cada membro do comitê em sequência (com paralelismo na Fase 1), gerando análises especializadas e um relatório final consolidado em Markdown.

## Estrutura do Comitê

```
Fase 1 (paralelo)
├── DESENVOLVEDOR  — viabilidade técnica e stack
├── INFRA          — infraestrutura e hospedagem
├── COMERCIAL      — mercado, ICP, monetização
└── RH             — pessoas, domínio e criação de expert dinâmico
    └── [EXPERT]   — especialista de domínio criado pelo RH (paralelo com Fase 1b)

Fase 2
└── ARQUITETO      — arquitetura de sistema (lê DESENVOLVEDOR + INFRA)

Fase 3
└── DEVOPS         — custos e operações (lê ARQUITETO)

Fase 4
└── AUDITOR        — questionamento e pontos cegos (lê todos)

Fase 5
└── MAESTRO        — relatório executivo consolidado (lê todos)
```

## Pré-requisitos

- Python 3.8+
- Conta Anthropic com API key

## Instalação

```bash
# Clone ou baixe o projeto
cd idea-committee

# Instale as dependências
pip install -r requirements.txt

# Configure a API key
cp .env.example .env
# Edite .env e adicione sua ANTHROPIC_API_KEY
```

## Uso

```bash
python comite.py "sua ideia aqui"
```

### Exemplos

```bash
python comite.py "Um app de telemedicina para idosos com interface simplificada"
python comite.py "Marketplace de freelancers especializados em automação industrial"
python comite.py "Plataforma SaaS de gestão financeira para MEIs"
```

## Saída

O relatório é salvo em `relatorios/` com o formato:

```
relatorios/20240315_143022_um_app_de_telemedicina.md
```

Cada relatório contém as análises completas de todos os membros do comitê e o relatório executivo final do MAESTRO.

## Expert Dinâmico (RH)

O membro RH identifica automaticamente o domínio não-técnico mais crítico para a ideia (medicina, direito, contabilidade, etc.) e cria um system prompt personalizado para esse expert. O expert criado:

1. Tem seu prompt salvo em `squad/experts/NOME_DO_EXPERT.md`
2. É acionado automaticamente na Fase 1b (paralelo)
3. Aparece no relatório final como "Expert Dinâmico"

## Estrutura de Arquivos

```
idea-committee/
├── comite.py              # Script principal
├── requirements.txt
├── .env.example
├── squad/
│   ├── DESENVOLVEDOR.md
│   ├── INFRA.md
│   ├── COMERCIAL.md
│   ├── RH.md
│   ├── ARQUITETO.md
│   ├── DEVOPS.md
│   ├── AUDITOR.md
│   ├── MAESTRO.md
│   └── experts/           # Experts dinâmicos criados pelo RH
└── relatorios/            # Relatórios gerados
```
