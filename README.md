# Python-Project-PetAvatar_Webapp

## 專案介紹
本專案是一個基於 `FluxPipeline` 文字生成圖片的應用，使用 **FLUX.1 [schnell]** 模型，並透過 `Gradio` 建立簡單易用的網頁介面，讓使用者可以根據輸入的文本描述生成對應的圖片。

## 功能特點
- **支援 GPU 加速**：若系統具備 CUDA，則自動使用 GPU 進行推理，提高圖片生成速度。
- **記憶體優化**：使用 `enable_model_cpu_offload()` 來減少 GPU 記憶體使用量。
- **可調整輸出圖片數量**：使用者可以選擇要生成的圖片數量（1-5 張）。
- **Web UI 介面**：透過 `Gradio` 提供直觀的網頁操作界面。

## 安裝與使用
### 1. 環境準備
請確保系統已安裝 Python 3.8 以上版本，並執行以下指令安裝必要的 Python 套件：
```bash
pip install torch diffusers pillow transformers sentencepiece gradio --quiet
```

### 2. 執行程式
直接運行 Python 腳本即可啟動 Web 應用程式：
```bash
python your_script.py
```

啟動後，Gradio 介面將在本地端運行，您可以使用瀏覽器打開顯示的 URL 來開始生成圖片。

## 使用方式
1. 在 `Enter image description` 欄位輸入圖片描述，例如：
   ```
   a cat in a space suit with a starry sky in the background.
   ```
2. 使用滑桿 (`Number of images generated`) 選擇要生成的圖片數量。
3. 點擊 **"Generate pictures"** 按鈕。
4. 幾秒後，生成的圖片將顯示在下方的 **"Generated Images"** 區域。

## 技術細節
### 1. **模型**
- 使用 `FluxPipeline` 來處理文字轉圖片的推理。
- 預載模型為 **`black-forest-labs/FLUX.1-schnell`**。
- 使用 `torch.bfloat16` 來降低記憶體使用。

### 2. **圖片生成流程**
- 使用 `pipe(prompt, num_inference_steps=10).images[0]` 來生成單張圖片。
- 預設推理步驟 (`num_inference_steps`) 設為 `10`，可視需求調整。

### 3. **Web UI 建置**
- 使用 `Gradio` 創建簡單直觀的界面，包含：
  - 文字輸入框 (`Textbox`) 讓使用者輸入描述。
  - 滑桿 (`Slider`) 讓使用者選擇生成圖片數量。
  - 圖片畫廊 (`Gallery`) 來顯示結果。

## 未來改進方向
- **支援更多 FLUX 模型**：增加不同 FLUX 模型的選擇，如 `FLUX.1-mega`。
- **增加參數調整功能**：例如 `num_inference_steps`、`guidance_scale` 等參數。
- **支援多語言描述**：目前適用英文，未來可支援中文或其他語言輸入。

## 授權條款
本專案採用 **MIT License**，允許自由使用與修改，惟請保留原始授權條款。
