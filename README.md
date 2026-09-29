# FarmTech Solutions — Fase 6
## Redes Neurais e Visão Computacional

Projeto acadêmico desenvolvido para a **Fase 6 da FIAP**, com foco em **Visão Computacional, Redes Neurais, YOLO e Deep Learning**.

O projeto trabalha com duas classes:

- `garrafa`
- `caneca`

A solução inclui as entregas obrigatórias e o **Ir Além 2**, contemplando:

- YOLO customizada;
- comparação entre treinamentos com 30 e 60 épocas;
- validação e teste da YOLO;
- YOLO padrão/pré-treinada;
- CNN criada do zero;
- Transfer Learning com MobileNetV2;
- Fine Tuning;
- segmentação automática;
- remoção do background;
- nova classificação das imagens segmentadas;
- comparação crítica entre as abordagens.

---

## Integrantes

- João Vitor Justino — RM572969
- Thiese Novaes — RM572659
- Talles Duran — RM572772
- Kevin Santiago — RM573808
- Renan Souza — RM568958

---

## Objetivo

O objetivo é demonstrar, na prática, diferentes abordagens de Visão Computacional para identificar **garrafas e canecas**.

O projeto compara duas tarefas diferentes:

### Detecção de objetos
Realizada com YOLO.

Além de classificar o objeto, a YOLO também localiza o objeto na imagem por meio de uma **bounding box**.

### Classificação de imagens
Realizada com CNN, Transfer Learning e Fine Tuning.

Nesse caso, o modelo recebe a imagem e decide se ela pertence à classe `caneca` ou `garrafa`.

> Por isso, métricas como `mAP` da YOLO não devem ser comparadas diretamente com `accuracy` da CNN.

---

# Entregas do projeto

## Entrega 1 — YOLO customizada

Foram utilizadas duas classes com 40 imagens cada, totalizando 80 imagens.

Divisão por classe:

| Conjunto | Imagens por classe | Total |
|---|---:|---:|
| Treino | 32 | 64 |
| Validação | 4 | 8 |
| Teste | 4 | 8 |
| Total | 40 | 80 |

Foram realizados dois treinamentos:

- 30 épocas;
- 60 épocas.

Os experimentos foram comparados usando principalmente:

- Precision;
- Recall;
- mAP@0.5;
- mAP@0.5:0.95;
- tempo de treinamento;
- análise visual das detecções.

O treinamento com **60 épocas** apresentou o melhor desempenho nos experimentos realizados.

---

## Entrega 2 — comparação de abordagens

A segunda parte compara:

1. YOLO customizada;
2. YOLO padrão/pré-treinada;
3. CNN criada do zero.

A YOLO padrão utiliza as classes originais do dataset COCO, enquanto a YOLO customizada foi treinada especificamente para:

```text
0 = garrafa
1 = caneca
```

A CNN realiza classificação da imagem inteira e foi avaliada com:

- Accuracy;
- Precision;
- Recall;
- F1-score;
- matriz de confusão;
- curvas de treinamento e validação.

---

## Ir Além 2

O Ir Além 2 adiciona técnicas de Deep Learning mais avançadas.

### Transfer Learning

Foi utilizada a **MobileNetV2**, com pesos pré-treinados na ImageNet.

A base convolucional é inicialmente congelada e somente as novas camadas de classificação são treinadas.

### Fine Tuning

Após o Transfer Learning, parte das últimas camadas da MobileNetV2 é liberada para ajustes usando uma taxa de aprendizado menor.

As camadas `BatchNormalization` permanecem congeladas para aumentar a estabilidade com o dataset pequeno.

### Segmentação automática

Também é investigada a hipótese:

> Remover o background e fornecer ao classificador somente os pixels relevantes do objeto melhora a classificação?

O fluxo é:

```text
Imagem original
      ↓
Segmentação automática
      ↓
Máscara
      ↓
Remoção do background
      ↓
Classificador
      ↓
Comparação das métricas
```

---

# Estrutura do projeto

Estrutura recomendada:

