# Contribuição para a skill de cálculo Ábacus: caso Residencial Trentino I

Origem: sessão de 13/10/2026, processo 0301612-15.2015.8.24.0038 (1ª Vara Cível de Joinville).
Objetivo: material para a skill analisar e incorporar as regras novas (índice mais atualizado, índice por componente, vincendas, ACP do Trentino e do Dante Minel, transparência do mês de índice).

Comece por `regras_propostas_para_a_skill.md` (regras em texto simples). O relatório completo está em `relatorio/RELATORIO_sessao_Trentino_e_regras_skill_calculo.docx`.

## Conteúdo
- `regras_propostas_para_a_skill.md`: as 6 regras e observações técnicas.
- `relatorio/`: relatório em Word, com tabelas.
- `tabelas/01_comparacao_linha_a_linha_skill_x_abacus.csv`: 145 parcelas, skill com TR até 09/2026 contra o Ábacus do usuário com TR até 10/2026.
- `tabelas/02_versoes_do_calculo.csv`: as 4 versões do cálculo e os totais.
- `tabelas/03_validacao_motor_contra_ev313.csv`: o motor reproduz o cálculo do ev. 313 ao centavo com TR até 06/2026.
- `tabelas/04_taxas_planilha_inicial_x_adequada_ACP.csv`: valores das taxas da inicial (ev. 115) contra os adequados à ACP, 67 datas.
- `casos/trentino_6104/entradas/`: CSVs de taxas, vincendas, taxas com vincendas e custas.
- `casos/trentino_6104/specs/`: JSONs usados (inclui o da versão errada, `ultimo_indice` 2026-09).
- `casos/trentino_6104/saidas_skill_final/`: 2_TAXAS.PDF (TR até 10/2026) e 3_CUSTAS.PDF (TJSC).
- `casos/trentino_6104/saida_versao_errada_TR_ate_09/`: PDF gerado com o índice limitado, sem observação sobre o mês (referência do erro).
- `casos/trentino_6104/referencia_abacus_usuario/`: cálculo manual do usuário no Ábacus (referência de conferência).

## Resultado final do caso
Taxas com vincendas (TR até 10/2026): R$ 50.937,61. Custas (TJSC até 09/2026): R$ 1.069,60. Total: R$ 52.007,21.
