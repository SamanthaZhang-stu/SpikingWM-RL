# SpikingWM-RL
代理实例中的端口到本地

ssh -CNg -L 6006:127.0.0.1:6006 root@connect.nmb1.seetacloud.com -p 49276

切换用户

su - simuser

生成 Github ssh key

ssh-keygen -t ed25519 -C "yanzhang@whu.edu.cn"

cat /root/.ssh/id_ed25519.pub

# 启动远程桌面

rm -rf /tmp/.X1*  # 如果再次启动，删除上一次的临时文件，否则无法正常启动

USER=root /opt/TurboVNC/bin/vncserver :1 -desktop X -auth /root/.Xauthority -geometry 1920x1080 -depth 24 -rfbwait 120000 -rfbauth /root/.vnc/passwd -fp /usr/share/fonts/X11/misc/,/usr/share/fonts -rfbport 6006

# 训练前准备

conda activate /root/autodl-tmp/conda_envs/dino_wm

export WANDB_MODE=offline

export DATASET_DIR=/root/autodl-tmp/swm_data/datasets

export DATASET_DIR=/mnt/e/wm_data/datasets

export PYFLEXROOT=/home/world_model/AdaptiGraph/PyFleX

export LD_LIBRARY_PATH=${PYFLEXROOT}/external/SDL2-2.0.4/lib/x64:/root/.mujoco/mujoco210/bin:/usr/lib/nvidia:$LD_LIBRARY_PATH

python train.py --config-name train.yaml ckpt_base_path=/root/autodl-tmp env=deformable_env frameskip=2 num_hist=3

/home/samantha_zhang/mambaforge/envs/dino_wm/bin/python /home/world_model/dino_wm/plan.py \
  --config-name plan_granular.yaml \
  ckpt_base_path=/mnt/e/wm_data/checkpoints \
  model_name=deformable_env/granular \
  n_evals=1 \
  n_plot_samples=1

原生ubuntu上

export PYFLEXROOT=/workspace/PyFleX

export WANDB_MODE=offline

python plan.py --config-name plan_granular.yaml \
  model_name=granular \
  ckpt_base_path=/world_model/checkpoints \
  n_evals=1 \
  planner.sub_planner.num_samples=16 \
  planner.sub_planner.topk=4 \
  planner.sub_planner.horizon=3 \
  planner.sub_planner.opt_steps=2 \
  n_plot_samples=1

# 将本地端口代理到远端

ssh -N -o ExitOnForwardFailure=yes -R 7897:127.0.0.1:7897 root@connect.nmb1.seetacloud.com -p 12609

unset HTTP_PROXY HTTPS_PROXY ALL_PROXY http_proxy https_proxy all_proxy

unset ANTHROPIC_API_KEY ANTHROPIC_AUTH_TOKEN

export HTTP_PROXY=http://127.0.0.1:7897

export HTTPS_PROXY=http://127.0.0.1:7897

export http_proxy=http://127.0.0.1:7897

export https_proxy=http://127.0.0.1:7897

export NO_PROXY=localhost,127.0.0.1


