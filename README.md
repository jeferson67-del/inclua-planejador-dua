# Inclua

Ferramenta web que gera planos de aula estruturados segundo o Desenho Universal para a Aprendizagem (DUA), usando *In-Context Learning* (ICL): planos de referência são inseridos no *prompt*, sem treinamento do modelo.

Desenvolvida como Trabalho de Conclusão de Curso da Licenciatura em Ciência da Computação da Universidade de Pernambuco (UPE), *Campus* Mata Norte.

**Ferramenta publicada:** https://inclua-planejador-dua-9jgukzejvqpvwgikxuq2gg.streamlit.app/

## Onde está cada coisa

| O quê | Onde |
|---|---|
| Exemplos de referência (os quatro planos usados no ICL) | `main.py`, variável `FEW_SHOT_EXAMPLES` |
| Seleção dos exemplos por perfil | `main.py`, função `selecionar_exemplos_icl` |
| Instruções do *prompt* (papel do modelo e formato de saída) | `main.py`, variáveis `INSTRUCOES_BASE` e `INSTRUCOES_SAIDA` |
| Montagem do *prompt* e envio ao modelo | `main.py`, funções `gerar_icl` e `LLM_Setup` |
| Cópia legível dos exemplos de referência | `Materiais do Inclua/Exemplos referência/` |
| Cenários usados na verificação | `Materiais do Inclua/Cenários pedagógicos/` |
| Planos gerados na verificação (nove planos) | `Materiais do Inclua/Plano de aulas/` |
| Script da verificação nos três modelos | `rodar_testes.py` |

Os exemplos ficam no próprio código: não há banco de dados separado. A cópia em `Materiais do Inclua` serve apenas para leitura; a versão usada pela ferramenta é a do `main.py`.

## Como executar a ferramenta

1. Instale as dependências: `pip install -r requirements.txt`
2. Crie um arquivo `.env` com a chave da API do Gemini: `GOOGLE_API_KEY=...`
3. Execute: `streamlit run main.py`

## Verificação descrita no TCC

Três cenários fictícios (TEA, TDAH e dislexia) foram submetidos a três modelos: Gemini 3.1 Flash-Lite (Google), gpt-oss-120b (via Groq) e GPT-4o mini (OpenAI). O script `rodar_testes.py` importa do `main.py` as mesmas funções de montagem do *prompt* e muda apenas o modelo, com temperatura 0. Foi feita uma geração por combinação, totalizando nove planos, em 16 de outubro de 2026.

Para repetir a verificação, além da `GOOGLE_API_KEY`, coloque no `.env` as chaves `GROQ_API_KEY` e `OPENAI_API_KEY`, instale `pip install langchain-groq langchain-openai` e execute `python rodar_testes.py`.

Os planos gerados exigem revisão do professor: a verificação avaliou a estrutura dos planos, não sua qualidade pedagógica.
