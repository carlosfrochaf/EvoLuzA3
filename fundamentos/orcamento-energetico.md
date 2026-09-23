# Orçamento Energético & Proteção de Bateria

O **Orçamento Energético** prevê e mensura a disponibilidade de potência elétrica em tempo real, garantindo que o bombeamento ocorra sem comprometer a integridade e a vida útil do sistema de armazenamento (baterias).

---

## ☀️ Geração Solar e Rastreamento de Potência (MPPT)

O sistema fotovoltaico converte a irradiância solar ($W/m^2$) em energia elétrica contínua (DC).

* **MPPT (*Maximum Power Point Tracking*):** Técnica algorítmica/hardware que ajusta dinamicamente a impedância do circuito para extrair sempre a máxima potência do painel solar, mesmo sob variações de nebulosidade ou temperatura.
* **Previsão de Janelas Solares:** O algoritmo monitora a inclinação da curva de geração (potência no $t_0$ vs $t_{-1}$) para prever se o sistema está entrando no pico diário (11h às 14h) ou se aproximando do entardecer.

---

## 🔋 Prevenção Ativa de Descarga Profunda (*Deep Discharge Protection*)

As baterias de ciclo profundo (Chumbo-Ácido estacionárias ou Lítio LiFePO4) sofrem degradação exponencial de ciclos de vida quando descarregadas abaixo de certos limites:

```
 Estado de Carga (SoC)     Ação do Sistema Evoluz
 ─────────────────────     ───────────────────────────────────────────
 [80% - 100%] (Alto)   ──► 🟢 Irrigação Total liberada (Potência Máx.)
 [50% - 79%]  (Médio)  ──► 🟡 Irrigação Oportunista (Potência Modulada PWM)
 [20% - 49%]  (Baixo)  ──► 🟠 Irrigação Apenas de Sobrevivência (Mínima)
 [< 20%]      (Crítico)──► 🔴 Bomba Desligada (Proteção total da bateria)
```

---

## ⚡ Monitoramento com INA219 (Tensão e Corrente $I^2C$)

O módulo **INA219** faz leituras de alta precisão via barramento $I^2C$:

```
                             +-------------------+
                             |    Painel Solar   |
                             +---------+---------+
                                       |
                                       v
                             +-------------------+
                             | Controlador Carga |
                             +---------+---------+
                                       |
                   +-------------------+-------------------+
                   |                                       |
                   v                                       v
         +-------------------+                   +-------------------+
         |  Bateria Chumbo/  |                   |  Módulo INA219    |
         |      LiFePO4      |                   | (Leitura V e I)   |
         +-------------------+                   +---------+---------+
                                                           |
                                                           v
                                                 +-------------------+
                                                 | ESP32 Decisor IA  |
                                                 +-------------------+
```

* **Cálculo da Potência Instantânea:**
  $$P(t) = V_{\text{bus}}(t) \times I_{\text{load}}(t)$$
* **Estado de Carga Estimado (SoC):**
  Calculado pela tensão de circuito aberto ($V_{oc}$) combinada com a contagem de Coulomb (integração de corrente no tempo).
