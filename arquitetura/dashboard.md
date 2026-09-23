# Dashboard & Interface do Produtor

A interface do produtor foi concebida para ser simples, visual e acessível, mesmo para agricultores sem familiaridade prévia com tecnologias complexas.

---

## 📱 Modos de Conexão com o Produtor

```
       ┌────────────────┐
       │ ESP32 (Evoluz) │
       └───────┬────────┘
               │
      ┌────────┴────────┬───────────────────┐
      │                 │                   │
      ▼ (Modo 1)        ▼ (Modo 2)          ▼ (Modo 3)
┌────────────┐   ┌─────────────┐     ┌──────────────┐
│ BLE Direto │   │ Wi-Fi AP    │     │ Nuvem / Web  │
│ (Bluetooth)│   │ (Ponto Web) │     │ (Se houver)  │
└────────────┘   └─────────────┘     └──────────────┘
```

1. **Bluetooth Low Energy (BLE - Sem Internet):**
   * O produtor aproxima o celular da caixa controladora e abre o app.
   * Conexão instantânea para verificar status da bateria, umidade do solo e forçar/pausar irrigação.
2. **Ponto de Acesso Local (Wi-Fi Captive Portal):**
   * O ESP32 cria uma rede Wi-Fi própria (`Evoluz-Config`).
   * Ao conectar, abre automaticamente no navegador uma página de diagnóstico e calibração de sensores.
3. **Dashboard Nuvem (Opcional):**
   * Exibição de gráficos históricos de $ET_0$, volume de água economizado e horas de sol aproveitadas.

---

## 📊 Principais Indicadores no Painel

* 🔋 **Status da Bateria:** Tensão ($V$), Corrente ($A$) e % de Carga com alerta de vida útil.
* 💧 **Umidade do Solo:** Indicador gráfico de "Zona Confortável", "Seco" ou "Saturado".
* ☀️ **Eficiência Solar:** Quantidade de litros de água bombeados exclusivamente com energia solar direta vs. energia da bateria.
* 📈 **Economia Acumulada:** Estimativa de litros de água e kWh poupados no mês.
