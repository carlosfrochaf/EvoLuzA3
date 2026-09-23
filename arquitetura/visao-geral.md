# Visão Geral da Arquitetura

A arquitetura do **Evoluz** é dividida em quatro camadas interdependentes e desacopladas, priorizando robustez para operação em ambiente rural agressivo:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       CAMADA DE MONITORAMENTO & APP                         │
│             Dashboard Web / App Mobile (Bluetooth / Wi-Fi / LoRa)           │
└──────────────────────────────────────▲──────────────────────────────────────┘
                                       │
┌──────────────────────────────────────┴──────────────────────────────────────┐
│                         CAMADA DE SOFTWARE & IA                             │
│       • Firmware C++ / ESP-IDF / Arduino Core                               │
│       • Motor TinyML (TensorFlow Lite for Microcontrollers)                 │
│       • Lógica de Orçamento Duplo (Hídrico + Energético)                    │
└──────────────────────────────────────▲──────────────────────────────────────┘
                                       │
┌──────────────────────────────────────┴──────────────────────────────────────┐
│                         CAMADA DE SENSORES & I/O                            │
│  [DHT22 - Temp/Umid]   [Sensor Capacitivo Solo]   [INA219 - Tensão/Corrente]│
└──────────────────────────────────────▲──────────────────────────────────────┘
                                       │
┌──────────────────────────────────────┴──────────────────────────────────────┐
│                    CAMADA DE POTÊNCIA & ATUAÇÃO FÍSICA                      │
│     [Painel Solar] ──► [Controlador Carga/MPPT] ──► [Bateria 12V/24V]       │
│                                                          │                  │
│                                                          ▼                  │
│                                            [Driver PWM / MOSFET]            │
│                                                          │                  │
│                                                          ▼                  │
│                                                  [Bomba DC Submersa]        │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 📋 Resumo das Camadas e Componentes

| Camada | Componente Principal | Protocolo / Interface | Função no Sistema |
| :--- | :--- | :--- | :--- |
| **Processamento** | ESP32-WROOM-32 | Dual Core 240MHz | Núcleo de processamento, cálculo de $ET_0$ e inferência TinyML. |
| **Sensoriamento Clima** | DHT22 (AM2302) | 1-Wire Digital | Leitura de temperatura e umidade relativa do ar. |
| **Sensoriamento Solo** | Sensor Capacitivo v1.2 | Analógico (ADC ESP32) | Medição de umidade volumétrica sem corrosão por eletrólise. |
| **Sensoriamento Elétrico**| INA219 | $I^2C$ (SDA/SCL) | Medição contínua de tensão de barramento, corrente e potência. |
| **Atuação / Bombeamento** | Driver MOSFET / PWM | GPIO ESP32 (LEDC) | Ajuste contínuo de rotação/vazão da motobomba de acordo com a energia. |
| **Interface / Conectividade**| BLE / WebServer Local / LoRa | Sem Fio | Configuração no campo pelo agricultor sem necessidade de internet. |
