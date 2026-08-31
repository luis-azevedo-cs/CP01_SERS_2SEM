### Soluções em Energias Renováveis e Sustentáveis 

Atividade prática com datasets de energia — Orange Data Mining, Python e Pandas
----------------------------------------------------------------------------------------------------------------------------------------------------
### Questão 01: Appliances Energy Prediction (UCI)

**Objetivo:** Identificar períodos de alto consumo elétrico e correlacioná-los com temperatura e umidade residenciais.

**A -  Orange Data Mining (Workflow):**
<img width="741" height="411" alt="image" src="https://github.com/user-attachments/assets/225f466a-7e30-4fd5-b25e-25640b32cce1" />

**B - Python / Pandas (Análise):**
* **Amostra:** 1.974 linhas × 8 colunas (sem nulos).
* **Renomeação:** Padronização dos nomes para `Consumo_Eletrodomesticos` e variáveis ambientais (`Temp_Cozinha`, etc.).
* **Mapeamento de Picos:**
  * **Consumo Máximo:** 770 W | **Limiar de 70%:** 539 W
  * **Registros com consumo > 70%:** 22 (1,11% da amostra).
  * **Registros com consumo > 70% E Temp_Cozinha > média (21,66 °C):** 8.
* **Conclusão:** O filtro duplo reduziu os eventos de 22 para 8, isolando picos de consumo que ocorreram em momentos de maior aquecimento ambiente.
-----------------------------------------------------------------------------------------------------------------------------------------------------
### Questão 02: Steel Industry Energy Consumption (UCI)

**Objetivo:** Identificar picos de consumo em uma indústria siderúrgica e avaliar se coincidem com alta carga operacional ou fatores de potência desfavoráveis.

**1. Orange Data Mining (Workflow):**
<img width="741" height="411" alt="image" src="https://github.com/user-attachments/assets/60d8f399-eec8-4ee6-929d-36c6eb3ddef0" />

**2. Python / Pandas (Análise):**
* **Amostra:** 7.008 linhas × 9 colunas.
* **Renomeação:** `Usage_kWh` ➔ `Consumo_kWh`, além de padronizar atributos de fator de potência (`FP_Atrasado`, `FP_Adiantado`).
* **Mapeamento de Picos:**
  * **Consumo Máximo:** 153.14 kWh | **Limiar de 75%:** 114.85 kWh
  * **Registros com consumo > 75%:** 129 (1,84% da amostra).
  * **Registros na categoria 'Maximum Load':** 0 (na amostra extraída).
* **Análise de Fator de Potência (Limite de Alerta FP < 0.92):**
  * **Registros com alto consumo E baixo FP (< 0.92):** 0 ocorrências no filtro específico.
* **Conclusão:** Eventos que combinam elevado consumo com baixo fator de potência representam ineficiência crítica (circulação excessiva de energia reativa). Essa situação sobrecarrega condutores, provoca quedas de tensão e pode gerar multas regulatórias, exigindo inspeção para instalação de bancos de capacitores.
-----------------------------------------------------------------------------------------------------------------------------------------------------
### Questão 03: Power Consumption of Tetouan City (UCI)

**Objetivo:** Identificar qual das três zonas de Tétouan apresenta o maior pico de consumo de energia e analisar as condições de temperatura associadas aos momentos de maior demanda.

**1. Orange Data Mining (Workflow):**
<img width="741" height="411" alt="image" src="https://github.com/user-attachments/assets/b6c46eeb-c393-47e4-a1d2-0dc446986d69" />

**2. Python / Pandas (Análise):**
* **Amostra:** 7.863 linhas × 4 colunas.
* **Renomeação:** Variáveis mapeadas para `Consumo_Zona_1`, `Consumo_Zona_2` e `Consumo_Zona_3`.
* **Identificação de Picos de Consumo:**
  * **Zona 1 (Máx):** 39.60 | **Zona 2 (Máx):** 94.70 | **Zona 3 (Máx):** 6.325
  * **Zona com maior pico:** **Consumo_Zona_2** (94.70).
* **Mapeamento do Limiar (70% da Zona 2):**
  * **Limiar de 70%:** 66.29.
  * **Registros acima de 70%:** 4.687 (59,61% da amostra total).
* **Filtragem Combinada (Consumo Zona 2 > 70% E Temperatura > Média):**
  * **Temperatura Média:** 18.79 °C.
  * **Registros com alto consumo E alta temperatura:** 1.886 (23,99% do total).
* **Conclusão:** A inclusão da temperatura acima da média como segundo critério reduziu o volume de registros em **59,76%** (de 4.687 para 1.886 ocorrências), evidenciando que uma parcela expressiva dos picos de consumo na Zona 2 ocorre sob temperaturas mais amrenas ou moderadas.
----------------------------------------------------------------------------------------------------------------------------------------------------
### Questão 04: Solar Power Generation Data (Kaggle)

**Objetivo:** Localizar períodos de alta geração na usina fotovoltaica e identificar quais inversores aparecem com maior frequência nesses momentos.

