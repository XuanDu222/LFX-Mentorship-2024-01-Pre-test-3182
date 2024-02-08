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

```
cmake --build build
```

```
sudo cmake --install build
```
