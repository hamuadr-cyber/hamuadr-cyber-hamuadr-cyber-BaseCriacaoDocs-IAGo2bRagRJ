# EXPLICAÇÃO CAMPOS FUTUROS - ESTRUTURAÇÃO JSON GO2B

## CAMPOS PARA INGESTÃO POSTERIOR VIA INTELIGÊNCIA ARTIFICIAL

### 📋 **PRIORIDADE_PROCESSUAL**
**CONCEITO:** Classificação hierárquica da importância estratégica de cada documento no contexto processual.

**ESTRUTURA PROPOSTA:**
```json
"prioridade_processual": {
    "nivel": null,           // "CRÍTICA|ALTA|MÉDIA|BAIXA"
    "justificativa": null,   // Razão técnico-jurídica
    "data_avaliacao": null,  // Timestamp da análise
    "status": "pendente_ingestao"
}
```

**CRITÉRIOS DE AVALIAÇÃO FUTURA:**
- **CRÍTICA**: Impedimento judicial, apropriação criminosa, prova DNS
- **ALTA**: Evidências diretas, violações processuais, timeline criminal
- **MÉDIA**: Contexto histórico, padrões comportamentais
- **BAIXA**: Infraestrutura técnica, metadados

**MÉTODO DE PREENCHIMENTO:** Via análise correlacional dos doc19-evidence_index + doc04-anexo_tabela_violacoes

---

### ⚖️ **RELEVANCIA_JURIDICA**  
**CONCEITO:** Impacto específico do documento nas diferentes esferas jurídicas (criminal, cível, administrativa).

**ESTRUTURA PROPOSTA:**
```json
"relevancia_juridica": {
    "grau": null,                    // "EXTREMA|ALTA|MODERADA|BAIXA"
    "area_juridica": null,           // ["criminal", "civel", "administrativa"]
    "impacto_processual": null,      // "GAME_CHANGER|ROBUSTA|COMPLEMENTAR"
    "status": "pendente_ingestao"
}
```

**METODOLOGIA DE CLASSIFICAÇÃO:**
- **EXTREMA**: Base para nulidade absoluta (doc01-impedimento, doc64-DNS)
- **ALTA**: Evidências para responsabilização (doc59/60-apropriação)
- **MODERADA**: Suporte argumentativo (doc10-comunicações PL)
- **BAIXA**: Contexto técnico (doc13-arquitetura)

**CORRELAÇÃO COM SISTEMA RAG:** Confidence scores > 0.85 indicam relevância ALTA/EXTREMA

---

### 🔍 **EVIDENCIAS**
**CONCEITO:** Catalogação estruturada das provas documentais, testemunhais e periciais contidas ou referenciadas no documento.

**ESTRUTURA PROPOSTA:**
```json
"evidencias": {
    "documentais": [],              // Emails, contratos, comprovantes
    "testemunhais": [],            // Depoimentos, declarações
    "periciais": [],               // Laudos técnicos, perícias
    "correlacoes_detectadas": [],  // Links para outros documentos
    "status": "pendente_ingestao"
}
```

**FONTES PRIMÁRIAS PARA POVOAMENTO:**
- **doc20-evidencias_all**: 67 evidências catalogadas
- **doc19-evidence_index**: Sistema hierarquizado A/B/C
- **doc01-actor_index**: Mapeamento de atores
- **doc04-anexo_tabela_violacoes**: 95+ violações sistematizadas

**EXEMPLO DE PREENCHIMENTO AUTOMÁTICO:**
```json
"evidencias": {
    "documentais": [
        "Email Dagoberto admitindo recebimento R$600k",
        "Comprovante bancário PL Consultoria",
        "Contrato inicial violado cláusula 3.3"
    ],
    "correlacoes_detectadas": [
        {"doc_ref": "doc12", "tipo": "comprova_padrao", "forca": "alta"}
    ]
}
```

---

### 🔗 **RELACIONAMENTOS** 
**CONCEITO:** Conexões funcionais entre documentos que evidenciam padrões, contradições ou complementaridade probatória.

