# Seleção, relatório e mensagens

## Priorização

Separe necessidade de avaliações, adequação comercial da placa e prontidão de contato. A classificação é qualitativa, não uma previsão de compra.

- **Alta:** menos de 50 avaliações, atendimento presencial adequado ao uso da placa e diferença expressiva de contagem para concorrentes comparáveis observados. Boa nota com poucas avaliações é uma oportunidade. Contato confirmado favorece a prontidão.
- **Média:** elegível, mas comparação limitada, diferença pequena ou contato ainda não confirmado.
- **Baixa:** adequação incerta ou evidências de reclamações recorrentes sobre problemas operacionais que a placa não resolve. Nota baixa isolada não basta para concluir que existem esses problemas.

Fundamente a categoria com fatos de cada caso; não aplique um corte máximo de nota. Agrupe os leads por bairro/rua/região, depois ordene dentro de cada grupo por prioridade e prontidão. Ordene grupos por concentração de oportunidades altas e proximidade verificável. Sem coordenadas ou rotas confirmadas, apresente agrupamento aproximado por endereço, não distância ou trajeto otimizado inventados.

## Arquivos de saída

Na pasta da rodada, crie `relatorio.md` e `leads.csv` (UTF-8 com BOM, separador ponto e vírgula). O Markdown é o documento para leitura; o CSV é para organização dos contatos. Escape aspas e quebras de linha no CSV e neutralize células que possam iniciar fórmulas (`=`, `+`, `-`, `@`, tabulação ou retorno), preservando o valor original no histórico. Não execute conteúdos coletados.

O relatório abre com cidade/UF, data, entrega informada, regiões cobertas, limitações, método de escolha da região e totais. Em seguida traz uma tabela ordenada por grupos e fichas dos leads, com:

- Ordem, prioridade e justificativa; necessidade e prontidão de contato separadas.
- Nome, segmento, endereço, bairro, cidade/UF e link Google.
- Nota, contagem de avaliações e data de consulta.
- Telefone, status de WhatsApp e fonte; link WhatsApp somente com número e canal confirmados. Não deduza DDD ou código de país quando houver ambiguidade.
- Concorrentes comparáveis, suas contagens/notas e links, ou indicação de comparação insuficiente.
- Três mensagens prontas, individualizadas, com uso indicado fora do texto copiável.

Colunas do CSV: ordem, grupo, prioridade, motivo, nome, segmento, endereco, bairro, cidade, uf, nota, avaliacoes, consultado_em, google_url, telefone, whatsapp_status, whatsapp_url, contato_fonte, concorrentes_resumo, entrega, mensagem_inicial, mensagem_video, mensagem_retomada.

Sem leads: entregue relatório de cobertura e CSV só com cabeçalhos. Não complete a lista com dados fictícios. O usuário envia o vídeo; não precisa fornecer o arquivo para gerar a mensagem que o acompanha.

## Tom obrigatório

PT-BR de conversa entre vendedor e comerciante. Frases curtas, ritmos variados, contrações como “pra” e “tá” quando naturais. Jargão do segmento só quando ajuda; não force gírias, erros ou intimidade. Um assunto central e no máximo uma pergunta por mensagem. Prefira 2–4 frases curtas, adaptando quando necessário.

Proibido: “potencializar sua presença digital”, “solução inovadora”, “alavancar seu negócio”, elogio genérico, texto de palestra, promessa de aumento de nota/vendas, urgência inventada, alegar perda de clientes ou visitas sem dados. Não dizer “sou cliente”, “passei aí”, “conheço vocês” ou que haverá entrega na rua amanhã sem base. Não copiar o mesmo texto trocando apenas o nome.

1. **Inicial:** cumprimento simples, observação verdadeira e oportunidade com tato. Boa nota/poucas avaliações: valorize o dado concreto sem exagerar. Nota baixa: não constranja nem prometa reparar reputação. Termine com pergunta fácil sobre como pedem avaliações. Não transforme uma primeira mensagem em diagnóstico longo.
2. **Vídeo:** texto para acompanhar a demonstração após a abordagem, sem presumir que houve resposta ou interesse. Explique aproximação do celular pelo NFC ou leitura do QR Code para acessar a avaliação. Apresente modelos e preços naturalmente, sem exigir resposta anterior para que o texto faça sentido. Inclua entrega somente conforme informado. Não diga que avaliar é automático, dispensa login ou funciona com qualquer aparelho.
3. **Retomada:** pergunta curta e respeitosa caso não haja resposta após mensagem/vídeo. Não presuma que a pessoa assistiu, não pressione e não invente escassez. O usuário decide o momento do envio; o agente não agenda nem envia.

Peça avaliações honestas aos clientes em geral. Não proponha comprar avaliações, recompensar nota, selecionar somente clientes satisfeitos ou esconder reclamações.

Revise as três mensagens como conversa em voz alta: corte palavras que um vendedor não usaria no WhatsApp. Confira cada número, preço e afirmação com os registros. Os textos copiáveis não podem conter placeholders, instruções internas ou nomes inventados do vendedor. A classificação e a comparação mais detalhada ficam no relatório interno, não precisam ser despejadas no contato comercial.
