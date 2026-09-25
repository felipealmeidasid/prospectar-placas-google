# Prospecção de placas de avaliação no Google

Agente em arquivos Markdown para Codex, Claude Code, Antigravity e outros assistentes de IA. Pesquisa comércios locais, organiza oportunidades próximas e prepara mensagens de WhatsApp para vender placas com QR Code e NFC.

**Status: experimental.** As instruções foram revisadas e avaliadas em cenários simulados. Pesquisa real no navegador e persistência entre rodadas ainda aguardam validação. Não é um aplicativo independente: precisa de um assistente com ferramentas de navegação e acesso a arquivos. A compatibilidade das instruções não equivale a um teste completo de execução em cada ferramenta.

## Como funciona

1. Você informa cidade/UF e, opcionalmente, bairro.
2. O agente pergunta as condições de entrega da rodada.
3. Pesquisa vários segmentos em uma região comercial e áreas próximas.
4. Seleciona até 20 novos comércios com **menos de 50 avaliações**, sem limite de nota: 4,8 e 5,0 também entram.
5. Compara perfis do mesmo segmento e região, organiza prioridades e agrupa por proximidade.
6. Entrega relatório Markdown, CSV e três mensagens por empresa: abordagem inicial, texto para acompanhar o vídeo e retomada.
7. Registra analisados e descartados num histórico local para evitar repetição em futuras rodadas.

O agente não envia mensagens nem vídeos. A classificação é uma estimativa fundamentada, não uma probabilidade de compra. Poucas avaliações não provam perda de clientes. A placa facilita o pedido de avaliações honestas; não resolve problemas de atendimento.

## Instalação por agente

Pré-requisitos: Git e o assistente escolhido já instalado/configurado, com acesso à web/navegador e leitura/escrita local. Clonar este repositório instala os arquivos de instrução; não instala o assistente, um navegador ou integrações. Os comandos abaixo servem para uma instalação nova. Se já clonou, entre na pasta existente e use `git pull --ff-only`, após preservar suas alterações locais.

### Claude Code

No terminal (PowerShell, bash ou zsh):

```sh
git clone https://github.com/felipealmeidasid/prospectar-placas-google.git
cd prospectar-placas-google
claude
```

Iniciado nessa pasta, o Claude Code lê `CLAUDE.md`, que importa `AGENTS.md` e direciona ao fluxo comum. Não precisa copiar arquivos para a configuração global. Na conversa, peça: “Pesquise comércios em MINHA CIDADE, UF, seguindo as instruções deste projeto”. Use `/context` para conferir os arquivos de instruções carregados. [Documentação do Claude Code](https://code.claude.com/docs/en/memory).

### Codex

Com o Codex CLI já instalado:

```sh
git clone https://github.com/felipealmeidasid/prospectar-placas-google.git
cd prospectar-placas-google
codex
```

No aplicativo Codex, abra essa pasta como projeto. A entrada é `AGENTS.md`; peça a pesquisa em linguagem natural. Para manter a skill disponível fora deste projeto, opcionalmente copie `skills/prospectar-placas-google` para `<CODEX_HOME>/skills/` (padrão: `~/.codex/skills/`). Preserve personalizações se já estiver instalada. A leitura de AGENTS.md não adiciona por si só ferramentas de navegador.

### Google Antigravity

Clone os arquivos:

```sh
git clone https://github.com/felipealmeidasid/prospectar-placas-google.git
cd prospectar-placas-google
```

Abra a pasta clonada como workspace no Antigravity e inicie uma conversa pedindo a pesquisa. A documentação atual reconhece `AGENTS.md` como regra do workspace; não é necessário um GEMINI.md duplicado. Confira as regras carregadas e peça explicitamente a leitura de `AGENTS.md` se sua versão não o carregar. Habilite o acesso ao navegador e permita acesso à pasta de histórico quando solicitado. Não há comando de instalação de extensão deste projeto: basta clonar e abrir a pasta. [Documentação do Antigravity](https://antigravity.google/docs/rules/).

### Outros agentes

Abra o repositório e peça: “Leia AGENTS.md e execute o fluxo de prospecção”. Agentes que reconhecem esse arquivo podem carregá-lo automaticamente; isso não é universal. Ferramentas que só conversam, sem acesso a arquivos e navegador, não executam o fluxo completo. Não presuma que a invocação `$prospectar-placas-google` funciona fora do Codex.

## Como usar

Dentro do projeto, em qualquer agente compatível, peça:

> Siga AGENTS.md para pesquisar comércios em MINHA CIDADE, UF. Entrego pessoalmente na cidade, sem taxa. Comece por uma região comercial.

Substitua cidade e condições pelas suas. Você também pode informar um bairro. As mensagens usam linguagem curta e natural, com fatos observados daquela empresa, sem intimidade inventada ou promessas de resultado.

A oferta padrão é:

| Modelo | Recursos | Preço |
| --- | --- | --- |
| Placa em L | QR Code e NFC | R$ 70 |
| Placa adesiva 10 × 10 cm com fita dupla face | QR Code e NFC | R$ 50 |

Informe ao agente se sua oferta for diferente antes de iniciar. Entrega e prazo nunca são presumidos.

## Histórico e privacidade

Os dados ficam em `<CODEX_HOME>/data/prospectar-placas-google/`, fora deste repositório. O agente deve informar o caminho resolvido no primeiro uso. Claude Code, Codex e Antigravity devem consultar essa mesma pasta; `.codex` é apenas um nome de diretório legado, não uma dependência do Codex. Ao alternar agentes, informe o caminho absoluto já usado para impedir históricos separados. Preserve essa pasta para manter o histórico entre atualizações e copie-a separadamente se mudar de computador.

Não publique histórico, relatórios, números de contato, capturas, credenciais ou arquivos de configuração pessoal. O `.gitignore` é uma proteção adicional, não substitui conferir o que será enviado ao GitHub.

O agente distingue telefone de WhatsApp confirmado, guarda fontes e datas, registra falhas como pendentes e interrompe a seleção se o histórico estiver ilegível. A cobertura é uma amostra das regiões consultadas; não há garantia de encontrar todos os comércios da cidade. CAPTCHA ou bloqueios de acesso podem interromper a rodada.

## Arquivos

- `CLAUDE.md`: entrada do Claude Code, importando as instruções comuns.
- `AGENTS.md`: entrada do Codex, Antigravity e demais agentes compatíveis.

- `skills/prospectar-placas-google/SKILL.md`: entrada e fluxo de pesquisa.
- `skills/prospectar-placas-google/references/history.md`: identidade, persistência e retomada.
- `skills/prospectar-placas-google/references/report.md`: priorização, relatório e tom das mensagens.

## Atualizações e feedback

Este repositório é a fonte da versão compartilhada. Melhorias serão publicadas aqui após os testes. Para atualizar, baixe a nova versão (ou execute `git pull --ff-only` num clone sem alterações locais) e, se usar a instalação global opcional, atualize a pasta da skill, preservando o histórico fora dela.

Abra uma issue descrevendo o comportamento esperado e o observado, com um exemplo anonimizado. Não inclua contatos, relatórios reais ou segredos. Antes de propor alterações, confira referências, elegibilidade (49 entra, 50 não), duplicatas por perfil, filiais, interrupções e mensagens sem fatos inventados.
