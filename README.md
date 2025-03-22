### DeepSeek R1 models

Trying to test and run DeepSeek R1 locally...

Official Repo: https://github.com/deepseek-ai/DeepSeek-R1

Running locally using VLLM:

```
pip install vllm

# Load and run the model:
vllm serve "deepseek-ai/DeepSeek-R1"
```

Need access to at least 8xH200 Gpus for latest models...

Consider using **distilled versions of DeepSeek R1 (like DeepSeek-R1-Distill-Llama-70B) if you have limited GPU resources** 


```
vllm serve "deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B" --max_model 4096 --port 800
```

The above will download the model's weights and run an inference endpoint...


To view Swagger docs, go to:
```
http://localhost:8000/docs#/default
```

Can confirm that the deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B is the only model that can run locally on RTX 3080, 16GB RAM

```
python -m vllm.entrypoints.api_server --model deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B --max_model 4096 --port 8000
```

To access model endpoint:
```
curl http://localhost:8000/v1/chat/completions \
    -H "Content-Type: application/json" \
    -d '{
        "model": "deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B",
        "messages": [
            {"role": "system", "content": "You are a helpful assistant."},
            {"role": "user", "content": "Who won the world series in 2020?"}
        ]
    }'
```


### References

https://docs.vllm.ai/en/latest/getting_started/quickstart.html

https://www.databasemart.com/blog/install-and-run-deepseek-r1-locally-with-vllm-v1?srsltid=AfmBOopB0Nch36ogyP7pBs_iPZuC_FlI566leZpawDscE7Q-XkrE_Xs-

https://github.com/deepseek-ai/DeepSeek-R1

https://ollama.com/