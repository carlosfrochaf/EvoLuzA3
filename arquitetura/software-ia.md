# Software & TinyML Embarcado

O ecossistema de software do **Evoluz** foi construído para operar de maneira resiliente, autônoma e prioritariamente **desconectada (offline-first)**.

---

## 💻 Arquitetura do Firmware (C++ / ESP-IDF / Arduino)

O firmware do microcontrolador é organizado em tarefas assíncronas no **FreeRTOS**:

```
 ┌─────────────────────────────────────────────────────────────┐
 │                     ESCALONADOR FREERTOS                    │
 ├──────────────────────────┬──────────────────────────────────┤
 │ Task_Sensoriamento (10s) │ Leitura DHT22, Solo e INA219     │
 ├──────────────────────────┼──────────────────────────────────┤
 │ Task_IA_Decisora (60s)   │ Orçamento Hídrico x Energético   │
 ├──────────────────────────┼──────────────────────────────────┤
 │ Task_Atuador_PWM (Cont.) │ Modulação de potência da bomba   │
 ├──────────────────────────┼──────────────────────────────────┤
 │ Task_Telemetria (5min)   │ Salva em Flash / BLE / Wi-Fi     │
 └──────────────────────────┴──────────────────────────────────┘
```

---

## 🧠 TinyML: Inteligência Artificial Local

Para zonas rurais sem cobertura 3G/4G/5G ou fibra óptica, **não é viável depender de APIs em nuvem** para decidir cada irrigação.

### Como funciona o TinyML no ESP32:
1. **Treinamento Offline:** Modelos de Machine Learning (Regressão / Árvores de Decisão / Redes Neurais Quantizadas) são treinados com bases históricas de evapotranspiração, radiação solar e perda de umidade do solo.
2. **Conversão para TensorFlow Lite Micro (TFLM):** O modelo é quantizado para inteiros de 8 bits (`int8`), reduzindo o consumo de memória RAM para menos de **25 KB**.
3. **Execução Local:** O ESP32 executa a inferência em milissegundos, gerando a recomendação de tempo e potência de bombeamento.

---

## 🌐 Conectividade Opcional & Sincronização

Quando há conexão disponível (Wi-Fi da sede da fazenda ou sinal 4G pontual):
* **API Meteorológica Externa (OpenWeather / INMET):** Sincronização diária de previsão de chuva para os próximos 3 a 5 dias.
* **Sincronização de Telemetria:** Envio assíncrono de históricos de consumo de água (litros) e energia gerada (Wh).
* **Operação Fallback:** Se a conexão cair, o sistema entra imediatamente em modo autônomo baseado no cálculo local de Hargreaves-Samani e sensores físicos.
