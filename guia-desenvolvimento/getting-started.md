# Getting Started / Montagem Rápida

Este guia passo a passo orienta a preparação do ambiente de desenvolvimento, montagem da bancada de testes e gravação do firmware no microcontrolador ESP32.

---

## 🧰 Pré-requisitos de Software

1. **IDE de Desenvolvimento:** [VS Code](https://code.visualstudio.com/) com a extensão [PlatformIO IDE](https://platformio.org/) (ou Arduino IDE 2.x).
2. **Bibliotecas Principais:**
   * `Adafruit INA219` (Leitura de corrente e tensão $I^2C$)
   * `DHT sensor library` (Leitura de temperatura e umidade)
   * `TensorFlowLite_ESP32` (Para o motor TinyML embarcado)
   * `ArduinoJson` (Manipulação de payloads de telemetria)

---

## ⚙️ Configuração do `platformio.ini`

Se estiver utilizando o PlatformIO, utilize a seguinte configuração:

```ini
[env:esp32dev]
platform = espressif32
board = esp32dev
framework = arduino
monitor_speed = 115200
lib_deps =
    adafruit/Adafruit INA219@^1.2.2
    adafruit/DHT sensor library@^1.4.6
    bblanchon/ArduinoJson@^7.0.0
```

---

## 🧪 Roteiro de Teste em Bancada

1. **Teste dos Sensores:**
   * Conecte o sensor capacitivo ao pino `GPIO34` (ADC1).
   * Conecte o DHT22 ao pino `GPIO4`.
   * Conecte o INA219 aos pinos $I^2C$ (`GPIO21` - SDA, `GPIO22` - SCL).
2. **Calibração do Sensor Capacitivo:**
   * Meça o valor analógico no ar seco ($V_{\text{ar}} \approx 3000$).
   * Meça o valor analógico imerso em copo com água ($V_{\text{água}} \approx 1300$).
   * Atualize as constantes de calibração no firmware.
3. **Teste do Driver da Bomba:**
   * Conecte o gate do MOSFET ao pino `GPIO18` (saída PWM).
   * Varie o *duty cycle* de 0 a 255 e confira a modulação de rotação da bomba.
