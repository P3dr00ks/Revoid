# REVOID — Diário de campo

Site independente para registrar vendas, assistências técnicas e outras atividades, com estética gótica inspirada no PS2 e cybertribal, com vinhas espinhosas no fundo.

## Uso

Abra `index.html` em um navegador moderno ou acesse [REVOID no GitHub Pages](https://p3dr00ks.github.io/Revoid/). O layout se adapta a celulares, tablets e computadores. O app pode ser instalado pelo navegador e a interface principal é armazenada para uso offline após a primeira visita.

## Recursos

- Registrar vendas (número e vendedor), assistências (status) e outras atividades, com data, hora e observações.
- Editar e excluir registros; ver contadores do dia e filtrar a linha do tempo por categoria e período.
- Ver totais de vendas no período, exportar o CSV filtrado ou apenas o diário de hoje e imprimir/salvar relatório como PDF.
- Fazer backup JSON e importar dados mesclando com os registros atuais.
- Guardar dados localmente no navegador ou configurar sincronização privada entre aparelhos via Supabase.

## Sincronização online

O projeto Supabase do REVOID já vem conectado no app. Basta criar uma conta e entrar com ela em cada aparelho. O cliente web usa uma chave publicável, protegida por políticas Row Level Security; nunca use uma chave `service_role` no site. Consulte [SUPABASE_SETUP.md](./SUPABASE_SETUP.md) para detalhes da tabela e das políticas.

Sem Supabase configurado, os registros ficam apenas no aparelho e navegador atuais. Exporte backups JSON para preservar ou transferir seus dados.





