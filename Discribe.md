### 需求1：运行复现H2O
安装了isaac-gym，并测试了example，但是错误出现在没有安装Vulkan图形库，这是一个和OpenGL一致的库。并且也难以加载对应的CUDA lib，鉴于该库似乎即将废弃，我需要想办法迁移到isaac-sim环境下

在尝试进行Retarget步骤时，依旧需要调用gym的库，按照GPT的指示，可以将手动连接anaconda下的libpython3.8.so.1.0
```
ls ~/anaconda3/envs/py38torch231/lib/libpython3.8.so*
export LD_LIBRARY_PATH=$HOME/anaconda3/envs/py38torch231/lib:$LD_LIBRARY_PATH
```
之后修改了np.float到float，再安装了SMPLSIM
```
pip install git+https://github.com/ZhengyiLuo/SMPLSim.git@master
```
修改了grad_fit_h1.py的路径部分，这两份代码都是迭代进行，后续需要研究下具体的实现  
注释了grad_fit_h1.py的import ipdb; ipdb.set_trace()这一行，这一行是用来调试的输入n执行下一行
运行了grad_fit_h1.py，对于第一个AMASS文件，内部有252个子动作，使用GPU和CPU没有本质的区别

运行了scripts/vis/vis_motion.py，报错需要Vulkan