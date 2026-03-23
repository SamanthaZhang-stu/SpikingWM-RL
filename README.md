# SpikingWM-RL
代理实例中的端口到本地

ssh -CNg -L 6006:127.0.0.1:6006 root@connect.nmb1.seetacloud.com -p 49276

切换用户

su - simuser

安装系统依赖
编译 UE4.27
编译 AirSim
打开 Blocks
写 settings.json
安装 Python airsim 包
跑 test_airsim.py
跑图像读取测试
