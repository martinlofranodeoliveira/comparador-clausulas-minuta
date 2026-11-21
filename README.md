# Comparador de Cláusulas de Minuta

Compare versões de uma minuta fictícia por identificador e localize o trecho textual que mudou.

## Como usar

Abra a [demonstração](https://martinlofranodeoliveira.github.io/comparador-clausulas-minuta/). Para uso local, execute `python3 -m http.server 8000` no diretório e abra `http://localhost:8000`.

Insira as cláusulas nas duas versões e use o mesmo identificador nos trechos que correspondem. Se quiser, marque **Mostrar somente diferenças**. Clique em **Comparar versões** e confira os trechos incluídos ou removidos. O relatório está disponível em CSV.

## Contrato público

input deve ser objeto com before e after, arrays de até 100 elementos {id,text}. id é string entre 1 e 32 caracteres, formada por letras ASCII (A-Z/a-z), números, ponto, hífen ou sublinhado, e deve ser única dentro da lista. text é string com até 2000 caracteres. onlyDifferences deve ser boolean se fornecido, com default false. Use o erro exato {error:"INVALID_INPUT"} para input inválido.
Retorne {rows,summary}. Cada linha é {id,status,removed,added}, com status SAME, CHANGED, ADDED ou REMOVED. Compare os textos após trim e separação por qualquer sequência de espaços em branco, respeitando capitalização e pontuação. Para uma cláusula CHANGED, retire primeiro o maior prefixo de palavras idênticas e depois o maior sufixo idêntico dos dois TRECHOS RESTANTES. removed e added são as palavras remanescentes do texto antigo e do novo, unidas por espaço. Para ADDED ou REMOVED, use todo o texto normalizado no campo correspondente. Um lado sem palavras recebe string vazia. SAME recebe dois campos vazios. A ordem é before seguido dos ids inéditos de after. summary tem added, removed, changed, same e conta também SAME quando onlyDifferences=true.

## Escopo

Demonstração offline com exemplos fictícios. A equipe responsável avalia documentação, conformidade e habilitação. A interface processa os dados no navegador. O motor foi gerado com Gemini 4 Neon no Vertex AI.

## Testes

Execute `node scripts/test.mjs public.json`.

## Licença

MIT. Acorn preserva sua licença em scripts/vendor/LICENSE-Acorn.txt.
