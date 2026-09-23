# Orçamento Hídrico (Evapotranspiração ET0)

O **Orçamento Hídrico** determina com exatidão científica quanta água o solo e a cultura perderam na atmosfera em um determinado período de tempo.

---

## 💧 O Conceito de Evapotranspiração ($ET_0$)

A evapotranspiração é a combinação de dois processos físicos simultâneos:
1. **Evaporação:** Perda de água da superfície do solo e folhas molhadas.
2. **Transpiração:** Água absorvida pelas raízes e liberada pelos estômatos das plantas.

$$\text{Necessidade de Irrigação (mm)} = ET_c - P_{\text{efetiva}}$$
$$\text{Onde } ET_c = ET_0 \times K_c \text{ (Coeficiente da Cultura)}$$

---

## 📐 Modelos de Cálculo Utilizados

### 1. Método Penman-Monteith (FAO-56) — *Padrão Ouro*
Quando há sensores meteorológicos completos disponíveis (temperatura, umidade relativa, velocidade do vento e radiação solar):

$$ET_0 = \frac{0.408 \Delta (R_n - G) + \gamma \frac{900}{T + 273} u_2 (e_s - e_a)}{\Delta + \gamma (1 + 0.34 u_2)}$$

* $\Delta$: Declividade da curva de pressão de vapor saturado;
* $R_n$: Radiação solar líquida na superfície da cultura;
* $G$: Densidade de fluxo de calor no solo;
* $T$: Temperatura média do ar a 2 metros de altura;
* $u_2$: Velocidade do vento a 2 metros de altura;
* $e_s - e_a$: Déficit de pressão de vapor de saturação;
* $\gamma$: Constante psicrométrica.

### 2. Método Hargreaves-Samani — *Versão Otimizada para ESP32 / Baixo Custo*
Para implementações com sensores simplificados (apenas DHT22 para medição de temperatura máxima, mínima e média):

$$ET_0 = 0.0023 \cdot R_a \cdot (T_{\text{méd}} + 17.8) \cdot \sqrt{T_{\text{máx}} - T_{\text{mín}}}$$

* $R_a$: Radiação solar extraterrestre (calculada com base na latitude e dia do ano);
* $T_{\text{máx}}, T_{\text{mín}}, T_{\text{méd}}$: Temperaturas diárias registradas pelo sensor DHT22.

---

## 🌾 Calibração com Sensor Capacitivo de Solo

O cálculo teórico de $ET_0$ projeta a taxa de perda hídrica. No entanto, o Evoluz utiliza a leitura contínua do **sensor capacitivo de umidade do solo** na zona radicular para:
* **Validar a necessidade real:** Impedir irrigação se a capacidade de campo ($CC$) já estiver preenchida (ex: após chuva).
* **Definir o Ponto de Murcha Permanente ($PMP$):** Disparar alerta de urgência hídrica caso o solo atinja o limiar crítico.
