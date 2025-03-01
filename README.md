# yolov12_dfl_rknn_Cplusplus
yolov12 rk3588 部署版本，将DFL放在后处理中，转换工具版本 rknn_toolkit2-2.2.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.


导出onnx、转rknn流程说明[【yolov12 部署瑞芯微rk3588、RKNN部署工程难度小、模型推理速度快】]()

## 编译和运行

1）编译

```
cd examples/rknn_yolov12_demo_dfl_open

bash build-linux_RK3588.sh

```

2）运行

```
cd install/rknn_yolo_demo_Linux

./rknn_yolo_demo 

```

注意：修改模型、测试图像、保存图像的路径，修改文件为src下的main.cc

```

int main(int argc, char **argv)
{
    char model_path[256] = "/home/zhangqian/rknn/examples/rknn_yolov12_demo_dfl_open/model/RK3588/yolov12n_zq.rknn";
    char image_path[256] = "/home/zhangqian/rknn/examples/rknn_yolov12_demo_dfl_open/test.jpg";
    char save_image_path[256] = "/home/zhangqian/rknn/examples/rknn_yolov12_demo_dfl_open/test_result.jpg";

    detect(model_path, image_path, save_image_path);
    return 0;
}
```


# 测试效果

## onnx 测试效果

![test_onnx_result](https://github.com/user-attachments/assets/aa29480e-c62a-420c-9b8a-7737adbee187)

## rk3588上测试效果

![test_result](https://github.com/user-attachments/assets/a06a950d-903c-43d8-95aa-7c3562badf33)

把板端模型推理和后处理时耗也附上，供参考，使用的芯片rk3588，yolov12n 模型输入640x640，检测类别80类。

![1740841045385](https://github.com/user-attachments/assets/29f2f7a2-c6e9-4141-adeb-1c02195ad7ee)

这个时耗非常高，查看转rknn时的日志，很多操作切换到cpu上进行计算。

![image](https://github.com/user-attachments/assets/7a4e6843-07ba-4657-b348-42b8fdcac912)


