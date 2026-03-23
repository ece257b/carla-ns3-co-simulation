# Cross Evaluation Report

**Project Title:** CARLA-NS3 Co-Simulation for V2X Communication Research
**Authors:** Heorhi Davydau, Tianqi (potatofried02)

## 1. Documentation

Is the artifact/code sufficiently documented? Rate from 0% to 100%, where 0% means **"documentation is completely insufficient"** and 100% means **"documentation is absolutely sufficient"**.

If you need to assess both a dataset and tools, please take the average and comment below. In assessing tools, please consider whether they are easy or difficult to install, set up, and run. In assessing datasets, please consider whether the metadata is sufficient.

**Choices:**

- [ ] 0%
- [ ] 20%
- [ ] 40%
- [ ] 60%
- [x] 80%
- [ ] 100%

**Documentation — Comment on/explain your choice above:**
The README is well-structured and genuinely useful: it clearly states system requirements (Ubuntu 22.04, GPU VRAM, disk space), walks through a three-phase installation process (CARLA, NS3, Python environment), and provides step-by-step execution instructions for both the main simulation and the brake validation test. The `config/settings.py` file documents key parameters including CARLA connection settings, map selections, and coordinate boundaries, making configuration straightforward. The four preset scenarios in `run_simulation.sh` are self-explanatory and easy to use. The main areas that bring this short of a full score are the absence of a high-level project overview or research motivation, no architecture diagram explaining how the three components (bridge, NS3 module, Python orchestrator) interact, and limited inline comments within the source code itself. A brief conceptual section in the README and some module-level docstrings would make this substantially more accessible to new users.

## 2. Completeness

Do the submitted artifacts/code include all of the key components described in the report? Rate from 0% to 100%, where 0% means **"does not include any key components"** and 100% means **"includes all key components"**.

**Choices:**

- [ ] 0%
- [ ] 20%
- [ ] 40%
- [ ] 60%
- [x] 80%
- [ ] 100%

**Completeness — Comment on/explain your choice above:**
The repository includes the major components needed for the co-simulation: the CARLA-NS3 bridge (`src/bridge/carla_ns3_bridge.py`) with lock-step synchronization, the NS3 VANET module in C++ with CAM sender/receiver applications, GeoNetworking headers, three propagation regimes, and brake-warning detection. The safety evaluation module (`src/common/safety_eval.py`) covers collision detection, TTC metrics, and inter-vehicle distance tracking. Visualization utilities produce trajectory plots, speed/heading graphs, and video recordings. Map assets for Town10 and Town07 are included. The main gap is that two installation scripts referenced in the README — `install_ns3.sh` and `installdependencies.sh` — are not present in the repository (404 errors), which puts some burden on the user to infer the NS3 build process. Including those scripts or folding their contents into the README would make this essentially complete.

## 3. Exercisability

Do the submitted artifacts/code include the scripts and data needed to run the experiments described in the paper, and can the software be successfully executed? Rate from 0% to 100%, where 0% means **"the scripts/software cannot be successfully executed and/or no data is included"** and 100% means **"the artifact includes all necessary scripts/software and data, and scripts/software (if present) can be successfully executed"**.

**Choices:**

- [ ] 0%
- [ ] 20%
- [ ] 40%
- [x] 60%
- [ ] 80%
- [ ] 100%

**Exercisability — Comment on/explain your choice above:**
Once the environment is set up, the simulation is easy to run: `run_simulation.sh` provides four ready-to-use preset scenarios, `main.py` exposes clean command-line arguments, and `requirements.frozen.txt` pins exact Python dependency versions to aid reproducibility. The brake validation test is a nice touch for sanity-checking the core physics behavior. The main friction is at the setup stage — the missing `install_ns3.sh` and `installdependencies.sh` scripts mean users have to piece together the NS3 build process independently, which is non-trivial. The system also requires coordinating three separate processes (CARLA server, NS3, Python orchestrator) in sequence, and a bit more documentation on that launch procedure would help. No pre-generated sample output is included to confirm a successful run without full hardware.

## 4. Results Attainable

Does the artifact/code make it possible, with reasonable effort, to obtain the key results from the artifact/code? Rate from 0% to 100%, where 0% means **"no results can be obtained"** and 100% means **"all results can be obtained"**.

**Choices:**

- [ ] 0%
- [ ] 20%
- [ ] 40%
- [ ] 60%
- [x] 80%
- [ ] 100%

**Results Attainable — Comment on/explain your choice above:**
For a reviewer with the required hardware and a working environment, the four preset scenarios produce a clear set of outputs: JSON vehicle telemetry logs, PCAP network captures, safety evaluation summaries (`v2x_eval_summary.json`), and PDF visualizations — all of which directly support the core comparisons between baseline, sensor-only, 802.11p, and 5G V2X modes. The safety metrics (TTC, collision rate, minimum inter-vehicle distance) are the central quantitative results and the code to generate them is present and well-organized. The main limitations are the hardware requirement (NVIDIA GPU with 6–8 GB VRAM), the setup friction from missing install scripts, and the lack of random seed control for the stochastic network components, which may introduce run-to-run variation. Including a small set of example output files would give reviewers a clear target to validate against.

## 5. Results Completeness

How many key results of the paper/report is the provided code meant to support? Rate from 0% to 100%, where 0% means **"the artifact is meant to support no key results"** and 100% means **"the artifact is meant to support all key results"**.

**Choices:**

- [ ] 0%
- [ ] 20%
- [ ] 40%
- [ ] 60%
- [x] 80%
- [ ] 100%

**Results Completeness — Comment on/explain your choice above:**
The codebase is well-aligned with the project's core research questions: the four preset scenarios cover the key independent variables (speed, following distance, communication method), and the safety evaluation module produces the central dependent metrics. The lock-step synchronization, propagation regime parameterization, and CAM protocol implementation are all present and tied to the experimental design. The code is scoped to a single leader-follower pair, so results for larger platoons or multi-hop routing scenarios are not directly supported, and there is no comparison against real-world field data. These appear to be intentional scope decisions rather than missing artifacts, and the code covers the primary claims of the report well.

## Signatures

- Reviewer Akshat Gupta, Signature: ___________________
- Reviewer Luke Wilson, Signature: ___________________
