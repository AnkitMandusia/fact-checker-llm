LLM-Powered Fact Checker
========================

This project implements a fact-checking system using large language models (LLMs), natural language processing (NLP), and vector-based retrieval. It extracts claims from text, retrieves relevant facts from a trusted fact base, and verifies the claims using an LLM. The application is built with Python and includes a Streamlit-based user interface for interactive fact-checking.

Features
--------

*   **Claim Extraction**: Uses spaCy to identify key claims or entities in input text.
    
*   **Fact Retrieval**: Employs FAISS and Sentence Transformers for efficient vector-based fact retrieval.
    
*   **LLM Verification**: Leverages a language model (e.g., Flan-T5-Large) to compare claims against retrieved facts and generate verdicts.
    
*   **Interactive UI**: Provides a Streamlit interface for users to input claims and view results.
    
*   **Fact Base**: Supports a customizable CSV-based fact base, with a default set of sample facts.
    

Prerequisites
-------------

*   **Python**: Version 3.11 or higher.
    
*   **GPU**: Optional but recommended for faster model inference (e.g., NVIDIA GPU with CUDA support).
    
*   **Hugging Face Account**: Required for accessing gated models (e.g., Llama-3.2-3B-Instruct).
    
*   **ngrok Account**: Required for exposing the Streamlit app publicly (optional for local use).
    

Installation
------------

1.  git clone cd
    
2.  python -m venv venvsource venv/bin/activate # On Windows: venv\\Scripts\\activate
    
3.  pip install -U transformerspip install --upgrade --ignore-installed blinkerpython -m spacy download en\_core\_web\_smpip install plotly dash numpypip install -q streamlit==1.32.0 pyngrokpip install spacy sentence-transformers faiss-cpu transformers torch streamlit
    
4.  huggingface-cli loginFollow the prompt to enter your Hugging Face token, which can be generated at [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens).
    
5.  **Set Up ngrok** (Optional):If you want to expose the Streamlit app publicly, sign up for an ngrok account and get an auth token from [https://dashboard.ngrok.com/](https://dashboard.ngrok.com/). Set the token in your environment or directly in the code (not recommended for security).
    

Usage
-----

1.  pip install jupyterjupyter notebookOpen fact\_checker\_llm.ipynb in your Jupyter environment.
    
2.  **Run the Notebook**:Execute the cells in the notebook sequentially. Key steps include:
    
    *   Installing dependencies.
        
    *   Logging in to Hugging Face.
        
    *   Downloading the spaCy model and other packages.
        
    *   Writing the app.py file for the Streamlit application.
        
    *   Setting up ngrok and running the Streamlit app.
        
3.  streamlit run app.pyAccess the app at http://localhost:8501 in your browser.
    
4.  from pyngrok import ngrok, confconf.get\_default().auth\_token = "your-ngrok-auth-token"ngrok.kill()public\_url = ngrok.connect(8501)print("Your Streamlit app is live at:", public\_url)!streamlit run app.py &> /dev/null &Visit the generated ngrok URL to access the app.
    
5.  **Interact with the App**:
    
    *   Enter a claim in the text area (e.g., "The Indian government has announced free electricity to all farmers starting July 2025.").
        
    *   Click the "Verify" button to get a JSON response with the verdict, reasoning, confidence, and evidence.
        
    *   Provide feedback using the "Yes" or "No" buttons.
        

Fact Base
---------

The fact base is stored in facts.csv. If not present, the app creates a default fact base with sample facts about Indian government policies. To customize:

1.  Create a facts.csv file with a fact column containing your facts.
    
2.  Place it in the same directory as app.py.
    
3.  The app will load this file automatically.
    

Troubleshooting
---------------

*   **Model Access Error**: Ensure you have access to the gated model on Hugging Face and have logged in with huggingface-cli login.
    
*   **Dependency Conflicts**: If you encounter version conflicts, try installing packages in a clean virtual environment.
    
*   **ngrok Issues**: Verify your auth token and ensure no other ngrok tunnels are running.
    
*   **Streamlit Not Loading**: Check if port 8501 is free or kill the Streamlit process and restart.
    
*   **GPU Not Detected**: Run !nvidia-smi to confirm GPU availability. If no GPU is available, the app will use CPU (slower).
    

Notes
-----

*   The notebook was tested in a Colab environment with a Tesla T4 GPU (CUDA 12.4). Adjust dependencies if running on a different setup.
    
*   The fact-checking system relies on the quality and coverage of the fact base. Expand facts.csv for better accuracy.
    
*   The LLM (Flan-T5-Large) is used for verdict generation. For better performance, consider using a larger model (if resources allow).
    
*   If the generated code snippets do not work, report issues to the [model repo](https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct) or [huggingface.js](https://github.com/huggingface/huggingface.js).
    

License
-------

This project is licensed under the MIT License. See the [LICENSE](https://grok.com/chat/LICENSE) file for details (if applicable).

Acknowledgments
---------------

*   Built with [Hugging Face Transformers](https://huggingface.co/docs/transformers), [spaCy](https://spacy.io/), [Sentence Transformers](https://www.sbert.net/), [FAISS](https://github.com/facebookresearch/faiss), and [Streamlit](https://streamlit.io/).
    
*   Sample facts are fictional and for demonstration purposes only.
