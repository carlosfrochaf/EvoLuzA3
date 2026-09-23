# Visão Geral & Resumo Executivo

O **Evoluz** é um sistema de irrigação inteligente que une, numa única inteligência artificial embarcada, duas decisões fundamentais que historicamente sempre foram tomadas de forma desconectada no campo:

1. **Quanto de água a planta precisa** — calculado por evapotranspiração de referência ($ET_0$) e confirmado pelo sensor de umidade do solo.
2. **Quanta energia solar está disponível naquele momento** — medindo a geração solar instantânea (painel) e o estado de carga da bateria.

---

## 🌾 O Foco: Agricultura Familiar e Zonas Rurais

Em vez de irrigar por horários fixos — ou considerar apenas a umidade sem avaliar a capacidade energética —, o Evoluz cruza os dois "orçamentos" (hídrico e energético) e encontra a **janela de oportunidade ideal** para acionar a motobomba com potência controlada via PWM.

### Principais Benefícios:
* 💧 **Zero desperdício de água:** Irrigação estritamente baseada no déficit hídrico real da cultura.
* ☀️ **Máximo aproveitamento solar:** Bombeamento acionado prioritariamente nos picos de radiação solar, poupando a bateria.
* 🔋 **Proteção e longevidade das baterias:** Prevenção ativa de descarga profunda (*Deep Discharge Prevention*).
* ⚡ **Independência de rede elétrica:** Totalmente funcional em locais remotos e comunidades isoladas (off-grid).
* 📡 **Operação Offline via TinyML:** Não requer conexão contínua com a internet para tomar decisões críticas.

---

## 📊 Síntese dos Dois Orçamentos

```
                               ┌───────────────────────────┐
                               │     SENSORES DE CAMPO     │
                               │ DHT22, Solo, INA219, Rad. │
                               └─────────────┬─────────────┘
                                             │
                      ┌──────────────────────┴──────────────────────┐
                      ▼                                             ▼
        ┌───────────────────────────┐                 ┌───────────────────────────┐
        │     ORÇAMENTO HÍDRICO     │                 │   ORÇAMENTO ENERGÉTICO    │
        ├───────────────────────────┤                 ├───────────────────────────┤
        │ • Evapotranspiração (ET0) │                 │ • Geração Solar Instant.  │
        │ • Umidade Radicular Solo  │                 │ • Tensão / Carga Bateria  │
        │ • Previsão Chuva (Offline)│                 │ • Curva de Vida da Bateria│
        └─────────────┬─────────────┘                 └─────────────┬─────────────┘
                      │                                             │
                      └──────────────────────┬──────────────────────┘
                                             ▼
                               ┌───────────────────────────┐
                               │    IA EMBARCADA ESP32     │
                               │ Decisão Ótima / TinyML    │
                               └─────────────┬─────────────┘
                                             │
                                             ▼
                               ┌───────────────────────────┐
                               │      BOMBA DC (PWM)       │
                               │ Vazão modulada e precisa  │
                               └───────────────────────────┘
```
