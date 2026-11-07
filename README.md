# 🤖 Smart Matcher — Analisador de Compatibilidade com IA

O **Smart Matcher** é uma ferramenta desenvolvida em Python que utiliza a API do **Google GenAI (Gemini)** para realizar triagens automáticas e inteligentes de compatibilidade entre perfis profissionais e descrições de vagas de tecnologia.

---

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python 3.13
* **IA / LLM:** SDK Oficial do Google GenAI (`google-genai`)
* **Testes & QA:** `pytest`
* **Ambiente:** Visual Studio Code / Windows PowerShell & CMD

---

## 🛡️ Arquitetura de Resiliência (Highlight de Engenharia)

Durante a integração com modelos LLM em nuvem, a aplicação foi projetada para lidar com instabilidades de rede, limitações de cota e mudanças de versões da API (erros HTTP 401, 404 e 503).

Para garantir **alta disponibilidade**, o sistema implementa **duas camadas de segurança**:

1. **Model Fallback Strategy (Failover em Nuvem):**
   * A aplicação mantém uma lista sequencial de modelos ativos (`gemini-3.8-flash`, `gemini-3.1-pro-preview`).
   * Caso o modelo principal apresente indisponibilidade por alta demanda (erro 503) ou alteração de suporte, o script realiza a alternância automática para o próximo modelo sem interromper a execução.

2. **Local Fallback Motor (Motor Offline):**
   * Caso toda a infraestrutura externa da API esteja temporariamente inacessível, o programa aciona um tratamento de exceções (`try-except`) que entrega um relatório local estruturado.
   * **Garantia:** O usuário final nunca fica sem resposta e a aplicação não sofre *crash*.

---

## 🚀 Como Executar o Projeto

1. **Clone o repositório:**
   ```bash
   git clone [https://github.com/seu-usuario/Smart-matcher.git](https://github.com/seu-usuario/Smart-matcher.git)
   cd Smart-matcher