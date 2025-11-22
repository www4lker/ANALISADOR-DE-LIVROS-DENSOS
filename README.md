# 📚 Analisador de Livros Densos para NotebookLM

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![NotebookLM](https://img.shields.io/badge/NotebookLM-Compatible-4285F4)](https://notebooklm.google.com/)
[![RAG-Aware](https://img.shields.io/badge/RAG--Aware-Architecture-667eea)]()

> Sistema de prompts estratificados para análise sistemática de textos acadêmicos densos usando Google NotebookLM, com compensações arquiteturais para limitações de RAG (Retrieval-Augmented Generation).

## 🔗 Parte da Tríade Ferramentas para NotebookLM

Esta ferramenta integra um ecossistema de três aplicações complementares para maximizar produtividade acadêmica com NotebookLM:

1. **[Gerador de Prompts para Flashcards](https://github.com/www4lker/gerador-prompt-flashcards)**  
   → Cria flashcards otimizados para repetição espaçada, maximizando retenção de longo prazo

2. **[Gerador de Prompts para Reports Customizados](https://github.com/www4lker/gerador-prompt-notebooklm)**  
   → Gera prompts para a funcionalidade "Create from zero" (Reports personalizados)

3. **Analisador de Livros Densos** *(este repositório)*  
   → Análise sistemática baseada na estrutura clássica de produção livreira + protocolos de verificação para limitações RAG

**Todas as ferramentas foram desenvolvidas com base em pesquisa científica sobre limitações de sistemas RAG e codificadas com assistência do Claude (Anthropic).**

---

## 🎯 Problema que Esta Ferramenta Resolve

Sistemas RAG como Google NotebookLM apresentam **limitações estruturais documentadas** que comprometem análise de textos densos:

- **Fragmentação por Chunking**: Sistema não lê textos integralmente; processa via segmentos semânticos
- **Semantic Locking**: Uma vez recuperados, chunks iniciais "monopolizam" análises subsequentes
- **Path Dependency**: Queries sucessivas não resetam prioridades; mantêm viés da primeira recuperação
- **Viés de Similaridade**: Algoritmo privilegia similaridade semântica sobre relevância factual
- **Missing Top-Ranked**: Informação existe no documento mas não alcança ranking suficiente para recuperação

**Consequências práticas:**
- Análises de "arco argumentativo" são tecnicamente impossíveis sem estratégia multi-prompt
- Conceitos periféricos mas semanticamente "ruidosos" dominam respostas
- Reformulações para buscar nuances retornam respostas idênticas (travamento)
- Primeiros livros carregados em corpus extenso permanecem estruturalmente sobre-representados

---

## ✨ Solução: Arquitetura RAG-Aware

Este sistema opera em **dois subsistemas complementares**:

### 🏗️ Modos de Análise Estrutural (8 tipos)
Baseados na arquitetura clássica de produção de livros acadêmicos:

| Modo | Descrição | Compensação RAG Embutida |
|------|-----------|--------------------------|
| **Introdução** | Problema, objetivos, tese central | Busca em prefácios, notas iniciais e capítulo 1 |
| **Desenvolvimento** | Argumentação principal e evidências | Estratégia multi-query por capítulo |
| **Metodologia** | Métodos, corpus, procedimentos | Busca em notas de rodapé e apêndices |
| **Conclusão** | Síntese, implicações, limitações | Force frame: implicações inesperadas |
| **Estrutura Retórica** | Estratégias persuasivas, estilo | Meta-análise para padrões globais |
| **Conceitos-Chave** | Glossário técnico contextual | Distinção: passagens de definição vs. aplicação |
| **Debates e Críticas** | Posicionamento no campo | Verificação: autores mencionados não discutidos |
| **Lacunas e Silêncios** | O que não foi abordado | Prompt "negativo": inferência por contraste |

Cada modo já vem com **compensações RAG específicas** para aquele tipo de análise, otimizando recuperação sem necessidade de intervenção manual.

### 🔬 Prompts Compensatórios Anti-Viés (6 tipos)
Ferramentas metacognitivas para auditoria do processo de recuperação:

| Prompt | Função | Quando Usar |
|--------|--------|-------------|
| **Reset Cognitivo** | Força nova recuperação semântica | Respostas sucessivas idênticas |
| **Auditoria de Omissões** | Lista chunks não-recuperados | Conceito conhecido ausente |
| **Diversidade Semântica** | Explora 4 lentes distintas | Garantir cobertura ampla |
| **Validação Pareto** | Audita os 20% essenciais | Distinguir importância de similaridade |
| **Verificação Cruzada** | Triangulação semântica | Testar robustez da análise |
| **Teste de Contradição** | Diagnóstico de travamento | Queries opostas geram respostas idênticas? |

---

## 🚀 Uso Rápido

### Instalação
Nenhuma instalação necessária. Abra `analisador-livros-densos.html` em qualquer navegador moderno.

### Workflow Básico

1. **Configure a análise:**
   ```
   Título: "Vigiar e Punir (Foucault, 1975)"
   Tipo: Livro Individual
   Contexto: "Analisando poder disciplinar para tese sobre vigilância"
   ```

2. **Selecione modo estrutural:**
   - Clique em "Introdução" (ou qualquer outro modo)

3. **Gere o prompt:**
   - Clique em "Gerar Prompt Estratificado"

4. **Copie e use:**
   - Clique em "Copiar"
   - Cole no NotebookLM
   - Analise a resposta usando o Protocolo de Auditoria Pós-Resposta

### Workflows Avançados

**Análise com Verificação:**
- Selecione modo estrutural + prompt compensatório
- Use quando trabalhar com textos extremamente densos

**Diagnóstico:**
- Selecione APENAS prompt compensatório (sem modo estrutural)
- Use para auditar resposta anterior do NotebookLM

**Progressivo em Camadas:**
- Múltiplas sessões: Introdução → Conceitos → Validação Pareto → Desenvolvimento → Conclusão
- Ideal para textos de 500+ páginas

---

## 📊 Diferenciais Técnicos

### 1. Fundamento Científico
Baseado em pesquisa sobre limitações documentadas de RAG:
- 7 pontos críticos de falha (FP1-FP7) mapeados por Barnett et al. (2024)
- Viés de recuperação em Dense Passage Retrieval (Chen et al., 2024)
- Bug Centrestage do NotebookLM (primeira fonte permanece dominante)
- Distracting effect (passagens de alta similaridade/baixa relevância)

### 2. Compensações Específicas por Contexto
Cada modo estrutural inclui estratégias customizadas:
```markdown
**Modo: Desenvolvimento**
⚠️ LIMITAÇÃO RAG CRÍTICA: Esta é a análise MAIS AFETADA por chunking.

ESTRATÉGIA COMPENSATÓRIA OBRIGATÓRIA:
1. Solicite análise POR CAPÍTULO (queries separadas)
2. Depois: "Como argumentos dos Capítulos X, Y, Z se conectam?"
3. Finalmente: "Liste transições QUE NÃO FORAM MENCIONADAS"
```

### 3. Protocolo de Auditoria Pós-Resposta
Checklist de 4 etapas integrado ao output:
- Verificação de Chunks (comparar citações com originais)
- Teste de Contradição (reformular query, checar consistência)
- Auditoria de Omissões (conceitos conhecidos ausentes)
- Validação Cross-Corpus (todos os livros considerados?)

### 4. Checklist Researcher-in-the-Loop
5 pontos de verificação manual antes de análise crítica:
- ✓ Realizei refresh do navegador?
- ✓ Confirmei ausência de "ghost summaries"?
- ✓ Identifiquei passagens citadas vs. omitidas?
- ✓ Respostas não repetem chunks anteriores?
- ✓ 20% Pareto = mais importantes (não mais similares)?

---

## 📖 Casos de Uso

### Pesquisa Acadêmica
- Análise sistemática de corpus teórico para revisão de literatura
- Extração de conceitos-chave para glossário de tese/dissertação
- Mapeamento de debates e posicionamentos no campo
- Identificação de lacunas para justificar originalidade da pesquisa

### Estudo de Textos Clássicos
- Deconstrução de obras densas (Heidegger, Deleuze, Derrida, Foucault)
- Análise estrutural de livros de 500+ páginas
- Compreensão de progressão argumentativa complexa
- Identificação de momentos de virada conceitual

### Preparação de Aulas
- Extração de estrutura retórica para discussão em seminários
- Criação de glossários conceituais para estudantes
- Mapeamento de debates para contextualização histórica
- Identificação de exemplos paradigmáticos para ilustração

### Escrita Acadêmica
- Revisão de metodologia de obras-referência
- Análise de estratégias retóricas bem-sucedidas
- Estudo de estruturas de introdução/conclusão eficazes
- Mapeamento de como autores canônicos posicionam suas contribuições

---

## 🔬 Base de Pesquisa

Este sistema foi desenvolvido com base em:

### Literatura Científica sobre Limitações RAG
- **Barnett et al. (2024)**: "Seven Failure Points When Engineering a Retrieval Augmented Generation System" - Identificação de FP1-FP7
- **Chen et al. (2024)**: "In RAG We Trust? Demystifying the Robustness of Retrieval-Augmented Generation" - Viés de recuperação em DPR
- **Zhang et al. (2025)**: "Beyond Vector Databases: RAG Without Embeddings" - Limitações de busca por similaridade vetorial
- **Gao et al. (2024)**: "The Distracting Effect in RAG Systems" - Passagens de alta similaridade/baixa relevância

### Documentação de Usuários NotebookLM
- Bug Centrestage (primeira fonte mantém prioridade)
- Janela de contexto restrita (acesso a intervalos específicos de páginas)
- Performance multimodal degradada (PDFs vs. Google Docs)
- Ausência de reset entre queries (path dependency)

### Relatórios Técnicos Próprios
Dois relatórios fundamentaram o desenvolvimento:
1. "Limitações Conhecidas do RAG e do NotebookLM ao Acessar Informações" (68 fontes)
2. "Viés de Recuperação em RAG e NotebookLM: Análise Técnica Fundamentada em Relatos de Usuários" (37 fontes)

---

## 🛠️ Requisitos Técnicos

- **Navegador:** Qualquer navegador moderno (Chrome, Firefox, Safari, Edge)
- **JavaScript:** Habilitado (sistema é Single Page Application pura)
- **NotebookLM:** Conta Google com acesso ao NotebookLM
- **Conhecimento:** Familiaridade básica com conceitos de RAG (opcional mas recomendado)

**Não requer:**
- Instalação de dependências
- Servidor backend
- Conexão contínua com internet (após carregar o HTML)

---

## 📝 Estrutura do Projeto

```
analisador-livros-densos/
│
├── analisador-livros-densos.html    # SPA completa (HTML + CSS + JS inline)
├── README-uso-analisador.md         # Guia detalhado de workflows
├── README.md                         # Este arquivo
│
└── docs/                            # (Opcional) Relatórios de pesquisa
    ├── limitacoes-rag-notebooklm.md
    └── vies-recuperacao-rag.md
```

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Áreas prioritárias:

### Expansão de Modos Estruturais
- [ ] Modo "Bibliografia Anotada" (análise de referências)
- [ ] Modo "Estrutura Narrativa" (para obras com componente literário)
- [ ] Modo "Análise Quantitativa" (para livros com dados empíricos)

### Novos Prompts Compensatórios
- [ ] "Diversidade Temporal" (forçar análise de seções iniciais/médias/finais)
- [ ] "Cross-Document Validation" (verificar consistência em corpus multi-livro)
- [ ] "Citation Network Analysis" (mapear estrutura citacional)

### Melhorias de UX
- [ ] Preset templates para disciplinas específicas (Filosofia, Sociologia, História)
- [ ] Export de histórico de análises (JSON)
- [ ] Integração com gestores de citação (Zotero API)

**Como contribuir:**
1. Fork este repositório
2. Crie uma branch para sua feature (`git checkout -b feature/NovoModoEstrutural`)
3. Commit suas mudanças (`git commit -m 'Adiciona modo Bibliografia Anotada'`)
4. Push para a branch (`git push origin feature/NovoModoEstrutural`)
5. Abra um Pull Request

---

## 🐛 Problemas Conhecidos

### Limitações do Sistema
- **Limite de caracteres NotebookLM:** Prompts gerados podem exceder 5.000 caracteres (alerta automático exibido)
- **Sem persistência:** Sistema não salva configurações entre sessões (use notepad para guardar prompts complexos)
- **Dependência de idioma:** Prompts em português podem gerar respostas em inglês dependendo da configuração do NotebookLM

### Limitações Inerentes ao NotebookLM
- **Sem API pública:** Impossível automatizar processo de análise
- **Sem cross-notebook queries:** Análises comparativas exigem consolidação manual
- **Versão gratuita:** 50 fontes/notebook, 500K palavras/fonte, 500 queries/dia

---

## 📚 Recursos Adicionais

### Documentação
- [Guia Completo de Workflows](./README-uso-analisador.md) - Exemplos detalhados de uso
- [Relatório: Limitações RAG](./docs/limitacoes-rag-notebooklm.md) - Base científica do sistema
- [Relatório: Viés de Recuperação](./docs/vies-recuperacao-rag.md) - Análise de comportamento do NotebookLM

### Comunidade
- **Issues:** Para reportar bugs ou sugerir features
- **Discussions:** Para compartilhar workflows e casos de uso
- **Wiki:** Documentação colaborativa (em desenvolvimento)

### Ferramentas Relacionadas
- [NotebookLM by Google](https://notebooklm.google.com/)
- [Gerador de Prompts para Flashcards](https://github.com/www4lker/gerador-prompt-flashcards)
- [Gerador de Prompts para Reports](https://github.com/www4lker/gerador-prompt-notebooklm)

---

## 👨‍💻 Autor

**Walker Brum**
- GitHub: [@www4lker](https://github.com/www4lker)
- Pesquisador PPGECCO/UFMT
- Área: Estudos de Cultura Contemporânea, IA e Epistemologia

---

## 📄 Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.

```
MIT License

Copyright (c) 2025 Walker Brum

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 🙏 Agradecimentos

- **Anthropic (Claude)** - Assistência na codificação e pesquisa técnica
- **Google Labs (NotebookLM)** - Plataforma que tornou esta ferramenta necessária
- **Comunidade acadêmica** - Relatos de usuários que documentaram limitações práticas do RAG
- **Colaboradores** - Todos que contribuíram com issues, PRs e feedback

---

## 📊 Status do Projeto

![Status](https://img.shields.io/badge/status-active-success)
![Maintenance](https://img.shields.io/badge/maintained-yes-brightgreen)
![Version](https://img.shields.io/badge/version-1.0.0-blue)

**Última atualização:** Janeiro 2025

---

## 🔮 Roadmap

### v1.1 (Planejado - Q1 2025)
- [ ] Presets disciplinares (Filosofia, História, Sociologia)
- [ ] Export de prompts em JSON
- [ ] Modo "dark theme"

### v1.2 (Planejado - Q2 2025)
- [ ] Integração com Zotero API
- [ ] Análise cross-notebook (via consolidação assistida)
- [ ] Biblioteca de exemplos de análises bem-sucedidas

### v2.0 (Futuro)
- [ ] Backend opcional para persistência
- [ ] Sistema de tags para categorização de prompts
- [ ] Analytics de uso (opt-in, anônimo)

---

## 💬 FAQ

**P: Este sistema substitui a leitura do texto original?**  
R: Não. Ele funciona como scaffold (andaime) metodológico que organiza o processo de análise, compensando limitações conhecidas do NotebookLM. Sempre audite respostas críticas manualmente.

**P: Por que não automatizar com API?**  
R: NotebookLM não possui API pública. Este sistema gera prompts otimizados que você copia manualmente para a plataforma.

**P: Funciona com outros sistemas RAG (ChatGPT, Claude Projects)?**  
R: Parcialmente. Prompts compensatórios são genéricos para RAG, mas modos estruturais foram otimizados especificamente para comportamento do NotebookLM.

**P: Preciso entender RAG para usar?**  
R: Não para uso básico. Mas entender conceitos como "chunking", "semantic locking" e "path dependency" ajuda a diagnosticar quando usar prompts compensatórios.

**P: Posso usar para análise de múltiplos livros?**  
R: Sim. Selecione "Corpus Extenso (6-30 obras)" e use notebooks temáticos isolados para evitar path dependency. Veja seção de Workflows no README-uso.

---

<p align="center">
  <strong>Se esta ferramenta foi útil para sua pesquisa, considere dar uma ⭐ no repositório!</strong>
</p>

<p align="center">
  Desenvolvido com 🧠 para a comunidade acadêmica
</p>
