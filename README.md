# Retrieval augmented generation for building datasets from battery literature abstracts
Contains the notebook `Battery_RAG.ipynb` used for creating datasets from battery literature abstracts.\
The metadata of the publications including abstracts, from where the datasets are generated for the 5 materials can be found in `LiFePO4_cathode_WOS.xls`, `TiO2_anode_WOS.xls`, `Li4Ti5O12_anode_WOS.xls`, `MoS2_anode_WOS.xls`, `LiCoO2_cathode_WOS.xls`. (Source: Web of Science, till June 2025)\
The dataset extracted by RAG can be found in `RAG_LiFePO4.csv`, `RAG_TiO2.csv`, `RAG_Li4Ti5O12.csv`, `RAG_MoS2.csv` and `RAG_LiCoO2.csv`.\
The notebook `RAG_Battery_post_prossesing.ipynb` containes steps for preprocessing the extracted data.

## RAG
Open `Battery_RAG.ipynb` in Google Colab.
<a target="_blank" href="https://colab.research.google.com/github/PoulamiSadhukhan5/RAG-for-battery/blob/main/Battery_RAG.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>\
Connect to T4 GPU.\
After installing the libraries open the terminal.
```python
#open the terminal
!pip install colab-xterm
%load_ext colabxterm
%xterm
```
Run the following commands in the terminal to load the LLM.
```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama serve & ollama pull llama3
ollama serve & ollama run llama3
```
Load the file containing the abstracts.
```python
selected_df = pd.read_excel("/content/LiFePO4_cathode_WOS.xls")
```
Define the query.
```python
     query = """
         Describe all the parameters of the material discussed in the text.
         If no information is available just write "N/A".
         The output should be concise and in the format as below:
         Strictly adhere to the format below and do not include any conversational text or explanations after the formatted output.

            Cathode                              :
            Capacity                             :
            C-rate                               :
            Voltage                              :
            Cycle Number                         :
     """
```
Follow the notebook to extract the data.

## Data post-processing
For details of the steps performed to post-process the extracted data before the analysis follow:\
`RAG_Battery_post_prossesing.ipynb` 
<a target="_blank" href="https://colab.research.google.com/github/PoulamiSadhukhan5/RAG-for-battery/blob/main/RAG_Battery_post_prossesing.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

## Curated Huang and Cole database
The Curated date for top 580 materials from Huang and Cole database are available in `Huang-Cole_curated_data.csv`. 



