# Projeto P1 — Do texto à decisão: sentimento e temas nas avaliações da Americanas

Projeto Integrado: Redes Sociais e Marketing · CDIA · PUC-SP · 2026.2 · Prof. Dr. Rooney R. A. Coelho

Pipeline completo de Processamento de Linguagem Natural aplicado à base B2W-Reviews01:
auditoria da base, limpeza do texto, representação (TF-IDF e Word2Vec), classificação de sentimento
com medição honesta, temas sem rótulo (NMF) e recomendações para o negócio.

## Equipe e divisão do trabalho

| # | Nome completo | RA | Responsável por |
|---|---|---|---|
| 1 | Dinis Maria Moura Lopes Barros Guereiro | RA00380070 | Notebook 01 — auditoria da base e decisão do rótulo (`01_auditoria.ipynb`) |
| 2 | Allan Yugi Miyazaki Silva | RA00361500 | Notebook 02 — pré-processamento, representação e classificação (`02_sentimento.ipynb`) |
| 3 | Lucas Ambra | RA00347011 | Notebook 03 — temas sem rótulo e recomendações (`03_temas.ipynb`) |
| 4 | Enzo Kato | RA00348190 | Relatório técnico (`relatorio.pdf`) |
| 5 | Arthur Navarrete da Silva Goes Mourad | RA00346746 | Apresentação em slides (`apresentacao.pptx`) |

## Estrutura da entrega

```
equipe-N-p1/
├── README.md              ← este ficheiro
├── 01_auditoria.ipynb     ← auditoria, as quatro perguntas, decisão do rótulo e baseline
├── 02_sentimento.ipynb    ← secções 3.2 (pré-processamento), 3.3 (representação) e 3.4 (classificação)
├── 03_temas.ipynb         ← secções 3.5 (temas sem rótulo) e 3.6 (recomendações e limites)
├── relatorio.pdf          ← relatório técnico (7 páginas)
└── apresentacao.pptx      ← slides da apresentação (12 minutos, roteiro nas notas do apresentador)
```

A base **não vai no zip**: cada notebook descarrega-a do repositório oficial pela URL raw.

## Instruções de execução

### Opção 1 — Google Colab (recomendada)

1. Abrir o Colab em <https://colab.research.google.com> e fazer **Ficheiro → Carregar notebook** com `01_auditoria.ipynb`.
2. Executar **Ambiente de execução → Reiniciar e executar tudo** (*Restart & Run All*).
3. Repetir os passos 1 e 2 com `02_sentimento.ipynb` e depois com `03_temas.ipynb`.

Cada notebook corre sozinho do zero: carrega a base, aplica as decisões dos notebooks anteriores e não depende de
ficheiros gravados por outro notebook. A ordem 01 → 02 → 03 é a ordem lógica de leitura, mas não é obrigatória.
O notebook 02 instala o `gensim` na própria célula `[C02.08]` (`!pip install gensim`); as stop words e o stemmer
RSLP do NLTK são descarregados dentro das células `[C02.04]` e `[C03.02]`.

### Opção 2 — ambiente local

Requer Python 3.10 ou superior e ligação à internet (para descarregar a base e os recursos do NLTK).

```bash
python -m venv venv
source venv/bin/activate            # no Windows: venv\Scripts\activate
pip install pandas numpy scipy scikit-learn gensim nltk matplotlib jupyter
jupyter notebook
```

Abrir cada notebook e executar **Kernel → Restart & Run All**. Num ambiente local, a célula `!pip install gensim`
pode ser ignorada se o `gensim` já estiver instalado.

Versões com que os números do relatório foram conferidos: Python 3.13, pandas 2.2, numpy 2.1, scipy 1.16,
scikit-learn 1.6.1, gensim 4.4.0.

### Tempo de execução aproximado

| Notebook | Tempo | Observação |
|---|---|---|
| 01_auditoria | ~1 min | inclui o download da base (~50 MB) |
| 02_sentimento | ~1–2 min | amostra estratificada de 40.000 avaliações; o Word2Vec é treinado três vezes |
| 03_temas | ~1–2 min | base inteira sem duplicados (126.721 avaliações); vários NMF |

### Reprodutibilidade

- Semente fixa `SEED = 42` em todas as divisões, amostras, modelos e sorteios de exemplos.
- Word2Vec com `seed=42` e `workers=1`. A célula `[C02.11]` treina também com `workers=4` de propósito, para mostrar
  que o resultado muda; os valores dessa comparação variam a cada execução.
- Cada célula de código começa com uma etiqueta `[C0N.MM]` (N = notebook, MM = ordem da célula de código).
  Todo número do relatório e dos slides cita a etiqueta da célula que o produziu.

## Base de dados e licença

- **B2W-Reviews01** — 132.373 avaliações da Americanas.com, 01/01 a 31/05/2018.
  Repositório oficial: <https://github.com/americanas-tech/b2w-reviews01> (ficheiro `B2W-Reviews01.csv`, carregado
  pela URL raw `https://raw.githubusercontent.com/americanas-tech/b2w-reviews01/main/B2W-Reviews01.csv`).
- Licença **Creative Commons BY-NC-SA 4.0** — uso não comercial, com atribuição obrigatória.
- Citação: Real, L.; Oshiro, M.; Mafra, A. “B2W-Reviews01: an open product reviews corpus”. STIL — Symposium in
  Information and Human Language Technology, 2019.
- O `reviewer_id` já vem pseudonimizado. Gênero, estado e idade do avaliador só foram usados em análise agregada;
  não houve qualquer tentativa de reidentificação nem cruzamento com outras fontes.

## Uso de IA generativa

A equipe usou o Claude (Anthropic) como ferramenta de apoio para escrever e rever código dos notebooks 02 e 03,
sugerir a estrutura dos testes e redigir rascunhos de texto do relatório e dos slides. As decisões de projeto,
a leitura das avaliações e os nomes dos temas foram verificados pela equipe, e os números foram conferidos contra
as saídas das células indicadas.
