#### 操作指南

```bash
conda activate ptyrad
cd ~/projects/plot_ptyrad
pip install -e .  #第一次使用需要

# 进入4Dregion01的母文件夹
plot_ptyrad --folder "F:\Data_ARM300\20260510 SCO_96K\All_Data" --file model_iter1000.hdf5

# 当前终端位置已经是母文件夹
F:\Data_ARM300\20260510 SCO_96K\All_Data
plot_ptyrad --folder . --file model_iter1000.hdf5 #这里的 . 表示当前文件夹

# 如果想强制重新生成结果
plot_ptyrad --folder . --file model_iter1000.hdf5 --force
```

