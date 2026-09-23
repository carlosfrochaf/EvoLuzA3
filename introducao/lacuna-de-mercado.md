# Lacuna de Mercado & Concorrentes

Ao analisar o panorama de tecnologias disponíveis no mercado agropecuário e de automação solar, observa-se uma divisão clara entre dois grandes polos de soluções que **não se comunicam entre si**:

---

## 🔎 Panorama Comparativo de Mercado

```
    ┌───────────────────────────────────┐       ┌───────────────────────────────────┐
    │    GRUPO 1: IRRIGAÇÃO COM IA      │       │     GRUPO 2: ENERGIA SOLAR        │
    ├───────────────────────────────────┤       ├───────────────────────────────────┤
    │ • IrrigaBot, IrriGate, IrriPro    │       │ • Wieza Energia, Kits MIDR/Gov    │
    │ • Decidem quando irrigar          │       │ • Levam energia limpa e poços     │
    │ • Foco: Solo, ET0, Clima          │       │ • Foco: Alimentar bombas solares  │
    └─────────────────┬─────────────────┘       └─────────────────┬─────────────────┘
                      │                                           │
                      └─────────────────────┬─────────────────────┘
                                            │
                                            ▼
                          ┌───────────────────────────────────┐
                          │         O QUE FALTAVA?            │
                          │   A união dos dois orçamentos     │
                          │  (Hídrico + Energia Disponível)   │
                          │  em hardware de baixíssimo custo  │
                          ├───────────────────────────────────┤
                          │       ⭐ EVOLUZ PREENCHE ⭐       │
                          └───────────────────────────────────┘
```

---

## 📊 Matriz de Comparação Detalhada

| Grupo de Soluções | O que faz | Exemplos de Mercado | O que falta / Desvantagem |
| :--- | :--- | :--- | :--- |
| **Irrigação Inteligente com IA** | Decide quando irrigar usando dados agronômicos, sensores de solo, fórmulas de evapotranspiração ($ET_0$) e previsões de clima. | *IrrigaBot* (IA embarcada de solo), *IrriGate/IrrigaPro* (monitoramento com sensores solares e clima). | **Não cruza a decisão com o estado real da energia fotovoltaica/bateria.** São produtos fechados e com preço inacessível para agricultura familiar. |
| **Energia Solar para Irrigação** | Alimenta bombas e válvulas a partir de painéis fotovoltaicos e baterias. | Programas do Governo (*MIDR / MME / Codevasf*), *Wieza Energia* (estações com acionamento automático de pivôs). | **Acionam a irrigação por regras fixas ou demandam infraestrutura industrial caríssima.** Não possuem IA unificada que aprenda com o microclima local. |
| **Evoluz (Nossa Abordagem)** | **Cruza em tempo real** a demanda de água com a oferta de energia solar e saúde da bateria. | **Evoluz Open Source** | Desenvolvido sob medida para agricultura familiar, operando 100% offline via TinyML no ESP32. |

---

## 💡 O Ponto de Inflexão Governamental

O Ministério da Integração e do Desenvolvimento Regional (**MIDR**), o Ministério de Minas e Energia (**MME**), o Ministério do Desenvolvimento Agrário (**MDA**) e a **Codevasf** vêm investindo pesadamente na instalação de painéis fotovoltaicos e poços artesianos no campo.

> **Oportunidade Estratégica:** Os programas públicos resolvem a *infraestrutura de geração*, mas deixam a bomba funcionando de maneira rústica. O **Evoluz** se apresenta como o módulo de inteligência e software ideal para maximizar o retorno desses investimentos sociais.
