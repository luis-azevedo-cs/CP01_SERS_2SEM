### Soluções em Energias Renováveis e Sustentáveis 

Atividade prática com datasets de energia — Orange Data Mining, Python e Pandas

### Questão 01: Appliances Energy Prediction (UCI)

**Objetivo:** Identificar períodos de alto consumo elétrico e correlacioná-los com temperatura e umidade residenciais.

** A -  Orange Data Mining (Workflow):**
<img width="741" height="411" alt="image" src="https://github.com/user-attachments/assets/225f466a-7e30-4fd5-b25e-25640b32cce1" />

** B - Python / Pandas (Análise):**
* **Amostra:** 1.974 linhas × 8 colunas (sem nulos).
* **Renomeação:** Padronização dos nomes para `Consumo_Eletrodomesticos` e variáveis ambientais (`Temp_Cozinha`, etc.).
* **Mapeamento de Picos:**
  * **Consumo Máximo:** 770 W | **Limiar de 70%:** 539 W
  * **Registros com consumo > 70%:** 22 (1,11% da amostra).
  * **Registros com consumo > 70% E Temp_Cozinha > média (21,66 °C):** 8.
* **Conclusão:** O filtro duplo reduziu os eventos de 22 para 8, isolando picos de consumo que ocorreram em momentos de maior aquecimento ambiente.
