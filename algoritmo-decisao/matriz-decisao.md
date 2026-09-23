# Matriz de Decisão Multivariável

A tomada de decisão do **Evoluz** não se resume a um simples termostato ou relógio. O sistema avalia simultaneamente múltiplos parâmetros para classificar o estado do sistema e executar a melhor ação de irrigação.

---

## 🚦 Tabela de Decisão do Algoritmo

| Umidade do Solo | Energia Solar / Bateria | Previsão de Chuva | Ação da IA | Explicação / Justificativa |
| :--- | :--- | :--- | :--- | :--- |
| **Seco** ($< PMP + \delta$) | **Alta** (Sol Pleno ou Bateria > 80%) | Sem chuva prevista | 🟢 **Irrigar Potência Máxima** | Momento perfeito: planta necessita e há abundância de energia renovável direta. |
| **Seco** ($< PMP + \delta$) | **Média** (Bateria 50-79% / Sol moderado) | Sem chuva prevista | 🟡 **Irrigação Otimizada (PWM 60%)** | Irriga com vazão reduzida para evitar pico de corrente e prolongar a bateria. |
| **Seco** ($< PMP$) | **Baixa** (Bateria < 30% / Noite ou nublado) | Sem chuva prevista | 🟠 **Irrigação Mínima de Sobrevivência** | Aplica apenas o volume estritamente necessário para a planta não morrer, aguardando o sol da manhã. |
| **Seco** ($< PMP$) | **Crítica** (Bateria < 15%) | Indiferente | 🔴 **Bloqueio Total de Bomba** | Protege a bateria contra morte permanente. Dispara alerta luminoso/BLE. |
| **Seco** | **Qualquer** | **Chuva Iminente** nas próximas 2h-4h | ⏳ **Adiar Irrigação** | Economiza ciclos de bombeamento e água de poço, aguardando a precipitação natural. |
| **Úmido / Adequado** | **Alta** (Excesso de geração solar) | Indiferente | ⚪ **Standby (Não irriga)** | Evita lixiviação do solo e apodrecimento radicular. Se aplicável, desvia energia para outros usos. |

---

## 🔄 Fluxograma Lógico de Decisão

```
                             [Início do Ciclo de Decisão]
                                          │
                                          ▼
                             ¿Chuva prevista nas próximas 3h?
                                  ├──► [SIM] ──► 🛑 Pausa irrigação (Economia)
                                  │
                                  └──► [NÃO]
                                          │
                                          ▼
                               ¿Umidade Solo < Limiar?
                                  ├──► [NÃO] ──► 🛑 Solo OK (Standby)
                                  │
                                  └──► [SIM]
                                          │
                                          ▼
                                ¿Estado da Bateria/Solar?
                                  ├──► Alta ──► 🚀 Irriga 100% PWM
                                  ├──► Média ──► ⚡ Irriga 60% PWM
                                  ├──► Baixa ──► 💧 Pulso Mínimo Sobrevivência
                                  └──► Crítica ─► 🔒 Corte de Proteção
```