```text
ML_IMAGENS/
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebook/
│   ├── FIAP_FASE6_ENTREGA_PRINCIPAL_SEM_IR_ALEM.ipynb
│   ├── IR_ALEM_2_FASE6.ipynb
|   ├── figura_autoral_ir_alem_2.png
│   │
│   ├── dataset/
│   │   ├── train/
│   │   │   ├── caneca/
│   │   │   └── garrafa/
│   │   ├── validation/
│   │   │   ├── caneca/
│   │   │   └── garrafa/
│   │   └── test/
│   │       ├── caneca/
│   │       └── garrafa/
│   │
│   ├── dataset_yolo/
│   │   ├── images/
│   │   │   ├── train/
│   │   │   ├── val/
│   │   │   └── test/
│   │   └── labels/
│   │       ├── train/
│   │       ├── val/
│   │       └── test/
│   │
│   └── yolov5/
│
└── assets/
    ├── yolo/
    ├── cnn/
    ├── segmentacao/
    └── graficos/
```

---

# Tecnologias utilizadas

Principais bibliotecas e ferramentas:

- Python
- Jupyter Notebook
- TensorFlow / Keras
- PyTorch
- YOLOv5
- Ultralytics
- OpenCV
- NumPy
- Pandas
- Matplotlib
- scikit-learn
- PyYAML
- MobileNetV2
- SAM / segmentação automática

O ambiente usado durante o desenvolvimento utilizou **Python 3.13.2**.

O treinamento foi executado principalmente em **CPU**, sem CUDA disponível.

---

# Instalação

## 1. Clonar o repositório

```bash
git clone URL_DO_REPOSITORIO
cd NOME_DO_REPOSITORIO
```

---

## 2. Criar um ambiente virtual

### Linux / macOS

```bash
python3 -m venv venv
source venv/bin/activate
```

### Windows — PowerShell

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

### Windows — CMD

```cmd
python -m venv venv
venv\Scripts\activate
```

---

## 3. Atualizar o pip

```bash
python -m pip install --upgrade pip
```

---

## 4. Instalar as dependências

Se o projeto possuir `requirements.txt`:

```bash
pip install -r requirements.txt
```

Principais dependências usadas pelo projeto:

```text
jupyter
tensorflow
torch
torchvision
numpy
pandas
matplotlib
opencv-python
scikit-learn
PyYAML
ultralytics
pillow
```

Caso seja necessário instalar somente o conjunto principal:

```bash
pip install jupyter tensorflow torch torchvision numpy pandas matplotlib opencv-python scikit-learn PyYAML ultralytics pillow
```

---

# Instalação da YOLOv5

A pasta `yolov5/` não precisa ser versionada no repositório.

Clone o projeto oficial dentro da pasta `notebook/`:

```bash
cd notebook

git clone https://github.com/ultralytics/yolov5.git
cd yolov5

pip install -r requirements.txt

cd ..
```

Depois disso, a estrutura deve conter:

```text
notebook/
├── yolov5/
├── dataset/
├── dataset_yolo/
└── notebooks...
```

---

# Dataset

O dataset não precisa ser armazenado diretamente no GitHub caso seja pesado.

O notebook espera esta estrutura:

```text
notebook/dataset/
├── train/
│   ├── caneca/
│   └── garrafa/
├── validation/
│   ├── caneca/
│   └── garrafa/
└── test/
    ├── caneca/
    └── garrafa/
```

Para YOLO:

```text
notebook/dataset_yolo/
├── images/
│   ├── train/
│   ├── val/
│   └── test/
└── labels/
    ├── train/
    ├── val/
    └── test/
```

---

# Formato dos labels YOLO

Cada imagem precisa possuir um arquivo `.txt` de mesmo nome.

Exemplo:

```text
images/train/garrafa1.jpg
labels/train/garrafa1.txt
```

Formato:

```text
classe x_centro y_centro largura altura
```

Exemplo:

```text
0 0.512500 0.481250 0.300000 0.700000
```

Classes:

```text
0 = garrafa
1 = caneca
```

As coordenadas devem estar normalizadas entre `0` e `1`.

---

# Como executar

## Notebook principal

Abra:

```text
notebook/FIAP_FASE6_ENTREGA_PRINCIPAL_SEM_IR_ALEM.ipynb
```

Execute as células **na ordem**.

Esse notebook contém:

