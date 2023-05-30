# ChatGPT + Azure OpenAI and Pinecone VectorDB Search


This sample is based upon the Azure Search OpenAI Demo that uses cognitive search.  This example uses the Pinecone VectorDB database instead of cognitive search.   

This requires the torch, pinecone client, and sentence-transformers libraries, however, the azure-search-documents library is not required.  

Feel free to experiment with other encoders.


## Getting Started

Please follow the Azure OpenAI instructions for setting up the application (https://github.com/Azure-Samples/azure-search-openai-demo).  

Note: You do not need the cognitive search, however, since all else remains the same, Azure blob storage is used to store the the chunked files.  

Besides your standard Azure Credentials required during setup (again, see Azure Search OpenAI Demo for instructions), you'll need the following environment variables:

####  /app/backend/app.py
##### Pinecone api key, environment, index and encoding model
- PINECONE_API_KEY =  os.environ.get('PINECONE_API_KEY') or 'PINECONE_API_KEY'
- PINECONE_ENV = os.environ.get('PINECONE_ENV') or 'PINECONE_ENV'
- PINECONE_INDEX_NAME = os.environ.get('PINECONE_INDEX_NAME') or 'gptkbindex'
- PINECONE_ENCODING_MODEL = os.environ.get('PINECONE_ENCODING_MODEL') or "all-MiniLM-L6-v2" 

####  /app/backend/approaches changed:
Now they receive pinecone_index and an encoder from app.py.  They then query pinecone.  Some variables (like use_semantic_captions) aren't used but remain in the files.

####  /app/backend/requirements.txt changed to add pinecone-client, sentence-transformers, torch:
- azure-identity==1.13.0b3
- Flask==2.2.2
- langchain==0.0.78
- openai==0.26.4
- azure-storage-blob==12.14.1
- pinecone-client==2.2.1
- sentence-transformers==2.2.2
- torch==2.0.1


#### To upload docs via /scripts/prepdocs.py, the following parameters were added to support Pinecone:
- parser.add_argument("--pineconekey", help="Pinecone account key.")
- parser.add_argument("--pineconeenv", help="Pinecone environment. Can be found in the Pinecone Console under Indexes.")
- parser.add_argument("--index", help="Name of the Pinecone index where content should be indexed (will be created if it doesn't exist)")

The PINECONE_ENCODING_MODEL is set to "all-MiniLM-L6-v2".  You can change that at the top of the file 

####  /scripts/Requirements.txt changed to add pinecone-client, sentence-transformers, torch:
- pypdf==3.5.0
- azure-identity==1.13.0b4
- azure-ai-formrecognizer==3.2.1
- azure-storage-blob==12.14.1
- pinecone-client==2.2.1
- sentence-transformers==2.2.2
- torch==2.0.1
