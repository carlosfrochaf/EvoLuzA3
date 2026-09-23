# Evolução do Modelo: Regras a Reinforcement Learning

O desenvolvimento do cérebro decisório do **Evoluz** segue um roadmap evolutivo em três fases, facilitando a validação em bancada e a posterior sofisticação científica em campo.

---

## 📈 Roadmap de Maturidade da IA

```
 ┌─────────────────────────┐     ┌─────────────────────────┐     ┌─────────────────────────┐
 │        FASE 1           │     │         FASE 2          │     │         FASE 3          │
 │ Sistema Especialista    │ ──► │  Modelos de Regressão   │ ──► │  Reinforcement Learning │
 │   Baseado em Regras     │     │     e TinyML Supervision│     │     (Q-Learning / RL)   │
 └─────────────────────────┘     └─────────────────────────┘     └─────────────────────────┘
  • Árvores condicionais          • Predição de $ET_0$            • Agente aprende política
  • Simples de defender           • Curva de geração solar          ótima localmente
  • Fácil depuração               • Otimização contínua           • Máxima eficiência
```

---

### Fase 1: Sistema Especialista Baseado em Regras (MVP)
* **Objetivo:** Estabelecer uma linha de base (*baseline*) determinística e transparente.
* **Vantagens:** Fácil de defender perante comissões acadêmicas e órgãos governamentais, com comportamento 100% previsível e seguro.
* **Implementação:** Conjunto de regras limiares com histerese no firmware em C++.

### Fase 2: Modelos Preditivos e TinyML Supervisionado
* **Objetivo:** Antecipar o comportamento do microclima e a curva de carga solar.
* **Algoritmos:** Random Forests / Gradient Boosting convertidos via `m2cgen` ou Redes Neurais Feedforward via TensorFlow Lite for Microcontrollers.
* **Entradas:** Histórico de 24h de temperatura, umidade, radiação solar estimada e velocidade da queda de tensão da bateria.

### Fase 3: Aprendizado por Reforço (*Reinforcement Learning* em Borda)
* **Objetivo:** O sistema passa a aprender a política de irrigação ideal para aquele lote específico de terra sem calibração manual do agrônomo.
* **Espaço de Estados ($S$):** $(Umidade_{solo}, SoC_{bateria}, P_{solar\_atual}, ET_{0\_previsto})$.
* **Espaço de Ações ($A$):** Potência do PWM da bomba $[0\%, 25\%, 50\%, 75\%, 100\%]$.
* **Função de Recompensa ($R$):**
  $$R = + w_1 \cdot \text{Produtividade}(\text{Umidade Ideal}) - w_2 \cdot \text{Desgaste Bateria}(SoC < 30\%) - w_3 \cdot \text{Consumo de Água}$$
