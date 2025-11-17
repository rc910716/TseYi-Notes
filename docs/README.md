## <span id="tseyi-notes--学习笔记合集✒️">TseYi-Notes ｜ 学习笔记合集✒️</span>

> Record end-to-end learning journeys across data science, machine learning and AI.
> 系统整理数据科学、机器学习与人工智能的学习路径、课堂笔记与实战练习。

- This repo is maintained as an Obsidian-friendly knowledge base, and you are very welcome to **fork and adapt it for your own learning notes**.
  - 本仓库以 Obsidian 为核心编辑工作流，欢迎大家 **fork 并按需改造**，用于搭建自己的学习笔记体系。
- This site is generated with **docsify**, so every Markdown file under `docs/` stays lightweight and instantly refreshes when updated.
  - 本站采用 docsify 搭建，`docs/` 下的 Markdown 会实时渲染，适合快速迭代与预览。

---

**Repo ｜ 项目仓库**：<https://github.com/FuTseYi/TseYi-Notes>

**Online reading ｜ 在线预览**：<https://edu.xieyi.org>

---

### <span id="table-of-contents--目录">Table of Contents ｜ 目录</span>

- [TseYi-Notes ｜ 学习笔记合集✒️](#tseyi-notes--学习笔记合集️)
  - [Table of Contents ｜ 目录](#table-of-contents--目录)
  - [Project Overview ｜ 项目简介](#project-overview--项目简介)
  - [Key Highlights ｜ 项目亮点](#key-highlights--项目亮点)
  - [Repository Structure ｜ 仓库结构](#repository-structure--仓库结构)
  - [Learning Materials ｜ 学习资料来源](#learning-materials--学习资料来源)
  - [Environment Setup ｜ 环境配置](#environment-setup--环境配置)
    - [A. Docs-only Preview ｜ 仅阅读模式](#a-docs-only-preview--仅阅读模式)
    - [B. Full Notebook Environment ｜ 完整运行环境](#b-full-notebook-environment--完整运行环境)
    - [C. Obsidian Workspace ｜ Obsidian 工作流](#c-obsidian-workspace--obsidian-工作流)
  - [Usage Guide ｜ 使用指南](#usage-guide--使用指南)
  - [Contribution ｜ 贡献指南](#contribution--贡献指南)
  - [License \& Citation ｜ 许可证与引用](#license--citation--许可证与引用)

---

### <span id="project-overview--项目简介">Project Overview ｜ 项目简介</span>

**EN**
TseYi Notes gathers multi-stage study notes, hands-on notebooks, and curated references from long-term learning programs (Datawhale, Stanford CS224W, MetaGPT, etc.). It aims to help self-learners quickly locate trustworthy materials, reproduce experiments, and internalize methodologies. The docs site is rendered by docsify from the `docs/` directory, and the project is maintained together with an Obsidian vault so that all Markdown notes in `docs/` and `notebook/` can be organized, searched and edited efficiently.

**CN**
TseYi Notes 汇集了多期组队学习、课程实战与自学整理的资料，涵盖数据分析、NLP、CV、图学习、推荐系统、可解释性与多智能体等方向。站点基于 docsify 渲染 `docs/` 目录，项目同时配套使用 Obsidian 进行管理，便于对 `docs/` 与 `notebook/` 中的 Markdown 笔记进行统一整理、检索与编辑，希望通过结构化的文档帮助学习者快速搭建知识网络、复现实验并形成自己的方法论。

### <span id="key-highlights--项目亮点">Key Highlights ｜ 项目亮点</span>

- **Curated Tracks 精选学习路径**：覆盖 20+ 期 Datawhale 课程与扩展专题，内容体系完整。
- **Docs + Notebooks 双形态**：`docs/` 适合在线阅读；`notebook/` 提供可运行的 Jupyter 实验。
- **Tooling Ready 工具化支撑**：附带 requirements、常用脚本与 Neo4j、PyTorch Geometric 等环境说明。
- **Continuous Expansion 持续扩展**：以「学习路线 → 实战项目 → 知识库」的节奏迭代更新。

### <span id="repository-structure--仓库结构">Repository Structure ｜ 仓库结构</span>

```bash
docs/                         文档化的学习笔记与项目说明
notebook/                     Jupyter Notebook 形式的实战记录
  pandas20/                   第20期 Pandas 课程
  knowledge_graph_basic21/    第21期 知识图谱实践
  ensemble_learning23-25/     第23-25期 集成学习
  gnn_learning26/             第26期 图神经网络
  pumpkin_learning27/         第27期 吃瓜课程（西瓜书+南瓜书）
  transformers_nlp28/         第28期 Transformers NLP
  matplotlib_learning29/      第29期 数据可视化
  tree_ensemble30/            第30期 树模型与集成学习
  unusual_deep_learning31/    第31期 深度学习专题
  recommender_system32/       第32期 推荐系统
  pytorch_learning35/         第35期 深入浅出 PyTorch
  lee_ml37/                   第37期 李宏毅机器学习
  pytorch_rechub_learning38/  第38期 推荐模型复现
  intel_openvino_learning39/40 Intel OpenVINO 初/高阶
  interpretable_ml44/         第44期 可解释性机器学习
  cs224w_learning46/          第46期 CS224W 图机器学习
  diffusion_model_learning51/ 第51期 扩散模型
  metagpt_learning55/         第55期 多智能体
  happyllm_learning202506/    2025.06 Happy-LLM 学习
QASystemOnMedicalGraph/       医疗知识图谱问答系统源码
requirements.txt              Conda 依赖快照
```

### <span id="learning-materials--学习资料来源">Learning Materials ｜ 学习资料来源</span>

对应的课程/资料入口如下，建议结合官方仓库使用：

1. [第20期 Pandas（Joyful Pandas）](https://datawhalechina.github.io/joyful-pandas)
2. [第21期 知识图谱基础](https://github.com/datawhalechina/team-learning-nlp/tree/master/KnowledgeGraph_Basic)
3. [医疗领域知识图谱问答系统](https://github.com/zhihao-chen/QASystemOnMedicalGraph)
4. [第23-25期 集成学习](https://github.com/datawhalechina/team-learning-data-mining/tree/master/EnsembleLearning)
5. [第26期 图神经网络](https://github.com/datawhalechina/team-learning-nlp/tree/master/GNN)
6. [第27期 吃瓜教程](https://www.bilibili.com/video/BV1Mh411e7VU)
7. [第28期 Transformers NLP](https://github.com/datawhalechina/learn-nlp-with-transformers)
8. [第29期 Matplotlib](https://github.com/datawhalechina/fantastic-matplotlib)
9. [Matplotlib 50 题实战](https://www.heywhale.com/mw/notebook/5ec2336f693a730037a4415c)
10. [第30期 树模型与集成学习](https://datawhalechina.github.io/machine-learning-toy-code/)
11. [第31期 深度学习专题](https://datawhalechina.github.io/unusual-deep-learning)
12. [第32期 推荐系统](https://github.com/datawhalechina/fun-rec)
13. [第35期 深入浅出 PyTorch](https://github.com/datawhalechina/thorough-pytorch)
14. [第37期 李宏毅机器学习](https://github.com/datawhalechina/leeml-notes)
15. [第38期 Rechub 推荐模型复现](https://www.wolai.com/rechub/2qjdg3DPy1179e1vpcHZQC)
16. [OpenVINO CV Beginner](https://vxr.h5.xeknow.com/s/3Eg4J8)
17. [OpenVINO CV Advanced](https://vxr.h5.xeknow.com/s/204VNE)
18. [可解释性机器学习｜同济子豪兄](https://datawhaler.feishu.cn/docx/OTROd2zCIoZlLyxjhSKclxKNnDe)
19. [CS224W 图机器学习｜同济子豪兄](https://github.com/TommyZihao/zihao_course/tree/main/CS224W)
20. [Hugging Face Diffusion Models](https://github.com/huggingface/diffusion-models-class)
21. [MetaGPT 0.6.6 多智能体实战](https://deepwisdom.feishu.cn/wiki/MLILw0EdRiyiYRkJLgOcskyAnUh)
22. [MetaGPT 开源项目](https://github.com/geekan/MetaGPT/)
23. [Happy-LLM](https://github.com/datawhalechina/happy-llm.git)

### <span id="environment-setup--环境配置">Environment Setup ｜ 环境配置</span>

#### <span id="a-docs-only-preview--仅阅读模式">A. Docs-only Preview ｜ 仅阅读模式</span>

1. Install docsify-cli ｜ 安装 docsify-cli

   ```shell
   npm install docsify-cli -g
   ```

2. Local preview ｜ 本地预览

   ```shell
   docsify serve ./docs
   ```

   Open `http://localhost:3000` to browse the documentation.

#### <span id="b-full-notebook-environment--完整运行环境">B. Full Notebook Environment ｜ 完整运行环境</span>

- **Python**: 3.10 (Windows)
- **Install dependencies ｜ 安装依赖**

  ```shell
  conda install --yes --file requirements.txt
  ```

- **PyTorch (CUDA 12.1)**

  ```shell
  pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
  ```

- **PyTorch Geometric**

  ```shell
  conda install pytorch-geometric -c rusty1s -c conda-forge
  ```

- **Ray Tune**

  ```shell
  conda install ray-tune -c conda-forge
  ```

- **Neo4j (optional ｜ 可选)**
  - [Windows10 安装指南](https://blog.csdn.net/lihuaqinqwe/article/details/80314895)
  - JDK 1.8 对应 [Neo4j 3.5.26 下载](https://go.neo4j.com/download-thanks.html?edition=community&release=3.5.26&flavour=winzip&_gl=1*cfbj98*_ga*MjIzOTA4ODkzLjE2MTAyOTEzODU.*_ga_DL38Q8KGQC*MTYxMDI5MTM4NS4xLjEuMTYxMDI5NDI0NS4w&_ga=2.141402866.1342715293.1610291386-223908893.1610291385)

Tips ｜ 小贴士：

使用 `conda list -e > requirements.txt` 可导出当前环境，便于协作者同步。

#### <span id="c-obsidian-workspace--obsidian-工作流">C. Obsidian Workspace ｜ Obsidian 工作流</span>

1. **Install Obsidian ｜ 安装 Obsidian**：前往 <https://obsidian.md> 下载桌面版本。
2. **Open vault ｜ 打开仓库**：在 Obsidian 中选择 “Open folder as vault”，指向本仓库根目录（推荐 `TseYi-Notes/`）。
3. **Folder mapping ｜ 目录映射**：将 `docs/` 与 `notebook/` 加入左侧收藏，便于快速检索双语笔记。
4. **Plugins ｜ 插件配置（节选）**
   本仓库已经在 `.obsidian/plugins/` 中预配置了一些常用插件，克隆后可直接作为 Obsidian 工作区使用：
   - `latex-suite`：用于更友好的 LaTeX 渲染；
   - `Advanced Tables`：优化 Markdown 表格编辑体验；
   - `Templater` / `templater-obsidian`：基于模板快速插入学习笔记或实验记录；
   - `obsidian-git`：将笔记变更与 GitHub 同步，方便版本管理与多端协作；
   - `obsidian-linter`：统一 Markdown 格式与 Frontmatter 书写风格；
   - `file-tree-alternative`：增强文件树视图，方便在 `docs/` 与 `notebook/` 间切换；
   - `obsidian-image-auto-upload-plugin` / `media-extended` / `pdf-plus`：优化图片、音视频与 PDF 的插入和预览体验；
   - `recent-files-obsidian` / `editing-toolbar`：提升常用文件访问与基础编辑效率；
   - 其他插件（如 `obsidian-excalidraw-plugin`、`number-headings-obsidian` 等）则用于辅助绘图、自动编号与排版细节。
   如需完整列表，可直接查看 `.obsidian/plugins/` 目录。
5. **Sync tips ｜ 同步提示**：Obsidian 仅作为编辑器，请继续通过 Git 进行版本管理，避免与 `docsify` 输出目录发生混淆。

### <span id="usage-guide--使用指南">Usage Guide ｜ 使用指南</span>

1. **Clone 仓库**

   ```shell
   git clone https://github.com/FuTseYi/TseYi-Notes.git
   cd TseYi-Notes
   ```

2. **Docs 模式**：执行 `docsify serve ./docs`。
3. **Notebook 模式**：激活 Conda 环境后在 `notebook/` 中打开对应 `.ipynb` 文件。
4. **知识图谱示例**：进入 `QASystemOnMedicalGraph/`，参考子目录 README 完成 Neo4j、Flask 或前端部署。

### <span id="contribution--贡献指南">Contribution ｜ 贡献指南</span>

- 欢迎提交 Issue 分享勘误、补充学习资料或提出改进建议。
- 提交 PR 时请：
  1. 新建分支并保持提交原子化；
  2. 更新相应的中英文文档；
  3. 附带必要的截图、运行日志或测试说明。
- 建议遵循 Git 提交信息格式：`feat: 添加 XXX 笔记` / `docs: 更新 README`.

### <span id="license-and-citation--许可证与引用">License & Citation ｜ 许可证与引用</span>

- 本仓库采用 MIT License，已在根目录提供 `LICENSE` 文件。
- 如引用本仓库内容，请注明来源：`TseYi-Notes (https://github.com/FuTseYi/TseYi-Notes)`。

---

若在使用或部署过程中遇到问题，欢迎通过 Issues 或邮件联系。Thanks for reading & happy learning! 学习愉快，持续精进！ 🚀
