# Snetimento — Brasil x Croácia (31/03/2026)

Análise da reação da torcida na transmissão da GE TV (YouTube) durante o amistoso da Seleção Brasileira. **102 020 mensagens** classificadas, agregadas em janelas de 30s, cruzadas com os eventos do jogo.

[**Ver análise completa →**](./index.html)

## Pipeline

1. **Coleta** — `yt-dlp` baixou o `live_chat.json` do replay da live e foi convertido para JSONL.
2. **Enriquecimento** — classificador local **Qwen2.5 7B Instruct Q4_K_M** rodando em llama.cpp (Vulkan, RTX 4070 Ti SUPER) classificou cada mensagem em polaridade (pos/neg/neu) e emoção (alegria/euforia/raiva/decepção/ansiedade/ironia/neutro). ~86 min, 19.5 msgs/s.
3. **Agregação** — janelas deslizantes de 30s com volume, distribuição de polaridade/emoção, samples representativas e casamento com eventos do CSV.
4. **Visualização** — Streamlit (interativo) ou Plotly HTML estático (este site).

Acurácia validada contra ground truth manual de 240 mensagens reais: ~75% polaridade, ~62% emoção (out-of-sample).

## Achados principais

- **Torcida da Seleção é exigente**: 44% neg, 32% pos, 24% neu. Decepção (22%) e ironia (12%) dominam o lado negativo.
- **Maior pico de volume foi *antes* do gol oficial do Danilo** — corresponde à JOGADA (Vini cruzando) que gerou debate ("Vini é mt ruim" vs "admito Vini ta melhor"), não à comemoração em si.
- **Pico mais positivo** (78% pos): 21:50 BRT — comemoração imediata do gol do Danilo com "TAPEEEGA", "vamooo", emojis de bola amarela.
- **Pós-jogo**: predominam crítica e ironia ("não convocou o Neymar", "Bento não pode ser titular", "Endrick fora?").

## Limitações

- Modelo classificou mensagens curtas com ambiguidade (palavras soltas, gírias internas) como neutro mais do que o ideal.
- Stream do YouTube tem latência variável (~15-60s); marquei eventos pelo timestamp da transmissão na live, não do relógio oficial.
