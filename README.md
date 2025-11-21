This is a repository for NYU HPC chatbot.
(latest version for tests; NYU-HPC-Assistant1 supports a chatbot outside NYU; NYU-HPC-Assistant3 supports a chatbot inside NYU)


## create a conda environment

`conda create -n chatbot-py310 python==3.10`

`conda activate chatbot-py310`

`pip install -r requirements.txt`

or better for the specific versions,

`pip install -r requirements-specific.txt`

`export JINA_API_KEY=xxx`

`export OPENAI_API_KEY=xxx` (if use portkey API the format is different)

## start the chatbot
`python -m streamlit run --server.port 8080 streamlit_app.py`

or the cloud version where files are stored in cloud (e.g., AWS, GCP, etc),

`python -m streamlit run --server.port 8080 streamlit_app.py`

