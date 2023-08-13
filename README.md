

# Generative Agents: Interactive Simulacra of Human Behavior

<p align="center" width="100%">
<img src="cover.png" alt="Smallville" style="width: 80%; min-width: 300px; display: block; margin: auto;">
</p>
This repository accompanies our research paper titled "[Generative Agents: Interactive Simulacra of Human Behavior](https://arxiv.org/abs/2304.03442)." It contains our core simulation module for  generative agents—computational agents that simulate believable human behaviors—and their game environment. Below, we document the steps for setting up the simulation environment on your local machine and for replaying the simulation as a demo animation.

该存储库是研究论文《[生成代理：人类行为交互模拟](https://arxiv.org/abs/2304.03442)》的附属内容。它包含了用于生成代理的核心模拟模块——这些计算代理可以模拟出可信的人类行为——以及它们的游戏环境。以下，将记录在您的本地计算机上设置模拟环境以及如何回放模拟作为演示动画的步骤。

## ⭐QuickStart

> 注意：填写OpenAI key，运行100step的花费大概需要十几块钱，如果没有什么刚需的话，建议直接运行作者仓库已有的demo即可。

- 首先还是要在`reverie/backend_server`目录，创建一个`utils.py`文件，填写下面的内容：

```python
# Copy and paste your OpenAI API Key
openai_api_key = "<Your OpenAI API>"
# Put your name
key_owner = "<Name>"

maze_assets_loc = "../../environment/frontend_server/static_dirs/assets"
env_matrix = f"{maze_assets_loc}/the_ville/matrix"
env_visuals = f"{maze_assets_loc}/the_ville/visuals"

fs_storage = "../../environment/frontend_server/storage"
fs_temp_storage = "../../environment/frontend_server/temp_storage"

collision_block_id = "32125"

# Verbose 
debug = True
```

- 安装依赖

```shell
conda create --name generative-agent python=3.9
conda activate generative-agent
pip install  -r requirements.txt
```

- 启动Django服务器

切换到`environment/frontend_server`目录，运行`manage.py`文件

```shell
cd ./environment/frontend_server
python manage.py
```

- 复制下面的链接到浏览器。

`http://localhost:8000/demo/July1_the_ville_isabella_maria_klaus-step-3-20/2400/300/`

## <img src="https://joonsungpark.s3.amazonaws.com:443/static/assets/characters/profile/Isabella_Rodriguez.png" alt="Generative Isabella">   设置环境步骤

To set up your environment, you will need to generate a `utils.py` file that contains your OpenAI API key and download the necessary packages.

要设置您的环境，您需要生成一个名为 `utils.py` 的文件，其中包含您的 OpenAI API 密钥，并下载必要的软件包。

### Step 1. 生成这个文件

在位于 `reverie/backend_server` 文件夹中（包含 `reverie.py` 的位置），创建一个名为 `utils.py` 的新文件，并将下面的内容复制粘贴到文件中：
```
# Copy and paste your OpenAI API Key
openai_api_key = "<Your OpenAI API>"
# Put your name
key_owner = "<Name>"

maze_assets_loc = "../../environment/frontend_server/static_dirs/assets"
env_matrix = f"{maze_assets_loc}/the_ville/matrix"
env_visuals = f"{maze_assets_loc}/the_ville/visuals"

fs_storage = "../../environment/frontend_server/storage"
fs_temp_storage = "../../environment/frontend_server/temp_storage"

collision_block_id = "32125"

# Verbose 
debug = True
```
请将 `<Your OpenAI API>` 替换为您的 OpenAI API 密钥，将 `<name>` 替换为您的名字。

### Step 2. Install requirements.txt

Install everything listed in the `requirements.txt` file (I strongly recommend first setting up a virtualenv as usual). A note on Python version: we tested our environment on Python 3.9.12. 

## <img src="https://joonsungpark.s3.amazonaws.com:443/static/assets/characters/profile/Klaus_Mueller.png" alt="Generative Klaus">   运行模拟

要运行新的模拟，您需要同时启动两个服务器：环境服务器和代理模拟服务器。

### Step 1. 启动环境服务器

再次强调，环境是作为一个 Django 项目实现的，因此您需要启动 Django 服务器。要做到这一点，首先在命令行中导航到 `environment/frontend_server` 目录（这是 `manage.py` 所在的位置）。然后运行以下命令：

    python manage.py runserver

然后，在您喜欢的浏览器中，访问 [http://localhost:8000/](http://localhost:8000/)。如果您看到一条消息，上面写着 "Your environment server is up and running"，则表示您的服务器正在正常运行。确保在运行模拟时环境服务器继续运行，因此保持这个命令行标签页保持打开状态！（注意：我建议使用 Chrome 或 Safari 浏览器。Firefox 可能会产生一些前端问题，尽管它不应该影响实际的模拟。）

### Step 2. 启动模拟服务器

打开另一个命令行窗口（您在步骤1中使用的命令行窗口应该仍在运行环境服务器，所以保持它不变）。导航到 `reverie/backend_server` 目录并运行 `reverie.py`。

    python reverie.py
这将启动模拟服务器。一个命令行提示将出现，询问以下内容：“Enter the name of the forked simulation: ”。要启动一个带有 Isabella Rodriguez、Maria Lopez 和 Klaus Mueller 的 3 个代理的模拟，请输入以下内容：
    
    base_the_ville_isabella_maria_klaus
然后提示会询问：“Enter the name of the new simulation: ”。键入任何名称以表示您当前的模拟（例如，只需输入 "test-simulation"）。

> 这里其实输入什么名称都可以。

    test-simulation
保持模拟服务器运行。在这个阶段，它将显示以下提示：“Enter option: ”。

然后接下来你可以输入下面的步骤，也就是`run step`。

### Step 3.  运行并保存模拟

在您的浏览器中，导航到 [http://localhost:8000/simulator_home](http://localhost:8000/simulator_home)。您应该会看到 Smallville 的地图，以及地图上活动代理的列表。您可以使用键盘箭头在地图上移动。请保持这个标签页打开。要运行模拟，请在模拟服务器上回应提示 “Enter option” 时，输入以下命令：

    run <step-count>
请注意，您需要在上述命令中将 `<step-count>` 替换为一个整数，以表示您想要模拟的游戏步数。例如，如果您想模拟100个游戏步骤，您应该输入 `run 100`。一个游戏步骤代表游戏中的10秒时间。

您的模拟应该正在运行，您将会在浏览器中看到代理在地图上移动。一旦模拟运行结束，"Enter option" 提示会再次出现。此时，您可以通过重新输入带有所需游戏步数的运行命令来模拟更多步骤，通过输入 `exit` 来退出不保存模拟，或者通过输入 `fin` 来保存并退出。

保存的模拟可以在下次运行模拟服务器时通过提供您的模拟名称作为 forked simulation 来访问。这将允许您从离开的地方重新启动模拟。

### Step 4. 重播模拟

要重新播放您已经运行过的模拟，只需确保您的环境服务器正在运行，并在浏览器中导航到以下地址：`http://localhost:8000/replay/<simulation-name>/<starting-time-step>`。请务必将 `<simulation-name>` 替换为您要重播的模拟名称，将 `<starting-time-step>` 替换为您希望从哪个整数时间步开始重播。

例如，通过访问以下链接，您将启动一个预先模拟的示例，从时间步1开始：
[http://localhost:8000/replay/July1_the_ville_isabella_maria_klaus-step-3-20/1/](http://localhost:8000/replay/July1_the_ville_isabella_maria_klaus-step-3-20/1/)

### Step 5. 演示模拟

您可能已经注意到，重播中的所有角色精灵看起来都是相同的。我们想澄清的是，重播功能主要用于调试目的，并不优先考虑优化模拟文件夹的大小或可视化效果。要正确展示带有适当角色精灵的模拟，您需要首先压缩模拟。要做到这一点，使用文本编辑器打开位于 `reverie` 目录中的 `compress_sim_storage.py` 文件。然后，执行 `compress` 函数，并将目标模拟的名称作为输入。通过这样做，模拟文件将被压缩，使其准备好用于演示。

要开始演示，请在浏览器中输入以下地址：`http://localhost:8000/demo/<simulation-name>/<starting-time-step>/<simulation-speed>`。注意， `<simulation-name>` 和 `<starting-time-step>` 与上述提到的内容相同。 `<simulation-speed>` 可以设置以控制演示速度，其中 1 是最慢的，5 是最快的。例如，访问以下链接将启动一个预先模拟的示例，从时间步1开始，演示速度为中等：  
[http://localhost:8000/demo/July1_the_ville_isabella_maria_klaus-step-3-20/1/3/](http://localhost:8000/demo/July1_the_ville_isabella_maria_klaus-step-3-20/1/3/)

### Tips
我们注意到当 OpenAI API 达到每小时请求限制时，可能会出现卡顿的情况。当出现这种情况时，您可能需要重新启动您的模拟。目前，我们建议您在进行模拟时经常保存，以确保在需要停止和重新运行模拟时损失尽量少的模拟数据。截至 2023 年初，运行这些模拟可能会比较昂贵，尤其是当环境中有许多代理时。

## <img src="https://joonsungpark.s3.amazonaws.com:443/static/assets/characters/profile/Maria_Lopez.png" alt="Generative Maria">   模拟存储位置

您保存的所有模拟将位于 `environment/frontend_server/storage` 文件夹中，而所有压缩的演示将位于 `environment/frontend_server/compressed_storage` 文件夹中。

## <img src="https://joonsungpark.s3.amazonaws.com:443/static/assets/characters/profile/Eddy_Lin.png" alt="Generative Eddy">   Authors and Citation

**Authors:** Joon Sung Park, Joseph C. O'Brien, Carrie J. Cai, Meredith Ringel Morris, Percy Liang, Michael S. Bernstein

Please cite our paper if you use the code or data in this repository. 
```
@inproceedings{Park2023GenerativeAgents,  
author = {Park, Joon Sung and O'Brien, Joseph C. and Cai, Carrie J. and Morris, Meredith Ringel and Liang, Percy and Bernstein, Michael S.},  
title = {Generative Agents: Interactive Simulacra of Human Behavior},  
year = {2023},  
publisher = {Association for Computing Machinery},  
address = {New York, NY, USA},  
booktitle = {In the 36th Annual ACM Symposium on User Interface Software and Technology (UIST '23)},  
keywords = {Human-AI interaction, agents, generative AI, large language models},  
location = {San Francisco, CA, USA},  
series = {UIST '23}
}
```

