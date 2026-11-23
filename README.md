# SisClass-CONARQ: classificador de documentos com a Tabela de Temporalidade (atividades-meio, 2024)

Sistema especialista com aprendizado supervisionado (Regressão Logística + regras SE…ENTÃO) para as classes
020 (Gestão de pessoas), 030 (Gestão de materiais) e 040 (Gestão de bens patrimoniais e de serviços).

**Fonte única de códigos, descritores e prazos:** Arquivo Nacional, *Código de classificação e tabela de temporalidade e
destinação de documentos relativos às atividades-meio/suporte do Poder Executivo federal*, atualização de 2024
(Portaria AN/MGI nº 174/2024). Fora do escopo: subclasse 080 (Pessoal militar), OCR/PDF, atividades-fim.

## Como rodar
    pip install -r requirements.txt
    jupyter notebook classificador_documentos.ipynb
Rode o notebook a partir desta pasta (ele lê `dados/`, `corpus/` e `tests/` por caminho relativo).

## O que falta para o relatório (o grupo)
1. Colocar textos públicos reais em `corpus/textos/` (um `.txt` por documento) e rotular à mão **150 a 300** deles em
   `corpus/rotulos_ouro.csv` (colunas `arquivo,codigo`), com o PDF aberto. Veja `corpus/LEIAME.txt`.
2. Rodar o notebook. Com menos de 30 textos ele roda em **modo demonstração** (16 textos sintéticos) e avisa:
   esses números **não valem** para o relatório.
3. Preencher no notebook as análises marcadas com "Preencha" (seções 13 e 15) e ajustar `LIMIAR_CONFIANCA` com a seção 8.2.

## Arquivos
- `classificador_documentos.ipynb`: notebook completo (autocontido).
- `dados/tabela_temporalidade.csv`: tabela extraída do PDF (classes 020, 030, 040).
- `dados/descricoes_codigos.csv`: descritor e descrição de cada código, extraídos do PDF.
- `scripts/`: extração do PDF (`extrai_tabela.py`, `limpa_tabela.py`, `extrai_descricoes.py`) e `gera_notebook_v2.py`.
- `corpus/`: textos reais e conjunto de ouro (vazio até o grupo preencher).
- `tests/demo_sintetico/`: 16 textos SINTÉTICOS só para testar o código.

## Conferência da extração
Destinação e prazos dos 217 códigos finais foram conferidos automaticamente contra o texto do PDF (217/217 após a
correção do código 041.7). A coluna `obs` (observações) tem quebras de linha do PDF e vale conferir à mão antes de citar.
O PDF imprime "52 anos" no arquivo intermediário de 022.1 e 022.22; o sistema reproduz o valor do documento.

## Limitações conhecidas
O sistema distingue compra, doação, venda etc. pelas palavras do texto; sem essa pista, códigos parecidos ficam
empatados e a regra R10 mostra as alternativas. Uma palavra solta não decide um código (R4 exige ao menos 2 termos
em comum); nesse caso ele pergunta ao operador. Palavras de cabeçalho de atos (portaria, decreto, resolve...) são ignoradas..
