# AIOS: LLM Agent Operating System

<a href='https://arxiv.org/abs/2403.16971'><img src='https://img.shields.io/badge/Paper-PDF-red'></a>
<a href='https://arxiv.org/abs/2312.03815'><img src='https://img.shields.io/badge/Paper-PDF-blue'></a>
[![Code License](https://img.shields.io/badge/Code%20License-MIT-green.svg)](https://github.com/agiresearch/AIOS/blob/main/LICENSE)
<a href='https://discord.gg/B2HFxEgTJX'><img src='https://img.shields.io/badge/Community-Discord-8A2BE2'></a>

AIOS, a Large Language Model (LLM) Agent operating system, embeds large language model into Operating Systems (OS) as the brain of the OS, enabling an operating system "with soul" -- an important step towards AGI. AIOS is designed to optimize resource allocation, facilitate context switch across agents, enable concurrent execution of agents, provide tool service for agents, maintain access control for agents, and provide a rich set of toolkits for LLM Agent developers.


## 🏠 Architecture of AIOS
<p align="center">
<img src="images/AIOS-Architecture.png">
</p>


## 📰 News
- **[2024-04-14]** 🚀 AIOS currently supports generation interrupt (for open-sourced llms) and customized console loggers. Feel free to try!
- **[2024-04-05]** 🛠️ AIOS codebase has been updated to add shell simulator, rapid API calls, and pre-commit test cases. Please see [CONTRIBUTE](https://github.com/agiresearch/AIOS/blob/main/CONTRIBUTE.md) for how to test your contributions and create pull requests.
- **[2024-04-02]** 🌟 AIOS [Discord Community](https://discord.gg/B2HFxEgTJX) is up. Welcome to join the community for discussions, brainstorming, development, or just random chats!
- **[2024-03-25]** ✈️ Our paper [AIOS: LLM Agent Operating System](https://arxiv.org/abs/2403.16971) is released and AIOS repository is officially launched!
- **[2023-12-06]** 📋 After several months of working, our perspective paper [LLM as OS, Agents as Apps: Envisioning AIOS, Agents and the AIOS-Agent Ecosystem](https://arxiv.org/abs/2312.03815) is officially released.


## ✈️ Getting Started

### Installation
To run AIOS, you will need to install our agent creation package, OpenAGI.
**Git clone AIOS and OpenAGI**
```bash
git clone https://github.com/agiresearch/AIOS.git
git clone git@github.com:agiresearch/OpenAGI.git
```
**Make sure you have Python = 3.11**
Install the required packages using pip
```bash
conda create -n AIOS python=3.11
source activate AIOS
cd AIOS
pip install -r requirements.txt
```
**Allow your code to be able to see 'openagi'**
```
cd ../OpenAGI
pip install -e .
```

### Usage
If you use open-sourced models from huggingface, you need to setup your [Hugging Face token](https://huggingface.co/settings/tokens) and cache directory
```bash
export HUGGING_FACE_HUB_TOKEN=<YOUR READ TOKEN>
export HF_HOME=<YOUR CACHE DIRECTORY>
```
If you use LLM APIs, you need to setup your API key such as [OpenAI API Key](https://platform.openai.com/api-keys), [Gemini API Key](https://aistudio.google.com/app/apikey)
```bash
export OPENAI_API_KEY=<YOUR OPENAI API KEY>
export GEMINI_API_KEY=<YOUR GEMINI API KEY>
```

Here we provide two modes to run the AIOS: interactive mode and deployment mode
#### Interactive Mode
In the interactive mode, you can interact with AIOS to see the output of each step in running multiple agents
For open-sourced LLMs, you need to setup the name of the LLM you would like to use the max gpu memory, the evaluation device and the maximum length of generated new tokens.
```python
# For open-sourced LLMs
python main.py --llm_name <llm_name> --max_gpu_memory <max_gpu_memory> --eval_device <eval_device> --max_new_tokens <max_new_tokens>
## Use Gemma-2b-it for example
python main.py --llm_name gemma-2b-it --max_gpu_memory '{"0": "24GB"}' --eval_device "cuda:0" --max_new_tokens 256
```
For close-sourced LLMs, you just need to setup the name of the LLM.
```python
# For close-sourced LLMs
python main.py --llm_name <llm_name>
## Use gpt-4 for example
python main.py --llm_name gpt-4
```

#### Deployment Mode
In the deployment mode, the outputs of running agents are stored in files. And in this mode, you are provided with multiple commands to run agents and see resource usage of agents (e.g., run \<xxxAgent\>: \<YOUR TASK\>, print agent).
Different from the interactive mode, you need to set all the default loggers as file loggers.
```python
# For open-sourced LLMs
python simulator.py --llm_name <llm_name> --max_gpu_memory <max_gpu_memory> --eval_device <eval_device> --max_new_tokens <max_new_tokens> --scheduler_log_mode file --agent_log_mode file --llm_kernel_log_mode file
## Use Gemma-2b-it for example
python simulator.py --llm_name gemma-2b-it --max_gpu_memory '{"0": "24GB"}' --eval_device "cuda:0" --max_new_tokens 256 --scheduler_log_mode file --agent_log_mode file --llm_kernel_log_mode file
```
```python
# For close-sourced LLMs
python simulator.py --llm_name <llm_name> --scheduler_log_mode file --agent_log_mode file --llm_kernel_log_mode file
## Use gpt-4 for example
python simulator.py --llm_name gpt-4 --scheduler_log_mode file --agent_log_mode file --llm_kernel_log_mode file
```
#### Supported LLM backbones
| LLM Name | Open-sourced                                     | Corporation |
|-------------|--------------------------------------------------|----------|
| gemma-2b-it      | Yes                                 | Google |
| gemma-1.1-7b-it       | Yes                                         | Google |
| Mistral-7B-Instruct-v0.2     | Yes | Mistral AI
| Mixtral-8x7B-Instruct-v0.1     | Yes | Mistral AI |
| Mixtral-8x22B-Instruct-v0.1      | Yes                              | Mistral AI |
| Meta-Llama-3-8B-Instruct  | Yes | Meta |
| Meta-Llama-3-70B-Instruct      | Yes                              | Meta |
| gemini-pro      | No | Google |
| gpt-3.5-turbo     | No   | OpenAI |
| gpt-4    | No                   | OpenAI |

## 🖋️ References
```
@article{mei2024aios,
  title={AIOS: LLM Agent Operating System},
  author={Mei, Kai and Li, Zelong and Xu, Shuyuan and Ye, Ruosong and Ge, Yingqiang and Zhang, Yongfeng}
  journal={arXiv:2403.16971},
  year={2024}
}
@article{ge2023llm,
  title={LLM as OS, Agents as Apps: Envisioning AIOS, Agents and the AIOS-Agent Ecosystem},
  author={Ge, Yingqiang and Ren, Yujie and Hua, Wenyue and Xu, Shuyuan and Tan, Juntao and Zhang, Yongfeng},
  journal={arXiv:2312.03815},
  year={2023}
}
```

## 🚀 Contributions
AIOS is dedicated to facilitating LLM agents' development and deployment in a systematic way, collaborators and contributions are always welcome to foster a cohesive, effective and efficient AIOS-Agent ecosystem!

For detailed information on how to contribute, see [CONTRIBUTE](https://github.com/agiresearch/AIOS/blob/main/CONTRIBUTE.md). If you would like to contribute to the codebase, [issues](https://github.com/agiresearch/AIOS/issues) or [pull requests](https://github.com/agiresearch/AIOS/pulls) are always welcome!

## 🌟 Discord Channel
If you would like to join the community, ask questions, chat with fellows, learn about or propose new features, and participate in future developments, join our [Discord Community](https://discord.gg/B2HFxEgTJX)!

## 📪 Contact

For issues related to AIOS development, we encourage submitting [issues](https://github.com/agiresearch/AIOS/issues), [pull requests](https://github.com/agiresearch/AIOS/pulls), or initiating discussions in the AIOS [Discord Channel](https://discord.gg/B2HFxEgTJX). For other issues please feel free to contact Kai Mei (marknju2018@gmail.com) and Yongfeng Zhang (yongfeng@email.com).

## 🌍 AIOS Contributors
[![AIOS contributors](https://contrib.rocks/image?repo=agiresearch/AIOS&max=300)](https://github.com/agiresearch/AIOS/graphs/contributors)


## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=agiresearch/AIOS&type=Date)](https://star-history.com/#agiresearch/AIOS&Date)
