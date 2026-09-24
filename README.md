# Prospecção de placas de avaliação no Google

Skill para o Codex pesquisar comércios locais, organizar oportunidades próximas e preparar mensagens de WhatsApp para vender placas com QR Code e NFC.

**Status: experimental.** As instruções foram revisadas e avaliadas em cenários simulados. Pesquisa real no navegador e persistência entre rodadas ainda aguardam validação. Não é um aplicativo independente: precisa do Codex com ferramentas de navegação e acesso a arquivos.

## Como funciona

1. Você informa cidade/UF e, opcionalmente, bairro.
2. O agente pergunta as condições de entrega da rodada.
3. Pesquisa vários segmentos em uma região comercial e áreas próximas.
4. Seleciona até 20 novos comércios com **menos de 50 avaliações**, sem limite de nota: 4,8 e 5,0 também entram.
5. Compara perfis do mesmo segmento e região, organiza prioridades e agrupa por proximidade.
6. Entrega relatório Markdown, CSV e três mensagens por empresa: abordagem inicial, texto para acompanhar o vídeo e retomada.
7. Registra analisados e descartados num histórico local para evitar repetição em futuras rodadas.

O agente não envia mensagens nem vídeos. A classificação é uma estimativa fundamentada, não uma probabilidade de compra. Poucas avaliações não provam perda de clientes. A placa facilita o pedido de avaliações honestas; não resolve problemas de atendimento.

## Instalação no Codex

Baixe este repositório ou clone com Git:

```sh
git clone https://github.com/felipealmeidasid/prospectar-placas-google.git
```

Copie a pasta `skills/prospectar-placas-google` para a pasta `skills` do seu `CODEX_HOME`. Quando essa variável não estiver definida, o destino é `~/.codex/skills/prospectar-placas-google` (a pasta `.codex` dentro da sua pasta pessoal, também no Windows).

Se já houver uma versão instalada, preserve suas personalizações antes de substituir os três arquivos da skill. Inicie uma nova conversa no Codex para verificar se ela aparece entre as skills disponíveis. O suporte depende das ferramentas de navegação e das permissões da sua instalação; Claude Code ainda não foi validado.

## Como usar

Peça ao Codex:

> Use $prospectar-placas-google para pesquisar comércios em MINHA CIDADE, UF. Entrego pessoalmente na cidade, sem taxa. Comece por uma região comercial.

Substitua cidade e condições pelas suas. Você também pode informar um bairro. As mensagens usam linguagem curta e natural, com fatos observados daquela empresa, sem intimidade inventada ou promessas de resultado.

A oferta padrão é:

| Modelo | Recursos | Preço |
| --- | --- | --- |
| Placa em L | QR Code e NFC | R$ 70 |
| Placa adesiva 10 × 10 cm com fita dupla face | QR Code e NFC | R$ 50 |

Informe ao agente se sua oferta for diferente antes de iniciar. Entrega e prazo nunca são presumidos.

## Histórico e privacidade

Os dados ficam em `<CODEX_HOME>/data/prospectar-placas-google/`, fora deste repositório. O agente deve informar o caminho resolvido no primeiro uso. Preserve essa pasta para manter o histórico entre atualizações e copie-a separadamente se mudar de computador.

Não publique histórico, relatórios, números de contato, capturas, credenciais ou arquivos de configuração pessoal. O `.gitignore` é uma proteção adicional, não substitui conferir o que será enviado ao GitHub.

O agente distingue telefone de WhatsApp confirmado, guarda fontes e datas, registra falhas como pendentes e interrompe a seleção se o histórico estiver ilegível. A cobertura é uma amostra das regiões consultadas; não há garantia de encontrar todos os comércios da cidade. CAPTCHA ou bloqueios de acesso podem interromper a rodada.

## Arquivos

- `skills/prospectar-placas-google/SKILL.md`: entrada e fluxo de pesquisa.
- `skills/prospectar-placas-google/references/history.md`: identidade, persistência e retomada.
- `skills/prospectar-placas-google/references/report.md`: priorização, relatório e tom das mensagens.

## Atualizações e feedback

Este repositório é a fonte da versão compartilhada. Melhorias serão publicadas aqui após os testes. Para atualizar, baixe a nova versão (ou execute `git pull --ff-only` num clone sem alterações locais) e atualize a pasta instalada, preservando o histórico fora dela.

Abra uma issue descrevendo o comportamento esperado e o observado, com um exemplo anonimizado. Não inclua contatos, relatórios reais ou segredos. Antes de propor alterações, confira referências, elegibilidade (49 entra, 50 não), duplicatas por perfil, filiais, interrupções e mensagens sem fatos inventados.