- conferência do dataset;
- YOLO customizada;
- treino de 30 épocas;
- treino de 60 épocas;
- comparação das métricas;
- validação e teste;
- YOLO padrão;
- CNN do zero;
- análise crítica.

---

## Notebook Ir Além 2

Abra:

```text
notebook/IR_ALEM_2_FASE6.ipynb
```

Esse notebook contém:

- Transfer Learning;
- MobileNetV2;
- Fine Tuning;
- segmentação;
- remoção do background;
- reclassificação;
- comparação final.

> Se o kernel do Jupyter for reiniciado, execute novamente as células desde o início para recriar variáveis como `history_transfer`, `history_fine`, modelos e datasets.

---

# Rodando o Jupyter

Na raiz do projeto:

```bash
jupyter notebook
```

ou:

```bash
jupyter lab
```

Depois abra a pasta `notebook/`.

No VS Code também é possível abrir diretamente os arquivos `.ipynb`, desde que a extensão Jupyter esteja instalada.

---

# Execução em CPU

O projeto foi ajustado para funcionar sem GPU.

Configuração utilizada na YOLO customizada:

```text
modelo: yolov5n.pt
imagem: 320 × 320
batch: 2
workers: 0
device: cpu
```

Essa configuração reduz:

- consumo de RAM;
- carga de CPU;
- risco de travamento;
- tempo de treinamento.

Avisos como:

```text
Could not find cuda drivers
GPU will not be used
```

não representam erro quando o projeto está sendo executado intencionalmente em CPU.

---

# Resultados observados

## YOLO customizada

Nos experimentos executados:

| Experimento | Melhor mAP@0.5:0.95 | Tempo aproximado |
|---|---:|---:|
| 30 épocas | 0.24349 | 110.44 s |
| 60 épocas | 0.59187 | 204.21 s |

No conjunto de teste, o modelo de 60 épocas apresentou melhora relevante em relação ao modelo de 30 épocas.

---

## CNN do zero

Resultados observados no conjunto de teste:

```text
Accuracy : 0.625
Precision: 0.6667
Recall   : 0.5000
F1-score : 0.5714
```

A CNN apresentou sinais de overfitting, reforçando a importância das abordagens de Transfer Learning e Fine Tuning para um dataset pequeno.

---

# Resultados e imagens no GitHub

Em vez de subir todas as pastas `runs/`, recomenda-se copiar apenas os resultados importantes para `assets/`.

Exemplo:

```text
assets/
├── yolo/
│   ├── comparacao_precision.png
│   ├── comparacao_recall.png
│   ├── comparacao_map50.png
│   ├── comparacao_map5095.png
│   └── deteccoes/
│
├── cnn/
│   ├── accuracy.png
│   ├── loss.png
│   └── matriz_confusao.png
│
└── segmentacao/
    ├── original.png
    ├── mascara.png
    └── background_removido.png
```

Assim, o repositório permanece leve e ainda apresenta evidências visuais dos resultados.

---

# O que deve subir para o GitHub

Recomendado:

```text
README.md
requirements.txt
.gitignore
notebook/*.ipynb
assets/
fase6_data.yaml          # opcional, se não possuir caminhos absolutos
```

Também podem ser incluídos:

- tabelas `.csv` pequenas;
- imagens de gráficos;
- matrizes de confusão;
- exemplos de detecção;
- imagens de segmentação;
- documentação adicional.

---

# O que NÃO deve subir para o GitHub

Evite versionar:

```text
venv/
.venv/
__pycache__/
.ipynb_checkpoints/

dataset/
dataset_yolo/

notebook/yolov5/

runs/
notebook/yolov5/runs/

*.pt
*.pth
*.onnx
*.keras
*.h5

*.cache
*.tmp
*.log
```

Motivos:

- ambientes virtuais podem ter milhares de arquivos;
- datasets aumentam muito o tamanho do repositório;
- YOLOv5 pode ser baixada novamente;
- pesos de modelos podem ser grandes;
- `runs/` contém muitos artefatos gerados automaticamente;
- caches e temporários não são necessários para reproduzir o código.

---

# Observação sobre pesos treinados

Se for necessário disponibilizar um modelo treinado, existem duas opções:

