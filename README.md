# Sentimento — Brasil x Croácia (31/03/2026)

Análise da reação da torcida na transmissão da GE TV (YouTube) durante o amistoso da Seleção Brasileira. **102 020 mensagens** classificadas, agregadas em janelas de 30s, cruzadas com os eventos do jogo.

[**Ver análise completa →**](./index.html)

## Pipeline

1. **Coleta** — `yt-dlp` baixou o `live_chat.json` do replay da live e foi convertido para JSONL.
2. **Enriquecimento** — classificador local **Qwen2.5 7B Instruct Q4_K_M** rodando em llama.cpp (Vulkan, RTX 4070 Ti SUPER) classificou cada mensagem em polaridade (pos/neg/neu) e emoção (alegria/euforia/raiva/decepção/ansiedade/ironia/neutro). ~86 min, 19.5 msgs/s.
3. **Agregação** — janelas deslizantes de 30s com volume, distribuição de polaridade/emoção, samples representativas e casamento com eventos do CSV.
4. **Visualização** — Streamlit (interativo) ou Plotly HTML estático (este site).

 
