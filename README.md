# Trabalho Final

## Descrição
Este trabalho final da disciplina Recuperação da Informação consiste em avaliar métricas (Precision, Recall e F1) dos modelos de recuperação de informação Solr, vetorial e BM25 a fim de compará-los perfomaticamente. Para isso, foi utilizado o dataset "Highwire (TREC Genomics 2006)".

---

## Clonando o repositório em `~/git/projeto-final-comparacao-ri`

```shell
mkdir ~/git
cd ~/git
git clone https://github.com/gbsantana/projeto-final-comparacao-ri.git
cd ~/git/projeto-final-comparacao-ri
```
## Configuração do Ambiente

### Pré-requisitos

- Miniconda (<https://www.anaconda.com/docs/getting-started/miniconda/>)

_Obs.: É preciso iniciar o conda com o comando `conda init` (uma única vez), e talvez seja necessário reiniciar o terminal para que a ativação seja efetiva. O conda só estará ativo se aparecer `(base)` logo no início da linha do terminal._

#### Instalando o Miniconda via chocolatey sem permissão de administrador

Usando o PowerShell:

```powershell
choco install miniconda3 --params="'/InstallationType=JustMe /AddToPath=1 /RegisterPython=0'"
conda init powershell
```

Fonte: https://community.chocolatey.org/packages/miniconda3

### 1. Preparando o conda

```shell
conda update conda -y
conda update --all -y
conda config --add channels conda-forge
```

**_[OPCIONAL]_** Os comandos abaixo são úteis APENAS caso esteja rodando em uma plataforma **Intel**:

```shell
conda config --add channels https://software.repos.intel.com/python/conda/
conda config --set channel_priority strict
```

### 2. Criação do ambiente

- APENAS em plataforma **Intel**

```shell
conda create -n projeto_final_ri intelpython3_full python=3.12
```

- Outras plataformas:

```shell
conda create -n projeto_final_ri python=3.12
```

### 3. Ativação do ambiente

```shell
conda activate projeto_final_ri
```
### 4. Instalação de dependências (_sempre prefira usar o `conda` ao `pip`_)

```shell
python -m pip install -U --upgrade-strategy only-if-needed pip
conda update --all -y

conda install gensim --no-update-deps -y
conda install nltk --no-update-deps -y
conda install numpy --no-update-deps -y
conda install pandas --no-update-deps -y
conda install matplotlib --no-update-deps -y
conda install jupyter --no-update-deps -y
conda install pysolr --no-update-deps -y

python -m pip install -U --upgrade-strategy only-if-needed ir_datasets
python -m pip install -U --upgrade-strategy only-if-needed rank_bm25

conda update --all -y
```

### 5. [ALTERNATIVA aos passos #2, #3 e #4] Criando, configurando e ativando o ambiente

- APENAS em plataforma **Intel**

```shell
conda env create -f environment_intel.yml -n projeto_final_ri
conda activate projeto_final_ri
conda update --all -y
```

- Outras plataformas:

```shell
conda env create -f environment.yml -n projeto_final_ri
conda activate projeto_final_ri
conda update --all -y
```

- Ativando o ambiente

### 6. Downloading NLTK and Spacy Data

```python
python -m nltk.downloader all
python -m spacy validate
python -m spacy download xx_ent_wiki_sm
python -m spacy download en_core_web_sm
python -m spacy download pt_core_news_sm
```

### 7. [SOMENTE SE NECESSÁRIO] Removendo o ambiente

```shell
conda remove -n projeto_final_ri --all -y
```

Então re-execute a partir do passo #2 (ou #5) em diante.
