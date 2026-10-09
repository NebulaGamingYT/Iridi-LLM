# Planned Features Board
The number next to the list determines the priority of the feature

- [ ] Attempt to work around sliding context windows **3** 
- [ ] App color themes **1**
- [ ] Custom Models built for the app **2** 
- [ ] Full Public Release **4**
- [x] Chat Compacting
- [x] Customizable Model Rules


#  **App Usage & Navigation**

## Model Settings

Inside the settings page on the top right, there is a button that says model settings, this includes options for local APIs, Streaming, Reasoning Levels, Sampling, Planning mode, and Tool Call limits. Each is explained below.

1\) Max Tool Calls: Changes the maximum amount of tool calls a model can use per response, numbers from 1-9999  
![image1](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/maxtoolcalls.png)

2\) Planning Mode: If active, the model will make a plan based on your prompt before doing anything and will ask you to approve, deny, or make changes to the plan it makes.  
![image2](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/planningmode.png)

3\) Sampling: For local models and APIs with support for these settings, Max tokens is the max number of tokens the model can output before getting stopped, Temperature is how random the model is (closer to 0 means more likely to produce same result multiple times, closer to 1+ means less likely to produce the same result) it is recommended to have this between 0.2-1. Top P Sampling is the minimum chance for the next token, ranges from 0-1, acts like temperature. Top K Sampling, limits next generated token from the top tokens by likelihood to this number. Min P Sampling is the minimum probability for a token to be selected.   
![image3](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/sampling.png)

4\) Reasoning level changes the reasoning level (if applicable) of the selected model, changes per model so expect light bugs. This defaults to the models default if none of the settings work.  
![image4](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/reasoninglevel.png)

5\) If Stream responses is turned on, displays each token as it is generated, if it is turned off it waits for the whole response before showing the generated text.  
![image5](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/streamresponses.png)

6\) Local API hosts the current model through the app as an api, it mimics an open ai compatible format, the API can be used to port forward from it and host it publicly, use in scripts, or anything else. You can disable or enable the harness to choose whether the model can use tools or not, or set an api key. You are also able to change the port in the text box.  
![image6](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/localapi.png)

# 

# **Providers:**

## Local Providers

Local providers allow unlimited free ai usage through running them locally on your own gpu, these are some of the most recommended for this app as they also have no rate limit, although they do take slightly longer to set up. The preferred local provider is LM Studio, but vLLM and Ollama are supported as well as any service that runs an open ai compatible api locally. Below is a guide on how to set up a local model, this guide assumes you have already hosted a model locally, if you have not check the guide below in the recommendations section. 

For these examples, we will use LM studio, this does not matter and is mostly interchangeable, but it is preferred.

1\) First open the Iridi-LLM app and click the settings icon in the top right.  
![image7](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/settingstopright.png)

2\) In the panel that opens, click the External Server tab.  
![image8](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/modelsource.png)

3\) If not already selected, click the LM Studio:1234 button under the Local Server Endpoint box to auto fill.  
![image9](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/settingpannelexternalsource.png)

4\) A drop down should appear in a new section titled Active Models, select the model you loaded into LM Studio or your provider.   
![image10](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/activemodels.png)

5 \- Optional) To change or confirm anything, feel free to check the Model Settings panel.  
![image11](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/modelsettingsbutton.png)

6\) Click the save button in the bottom right and you have finished setting up the model and are now able to chat with it\!

#  **Recommendations**

Below are recommendations on how to use the app or fixes to common errors. They are grouped into general categories.

## Model Selection

It is recommended to use a model that does not have a sliding context window (Example: Gemma 4 model series), as it may cause issues with tool calling and context degradation during replies.

Recommendations based on vram available are below in the table. These models are recommended to be hosted using lm studio, hosting instructions are below. (At 32k-64k context) All models tested quantized to q4/q8.

| VRAM | Top Model | 2nd Best | 3rd Best |
| :---- | :---- | :---- | :---- |
| Below 6gb | unsloth/NVIDIA-Nemotron-3-Nano-4B-GGUF | google/gemma-4-e2b | unsloth/Qwen3.5-4B-GGUF |
| 6-8gb | unsloth/Qwen3.5-9B-GGUF | google/gemma-4-e4b | unsloth/NVIDIA-Nemotron-3-Nano-4B-GGUF |
| 8-12gb | zai-org/glm-4.6vflash | deepseek/deepseek-r1-0528-qwen3-8b | unsloth/Qwen3.5-9B-GGUF |
| 12-16gb | unsloth/gemma-4-12B-it-qat-GGUF | unsloth/Qwen3.5-9B-GGUF | unsloth/Qwen2.5-Coder-7B-Instruct-GGUF |
| 16-24gb | unsloth/Qwen3.8-27B-GGUF | meta/muse-glimmer | jorge-erdb/GLM-4.7-Flash-D-IQ4NL-GGUF |
| 24-48gb | unsloth/NVIDIA-Nemotron-3-Nano-Omni-30B-A3B-Reasoning-GGUF | meta/muse-glimmer | qwen/qwen3.6-35b-a3b |
| 48gb+ | lmstudio-community/llama-3-groq-70b-tool-use-gguf | meta/llama-3.3-70b | qwen/qwen3.8-27b |

