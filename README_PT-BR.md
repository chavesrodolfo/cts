# Complete Trading Setup (CTS) - Indicador Pine Script

## 📊 Visão Geral

O Complete Trading Setup é um sistema avançado multi-indicador projetado para análise abrangente de mercado. Este indicador Pine Script combina múltiplas ferramentas de análise técnica para fornecer um setup completo de trading para swing trading e position trading em timeframes diários, com particular eficácia em mercados de criptomoedas e forex.

## 🎯 Principais Funcionalidades

### 1. **Médias Móveis Exponenciais (EMAs)**
- **EMA 7** (Verde): Identificação de tendência de curto prazo
- **EMA 21** (Amarela): Sinais de swing trading de médio prazo
- **EMA 50** (Azul): Confirmação de tendência intermediária
- **EMA 100** (Branca): Análise de tendência de longo prazo
- **EMA 200** (Roxa): Linha de tendência principal - suporte/resistência chave

### 2. **Bandas de Bollinger**
- Suporte/resistência dinâmicos baseados na volatilidade do preço
- Bandas superior/inferior mostram zonas de potencial reversão
- Linha central (SMA 20) atua como linha de tendência dinâmica
- Multiplicador de desvio padrão: 2.0 (95% da ação do preço)

### 3. **Bull Market Support Band (BMSB)**
- **SMA 20 Semanal** (Vermelho) e **EMA 21 Semanal** (Verde)
- Zona de suporte crítica em mercados altistas
- Preço se mantendo acima do BMSB indica forte momentum altista
- Essencial para identificar mudanças de tendência principal

### 4. **Zonas Simples de Liquidez**
- **4 linhas horizontais** marcando **3 zonas de liquidez**:
  - **Zona Superior** (Vermelha): Área de resistência forte
  - **Zona Atual** (Laranja): Área de consolidação do preço
  - **Zona Inferior** (Verde): Área de suporte forte
- Ajusta-se dinamicamente ao preço atual
- Distância configurável entre zonas (padrão: 2.5%)

### 5. **Sinais de Trading**
- **Golden Cross**: EMA 50 cruza acima da EMA 200 (altista)
- **Death Cross**: EMA 50 cruza abaixo da EMA 200 (baixista)
- **Strong Buy**: Confluência de múltiplas condições para entradas longas de alta probabilidade
- **Strong Sell**: Confluência de múltiplas condições para entradas curtas de alta probabilidade

### 6. **Tabela de Dados em Tempo Real**
- Valores atuais de todas as EMAs e limite superior das Bandas de Bollinger
- Posicionada no canto superior direito para fácil referência
- Atualiza em tempo real com dados de mercado

## ⚙️ Parâmetros de Configuração

### Bandas de Bollinger
- **BB Length**: Período para cálculo (padrão: 20)
- **BB Multiplier**: Multiplicador de desvio padrão (padrão: 2.0)

### Médias Móveis
- **EMA 7 Length**: Período da EMA rápida (padrão: 7)
- **EMA 21 Length**: Período da EMA média (padrão: 21)
- **EMA 50 Length**: Período da EMA intermediária (padrão: 50)
- **EMA 100 Length**: Período da EMA de longo prazo (padrão: 100)
- **EMA 200 Length**: Período da EMA de tendência principal (padrão: 200)

### Bull Market Support Band
- **BMSB SMA Length**: Período da SMA semanal (padrão: 20)
- **BMSB EMA Length**: Período da EMA semanal (padrão: 21)
- **BMSB Timeframe**: Timeframe de análise (padrão: Semanal)

### Zonas de Liquidez
- **Show Liquidity Zones**: Ativar/desativar exibição das zonas (padrão: true)
- **Zone Distance %**: Distância inicial entre zonas (padrão: 8.0%, faixa: 6.0-25.0%)
- **Pivot Lookback**: Período para encontrar pontos de pivô (padrão: 20)

**Importante**: O sistema **automaticamente força** o intervalo total das zonas entre 6% e 25%:
- Se intervalo calculado > 25%: **Comprime zonas proporcionalmente** para exatamente 25%
- Se intervalo calculado < 6%: **Expande zonas proporcionalmente** para exatamente 6%
- Mantém o preço central como ponto de referência para ajustes
- A etiqueta de percentual sempre exibe o intervalo final ajustado

### Cores
- Cores totalmente customizáveis para todas as linhas EMA
- Esquema de cores padrão otimizado para temas escuros

## 📈 Diretrizes de Estratégia de Trading

### Condições do Sinal Strong Buy
1. Preço acima da EMA 7
2. Alinhamento das EMAs: EMA 7 > EMA 21 > EMA 50
3. Preço acima da linha central das Bandas de Bollinger
4. Preço acima do Bull Market Support Band
5. Cruzamento do preço acima da EMA 21
6. Confirmação de volume (1.5x da média)

### Condições do Sinal Strong Sell
1. Preço abaixo da EMA 7
2. Alinhamento baixista das EMAs: EMA 7 < EMA 21 < EMA 50
3. Preço abaixo da linha central das Bandas de Bollinger
4. Cruzamento do preço abaixo da EMA 21
5. Rejeição da banda superior BB ou preço abaixo da banda inferior BB
6. Confirmação de volume (1.2x da média)

