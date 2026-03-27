# 🚀 Ollama Model Quantizer

Accessible Google Colab notebook for quantizing Hugging Face models to GGUF format for Ollama, based on the work of [Ollama](https://ollama.com/) and [llama.cpp](https://github.com/ggerganov/llama.cpp).

| |🇬🇧 English|🇮🇹 Italiano|
|:--|:-:|:-:|
| 🚀 **Ollama Quantizer** | [![Open in Colab](https://raw.githubusercontent.com/hollowstrawberry/kohya-colab/main/assets/colab-badge.svg)](https://colab.research.google.com/github/yourusername/ollama-quantizer/blob/main/Ollama_Quantizer.ipynb) | [![Apri in Colab](https://raw.githubusercontent.com/hollowstrawberry/kohya-colab/main/assets/colab-badge-spanish.svg)](https://colab.research.google.com/github/yourusername/ollama-quantizer/blob/main/Ollama_Quantizer_Italian.ipynb) |

---

## 🚀 Ollama Quantizer - Features

* **One-click installation** - Automatically installs all dependencies (UV, Hugging Face Hub, Ollama) with a single cell
* **Simple configuration** - Just paste your Hugging Face model URL and select desired quantizations
* **Multiple quantization types** - Supports all GGUF formats from fp32 (lossless) to iq2_xs (extreme compression)
* **Smart caching** - Skips already generated quantizations to save time and bandwidth
* **Google Drive integration** - Automatically saves all quantized models to your Google Drive
* **Resume capability** - Can resume from interruptions, keeping track of completed quantizations
* **Space management** - Includes disk space checker and cleanup utilities
* **Real-time progress** - Clear output between quantizations for better visibility
* **Comprehensive reporting** - Shows file sizes, total time, and success/failure statistics

---

## 📊 Quantization Guide

GGUF (GGUF Universal Format) is the native format for llama.cpp and Ollama. Quantization reduces model size while sacrificing minimal quality.

### Quality vs Size Trade-off

| Type | Bits | Quality | Relative Size | Recommended Use |
|------|------|---------|---------------|-----------------|
| **fp32** | 32 | ★★★★★ | 100% | Pure CPU, maximum precision |
| **fp16** | 16 | ★★★★★ | 50% | Modern GPUs, lossless quality |
| **q8_0** | 8.0 | ★★★★☆ | 25% | Almost lossless, great compromise |
| **q6_K** | 6.5 | ★★★★☆ | 20% | Excellent for most cases |
| **q5_K_M** | 5.5 | ★★★★☆ | 17% | Very high quality, good compression |
| **q5_K_S** | 5.5 | ★★★☆☆ | 17% | High quality, slight savings |
| **q4_K_M** | 4.5 | ★★★★☆ | 14% | 🏆 **BEST BALANCE** quality/size |
| **q4_K_S** | 4.5 | ★★★☆☆ | 14% | Good balance for general use |
| **iq4_xs** | 4.25 | ★★★☆☆ | 13% | Better quality for size with I-Matrix |
| **q3_K_M** | 3.5 | ★★★☆☆ | 11% | Good compression for limited devices |
| **q3_K_S** | 3.5 | ★★☆☆☆ | 11% | High compression for very limited devices |
| **iq3_m** | 3.66 | ★★☆☆☆ | 11% | Medium compression with I-Matrix |
| **iq3_xs** | 3.3 | ★★☆☆☆ | 10% | High compression with I-Matrix |
| **q2_K** | 2.5 | ★☆☆☆☆ | 8% | Maximum compression, minimum quality |
| **iq2_m** | 2.4 | ★☆☆☆☆ | 7% | Extreme compression with I-Matrix |
| **iq2_xs** | 2.2 | ★☆☆☆☆ | 7% | Extreme compression for testing |

### How to Choose:

1. **For professional/scientific use**: fp16 or q8_0
2. **Best quality/size balance**: q4_K_M (recommended)
3. **Limited RAM devices (8-16GB)**: q4_K_M or q4_K_S
4. **Very limited devices (4-8GB)**: q3_K_M or q3_K_S
5. **Testing/experimentation only**: q2_K or iq versions

### Notes on Versions:
- **K-means** (q*_K_*): K-means optimizations for better quality
- **I-Matrix** (iq*_*): Uses Importance Matrix to preserve most important weights
- **S/M/L**: Small, Medium, Large indicate different optimization configurations

### 💡 Pro Tip:
For most users, **q4_K_M** offers the best balance between quality and size. You can generate multiple quantizations to test which works best on your hardware.

---

## 🚀 How to Use

### Step 1: Open in Colab
Click the "Open in Colab" button above to launch the notebook.

### Step 2: Run Installation Cell
Execute the first cell to install all dependencies. This will:
- Install UV package manager
- Install Hugging Face Hub and Transformers
- Install Ollama framework
- Mount Google Drive
- Start the Ollama service

### Step 3: Configure & Quantize
Run the main configuration cell where you can:
- Paste your Hugging Face model URL (or model ID)
- Select quantizations by number (e.g., "3,5,7" for q8_0, q5_K_M, q4_K_M)
- Choose output folder structure
- Set options like skip_existing and clear_output

### Step 4: Wait for Completion
The notebook will automatically:
1. Download the model from Hugging Face
2. Generate each selected quantization
3. Save GGUF files to your Google Drive
4. Show a final report with file sizes and locations

### Step 5: Use Your Model
Once complete, you can:
- Download the GGUF files from Google Drive
- Use them with Ollama: `ollama run your-model:quantization`
- Or use them directly with llama.cpp

---

## 🛠️ Requirements

- **Google Account** - To use Google Colab and Google Drive
- **Colab Runtime** - T4 GPU recommended (free tier works)
- **Storage Space** - At least 2x the model size for intermediate files
- **Internet Connection** - For downloading models and dependencies

---

## 📝 Examples

### Basic Usage
```python
# Model URL
model_url = "https://huggingface.co/meta-llama/Llama-2-7b-hf"

# Quantizations to generate (q8_0, q5_K_M, q4_K_M)
quant_choice = "3,5,7"
