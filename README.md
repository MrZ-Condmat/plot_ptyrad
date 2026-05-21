# PtyRAD数据可视化工具

用于批量处理和可视化PtyRAD重构数据的交互式工具。

## 功能特性

- 交互式3D数据可视化
- 批量生成重构数据的视频
- MAT文件自动导出

## 安装
将 plot_ptyrad 安装在`/path/plot_ptyrad/`路径的步骤如下：
```bash
conda activate ptyrad

cd /path/
git clone https://github.com/dong-zehao/plot_ptyrad.git

cd ./plot_ptyrad
pip install -e .
```

## 使用方法

安装后，可以直接使用 `plot_ptyrad` 命令：

```bash
# 基本用法: 处理parent_folder文件夹下的重构输出，支持 .pt 或 .hdf5
# 数据文件夹组织形式为  ./parent_folder/region_name/some/nested/folders/model_iter1000.pt
# 输出文件的结构:      ./parent_folder/Data_Saved/region_name/saved_file.png
plot_ptyrad --folder /path/to/parent_folder --file model_iter1000.pt

# 同样支持 hdf5 文件
plot_ptyrad --folder /path/to/parent_folder --file model_iter1000.hdf5

# 若不想跳过已经处理过的数据，可强制重新处理
plot_ptyrad --folder /path/to/parent_folder --file model_iter1000.pt --force

# 使用短参数名
plot_ptyrad -f /path/to/parent_folder -F model_iter1000.pt --force
```

## 数据文件夹目录结构

```
/path/to/parent_folder/
├── 4Dregion01/
│   └── some/nested/folder/
│       └── model_iter1000.pt          # 深层嵌套（也可为 .hdf5）
├── 4Dregion02/
│   └── any_structure/
│       └── sub/folder/
│           └── model_iter1000.pt      # 任意结构（也可为 .hdf5）
├── ...
│
└── Data_Saved/
    ├── plot_params.json          # 全局参数文件
    ├── 4Dregion01/               # 区域1的处理结果
    │   ├── *.png
    │   ├── *.mp4
    │   └── *.mat
    ├── 4Dregion02/               # 区域2的处理结果
        ├── *.png
        ├── *.mp4
        └── *.mat
```



## Qt GUI 版本

该版本提供基于 Qt 的图形界面后端，用于交互式查看和处理 PtyRAD 重构结果。

### 1. 激活运行环境

打开 PowerShell，并激活 `ptyrad` conda 环境：

```powershell
conda activate ptyrad
```

### 2. 进入项目目录

```powershell
cd /path/to/plot_ptyrad
```

### 3. 确认当前分支

确认当前位于 `qt-gui` 分支：

```powershell
git branch --show-current
```

期望输出为：

```text
qt-gui
```

### 4. 启动 Qt GUI

使用以下命令启动 Qt GUI：

```powershell
plot_ptyrad --folder "/path/to/parent_folder" --file model_iter1000.hdf5 --gui-backend qt --force
```

其中：

- `--folder` 指定包含所有重构 region 的父文件夹。
- `--file` 指定需要搜索和读取的重构结果文件名。
- `--gui-backend qt` 表示使用 Qt GUI 后端。
- `--force` 表示即使某个 region 已经处理过，也强制重新打开 GUI。

### 5. 不强制重新打开已处理 region

如果不想强制重新打开已经处理过的 region，可以去掉 `--force`：

```powershell
plot_ptyrad --folder "/path/to/parent_folder" --file model_iter1000.hdf5 --gui-backend qt
```

### 6. 如果 GUI 预览卡顿，降低预览尺寸

如果交互预览比较卡顿，可以降低预览最大尺寸：

```powershell
plot_ptyrad --folder "/path/to/parent_folder" --file model_iter1000.hdf5 --gui-backend qt --force --preview-max-size 768
```

`--preview-max-size` 用于控制 GUI 预览图像的最大边长。数值越小，交互越流畅，但预览分辨率也会降低。

### 推荐常用命令

一般情况下，推荐使用以下流程：

```powershell
conda activate ptyrad
cd /path/to/plot_ptyrad
plot_ptyrad --folder "/path/to/parent_folder" --file model_iter1000.hdf5 --gui-backend qt --force
```
