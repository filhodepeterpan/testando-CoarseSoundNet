# Testando o CoarseSoundNet

## Introdução
Estou desenvolvendo uma pesquisa

## Dicionário de Arquivos de Áudio

- **A01.wav** - Chuva (Geofonia)
- **A02.wav** - Sanhaço-cinzento (Biofonia) e cachorro **doméstico** latindo ao fundo (Antropofonia)
- **A03.wav** - Tapicuru (Biofonia)
- **A04.wav** - Pneu (Antropofonia)
- **A05.wav** - Ventania (Geofonia)
- **A06.wav** - Mar (Geofonia)
- **A07.wav** - Morcego (Biofonia)
- **A08.wav** - Fritura (Antropofonia)
- **A09.wav** - Trecho de música (Antropofonia)

## Dependências
**Criação do ambiente virtual**
```
py -3.12 -m venv .venv
```

**Ativação do ambiente virtual**
```
.venv\Scripts\activate
```

**Instalação de Dependências**
```
pip install "autrainer==0.6.0" "auglib>=1.0.4" "cowsay>=6.1" "hear21passt>=0.0.26" "pydub>=0.25.1"
```

## Código de Inferência

```
autrainer inference hf:HearTheSpecies/CoarseSoundNet -r data output -w 5 -s 5 -sr 48000 --trust-remote
```

## Resultados
- **A01.wav** - ACERTOU. Maioria: Geofonia. Antropofonia apareceu como falso positivo nos primeiros 10 s.
- **A02.wav** - ACERTOU. Detectou Biofonia e Antropofonia, mas também Geofonia (falso positivo). Apenas 1 janela de 5 s analisada.
- **A03.wav** - ACERTOU. Biofonia em todas as janelas; Geofonia extra (falso positivo) a partir de ~40 s.
- **A04.wav** - INCERTO. Retornou as três classes na única janela analisada, sem distinguir a Antropofonia.
- **A05.wav** - ACERTOU. Geofonia em todas as janelas; Antropofonia extra (falso positivo) até ~25 s.
- **A06.wav** - ACERTOU. Apenas Geofonia, em todas as janelas.
- **A07.wav** - ERROU. Maioria: Geofonia. Biofonia só na primeira janela (0-5 s).
- **A08.wav** - ERROU. Maioria: Geofonia. Antropofonia só na janela de 5-10 s.
- **A09.wav** - ACERTOU. Maioria: Antropofonia, com Geofonia extra (falso positivo). Biofonia pontual em duas janelas.

> Janelas `.nan` no `results.yaml` indicam trechos sem áudio (arquivo mais curto que 90 s).

## Créditos
Abaixo, credito os desenvolvedores do CourseSoundNet, aplicando a licença e direitos autorais, além da referenciação do artigo original do projeto.

**Repositório do modelo**
```
https://github.com/CHI-TUM/CoarseSoundNet
```

**Artigo**
```
@article{Gebhard26-CBA,
  title = {CoarseSoundNet: Building a reliable model for ecological soundscape analysis},
  journal = {Ecological Informatics},
  volume = {99},
  pages = {104101},
  year = {2026},
  issn = {1574-9541},
  doi = {https://doi.org/10.1016/j.ecoinf.2026.104101},
  author = {Alexander Gebhard and Andreas Triantafyllopoulos and Dominik Arend and Sandra Müller and Svenja Schmidt and Michael Scherer-Lorenzen and Björn W. Schuller}
}
```

## Licença MIT
```
Copyright (c) 2026 Chair of Health Informatics (TUM)

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