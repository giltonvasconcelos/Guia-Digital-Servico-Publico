# 🔢 Dados Anonimizados

## 📋 O que são dados anonimizados?

### Definição legal (Art. 5º, III da LGPD)
"Dado anonimizado: dado relativo a titular que não possa ser identificado, considerando a utilização de meios técnicos razoáveis e disponíveis na ocasião de seu tratamento"

### Características principais
- **Não permitem identificar** o titular direta ou indiretamente
- **Não são considerados dados pessoais** para fins da LGPD
- **Podem ser utilizados livremente** (desde que realmente anônimos)
- **Risco de reidentificação** deve ser considerado e mitigado
- **Responsabilidade** de quem realiza a anonimização

### Importância no setor público
- Permite **compartilhamento** de dados para pesquisa
- Viabiliza **transparência** sem expor cidadãos
- Contribui para **políticas públicas** baseadas em evidências
- **Incentiva inovação** com dados governamentais

### Processo de anonimização
Dados pessoais (protegidos pela LGPD)
↓
[Processo de anonimização]
↓
Dados anonimizados (fora do escopo da LGPD)
↓
Podem ser compartilhados, publicados, utilizados para pesquisa


## 🔬 Técnicas de anonimização

### 1. Supressão (Remoção)
Remoção completa de identificadores diretos que possam identificar o titular.

**Como funciona:**
- Elimina campos como nome, CPF, RG, matrícula
- Remove informações únicas ou muito específicas

**Exemplo:**
| Antes | Depois |
|-------|--------|
| João Silva, CPF 123.456.789-00 | [Removido] |
| Maria Oliveira, RG 12.345.678 | [Removido] |
| Pedro Santos, matrícula 2023001 | [Removido] |

**Vantagens:** Simples de implementar, eficaz para identificadores diretos
**Desvantagens:** Pode perder informação útil, não protege contra identificadores indiretos

### 2. Generalização
Substituição de valores específicos por categorias mais amplas.

**Como funciona:**
- Transforma idade exata em faixa etária
- Converte endereço completo em bairro ou região
- Agrupa profissões em categorias

**Exemplo:**
| Atributo | Antes | Depois |
|----------|-------|--------|
| **Idade** | 42 anos | 40-49 anos |
| **CEP** | 70040-010 | 70000-000 (região) |
| **Profissão** | Auditor fiscal | Servidor público |
| **Renda** | R$ 8.542,00 | R$ 8.000 - R$ 9.000 |
| **Data de nascimento** | 15/03/1982 | Março/1982 ou 1980-1985 |

**Vantagens:** Mantém utilidade analítica, protege contra identificação
**Desvantagens:** Perde precisão, requer definição de categorias adequadas

### 3. Perturbação (Adição de ruído)
Inserção de pequenas variações aleatórias nos dados numéricos.

**Como funciona:**
- Adiciona ou subtrai pequenos valores
- Mantém tendências estatísticas
- Impede identificação exata

**Exemplo:**
| Antes | Depois |
|-------|--------|
| Renda: R$ 5.432,00 | R$ 5.400,00 (-32) |
| Altura: 1,75m | 1,76m (+0,01) |
| Peso: 70,5 kg | 70,2 kg (-0,3) |
| Temperatura: 36,5°C | 36,6°C (+0,1) |

**Vantagens:** Preserva propriedades estatísticas, difícil de reverter
**Desvantagens:** Não adequado para dados categóricos, requer cálculo cuidadoso

### 4. Agregação
Apresentação de dados em grupo, não individualmente.

**Como funciona:**
- Agrupa registros individuais
- Apresenta estatísticas do grupo
- Elimina dados individuais

**Exemplo:**
| Individual | Agregado |
|------------|----------|
| João: 35 anos | Faixa etária 30-39: 45 pessoas |
| Maria: 38 anos | Média de idade: 36,5 anos |
| Pedro: 42 anos | Total de pessoas: 120 |
| Ana: 31 anos | Percentual por gênero: 52% feminino |

**Vantagens:** Alta proteção, útil para estatísticas públicas
**Desvantagens:** Perde dados individuais, não permite análises granulares

### 5. K-anonimato
Garantia que cada registro é indistinguível de pelo menos k-1 outros registros.

**Como funciona:**
- Cada combinação de atributos aparece pelo menos k vezes
- Quanto maior o k, maior a proteção
- Identificadores são generalizados até atingir o k desejado

**Exemplo com k=3:**
| Grupo | Idade | CEP | Profissão |
|-------|-------|-----|-----------|
| Grupo A | 30-39 | 70000-*** | Servidor |
| Grupo A | 30-39 | 70000-*** | Servidor |
| Grupo A | 30-39 | 70000-*** | Servidor |
| Grupo B | 40-49 | 71000-*** | Professor |
| Grupo B | 40-49 | 71000-*** | Professor |
| Grupo B | 40-49 | 71000-*** | Professor |

