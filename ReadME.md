For the Fine tune the model need to crate the dataset according to model like for the mistral we can use the data 

{"messages":[{"content":"You are an text to SQL query translator. Users will ask you questions in English and you will generate a SQL query based on the provided SCHEMA.\nSCHEMA:\nCREATE TABLE table_name_97 (tie_no VARCHAR, away_team VARCHAR)","role":"system"},{"content":"How many ties does Walsall have?","role":"user"},{"content":"SELECT tie_no FROM table_name_97 WHERE away_team = \"walsall\"","role":"assistant"}]}

with jsonl file 



we have seprate file for the train.jsonl and valid.jsonl and test.jsonl

I am using the mlx libary to train my model this mlx libary supported by the apple silicaon chip 

For that we need to install the library 


pip install mlx_lm 


For the download the model using the command line 



mlx_lm.generate --model mistralai/Mistral-7B-Instruct-v0.2 --prompt "hello"

it will download model from the hugginface and store it in to locally 


For the training the we use the dataset we created 

and then we can run the traing using the command 

mlx_lm.lora --train --model mistralai/Mistral-7B-Instruct-v0.2 --data my-data-chat --batch-size 2


it will take some time and then it will train the model 

it will create the adapters folder in that we have weight for the model using this weight we can creat the ollam model and then use this model locally 


here is setups 

1. create the Modelfile 
    FROM mistral //model name
    ADAPTER ./adapters //adapter location 

2. run ollam command to create the model 

    ollama create <sqlmistral> -f Modelfile

3. run newly created model locally 
    ollama run sqlmistral


    



