# SpikingWM-RL
代理实例中的端口到本地

ssh -CNg -L 6006:127.0.0.1:6006 root@connect.nmb1.seetacloud.com -p 49276

切换用户

su - simuser

生成 Github ssh key

ssh-keygen -t ed25519 -C "yanzhang@whu.edu.cn"

cat /root/.ssh/id_ed25519.pub

conda activate /root/autodl-tmp/conda_envs/dino_wm

export WANDB_MODE=offline

export DATASET_DIR=/root/autodl-tmp/swm_data/datasets

python train.py --config-name train.yaml ckpt_base_path=/root/autodl-tmp env=deformable_env frameskip=5 num_hist=3

安装系统依赖
编译 UE4.27
编译 AirSim
打开 Blocks
写 settings.json
安装 Python airsim 包
跑 test_airsim.py
跑图像读取测试
