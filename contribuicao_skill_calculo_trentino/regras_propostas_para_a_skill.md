# Regras propostas para a skill calculo-debito-abacus (origem: caso Residencial Trentino I, processo 0301612-15.2015.8.24.0038)

Status: propostas do usuário, ainda não incorporadas à skill. Confirmar os pontos marcados como "a confirmar" em cada caso.

## REGRA 1. Usar sempre o índice mais atualizado
- Usar o último mês disponível nas tabelas de `assets/indices/`, inclusive o mês da data final do cálculo.
- NÃO limitar o índice por iniciativa própria. O parâmetro `ultimo_indice` só pode ser usado para reproduzir cálculo antigo que conste dos autos (ex.: validação do ev. 313 do caso, que só bate ao centavo com TR até 06/2026), e a resposta ao usuário deve dizer isso expressamente.
- A linha "COMPARAÇÃO" do script (total com um mês a menos) é só informativa. O total a indicar na peça é sempre o do índice mais atualizado.
- Se a tabela não cobrir o mês da data final, avisar expressamente.
- Ao receber cálculo manual do Ábacus do usuário para conferência: comparar linha a linha e, havendo diferença, verificar primeiro o último mês de índice aplicado em cada lado.

## REGRA 2. Índice por componente (Trentino I e II)
- Taxas condominiais: TR (convenção, arts. 45 e 46; decisão da ACP).
- Custas: TJSC, salvo deliberação diversa no processo (normalmente não há). Procurar nos autos antes de calcular.
- Hoje o `calcular.py` aceita um único `indice` por especificação; foi preciso rodar duas vezes (taxas com TR, custas com TJSC). Implementar `indice` próprio para o bloco `custas`.

## REGRA 3. Vincendas
- Enquanto NÃO houver levantamento nem recebimento de valor a ser abatido, as vincendas entram no MESMO cálculo das taxas (um só PDF).
- Só calcular vincendas em separado quando existir levantamento ou abatimento (aí vale o fluxo atual de remanescente + vincenda separada).
- Isto altera o texto atual de `references/parametros.md` §1-A ("VINCENDAS = SEMPRE CÁLCULO SEPARADO").
- Custas continuam sempre em cálculo próprio, somadas às taxas só no final.

## REGRA 4. Cautela com as ações civis públicas do Trentino (I e II) e do Dante Minel (GATE ANTES DE CALCULAR)
1. Identificar o condomínio. Se for Trentino I, Trentino II ou Dante Minel, aplicar este gate.
2. Conferir se os valores das taxas recebidos são os adequados à ACP ou os da petição inicial (comparar com a planilha de débitos, o relatório de débitos ou os boletos da inicial). Exemplo do caso: 02/2013, inicial R$ 114,85, adequado R$ 104,41; razão adequado/inicial de 0,9091 ou 0,8696 em todas as 67 datas comparáveis (02/2013 a 10/2018). Ver `tabelas/04`.
3. Se os valores forem IGUAIS aos da inicial: NÃO FAZER O CÁLCULO. Emitir alerta expresso e destacado, no início da resposta, dizendo que as taxas parecem não ter sido adequadas à ACP, e perguntar se o usuário deseja continuar ou não.
4. Verificar nos autos: (a) decisão que condicionou o andamento à adequação do cálculo (no caso, ev. 293); (b) se a ACP foi baixada (no caso, ev. 302); (c) parâmetros da convenção (TR, juros 1%, multa 2%).
5. ACP do caso: nº 5033243-81.2023.8.24.0038, 1ª Vara da Fazenda Pública de Joinville, tutela de urgência de 25/08/2023 (ev. 291, OUT2).
6. A confirmar com o usuário em cada caso: a faixa de datas afetada (informada como "taxas anteriores a 2023, se não me engano") e a existência da ACP do Dante Minel (informada pelo usuário, não verificada nos autos desta sessão).

## REGRA 5. Conferência com o Ábacus
- Entregar sempre o total decomposto (taxas, custas, total) e registrar o último mês de índice usado de cada índice.
- Se o usuário trouxer o PDF do Ábacus: comparar linha a linha (modelo em `tabelas/01`).

## REGRA 6. Transparência do mês de índice (erro gravíssimo apontado pelo usuário)
- Em TODO PDF e em TODA resposta ao usuário, declarar até qual mês cada índice foi aplicado (ex.: "TR aplicada até 10/2026; TJSC até 09/2026").
- Se o último mês aplicado for anterior ao mês da data final, mesmo que por UM mês, imprimir observação expressa no PDF ("Não foi aplicada correção monetária após <data>, pois o índice <ÍNDICE> não está atualizado até a data final do cálculo") e destacar o fato no início da resposta.
- A regra atual (observação só quando falta o índice do mês ANTERIOR ao da data final) é enganosa e deve ser abandonada.
- Toda linha "INFO" ou "ATENÇÃO" que o script imprimir no terminal deve ser repassada ao usuário.
- Incidente de origem: no caso, o índice foi limitado a 09/2026 com a TR de 10/2026 disponível, o PDF saiu sem observação e a informação não foi repassada, gerando divergência de R$ 34,52 com o Ábacus do usuário. Ver `tabelas/01` e `tabelas/02`.

## Observações técnicas
- Dependências ausentes no ambiente: `pymupdf` e `docxtpl`. Verificar e instalar ao iniciar.
- Aviso V6 sem sentido quando não há abatimento e data-base = data final. Suprimir nesse caso.
- Manter a validação do motor contra um cálculo dos autos antes de cada cálculo novo (`tabelas/03`).
