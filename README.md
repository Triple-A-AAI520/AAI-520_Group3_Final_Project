# Multi-Agent Financial Analysis System

This project is a part of the AAI-520: NLP and GenAI course in the Applied Artificial Intelligence Program at the University of San Diego (USD).

**Project Status:** Active
---

## Installation

**Quick start**

```bash
# Install Python dependencies
pip install -r requirements.txt

# Download spaCy English model
python -m spacy download en_core_web_sm
```
---

## Project Intro/Objective

This project implements a **notebook‑driven, multi‑agent financial analysis workflow** for AAI‑520 (NLP & GenAI). Given a stock ticker, the system:
- pulls **market data** (30‑day history and simple trend features),
- fetches **recent news** from trusted sources,
- applies light **NLP (spaCy NER)** to assist routing and extraction,
- and uses an **LLM** to compose a concise, structured research summary with basic evidence and a quick chart.

The goal is to provide a compact, reproducible example of **agentic orchestration** over heterogeneous signals (prices, news, light NLP) suitable for exploration and extension.

---

## Contributors

- Ashley Moore  
- Quang Tran  
- Alyona Kosobokova  

---

## Methods Used

- Natural Language Processing (spaCy NER)  
- Retrieval & Summarization (news intake → LLM synthesis)  
- Basic Time‑Series Feature Engineering (SMA/price trend)  
- Lightweight Agentic Orchestration (plan → route → analyze → evaluate → assemble)  
- Data Visualization (matplotlib)  

---

## Technologies

- **Python 3.10+**
- **Key libraries**: `yfinance`, `requests`, `gnews`, `langchain`, `spacy`, `matplotlib`, `streamlit`
- **Jupyter / IPython** for notebook execution & display helpers  

---

## Imports Used in the Notebook

```python
import re, os, requests, json, yfinance as yf
from datetime import datetime, timedelta
from getpass import getpass
from langchain.llms.base import LLM
import matplotlib.pyplot as plt
from langchain.agents import initialize_agent, Tool, AgentType
from gnews import GNews
import spacy
import os, requests
from getpass import getpass
from langchain.llms.base import LLM
import math
import streamlit as st
from IPython.display import display, Markdown, HTML
from textwrap import dedent
```
---

## Project Description

**Pipeline (notebook‑driven):**
1. **Plan** tasks & prompts for the chosen ticker.  
2. **Fetch** market data with `yfinance` (last 30 days) & compute simple trend signals.  
3. **Collect** recent news for the ticker (curated to trusted outlets; recent window).  
4. **Route & Extract** entities/key facts (spaCy NER) for targeted prompts.  
5. **Analyze** with an LLM: concise synthesis + sanity checks.  
6. **Assemble** final JSON/markdown report and **visualize** the price trend.

**Running the notebook:** execute cells top‑to‑bottom, set `GOOGLE_API_KEY` for LLM access, and call the agent on a ticker (e.g., `MSFT`, `NVDA`, `TSLA`, `MDT`).

---

## License

MIT License

Copyright (c) 2023 p-parks

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

---

## Acknowledgments

- **USD Applied Artificial Intelligence Program**
- With gratitude to **Professor Mirsardar Esmaeili** for guidance and feedback in AAI-520 (NLP & GenAI).  
- **AAI‑520: NLP and GenAI** faculty & classmates
- Group 6: **Ashley Moore, Quang Tran, and Alyona Kosobokova**
- Open‑source maintainers of `yfinance`, `gnews`, `spaCy`, `LangChain`, `matplotlib`  