The following models are intended for use in IQ4_NL (or IQ4_NL_XL) quantization, as this is tested to improve performance in the app. The only outlier in this list is ***unsloth/Qwen3.8-27B-GGUF***, ran at UD_IQ4_XS quantization instead.

* ***unsloth/NVIDIA-Nemotron-3-Nano-Omni-30B-A3B-Reasoning-GGUF*** 
* ***jorge-erdb/GLM-4.7-Flash-D-IQ4NL-GGU*** 
* ***unsloth/Qwen3.5-4B-GGUF***
* ***Aldaris/DeepSeek-R1-Distill-Qwen-7B-IQ4_NL-GGUF***
*  ***unsloth/Qwen3.5-9B-GGUF***
*  ***unsloth/Qwen3.8-27B-GGUF***

### Potential Model Issues
The following models below work, however they are likely to cause issues or conflicts with the harness. One example would be ***prism-ml/bonsai-27b***, even though it achieves similar results to the original fp16 model, in testing it does considerably worse compared even to models smaller than it (at q4/q8) on tasks that are open ended, require long context retrieval, memory recollection, or non verifiable coding tasks. For uses that are verifiable or simpler tasks, QAT models quantized to low bit precision (q3, q2, q1, ect.) still work with relative performance to their fp16 counterparts. Here is the list of models that were tested and fall under this category.

* **prism-ml/bonsai-27b**
	- Tested, q8 Qwen 3.6 27b model retained 27% better long context retrieval with 14% less tool call error rate.
* **sdkyuan/qwen3.8-27B-qat-q2_0-gguf**
	- Tested, q4 Qwen 3.8 27b model retained 16% better context retrieval, 18% less tool call error rate, and better goal tracking. 

### Known Model Issues

FIXED ANY KNOWN MODEL ISSUES AS OF v0.6, GEMMA 4 AND GEMMA 3 IS WORKING NOW (if you decided to use this model family, use the ones with fixed chat templates.)

## How to start a local server for LM Studio

This is a simple quick guide to starting a local server on LM Studio using images below.

1\) Get to home page and click the developer icon (or click ctrl \+ z)  
![image12](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/developertab.png)]

2\) Click the Local Server button on the left if not already selected  
![image13](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/developerlocalserver.png)

3\) In the middle of the screen, click the slider button that says “Status: Stopped/Running” or press ctrl \+ r  
![image14](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/statusstopped.png)

4\) In the middle right of the screen click the \+ Load Model button  
![image15](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/loadmodel.png)

5\) Select what model you want to use in the app (This shows a list of all your previously downloaded models, if you have not downloaded a model, please go and download one first using the guide above or use an API instead.)  
![image16](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/modelsettingspanel.png)

6\) This opens a panel with settings for the model, recommended settings for most models are as follows:  
Context: 32768+ Recommended Context, Minimum 16384 Context.  
Gpu Offload: Max (Fill Slider)  
Max Concurrent Predictions: 1  
Unified KV Cache: On  
Offload KV Cache to GPU Memory: On  
Keep Model in Memory: On  
Flash Attention (If available): On  
K Cache Quantization Type: On, Q4\_0  
V Cache Quantization Type: On, Q4\_0

If all settings do not appear, click Show Advanced Settings in the bottom left.

7\) Click the Load Model button or press ctrl \+ enter:  
![image17](https://file.garden/aZ0Ejl312E5LWDAV/iridi-llm/Loadmodelsettingspannel.png)

8\) Wait for the model to finish loading and the LM Studio server is finished, To connect it to the app, you may follow the previous guide in the **Providers** section above.

## Paid API Keys

Paid API keys can be obtained from lots of providers such as Anthropic, Google, or ChatGPT, but there are many others who offer paid api keys. Typically documentation on their websites is provided for obtaining and using an api key, so below are some recommended paid api key providers for you to use.

1\) Openrouter: [https\://openrouter.ai/](https://openrouter.ai/)

2\) Anthropic: [https\://platform.claude.com/](https://platform.claude.com/) 

3\) Google: [https\://aistudio.google.com/api-keys](https://aistudio.google.com/api-keys)

4\) Groq: [https\://console.groq.com/keys](https://console.groq.com/keys) 

5\) Grok: [https\://x.ai/api](https://x.ai/api) 

6\) Deepseek: [https\://platform.deepseek.com/api\_keys](https://platform.deepseek.com/api_keys) 

## Free API Keys

Free api keys are less common compared to paid ones, but a list of providers who offer free, or free tiers for some of their api keys are below.

1\) Openrouter: [https\://openrouter.ai/](https://openrouter.ai/)

2\) Groq: [https\://console.groq.com/keys](https://console.groq.com/keys) 

3\) Google: [https\://aistudio.google.com/api-keys](https://aistudio.google.com/api-keys)

4\) Requesty: [https\://www\.requesty.ai/free-models](https://www.requesty.ai/free-models) 