### Uso das Zonas de Liquidez
- **Zona Superior** (Vermelha): Buscar resistência e potenciais entradas vendidas
- **Zona Atual** (Laranja): Área de consolidação - aguardar rompimento
- **Zona Inferior** (Verde): Buscar suporte e potenciais entradas compradas

### Regras para Cenários Complexos

#### Lógica de Ajuste Automático das Zonas
1. **Cálculo Inicial**: Usa o parâmetro Zone Distance % para criar 4 linhas (3 zonas)
2. **Integração de Pivôs**: Ajusta para máximas/mínimas de pivô próximas se dentro da distância da zona
3. **Validação de Intervalo**: Calcula o percentual total do intervalo da zona mais alta à mais baixa
4. **Imposição Automática**:
   - **Cenário Acima de 25%**: Comprime todas as zonas proporcionalmente ao redor do preço central
   - **Cenário Abaixo de 6%**: Expande todas as zonas proporcionalmente ao redor do preço central
   - **Intervalo Válido (6-25%)**: Usa as zonas calculadas como estão

#### Comportamento da Bull Market Support Band (BMSB)
- **Linhas Suaves**: Usa `barmerge.gaps_on` e `barmerge.lookahead_off` para renderização limpa
- **Dados Semanais**: Busca SMA 20S e EMA 21S do timeframe semanal
- **Confirmação de Tendência**: Preço acima do BMSB indica forte suporte de mercado altista
- **Multi-timeframe**: Funciona em qualquer timeframe do gráfico usando dados semanais

#### Confluência de Sinais de Trading
- **Strong Buy**: Requer TODAS as condições: posição do preço, alinhamento das EMAs, suporte BMSB, confirmação de volume
- **Strong Sell**: Requer TODAS as condições: alinhamento baixista, rejeição BB, confirmação de volume
- **Golden/Death Cross**: Cruzamentos EMA 50 vs EMA 200 para mudanças de tendência principal

## 🚨 Condições de Alerta

O indicador inclui alertas automatizados para:
- Golden Cross (EMA 50 > EMA 200)
- Death Cross (EMA 50 < EMA 200)
- Rompimentos das Bandas de Bollinger (superior/inferior)
- Disparo de sinais Strong Buy
- Disparo de sinais Strong Sell

## 🔧 Instalação

1. Abra o TradingView e vá para o Pine Editor
2. Copie o código completo do Pine Script
3. Cole no Pine Editor
4. Clique em "Adicionar ao Gráfico"
5. Configure os parâmetros conforme necessário

## 📋 Melhores Práticas

### Timeframes
- **Principal**: Gráficos diários para swing trading
- **Confirmação**: Gráficos de 4H para timing de entrada
- **Semanal**: Para análise de tendência principal

### Gerenciamento de Risco
- Use zonas de liquidez para posicionamento de stop-loss
- Confirme sinais com múltiplos timeframes
- Considere confirmação de volume para todas as entradas
- Respeite a direção da tendência principal (alinhamento das EMAs)

### Condições de Mercado
- **Mercado Altista**: Foque no suporte das EMAs e BMSB
- **Mercado Baixista**: Observe níveis de resistência das EMAs
- **Lateral**: Use Bandas de Bollinger para trading de range

## 🎨 Elementos Visuais

### Estilos de Linha
- **Linhas sólidas**: Suporte/resistência principal (zonas de liquidez)
- **Linhas tracejadas**: Níveis secundários e divisões de zona
- **Linhas grossas**: EMAs primárias
- **Linhas finas**: Bandas de Bollinger

### Codificação de Cores
- **Vermelho**: Resistência, sinais baixistas, liquidez superior
- **Verde**: Suporte, sinais altistas, liquidez inferior
- **Laranja**: Zonas neutras, área do preço atual
- **Azul**: Bandas de Bollinger
- **Personalizado**: Cores das EMAs (configurável)

## 📊 Notas de Performance

- Otimizado para Pine Script v6
- Cálculos eficientes para uso em tempo real
- Repintura mínima (zonas atualizam apenas na última barra)
- Compatível com todos os planos do TradingView
- Funciona em todos os timeframes (otimizado para diário)
- **Gerenciamento Inteligente de Zonas**: Desenha apenas zonas de liquidez atuais para evitar poluição do gráfico
- **Validação em Tempo Real**: Restrições de percentual aplicadas automaticamente a cada barra

## ⚠️ Aviso Legal

Este indicador é apenas para fins educacionais e informativos. Não deve ser considerado como aconselhamento financeiro. Sempre conduza sua própria pesquisa e considere sua tolerância ao risco antes de tomar decisões de trading. Performance passada não garante resultados futuros.

## 🔄 Histórico de Versões

- **v1.0**: Lançamento inicial com todas as funcionalidades principais
- Compatível com Pine Script v6
- Sistema de zonas de liquidez com imposição automática de limites 6-25%
- Bull Market Support Band com linhas suaves
- Tratamento de erros aprimorado
- Gerenciamento inteligente de zonas para evitar poluição visual

## 🤝 Suporte

Para dúvidas, sugestões ou problemas:
- Revise os parâmetros de configuração
- Teste em diferentes timeframes
- Ajuste as configurações de sensibilidade conforme necessário

---

**Bons Trades! 📈**