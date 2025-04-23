`conda create -n nerf-det python=3.10.12`
`conda install pytorch==2.4.1 torchvision torchaudio pytorch-cuda==12.1 cuda-toolkit==12.1 -c pytorch -c nvidia `
`pip install fsspec`
`pip install -U openmim`
`CUDA_HOME=$CONDA_PREFIX mim install mmcv==2.1.0 mmdet==3.2.0 mmdet3d==1.4.0 mmengine==0.10.6 `

`pip install numpy==1.24.0 matplotlib==3.5.3`
`pip install cython==0.29.21`
`conda install cuda-compiler=12.1.0`    # Optional ?
`git submodule add https://github.com/saic-vul/imvoxelnet.git submodules/mmdetection3d`
`git submodule add https://github.com/lilanxiao/Rotated_IoU submodules/rotated_iou `

`cp -r submodules/rotated_iou/cuda_op submodules/mmdetection3d/mmdet3d/ops/rotated_iou`
# known issue:
- /home/matt/miniconda3/envs/nerf-det/include/cuda_runtime_api.h:148:10: fatal error: crt/host_defines.h: No such file or directory
- replace version at 
  - `submodules/mmdetection3d/requirements/runtime.txt`
    ```txt
    # numba==0.48.0
    numba
    # nuscenes-devkit==1.1.2
    nuscenes-devkit
    ```
- In docker
  - [TypeError: FormatCode() got an unexpected keyword argument 'verify' #10962](https://github.com/open-mmlab/mmdetection/issues/10962)
  - `pip install yapf==0.40.1`
  - `pip install protobuf==3.20.3`
  - [fatal error: maskApi.h: No such file or directory](https://github.com/cocodataset/cocoapi/issues/141#issuecomment-1663699065)
  - Dockerfile.pytorch2.4.1-cuda12
    - ```log
      Traceback (most recent call last):
      File "/mmdetection3d/tools/train.py", line 14, in <module>
        from mmdet3d import __version__
      File "/mmdetection3d/mmdet3d/__init__.py", line 24, in <module>
        assert (mmcv_version >= digit_version(mmcv_minimum_version)
                ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      AssertionError: MMCV==2.1.0 is used but incompatible. Please install mmcv>=1.1.5, <=1.3.
    ```
