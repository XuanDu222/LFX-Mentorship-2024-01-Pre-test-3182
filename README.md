# LFX-Mentorship-2024-01-Pre-test-3182

## 1 Framework Execution: whisper.cpp
1-Clone the repository:
```
git clone https://github.com/ggerganov/whisper.cpp.git
```
2-Download one of the Whisper models converted in ggml format:
```
bash ./models/download-ggml-model.sh base.en
```
3-Build the main example:
```
make
```
![alt text](https://github.com/XuanDu222/LFX-Mentorship-2024-01-Pre-test-3182/blob/main/make.png?raw=true)
4-Transcribe the audio file:
```
./main -f samples/jfk.wav
```
```
ffplay samples/jfk.wav
```
![alt text](https://github.com/XuanDu222/LFX-Mentorship-2024-01-Pre-test-3182/blob/main/Transcribe%20the%20audio%20file.png?raw=true)

## 2 Build WasmEdge with WASI-NN llama.cpp Backend
1-Build and install WasmEdge
```
cmake -GNinja -Bbuild -DCMAKE_BUILD_TYPE=Release \
  -DWASMEDGE_PLUGIN_WASI_NN_BACKEND="GGML" \
  -DWASMEDGE_PLUGIN_WASI_NN_GGML_LLAMA_METAL=ON \
  -DWASMEDGE_PLUGIN_WASI_NN_GGML_LLAMA_BLAS=OFF \
  .
```
![alt text](https://github.com/XuanDu222/LFX-Mentorship-2024-01-Pre-test-3182/blob/main/Build%20and%20install%20WasmEdge-1.png?raw=true)
```
cmake --build build
```
![alt text](https://github.com/XuanDu222/LFX-Mentorship-2024-01-Pre-test-3182/blob/main/Build%20and%20install%20WasmEdge-2.png?raw=true)
```
sudo cmake --install build
```
![alt text](https://github.com/XuanDu222/LFX-Mentorship-2024-01-Pre-test-3182/blob/main/Build%20and%20install%20WasmEdge-3.png?raw=true)
2-Prepare WASM application
```
cd llama
cargo build --target wasm32-wasi --release
```
3-Output WASM file
```
cp target/wasm32-wasi/release/wasmedge-ggml-llama.wasm ./wasmedge-ggml-llama.wasm
```
4-Execute the WASM with the wasmedge
```
wasmedge --dir .:. \                                                             
  --nn-preload default:GGML:AUTO:llama-2-7b-chat.Q5_K_M.gguf \
llama/wasmedge-ggml-llama.wasm default
```
5-Test
