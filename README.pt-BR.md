# Guia de Agent Skills Jurídicas

Guia prático e independente para descobrir, avaliar e usar Agent Skills jurídicas com segurança.

> Este repositório é uma **camada de curadoria e recomendação**. Ele não copia, certifica ou redistribui os projetos indicados.

[English](README.md) · [Catálogo](catalog/projects.yml) · [Contribuição](CONTRIBUTING.md) · [Segurança](SECURITY.md)

## Por que este repositório existe

Os projetos de skills jurídicas têm objetivos diferentes: implementação oficial, catálogo de descoberta, coleção criada por profissionais, skill especializada ou biblioteca em escala. Quantidade não significa automaticamente qualidade, precisão ou segurança.

Este guia responde a quatro perguntas:

1. O que é uma Agent Skill?
2. Qual projeto usar em cada situação?
3. Como instalar e testar uma skill?
4. Quais controles são necessários antes de usar documentos jurídicos reais?

## O que é uma Agent Skill?

Uma Agent Skill é um pacote portátil de instruções, metadados e recursos opcionais que ensina um agente de IA a executar um workflow específico.

A especificação aberta exige pelo menos um arquivo `SKILL.md`:

```text
nome-da-skill/
├── SKILL.md       # Obrigatório: metadados e instruções
├── scripts/       # Opcional: código executável
├── references/    # Opcional: referências
└── assets/        # Opcional: modelos e recursos
```

Exemplos jurídicos:

- revisar um NDA segundo um playbook;
- criar uma cronologia processual com fontes;
- verificar se uma decisão sustenta uma afirmação;
- extrair obrigações e prazos;
- montar uma matriz de due diligence;
- revisar um DPA contra um regime regulatório.

A skill **não é o modelo**. Ela funciona como um procedimento operacional reutilizável que orienta o modelo e pode acessar ferramentas, scripts e fontes externas.

