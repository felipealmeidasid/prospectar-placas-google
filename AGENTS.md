# Agente de prospecção de placas Google

Este projeto contém instruções de prospecção, não um aplicativo que precisa de build. Responda em português do Brasil.

Quando o usuário pedir pesquisa de comércios, leia `skills/prospectar-placas-google/SKILL.md` e siga as referências `history.md` e `report.md` daquela pasta. Os caminhos dentro da skill são relativos à sua pasta. Essas são as regras comuns para Codex, Claude Code, Antigravity e outros agentes; não mantenha cópias divergentes.

Peça somente os dados ainda ausentes: cidade/UF, bairro opcional e condições de entrega. Confira as ferramentas realmente disponíveis de navegação pública e leitura/escrita de arquivos antes da pesquisa. Não presuma ferramentas do Codex em outro ambiente. Se não houver navegador, explique o recurso ausente; não invente resultados nem declare a pesquisa executada.

O histórico é compartilhado entre os agentes conforme `references/history.md`. Informe o caminho absoluto e confira registros existentes antes de criar uma rodada. Não abra histórico vazio por trocar de agente. Uma única rodada por vez, usando o lock definido na referência.

Entregue relatório Markdown e CSV com até 20 leads novos com menos de 50 avaliações, sem corte de nota, agrupados por proximidade e com três mensagens humanas por empresa. Não envie mensagens ou vídeos. Preserve fontes e datas; telefone não prova WhatsApp.

Pedidos de manutenção deste repositório não iniciam prospecção. Não publique dados de leads, relatórios, credenciais ou configuração pessoal. A leitura destas instruções não concede acesso a ferramentas nem autorização para instalar integrações.