**Vantagens:** Proteção comprovada matematicamente, padrão internacional
**Desvantagens:** Complexo de implementar, pode perder muita informação

### 6. L-diversidade (Avançado)
Evolução do k-anonimato que garante diversidade de valores sensíveis.

**Como funciona:**
- Além de k registros iguais, garante l valores diferentes para atributos sensíveis
- Protege contra ataques de homogeneidade

**Exemplo:**
Sem l-diversidade (problema):
Grupo | Idade | CEP | Doença
A | 30-39 | 70000-* | Câncer
A | 30-39 | 70000-* | Câncer
A | 30-39 | 70000-* | Câncer

Com l-diversidade (l=3):
Grupo | Idade | CEP | Doença
A | 30-39 | 70000-* | Câncer
A | 30-39 | 70000-* | Diabetes
A | 30-39 | 70000-* | Hipertensão


## ⚠️ Diferença: Anonimização vs Pseudonimização

### Pseudonimização
- Substituição de identificadores por códigos ou pseudônimos
- **Permite reidentificação** com informação adicional (chave)
- **Ainda é dado pessoal** (sujeito à LGPD)
- Técnica recomendada para segurança, mas não remove da lei

### Comparativo detalhado

| Aspecto | Anonimização | Pseudonimização |
|---------|--------------|-----------------|
| **Reversível** | Não (irreversível) | Sim (com chave) |
| **É dado pessoal?** | Não | Sim |
| **Sujeito à LGPD?** | Não | Sim |
| **Risco principal** | Reidentificação | Quebra da chave |
| **Exemplo** | Estatísticas agregadas | ID numérico em pesquisa |
| **Onde usar** | Dados públicos, pesquisas | Bancos de dados operacionais |
| **Segurança** | Alta (se bem feito) | Média (dependente da chave) |

### Exemplo de pseudonimização
Prontuário original:
Paciente: João Silva, CPF 123.456.789-00
Data nasc: 15/03/1982, Diagnóstico: Hipertensão

Após pseudonimização:
ID: PAC-98765, Diagnóstico: Hipertensão
Data nasc: 15/03/1982

Chave de decodificação (armazenada separadamente):
PAC-98765 → João Silva, CPF 123.456.789-00


### Quando usar cada técnica

| Cenário | Técnica recomendada |
|---------|---------------------|
| **Pesquisa científica** | Anonimização (se possível) ou pseudonimização |
| **Base de dados operacional** | Pseudonimização com acesso restrito |
| **Publicação de dados abertos** | Anonimização obrigatória |
| **Compartilhamento entre órgãos** | Anonimização ou pseudonimização com acordo |
| **Análise estatística interna** | Pseudonimização |

## 🎯 Aplicações no setor público

### Onde usar dados anonimizados

1. **Estatísticas públicas**
   - Censos demográficos (IBGE)
   - Indicadores de saúde (DATASUS)
   - Dados educacionais (Censo Escolar)
   - Estatísticas econômicas

2. **Pesquisas acadêmicas**
   - Estudos epidemiológicos
   - Análises socioeconômicas
   - Avaliação de políticas públicas
   - Pesquisas em ciências sociais

3. **Transparência ativa**
   - Dados abertos (dados.gov.br)
   - Portais de transparência
   - Prestação de contas
   - Controle social

4. **Desenvolvimento de políticas**
   - Planejamento urbano
   - Alocação de recursos
   - Identificação de necessidades
   - Avaliação de impacto

5. **Inovação e tecnologia**
   - Desenvolvimento de aplicativos cívicos
   - Hackathons de dados públicos
   - Soluções baseadas em evidências
   - Startups de impacto social

### Exemplos práticos detalhados

#### Exemplo 1: Dados de saúde (DATASUS)

Cenário: Hospital público quer compartilhar dados de internações para pesquisa

Antes (dados pessoais - NÃO COMPARTILHAR):
Paciente: Maria Oliveira, CPF 987.654.321-00
Internação: 10/05/2024, Hospital das Clínicas
Diagnóstico: Diabetes tipo 2, CID10 E11
Médico: Dr. Roberto Alves, CRM 12345
Endereço: Rua das Flores, 123, apto 45

Depois (dados anonimizados - PODE COMPARTILHAR):
ID anonimizado: PAC-98765
Internação: Maio/2024, Região Centro-Oeste
Diagnóstico: Doença crônica não transmissível
Faixa etária: 50-59 anos
Sexo: Feminino
[Médico e endereço removidos]

Cenário: Secretaria de Educação quer publicar dados de desempenho escolar

Antes (dados pessoais):
Aluno: João Pereira, matrícula 2023001234
Escola: EMEF Professor Silva, 5º ano
Notas: Matemática 8,5, Português 7,0
Nome da mãe: Ana Pereira
Endereço: Rua da Escola, 456

