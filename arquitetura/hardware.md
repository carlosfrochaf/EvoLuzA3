# Especificação de Hardware

Todos os componentes de hardware foram selecionados com base em quatro critérios rigorosos: **baixo custo**, **ampla disponibilidade no Brasil**, **baixo consumo energético (*Low Power*)** e **resistência à corrosão/intempéries**.

---

## 🎛️ Lista de Materiais (*Bill of Materials - BOM*)

### 1. Unidade Central de Controle: ESP32
* **Modelo:** ESP32 NodeMCU (30 ou 38 pinos).
* **Frequência:** Até 240 MHz Dual-Core.
* **Memória:** 520 KB SRAM, 4 MB Flash.
* **Conectividade:** Wi-Fi 802.11 b/g/n + Bluetooth 4.2 BLE.
* **Consumo em Deep Sleep:** ~10-15 µA (ideal para baterias solares).

### 2. Sensor de Umidade do Solo Capacitivo (v1.2)
* **Princípio:** Medição dielétrica de capacitância.
* **Vantagem crítica:** Não sofre corrosão galvânica acelerada (diferente dos sensores resistivos de pontas metálicas comuns).
* **Sinal:** Tensão analógica proporcional à umidade volumétrica ($0 - 3.3V$).

### 3. Sensor Meteorológico de Ar: DHT22 (AM2302)
* **Faixa de Temperatura:** -40°C a +80°C (Precisão ±0.5°C).
* **Faixa de Umidade:** 0 a 100% RH (Precisão ±2%).
* **Saída:** Sinal digital 1-Wire calibrado.

### 4. Sensor de Energia: Módulo INA219
* **Barramento:** $I^2C$ (endereço padrão `0x40`).
* **Faixa de Tensão:** 0 a 26V DC.
* **Faixa de Corrente:** Até 3.2A (extensível com resistor *shunt* externo).
* **Resolução:** 0.8mA e 4mV.

### 5. Sistema de Alimentação & Potência Solar
* **Painel Solar Fotovoltaico:** Módulo Policristalino/Monocristalino (50W a 150W conforme a bomba).
* **Controlador de Carga:** MPPT ou PWM com corte por subtensão (*LVD*).
* **Bateria:** Chumbo-ácido estacionária (12V 30Ah - 60Ah) ou LiFePO4 (12.8V).
* **Driver de Acionamento da Bomba:** Módulo MOSFET LR7843 ou Relé de Estado Sólido (SSR) compatível com sinal PWM 3.3V/5V.
* **Motobomba:** Bomba d'água DC 12V submersa ou diafragma (vazão de 4 a 15 L/min).
