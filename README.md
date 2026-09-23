# Evoluz — Irrigação Inteligente com IA, Energia Solar e Evapotranspiração

Bem-vindo à documentação oficial do **Evoluz**.

O **Evoluz** é uma solução de engenharia e inteligência artificial aberta e de baixo custo, projetada para a agricultura familiar em regiões com infraestrutura energética precária ou isolada (como o semiárido brasileiro).

---

## 💡 A Proposta de Valor

> O Evoluz une, em um único algoritmo de inteligência artificial embarcada (TinyML), duas decisões cruciais que hoje são tomadas de forma isolada no campo:
>
> 1. **Quanto de água a planta realmente precisa** (calculado via Evapotranspiração $ET_0$ e umidade do solo);
> 2. **Quanta energia solar está disponível no momento** (geração fotovoltaica instantânea + saúde da bateria).

```
   ┌───────────────────────────┐      ┌───────────────────────────┐
   │     Orçamento Hídrico     │      │   Orçamento Energético    │
   │  (Evapotranspiração ET0)  │      │ (Painel Solar + Bateria)  │
   └─────────────┬─────────────┘      └─────────────┬─────────────┘
                 │                                  │
                 └──────────────► 🧠 ◄──────────────┘
                           IA Decisora
                        (ESP32 / TinyML)
                                │
                                ▼
                   💧 Irrigação Inteligente
                 (Momento Certo & Volume Exato)
```

---

## 🎯 Por que o Evoluz é diferente?

| Abordagem Tradicional | Soluções Comerciais com IA | **Evoluz (Nossa Solução)** |
| :--- | :--- | :--- |
| Irrigação por timer fixo (relógio). | IA decide com base em clima/solo, mas ignora o estado da energia solar/bateria. | **Cruza hídrico + energético** em tempo real. |
| Depende de energia da concessionária ou queima baterias solares rapidamente. | Soluções proprietárias, fechadas e com custo proibitivo para pequenos produtores. | **Hardware acessível (ESP32)**, código aberto e operação **100% offline**. |
| Desperdício de água e desgaste de bomba. | Alto custo de licenciamento e nuvem obrigatória. | Alinhado a programas governamentais existentes (**MIDR/MME/MDA/Codevasf**). |

---

## 🧭 Navegação Rápida

- [Visão Geral & Contexto](introducao/visao-geral.md)
- [As Dores que o Evoluz Resolve](introducao/o-problema.md)
- [Análise da Lacuna de Mercado](introducao/lacuna-de-mercado.md)
- [Fundamento: Orçamento Hídrico ($ET_0$)](fundamentos/orcamento-hidrico.md)
- [Fundamento: Orçamento Energético (Solar + Bateria)](fundamentos/orcamento-energetico.md)
- [Arquitetura de Hardware & Software](arquitetura/visao-geral.md)
- [Matriz de Decisão da IA](algoritmo-decisao/matriz-decisao.md)
- [Impacto Social e Políticas Públicas](impacto-social-publico/impacto-social.md)
- [Guia de Início Rápido (Hardware & Firmware)](guia-desenvolvimento/getting-started.md)