1. remover `*.pt` do `.gitignore` e versionar somente um peso pequeno, como `best.pt`;
2. disponibilizar os pesos externamente e adicionar o link no README.

Não é necessário subir todos os pesos e checkpoints gerados durante os treinamentos.

---


# Assets e datasets

Para manter o repositório leve, os arquivos de evidência e os datasets foram organizados separadamente.

## Assets do projeto

Os gráficos, matrizes de confusão, exemplos de detecção e previsões estão documentados em um README específico:

➡️ [Acessar o README dos assets](assets/README_ASSETS.md)<br>
➡️ [Acessar Imagem de FIGURA AUTORAL](notebook/figura_autoral_ir_alem_2.png)

A pasta `assets/` contém apenas arquivos leves e relevantes para comprovar os resultados apresentados no notebook.

## Download dos datasets

Os dois datasets utilizados no projeto não são versionados diretamente no GitHub por causa do tamanho.

Eles serão disponibilizados em um único arquivo `.zip` pelo Google Drive:

➡️ [Baixar os datasets pelo Google Drive](https://drive.google.com/drive/folders/1XJ7Omf0RVH7FTYd7EV-RndP7XlD3nE9T?usp=sharing)

Conteúdo esperado do `.zip`:

```text
datasets_fase6.zip
├── dataset/
│   ├── train/
│   ├── validation/
│   └── test/
└── dataset_yolo/
    ├── images/
    │   ├── train/
    │   ├── val/
    │   └── test/
    └── labels/
        ├── train/
        ├── val/
        └── test/
```

Após baixar, extraia as duas pastas dentro de:

```text
ML_IMAGENS/notebook/
```

Assim:

```text
ML_IMAGENS/
└── notebook/
    ├── dataset/
    ├── dataset_yolo/
    ├── yolov5/
    └── notebooks...
```
---

# Vídeo demonstrativo

A entrega prevê um vídeo de demonstração de até **5 minutos**, publicado no YouTube como **não listado**.

Adicionar o link abaixo:

```text
Vídeo: ADICIONAR_LINK_DO_YOUTUBE
```

No vídeo, recomenda-se demonstrar:

1. estrutura do projeto;
2. dataset;
3. YOLO 30 × 60 épocas;
4. detecções da YOLO customizada;
5. YOLO padrão;
6. CNN;
7. Transfer Learning e Fine Tuning;
8. segmentação;
9. principais conclusões.

---

## Notebook da entrega

- [Notebook principal](notebook/FIAP_FASE6_ENTREGA_PRINCIPAL.ipynb)
- [Ir Além 2](notebook/IR_ALEM_2_FASE6.ipynb)

---

# Principais limitações

- dataset pequeno;
- apenas duas classes;
- poucas imagens de validação e teste;
- execução em CPU;
- qualidade das bounding boxes afeta diretamente a YOLO;
- variedade visual das canecas e garrafas;
- possibilidade de overfitting;
- segmentação pode remover partes relevantes do objeto.

---

# Possíveis melhorias futuras

- aumentar o dataset;
- aumentar a diversidade de fundos;
- adicionar mais ângulos e condições de iluminação;
- revisar manualmente todas as bounding boxes;
- testar modelos YOLO maiores;
- utilizar GPU;
- executar otimização de hiperparâmetros;
- avaliar Data Augmentation adicional;
- avaliar outras arquiteturas de Transfer Learning;
- comparar diferentes redes de segmentação;
- testar o modelo em imagens externas ao dataset.

---

# Reprodutibilidade

Antes de executar:

```bash
git clone URL_DO_REPOSITORIO
cd NOME_DO_REPOSITORIO

python3 -m venv venv
source venv/bin/activate

pip install --upgrade pip
pip install -r requirements.txt
```

Depois:

```bash
cd notebook
git clone https://github.com/ultralytics/yolov5.git
pip install -r yolo_SEM_IR_ALEM.v5/requirements.txt
jupyter notebook
```

Adicione os datasets nas pastas esperadas e execute os notebooks na ordem.

---

# Licença e uso

Projeto desenvolvido exclusivamente para fins acadêmicos no contexto da FIAP.

As imagens utilizadas no dataset devem respeitar suas respectivas fontes, licenças e permissões de uso.