<div align="center">

<h1>EPoG: Integrated Exploration and Sequential Manipulation on Scene Graph with LLM-based Situated Replanning</h1>

<div>
    <a href='https://scholar.google.com' target='_blank'>Heqing Yang</a><sup>1,2</sup>&emsp;
    <a href='https://scholar.google.com' target='_blank'>Ziyuan Jiao</a><sup>1,2</sup>&emsp;
    <a href='https://scholar.google.com' target='_blank'>Shu Wang</a><sup>3</sup>&emsp;
    <a href='https://scholar.google.com' target='_blank'>Yida Niu</a><sup>4</sup>&emsp;
    <a href='https://scholar.google.com' target='_blank'>Si Liu</a><sup>1</sup>&emsp;
    <a href='https://scholar.google.com' target='_blank'>Hangxin Liu</a><sup>2</sup>
</div>
<div>
    <sup>1</sup>Beihang University
    <sup>2</sup>State Key Laboratory of General Artificial Intelligence, BIGAI, Beijing, China.
    <sup>3</sup>University of California, Los Angeles.
    <sup>4</sup>Institute for Artificial Intelligence, Peking University.
</div>

<div>
    <strong>ICRA 2026</strong>
</div>

<div>
    <h4 align="center">
        <a href="https://arxiv.org/abs/2602.04419" target='_blank'>
        <img src="https://img.shields.io/badge/arXiv-2602.04419-b31b1b.svg">
        </a>
        <a href="URL_HERE" target='_blank'>
        <img src="https://img.shields.io/badge/Project-Page-green">
        </a>
        <a href="#-citation" target='_blank'>
        <img src="https://img.shields.io/badge/Cite-BibTeX-blue">
        </a>
    </h4>
</div>

<strong>EPoG integrates graph-based global planning with LLM-based situated replanning on scene graphs, seamlessly combining exploration and sequential manipulation for long-horizon robotic tasks in partially known environments.</strong>

<div style="text-align:center">
<img src="assets/structure.png"  width="100%" height="100%">
</div>

---

</div>

## 📢 News

* **[2026-02]** 🔥 EPoG paper is accepted by ICRA 2026.
* **[2026-02]** 🚀 Code and evaluation scripts are open-sourced.

## 💡 Highlights

* **Integrated Exploration & Manipulation**. EPoG naturally combines exploration and sequential manipulation planning on scene graphs, reducing total execution effort.
* **LLM-based Belief Graph Estimation**. Leverages LLM commonsense knowledge to estimate unknown object locations, enabling planning before full exploration.
* **Situated Replanning**. Handles motion planning exceptions (blocking, collision, inaccessibility, instability) through LLM-guided recovery actions.
* **State-of-the-Art Performance**. Achieved 91.3% success rate with 36.1% reduction in travel distance across 46 realistic household scenes.

## 🛠️ Usage

### Installation

We recommend using `uv` for environment management:

```bash
git clone git@github.com:buaa-colalab/Guidelines.git
cd epog

# Install with uv (recommended)
uv sync

# Or install with pip
pip install -e .
```

### Data Preparation

We evaluate on 5 long-horizon daily object transportation tasks across 46 household scenes from the [ProcThor-10k](https://procthor.allenai.org/) dataset:

| Task | # Scenes | Goals |
|------|----------|-------|
| Breakfast Preparation | 10 | apple on plate, bread on plate, fork on plate, plate on diningtable |
| Bedroom Work | 10 | alarmclock on desk, CD on desk, laptop on desk, pencil on desk |
| Movie & Snack Preparation | 10 | remotecontrol on sofa, bread on plate, plate on diningtable |
| Tea Making & Relaxation | 10 | kettle on countertop, cup on diningtable, remotecontrol on sofa |
| Bath Preparation | 6 | soapbottle on faucet, cloth on faucet |

To generate the benchmark dataset:

```bash
uv run python epog/data_gen/task_proc_scene.py
```

To visualize scene graphs (`*.gexf` files), use [Gephi](https://gephi.org/).

### Model Preparation

Set your OpenAI API key:

```bash
export OPENAI_API_KEY="your-key-here"
```

### Training

This project is a planning-based framework and does not require training.

### Evaluation

```bash
# EPoG (Ours) - Full framework with LLM-based belief estimation and local replanning
uv run python epog/evaluation/eval.py --algorithm_name EPoG

# EFS - Exploration-First Search baseline
uv run python epog/evaluation/eval.py --algorithm_name EFS

# LLM+Explore - Exploration followed by LLM planning
uv run python epog/evaluation/eval.py --algorithm_name "LLM+Explore"

# LLM Pure - Pure LLM-based planning
uv run python epog/evaluation/eval.py --algorithm_name LLM_Pure
```

**Command Line Arguments:**

| Argument | Default | Description |
|----------|---------|-------------|
| `--algorithm_name` | `LLM_Pure` | Algorithm to evaluate: `EPoG`, `EFS`, `LLM+Explore`, `LLM_Pure` |
| `--data_root_dir` | `data/task` | Root directory for task data |
| `--work_dir` | `work_dir` | Output directory for results |

## 📝 Citation

If you find this work useful, please consider citing our paper:

```bibtex
@inproceedings{yang2026epog,
  title={Integrated Exploration and Sequential Manipulation on Scene Graph with LLM-based Situated Replanning},
  author={Yang, Heqing and Jiao, Ziyuan and Wang, Shu and Niu, Yida and Liu, Si and Liu, Hangxin},
  booktitle={IEEE International Conference on Robotics and Automation (ICRA)},
  year={2026}
}
```

## 📄 License

See [LICENSE](./LICENSE) for more information.

## 🙏 Acknowledgement

This work builds upon several open-source projects:
- [AI2-THOR](https://ai2thor.allenai.org/) for the simulation environment
- [ProcThor-10k](https://procthor.allenai.org/) for procedurally generated household scenes
- [NetworkX](https://networkx.org/) for graph algorithms
