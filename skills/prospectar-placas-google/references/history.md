# Histórico persistente

Raiz persistente padrão: `<CODEX_HOME>/data/prospectar-placas-google/`. Resolva CODEX_HOME pelo ambiente; quando ausente, use `.codex` na pasta pessoal do usuário. Resolva e informe o caminho absoluto antes do primeiro uso. O histórico fica fora do repositório e da pasta da skill, para sobreviver às atualizações.
Não crie outra raiz automaticamente em outra conversa. Se não estiver acessível, peça ao usuário para disponibilizar essa pasta. Ao transferir o agente para outra máquina, transfira também o histórico e ajuste esta referência explicitamente.

## Organização

- `runs/<run-id>/`: entrada da rodada, cobertura, relatório e CSV. Use data/hora UTC mais identificador aleatório para impedir colisões.
- `events/<event-id>.json`: um arquivo novo por evento, com identificador aleatório. Nunca sobrescreva, apague ou reescreva registros anteriores. Salve através de arquivo temporário e criação final sem substituição; só considere persistido depois de reler e validar o JSON.
- `active-run.lock`: crie exclusivamente antes de iniciar a rodada, com run-id e horário. Se já existir, não inicie outra rodada concorrente. Confira com o usuário se a anterior ainda está em andamento. Nunca remova um lock de outra rodada automaticamente. Ao concluir, remova somente o lock que pertence à rodada atual; essa limpeza deve ser informada antes da operação. Se houver interrupção, preserve o lock e o histórico para retomada.

O primeiro uso pode criar as pastas vazias: isso não constitui pesquisa realizada. Em todos os usos seguintes, leia todos os eventos; JSON inválido ou erro de acesso interrompe a seleção, em vez de tratar o histórico como vazio. Não basta ler o relatório anterior.

Para retomar uma rodada interrompida, confirme que a execução anterior encerrou e reutilize seu `run_id`, pasta e lock; não crie uma segunda execução concorrente. Antes de gerar arquivos, confira quais já existem e recupere-os. Se precisar corrigir um relatório existente, crie uma versão com sufixo novo e registre o caminho, preservando a versão anterior.

## Identidade e eventos

Cada evento contém `schema_version: 1`, `event_id`, `run_id`, `observed_at` (ISO 8601 com fuso), `event_type`, `identity`, `data` e `sources`.

Use `identity: null` em eventos de cobertura ou encerramento da rodada. Eventos de candidatos e referências exigem identidade com os campos efetivamente conhecidos; campos não confirmados ficam null. Fontes podem ser uma lista vazia somente em eventos operacionais, nunca para sustentar dados comerciais.

`identity`: nome original, nome normalizado, endereço original, endereço normalizado, cidade, UF, Google place ID/CID quando realmente disponível, URL observada e aliases conhecidos. Normalize caixa, acentos, pontuação e espaços para comparação; preserve números de endereço e unidades. Não fabrique identificadores Google.

Compare por identificador estável Google; sem ele, por nome + endereço + cidade/UF normalizados. Confira também aliases e URLs de perfis anteriormente registrados. Mesmo ID prevalece sobre mudança de nome; identidades conflitantes, nomes parecidos com mesmo endereço ou endereço incompleto pedem conferência mínima, não novo lead automático. Telefone sozinho nunca identifica uma unidade, pois filiais podem compartilhá-lo. Uma conferência de identidade não é uma nova análise comercial.

Eventos possíveis:

- `candidate_analyzed`: análise concluída, com `decision` igual a `selected` ou `discarded`, motivo, nota (número ou null), contagem inteira, contatos com status e evidências, segmento, endereço, comparação e prioridade. Repetições futuras são puladas independentemente da decisão. Conteúdos de comparação ainda insuficientes devem ser sinalizados, não inventados.
- `candidate_pending`: falha técnica ou informação essencial não confirmada, com motivo e dados parciais. Pode ser retomado; não vira analisado automaticamente.
- `reference_observed`: concorrente usado somente para comparação. Não bloqueia sua futura análise como candidato.
- `lead_delivered`: referência ao candidato selecionado e aos caminhos do relatório/CSV já gerados e conferidos. Salve só depois de verificar os arquivos.
- `coverage_recorded`: região, cidade/UF, buscas executadas, segmentos, limitações e próxima área sugerida. Área pesquisada não significa todos os seus comércios analisados.
- `run_completed` ou `run_interrupted`: totais reais, arquivos existentes e pendências.

Um candidato analisado e selecionado, mas ainda sem `lead_delivered`, deve ser recuperado para entrega antes de procurar novos: reutilize a análise, sinalize a data e não o perca após uma interrupção. Um candidato entregue não volta ao relatório de novos leads. Se o usuário pedir reanálise explicitamente, registre um novo evento vinculado ao anterior, preservando o histórico e marcando-o como reanálise, fora da contagem de novos.

Cada fonte precisa de URL pública, data da consulta e resumo factual do que sustenta. Nome/telefone de pessoa privada não são necessários: registre contatos comerciais publicados. A confirmação de WhatsApp deve ter evidência específica e status `confirmed`, `unconfirmed` ou `not_found`.

## Verificação da persistência

Antes de entregar, releia os eventos da rodada e confira unicidade de IDs, identidade dos candidatos, totais e referências aos arquivos. Na rodada seguinte, demonstre a consulta ao histórico e contabilize duplicatas puladas. Não declare esse comportamento testado em produção com base apenas numa leitura da skill.
