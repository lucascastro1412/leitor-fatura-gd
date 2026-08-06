# Leitor de Fatura — Medição de Usina GD

Página única que lê a fatura de energia da unidade geradora e devolve a **planilha de
medição preenchida**, com as abas Conferência, Dados e máscara.

A leitura acontece **inteiramente no navegador de quem usa**. O PDF não é enviado para
servidor nenhum e a página não guarda nada. Não há backend, banco de dados nem custo de
hospedagem.

## Distribuidoras suportadas

| Distribuidora | Layout | Situação |
|---|---|---|
| Celesc | Grupo A horossazonal, anterior à REN 1095/24 | validado |
| Celesc | Grupo A horossazonal, posterior à REN 1095/24 | validado |
| Copel | DANF3E, unidade geradora | validado |

Outras distribuidoras ainda não são reconhecidas. Um PDF sem texto (digitalizado ou
fotografado) é recusado com mensagem explícita — o leitor não usa OCR de propósito, para
não introduzir erro de dígito em valor financeiro.

## Como usar

1. Carregue o perfil da usina em **Carregar de arquivo** (arquivo `.json`).
2. Solte o PDF da fatura na área indicada. Pode soltar vários meses de uma vez.
3. Confira os campos lidos na tela e baixe a planilha.

Para usinas com mais de uma unidade consumidora, marque **Somar as faturas numa única
medição** antes de soltar os PDFs.

Confira sempre o bloco 1 da aba Conferência antes de usar a planilha.

## Perfis das usinas

Os perfis **não acompanham este repositório**: contêm CNPJ, dados bancários, deságio e
valores de contrato. Cada pessoa carrega o `.json` da usina que vai processar.

O arquivo `perfil-exemplo.json` mostra o formato. Para criar um perfil novo, preencha os
campos na tela e clique em **Exportar este perfil**.

`perfis/` está no `.gitignore` — perfis reais colocados ali não sobem para o repositório.

## O que a planilha calcula

Reproduz o modelo de medição de GD: tarifa compensada, Vunit após deságio, VB (rateio de
tributos), Vcusto, Vperf e Vlocação, com vencimento por contrato.

Pontos que o leitor confere sozinho e sinaliza na aba Conferência:

- soma dos itens da fatura contra o total
- fator de conversão entre postos efetivo contra o teórico (razão das TEs)
- excedente declarado na fatura contra o recalculado
- Vperf da aba Dados contra o da máscara

As alíquotas de PIS, COFINS e ICMS são sempre lidas da fatura do mês, nunca do perfil.

## Publicação

Arquivo único, sem build. Basta o `index.html` na raiz e o GitHub Pages ligado em
Settings → Pages.

## Licença

Uso interno.
