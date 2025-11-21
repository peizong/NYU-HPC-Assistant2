This is a repository for NYU HPC chatbot.
(latest version for tests; NYU-HPC-Assistant1 supports a chatbot outside NYU; NYU-HPC-Assistant3 supports a chatbot inside NYU)


# create a conda environment

`conda create -n chatbot-py310 python==3.10`

`conda activate chatbot-py310`

`pip install -r requirements.txt`

or better for the specific versions,

`pip install -r requirements-specific.txt`

# start the chatbot

Before start the chatbot, first import the API KEYs,

`export JINA_API_KEY=xxx`

`export OPENAI_API_KEY=xxx` (if use portkey API the format is different)

After it, then start the chatbot,

`python -m streamlit run --server.port 8080 streamlit_app.py`

or the cloud version where files are stored in cloud (e.g., AWS, GCP, etc),

`python -m streamlit run --server.port 8080 streamlit_app.py`

## some notes
Packages is critical
(my NYU MacBook)
conda create -n chatbot2 python==3.10
need numpy<=2.0:
pip install "numpy<2"

different versions of Python, FAISS, etc. serious affect the functionality of the code. How to control the verion of code? Prepare a requirement file.

tf-keras

Faiss related issues, a popular one due to using different faiss.swigfaiss_avx512 or faiss.swigfaiss (TypeError: IndexFlat.search() missing 3 required positional arguments: 'k', 'distances', and 'labels’)
Solution is to uninstall the old packages and use the standard one:

pip uninstall faiss
pip uninstall faiss-cpu
pip uninstall faiss-gpu
conda remove faiss faiss-cpu faiss-gpu
conda install -c conda-forge faiss-cpu

if another issue appear: could not find faiss.swigfaiss_avx2 or faiss.swigfaiss_avx512
in file 
import sys
sys.modules['faiss.swigfaiss_avx2'] = faiss
sys.modules['faiss.swigfaiss_avx512'] = faiss

JINA API

this needs to be updated when there is related issues. You can check the latest API keys here: https://jina.ai/api-dashboard/embedding

The key can be set in a terminal (the local version) or explicitly (the cloud version) in a secret session or directly in the code (not recommended for security, some platform may even forbit it).

LLM API Keys

there is personal version and NYU provided ones. Different rules apply. Need to be careful to check the format differences and VPN is needed for NYU KEYS through PortKey.

Foundation model version:

gpt-4o, got-4o-mini

AWS S3 bucket

homemade cloud version

Google cloud

Data storage and priority management
Burwood version, and Gemini

Tunneling from compute node, localhost
(i) first, start a short srun job;

(ii) then open a new terminal and try the following:
### On your local machine
ssh -L 8080:localhost:8080 your_netid@login.hpc.nyu.edu
### Then, from inside login node:
ssh -L 8080:localhost:8080 node123

(iii) After this, log in to the node 123 and start the application app.py
