# Pinout & Esquema Elétrico

A tabela e o diagrama a seguir especificam o mapa de pinos (*pinout*) do microcontrolador ESP32 com os sensores e atuadores do projeto **Evoluz**.

---

## 📌 Tabela de Conexões do ESP32

| Componente | Pino do Módulo | Pino ESP32 | Tipo de Sinal | Observações |
| :--- | :--- | :--- | :--- | :--- |
| **DHT22** | VCC | 3V3 / 5V | Alimentação | Requer resistor pull-up de 10kΩ entre VCC e DATA |
| **DHT22** | DATA | `GPIO 4` | Digital I/O | Leitura de temperatura e umidade |
| **DHT22** | GND | GND | Terra | Terra comum |
| **Sensor Solo Capacitivo** | VCC | 3V3 | Alimentação | Uso em 3.3V para compatibilidade ADC |
| **Sensor Solo Capacitivo** | AOUT | `GPIO 34` | Analógico (ADC1) | Não usar ADC2 (conflita com Wi-Fi) |
| **Sensor Solo Capacitivo** | GND | GND | Terra | Terra comum |
| **Módulo INA219** | VCC / GND | 3V3 / GND | Alimentação | Barramento $I^2C$ padrão |
| **Módulo INA219** | SDA | `GPIO 21` | $I^2C$ Dados | Linha de comunicação de dados |
| **Módulo INA219** | SCL | `GPIO 22` | $I^2C$ Clock | Linha de clock |
| **Módulo INA219** | Vin+ / Vin- | Barramento Bateria | Sensor Shunt | Em série com o polo positivo da carga |
| **Driver MOSFET Bomba** | PWM IN | `GPIO 18` | Digital / PWM | Saída LEDC modulada de 0 a 100% |
| **Driver MOSFET Bomba** | GND | GND | Terra | Terra de sinal compartilhado |

---

## 🔌 Diagrama Esquemático em Bloco

```
                      +-------------------+
                      |   Painel Solar    |
                      +---------+---------+
                                |
                                v
                      +-------------------+
                      | Controlador Carga |
                      +----+---------+----+
                           |         |
                  +--------+         +--------+
                  |                           |
                  v                           v
          +---------------+           +---------------+
          | Bateria 12V   |           | Módulo INA219 |
          +-------+-------+           +-------+-------+
                  |                           | (I2C: 21, 22)
                  |                           v
                  |               +=======================+
                  |               |     ESP32 DEVKIT      |
                  |               +=======================+
                  |                 | (4)    | (34)   | (18 PWM)
                  |                 |        |        |
                  |                 v        v        v
                  |              [DHT22]  [Solo]   [MOSFET]
                  |                                   |
                  +-----------------------------------+
                                    |
                                    v
                           [ Motobomba 12V DC ]
```