**ESTRUTURA PROPOSTA:**
```json
"relacionamentos": {
    "docs_origem": [],           // Documentos que referenciam este
    "docs_destino": [],          // Documentos referenciados por este  
    "tipo_relacao": [],          // "comprova|contradiz|complementa|contextualiza"
    "forca_correlacao": null,    // 0.0 - 1.0 (calculado via RAG)
    "status": "pendente_ingestao"
}
```

**DIFERENÇA CONCEITUAL COM EVIDÊNCIAS:**
- **EVIDÊNCIAS**: Provas materiais diretas contidas no documento
- **RELACIONAMENTOS**: Conexões lógicas entre diferentes documentos

**EXEMPLO PRÁTICO:**
- **doc59 (Evidência)**: Email Dagoberto sobre CMZ
- **doc03 (Relacionamento)**: Fluxo visual do dinheiro CMZ → PL
- **Tipo relação**: doc59 "comprova" doc03 com força 0.92

**MÉTODO DE DETECÇÃO:** Análise vetorial via embeddings + correlação semântica

---

## 🔮 CAMPOS FUTUROS SUGERIDOS

### **ANALISE_CONTRATOS**
**JUSTIFICATIVA:** Preparação para análise correlacional de contratos bancários mencionada.

```json
"analise_contratos": {
    "bancarios": [],                 // Contratos financeiros
    "comerciais": [],                // B2B, prestação serviços  
    "prestacao_servicos": [],        // PL Consultoria, AJ
    "correlacoes_contratuais": [],   // Vícios, descumprimentos
    "status": "futuro"
}
```

### **NEXO_CAUSAL_ECT**  
**JUSTIFICATIVA:** Base robusta para ação de cobrança/inadimplência ECT (R$ 387 milhões).

```json
"nexo_causal_ect": {
    "conexao_detectada": null,       // true/false
    "grau_correlacao": null,         // 0.0 - 1.0
    "impacto_quantificado": null,    // Valor monetário
    "base_probatoria": [],           // Documentos suporte
    "status": "futuro"  
}
```
**CORRELAÇÃO COM CASO:** 49.6% do passivo RJ + 70% validação P2 + omissões AJ documentadas

### **execucoes_socios_go2b**  

**JUSTIFICATIVA:** 
Campo estratégico fundamental
Adriano e Lidiane como avalistas/devedores solidários
Correlação direta com RJ e capacidade de pagamento
Impacto nas execuções individuais vs. recuperação empresarial

RELEVÂNCIA JURÍDICA: Execuções contra sócios podem influenciar plano RJ, Avalistas têm responsabilidade solidária/subsidiária,Correlação com capacidade econômica para honrar acordos
---

## 🚀 ESTRATÉGIA DE IMPLEMENTAÇÃO

### **FASE 1 - IMEDIATA (Script atual)**
✅ Criar estrutura de campos vazios  
✅ Aplicar categorização A-I  
✅ Inserir descrições Adriano  

### **FASE 2 - INGESTÃO INTELIGENTE (Próximo ciclo)**
🔄 Varredura correlacional entre doc19 ↔ doc20 ↔ doc01 ↔ doc04  
🔄 Aplicação de confidence scores do sistema RAG existente  
🔄 Detecção automática de relacionamentos via análise vetorial  

### **FASE 3 - ESPECIALIZAÇÃO (Futuro)**
🎯 Análise contratos bancários + correlação  
🎯 Nexo causal ECT robusto  
🎯 Validação cruzada MPF/inquérito  

---

## ✅ VANTAGENS DESTA ABORDAGEM

1. **ESTRUTURAL**: Campos vazios permitem ingestão organizada
2. **CORRELACIONAL**: Base para análise automática doc19/20/01/04  
3. **EXTENSÍVEL**: Campos futuros preparados para novos módulos
4. **COMPATÍVEL**: Mantém estrutura atual `analise_ia_real`
5. **ESCALÁVEL**: Sistema RAG futuro já encontrará estrutura preparada

**CONCLUSÃO:** Esta estruturação cria fundação sólida para ingestão inteligente, mantendo flexibilidade para expansões futuras correlacionais específicas do caso GO2B.
