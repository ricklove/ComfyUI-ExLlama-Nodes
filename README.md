# ExLlama nodes for ComfyUI
A simple prompt generator for [ComfyUI](https://github.com/comfyanonymous/ComfyUI) utilizing [ExLlama](https://github.com/turboderp/exllama).

## Installation
Clone the repository to `custom_nodes` in your ComfyUI directory and install dependencies:
```
git clone https://github.com/Zuellni/ComfyUI-ExLlama-Nodes
python -m pip install -r requirements.txt
```

Next, install the latest pre-built ExLlama wheel from [here](https://github.com/jllllll/exllama/releases/latest).  
Choose the version matching your platform, Python, and PyTorch CUDA/ROCm.

Example for Windows with Python 3.10 and CUDA 11.8 which should match the portable ComfyUI build:
```
python -m pip install https://github.com/jllllll/exllama/releases/download/0.0.17/exllama-0.0.17+cu118-cp310-cp310-win_amd64.whl
```

## Nodes
Name | Description
:--- | :---
Loader | Loads 4-bit GPTQ Llama/2 models. You can find a lot of them on [Hugging Face](https://huggingface.co/TheBloke).<br>Clone the model repository or download all the files in it to an empty directory, then point to it in `model_dir`. The `model.safetensors` file won't work on its own.<br><br>ExLlama allocates memory based on `max_seq_len`. Lowering it is a good way to save on VRAM. It's currently not possible to [offload](https://github.com/turboderp/exllama/issues/177) the model to RAM.
Generator | Returns a `string` based on the given `prompt` for use with other nodes. Default values correspond to the `simple-1` preset from [text-generation-webui](https://github.com/oobabooga/text-generation-webui). ExLlama isn't [deterministic](https://github.com/turboderp/exllama/issues/201), so the outputs may differ even with the same seed.<br><br>To load a LoRA specify its directory in `lora_dir`. It should contain `adapter_model.bin` and `adapter_config.json`.
Previewer | Displays generated outputs in the UI.

## Workflow
Can be loaded directly in ComfyUI. Model used: [MythoLogic-Mini-7B](https://huggingface.co/TheBloke/MythoLogic-Mini-7B-GPTQ).

![workflow](https://github.com/Zuellni/ComfyUI-ExLlama-Nodes/assets/123005779/91fc6b64-3734-456b-975d-ee0b77386841)