Especificação: [agentskills.io/specification](https://agentskills.io/specification)

## Projetos recomendados

Informações revisadas nas documentações dos projetos em **03/08/2026**.

| Projeto | Melhor uso | Principal força | Limitação principal | Recomendação |
|---|---|---|---|---|
| [anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal) | Times jurídicos que usam Claude | Referência oficial ampla, com plugins, agentes, conectores e controles jurídicos | Ecossistema centrado no Claude e sem especialização profunda em direito brasileiro | **Melhor referência geral** |
| [lawvable/awesome-legal-skills](https://github.com/lawvable/awesome-legal-skills) | Descobrir skills de terceiros | Catálogo amplo e organizado para workflows jurídicos | Qualidade, licença, segurança e manutenção variam em cada projeto listado | **Melhor catálogo de descoberta** |
| [LegalQuants/lq-skills](https://github.com/LegalQuants/lq-skills) | Workflows criados por profissionais | Skills transparentes, construídas por lawyer-builders e organizadas por jurisdição | Biblioteca menor e cobertura variável entre jurisdições | **Melhor coleção de alto sinal** |
| [evolsb/claude-legal-skill](https://github.com/evolsb/claude-legal-skill) | Primeira revisão de contratos | Revisão focada, sensível à posição da parte, com riscos, benchmarks e redlines | Foco em contratos e orientação predominante ao direito norte-americano | **Melhor ponto de partida para contratos** |
| [ThomasMoreAI/legal-skills-open](https://github.com/ThomasMoreAI/legal-skills-open) | Explorar ampla cobertura de jurisdições e áreas | Grande biblioteca organizada por jurisdição e prática | Escala exige validação individual de profundidade, atualização e segurança | **Melhor referência de abrangência e taxonomia** |

## Qual projeto usar

### Referência completa no ecossistema Claude

Use [`anthropics/claude-for-legal`](https://github.com/anthropics/claude-for-legal).

É a melhor referência para estudar estrutura de plugins, perfis de prática, conectores MCP, agentes agendados, citações, trust gates e workflows por área jurídica.

### Descoberta de skills

Use [`lawvable/awesome-legal-skills`](https://github.com/lawvable/awesome-legal-skills).

Considere-o um índice. A presença no catálogo não substitui a revisão do repositório original, licença, scripts, permissões e histórico de manutenção.

### Skills construídas por profissionais jurídicos

Use [`LegalQuants/lq-skills`](https://github.com/LegalQuants/lq-skills).

A coleção é especialmente útil para estudar verificação de citações, proposition checking, cronologias, contract QA, redlines e controle de qualidade jurídico.

### Revisão inicial de contratos

Use [`evolsb/claude-legal-skill`](https://github.com/evolsb/claude-legal-skill).

Ela é adequada para issue spotting e revisão estruturada. Confirme a jurisdição, a posição comercial, as fontes e as sugestões de redação antes de utilizar o resultado.

### Cobertura ampla

Use [`ThomasMoreAI/legal-skills-open`](https://github.com/ThomasMoreAI/legal-skills-open).

A taxonomia ajuda a descobrir workflows. Cada skill selecionada deve ser validada individualmente.

## Como usar

A instalação depende do agente e do projeto. Siga sempre as instruções atuais do repositório original.

### Fluxo local mínimo

```bash
# Clonar
git clone https://github.com/OWNER/REPOSITORY.git
cd REPOSITORY

# Localizar instruções e código executável
find . -name "SKILL.md" -o -name "*.py" -o -name "*.sh" -o -name "*.js"

# Inspecionar mudanças recentes
git log -10 --oneline

# Copiar somente a skill revisada para o diretório do agente
```

### Exemplo para plugin no Claude Code

```text
/plugin marketplace add https://github.com/anthropics/claude-for-legal
/plugin install commercial-legal@claude-for-legal
```

Execute o setup ou cold-start interview antes das demais skills. Sem o perfil de prática, o resultado tende a ser genérico.

### Exemplo de skill isolada

```bash
# Exemplo documentado para Claude Code
git clone https://github.com/evolsb/claude-legal-skill \
  ~/.claude/skills/contract-review

# Exemplo documentado para Codex
git clone https://github.com/evolsb/claude-legal-skill \
  ~/.codex/skills/contract-review
```

Confirme as convenções atuais do agente antes da instalação.

## Cuidados obrigatórios

### Jurisdição

Verifique país, estado, tribunal, regulador, data aplicável, lei de regência e pressupostos padrão. Uma skill norte-americana não se transforma em skill brasileira apenas porque o workflow parece genérico.

### Fontes e atualização

A skill deve identificar fontes, distinguir autoridade primária e secundária, exigir citações, registrar datas e sinalizar incerteza.

### Confidencialidade e privilégio

Antes de usar documentos reais, descubra onde os dados são processados, quem os recebe, por quanto tempo são retidos, quais conectores têm acesso e se a política da organização permite o uso.

Nos testes iniciais, use documentos sintéticos ou anonimizados.

### Código executável

Revise scripts, chamadas de rede, instalação de pacotes, subprocessos, variáveis de ambiente, acesso a arquivos, credenciais e instruções codificadas ou ocultas.

Execute skills desconhecidas em ambiente isolado e com privilégios mínimos.

### Prompt injection

Documentos e páginas externas são dados não confiáveis. O agente deve separar instruções de evidências, limitar ferramentas, registrar ações e exigir confirmação antes de escrever, enviar ou alterar sistemas externos.

### Revisão humana

Use skills para primeira revisão, extração, organização, comparação, drafting assistido e quality control. Conclusões materiais, prazos, petições, pareceres e comunicações externas exigem revisão profissional responsável.

### Licença

Verifique a licença do repositório, das skills importadas, datasets, modelos, scripts e referências. Um catálogo não concede direito de copiar, modificar ou incorporar comercialmente os projetos listados.

### Controle de versão

Em produção, fixe commit ou release, registre o hash revisado, avalie atualizações, mantenha inventário e preserve rollback.

## Framework de avaliação

| Dimensão | Pergunta |
|---|---|
| Workflow | Quando usar, quais entradas fornecer, quais etapas executar e qual saída produzir estão claros? |
| Jurisdição | O escopo jurídico está explícito? |
| Autoridade | As fontes são identificáveis, atuais e hierarquizadas? |
| Rastreabilidade | As conclusões podem ser ligadas ao documento ou à autoridade citada? |
| Segurança | Scripts, conectores, ferramentas e permissões são compreensíveis e limitados? |
| Confidencialidade | O tratamento de dados atende às políticas da organização? |
| Testes | Existem casos, resultados esperados ou regressões? |
| Manutenção | O projeto possui versões e histórico recente? |
| Licença | O uso pretendido é permitido? |
| Controle humano | Existem gates de revisão e aprovação? |

Classificação sugerida:

```text
Adotar      → revisada, testada, limitada e aprovada para workflow definido
Pilotar     → candidata útil; somente dados sintéticos ou anonimizados
Referência  → bom padrão de projeto, sem aprovação para casos reais
Rejeitar    → origem obscura, permissões inseguras, direito desatualizado ou licença inadequada
```

## Lacuna brasileira

A principal oportunidade ainda é uma coleção brasileira profundamente revisada, com:

- fontes oficiais brasileiras;
- metadados de jurisdição federal e estadual;
- conhecimento dos sistemas processuais;
- terminologia jurídica em português;
- verificação de citações;
- identificação dos revisores;
- validade temporal das fontes;
- casos de avaliação;
- controles de confidencialidade e LGPD;
- workflows de contencioso, contratos, compliance, insolvência e legal operations.

## Política de inclusão

Um projeto pode entrar no guia quando possuir repositório público, finalidade jurídica clara, mantenedores identificáveis, instruções de uso, licença visível e documentação suficiente para avaliação independente.

Inclusão não significa certificação ou aprovação.

## Aviso

Este repositório fornece informações técnicas e de pesquisa sobre software de terceiros. Não possui afiliação com os projetos listados, salvo quando expressamente indicado. Marcas e nomes pertencem aos respectivos titulares.

## Licença

O conteúdo original deste guia é disponibilizado sob a [Licença MIT](LICENSE). Projetos de terceiros mantêm suas próprias licenças.
