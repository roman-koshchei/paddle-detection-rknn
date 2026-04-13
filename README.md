# Paddle Detection RKNN

Paddle Detection release/2.5 with applied RKNN patch for PP-YOLOE from [airockchip/rknn_model_zoo/blob/main/examples/ppyoloe/patch_for_model_export](https://github.com/airockchip/rknn_model_zoo/blob/main/examples/ppyoloe/patch_for_model_export) and fix for newer Paddle Paddle version (it seems they changed default value of one of keys)

## Installation

```bash
uv venv --python 3.9
```

I use CPU installation of PaddlePaddle, becasue this will be used just for export of model.

```bash
uv pip install paddlepaddle==2.6.2 -i https://www.paddlepaddle.org.cn/packages/stable/cpu/
```

```bash
uv pip install "setuptools<81"
```

```bash
uv run check.py
```

```bash
uv pip install -r requirements.txt
```

```bash
uv run setup.py install
```

```bash
uv pip install scikit-learn "numba==0.56.4"
```

```bash
uv run ppdet/modeling/tests/test_architectures.py
```

## RKNN Export

Test run export from RKNN model zoo:

```bash
uv run tools/export_model.py -c configs/ppyoloe/ppyoloe_plus_crn_s_80e_coco.yml -o weights=https://paddledet.bj.bcebos.com/models/ppyoloe_plus_crn_s_80e_coco.pdparams exclude_nms=True trt=True exclude_post_process=True use_gpu=False --rknn
```

## ONNX Export

After exported model for RKNN format using previous section export to ONNX.

```bash
uv pip install "paddle2onnx==1.3.1"
```

```bash
uv run paddle2onnx --model_dir output_inference/ppyoloe_plus_crn_s_80e_coco --model_filename model.pdmodel --params_filename model.pdiparams --opset_version 11 --save_file ppyoloe_plus_crn_s_80e_coco.onnx
```
