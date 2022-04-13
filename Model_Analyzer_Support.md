# Nvidia Model Analyzer Support

To use OLive optimization result in Nvidia Model Analyzer, user needs to provide ONNX model and config.pbtxt file to be used in Model Analyzer.

## Setup Environment
### OLive Setup 
Download OLive package [here](https://olivewheels.blob.core.windows.net/repo/onnxruntime_olive-0.2.0-py3-none-any.whl) and install with command `pip install onnxruntime_olive-0.2.0-py3-none-any.whl`

ONNX Runtime package can be installed with

`pip install --extra-index-url https://olivewheels.azureedge.net/test onnxruntime_openvino_dnnl==1.9.0` for cpu

or 

`pip install --extra-index-url https://olivewheels.azureedge.net/test onnxruntime_gpu_tensorrt==1.9.0` for gpu

### Model Analyzer Setup
Please refer to [Model Analyzer Installation Guide](https://github.com/triton-inference-server/model_analyzer/blob/main/docs/install.md)


## Run OLive optimization
To enable optimization for Model Analyzer, user needs to provide argument `--model_analyzer_config path_to_model_analyzer_config_pbtxt`.

For example, to optimize model with TensorRT backend and precision mode FP16, use can call 

`olive optimize --model_path bertaquad.onnx --model_analyzer_config config.pbtxt --providers_list tensorrt --trt_fp16_enabled --result_path bertsquad_model_analyzer`

Optimized model and new generated configuration file will be saved in bertaquad_model_analyzer. User needs to rename model and configuration files, and change location of the files with structure rules of Model Analyzer. 

## Run Model Analyzer
User can run model analyzer profile with command 

`model-analyzer profile --model-repository models --profile-models bertsquad_trt_fp16`

Then user can run model analyzer analyze to generate report for proflie result with command 

`model-analyzer analyze --analysis-models bertsquad_trt_fp16/ -e analysis_result`