**1. Orange Data Mining (Workflow):**
<img width="741" height="411" alt="image" src="https://github.com/user-attachments/assets/12dd2ecc-13cc-4ada-9640-2f1aa87beb22" />

**2. Python / Pandas (Análise):**
* **Amostra:** 13.540 linhas × 6 colunas.
* **Renomeação:** Variáveis padronizadas para `Potencia_CC`, `Potencia_CA` e `Geração Diária`.
* **Mapeamento de Potência CA Máxima e Limiar:**
  * **Potência CA Máxima:** 1366.26 kW
  * **Limiar de 70%:** 956.38 kW
* **Filtragem de Alta Geração (> 70% CA Máxima):**
  * **Registros acima do limiar:** 1.019 (7,53% da amostra total).
* **Frequência de Inversores no Recorte:**
  * **Inversor mais frequente:** `oZ35aAeoifZaQzV` com **74 registros**.
* **Conclusão:** A maior contagem de um inversor em períodos de pico aponta que ele operou mais vezes próximo ao teto de sua capacidade nominal durante a janela amostrada. No entanto, esse recorte isolado não permite inferir falha ou superioridade técnica sem o cruzamento com dados de irradiação solar e temperatura dos painéis (arquivo de sensores).
--------------------------------------------------------------------------------------------------------------------------------------------------
### Questão 05 - Solar & Wind Energy Production (Kaggle)

**Objetivo:** Comparar a ocorrência de períodos de alta produção solar e eólica, ajustando cada fonte ao seu próprio valor máximo para respeitar as diferenças de escala.

**1. Orange Data Mining (Workflow):**
<img width="741" height="411" alt="image" src="https://github.com/user-attachments/assets/1e4cc9c2-72a4-47eb-a9e5-72a2ba33e48b" />

**2. Python / Pandas (Análise):**
* **Amostra:** 10.373 linhas (após pivotagem por data e hora).
* **Renomeação e Estruturação:** Pivotagem dos dados para gerar as colunas `Geracao_Solar` e `Geracao_Eolica`.
* **Valores Máximos Registrados:**
  * **Máximo Solar:** 16.316,00
  * **Máximo Eólico:** 22.929,00
* **Limiares de 70% por Fonte:**
  * **Limiar Solar (70%):** 11.421,20
  * **Limiar Eólico (70%):** 16.050,30
* **Ocorrências de Alta Geração:**
  * **Alta Geração Solar:** 45 registros (0,43% do total).
  * **Alta Geração Eólica:** 245 registros (2,36% do total).
* **Comparação:** A fonte **EÓLICA** apresentou maior frequência acima do seu limiar de 70% (245 vs 45 registros).
* **Conclusão:** Utilizar um mesmo valor numérico absoluto como limite geraria uma distorção grave na análise. Como a capacidade instalada e a escala operacional da fonte eólica são significativamente maiores (pico de 22.929 contra 16.316 da solar), adotar o limite eólico na solar faria com que ela parecesse sub-representada ou inativa. A normalização relativa (70% do máximo de cada variável) garante uma comparação justa entre as fontes.
-----------------------------------------------------------------------------------------------------------------------------------------------------
### Questão 06 - Individual Household Electric Power Consumption (UCI)

**Objetivo:** Identificar episódios de demanda elétrica elevada e analisar o impacto da inclusão da corrente elétrica acima da média como segundo critério de filtragem.

**1. Orange Data Mining (Workflow):**
<img width="782" height="380" alt="image" src="https://github.com/user-attachments/assets/8be5671a-1276-4c51-a65e-1dc05ff9346d" />

**2. Python / Pandas (Análise):**
* **Amostra:** 204.928 linhas × 7 colunas.
* **Renomeação:** `Global_active_power` ➔ `Potencia_Ativa`, `Global_reactive_power` ➔ `Potencia_Reativa`, `Voltage` ➔ `Tensao`, `Global_intensity` ➔ `Corrente`.
* **Mapeamento de Potência Ativa Máxima e Limiar (75%):**
  * **Potência Ativa Máxima:** 10,536 kW
  * **Limiar de 75% da Potência Ativa:** 7,90 kW
* **Filtro 1 — Apenas Potência Ativa (> 75% do Máximo):**
  * **Registros selecionados:** 58 (0,03% da amostra total).
* **Parâmetro de Corrente Média:**
  * **Corrente Média da Amostra:** 4,63 A
* **Filtro 2 — Dupla Condição (Potência Ativa > 75% E Corrente > Média):**
  * **Registros selecionados:** 58 (0,03% da amostra total).
  * **Diferença entre os conjuntos:** 0 registros a menos.
* **Conclusão:** Devido à relação física direta entre potência e corrente elétrica ($P = V \cdot I$), todos os momentos de consumo extremo de potência ativa (picos acima de 7,90 kW) ocorreram inevitavelmente acompanhados de correntes elétricas bastante elevadas — substancialmente maiores que a média de 4,63 A. Por essa razão, a adição do filtro secundário de corrente não removeu nenhum registro adicional na amostra analisada.