Depois (dados anonimizados):
Aluno: [anonimizado]
Escola: Escola pública municipal, 5º ano
Média da turma: 7,8
Taxa de aprovação: 92%
Distribuição de notas por faixa: 0-5: 8%, 5-7: 25%, 7-9: 45%, 9-10: 22%
[Dados individuais e endereço removidos]

Cenário: Prefeitura quer planejar melhorias no transporte público

Antes (dados individuais - bilhetagem eletrônica):
Usuário: Carlos Santos, CPF 456.789.123-00
Cartão: 1234-5678-9012-3456
Trajeto: 08:15 - Linha 101 (Casa → Trabalho)
17:45 - Linha 101 (Trabalho → Casa)
Recarga: R$ 50,00 em 05/05/2024

Depois (dados anonimizados - análise de fluxo):
Hora: 08:00-09:00, Linha 101, Sentido Bairro-Centro: 234 passageiros
Hora: 17:00-18:00, Linha 101, Sentido Centro-Bairro: 289 passageiros
Ponto mais movimentado: Terminal Central (1.234 embarques/dia)
Tempo médio de viagem: 45 minutos
[Dados individuais e forma de pagamento removidos]

Cenário: Ministério quer avaliar impacto do Bolsa Família

Antes (dados cadastrais):
Beneficiário: Maria da Silva, NIS 1234567890
Endereço: Rua Projetada, 789, Comunidade São João
Composição familiar: 4 pessoas (2 adultos, 2 crianças)
Renda declarada: R$ 350,00
Benefício: R$ 600,00

Depois (dados anonimizados para pesquisa):
Região: Nordeste, Zona urbana
Composição familiar média: 3,8 pessoas
Renda média declarada: R$ 380,00
Benefício médio: R$ 620,00
Perfil: 78% chefiado por mulheres
[Dados individuais e localização exata removidos]###
###

⚖️ Cuidados legais e riscos
Risco de reidentificação
Dados aparentemente anônimos podem permitir identificação quando combinados com outras bases.

Exemplos clássicos de reidentificação:

Estudo de Latanya Sweeney (2000)

87% da população americana pode ser identificada com (CEP + data de nascimento + sexo)

O então governador de Massachusetts foi identificado em dados "anônimos" de saúde

Netflix Prize (2006)

Pesquisadores reidentificaram usuários cruzando dados "anônimos" do Netflix com IMDb

Mesmo sem nomes, padrões de avaliação identificavam pessoas

Dados de táxi em Nova York (2014)

Dados de corridas foram reidentificados cruzando com fotos de paparazzi

Celebridades tiveram trajetos expostos

Fatores que aumentam risco de reidentificação
Fator	Descrição	Exemplo
Pouca generalização	Dados muito precisos	CEP completo, idade exata
Combinação de atributos	Vários campos juntos	Profissão + bairro + idade
Dados raros	Valores incomuns	Doença rara, profissão específica
Bases externas disponíveis	Outros dados públicos	Redes sociais, cadastros
Série temporal	Múltiplas medições	Histórico de localização
Boas práticas para evitar reidentificação
Avaliar risco residual

Considerar outras bases de dados disponíveis publicamente

Analisar combinações possíveis de atributos

Testar com amostra antes de publicar

Documentar processo

Técnica utilizada e parâmetros aplicados

Decisões sobre níveis de generalização

Riscos identificados e mitigados

Revisar periodicamente

Novas técnicas podem permitir reidentificação

Novas bases de dados podem ser publicadas

Atualizar anonimização conforme necessário

Adotar camadas de proteção

Combinar múltiplas técnicas

Quanto mais sensível o dado, mais proteção

Considerar acesso controlado mesmo para anonimizados

Termo de responsabilidade
Para acesso a dados anonimizados, considerar:

TERMO DE RESPONSABILIDADE PARA USO DE DADOS ANONIMIZADOS

O usuário declara que:
1. Não tentará reidentificar os titulares dos dados
2. Não cruzará os dados com outras bases para fins de identificação
3. Utilizará os dados apenas para a finalidade declarada
4. Comunicará imediatamente se identificar algum indivíduo acidentalmente
5. Responsabiliza-se por eventuais danos decorrentes de reidentificação

Ciência: __________________________
Data: ___/___/___

⬆ Voltar ao topo


Este arquivo está **completo e unificado**, com:
- ✅ Definição legal e conceitos
- ✅ Todas as técnicas de anonimização detalhadas
- ✅ Comparativo com pseudonimização
- ✅ Exemplos práticos no setor público
- ✅ Riscos e cuidados legais
- ✅ Processo passo a passo
- ✅ Checklist completo
- ✅ Exemplo prático detalhado
- ✅ Legislação e glossário
