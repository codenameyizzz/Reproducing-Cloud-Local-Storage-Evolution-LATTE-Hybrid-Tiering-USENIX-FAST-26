# Chameleon Cloud Trovi Artifact: Reproducing USENIX FAST '26 LATTE & Q-LATTE

This experimental artifact is specifically tailored for the **Trovi portal on Chameleon Cloud** ([trovi.chameleoncloud.org](https://trovi.chameleoncloud.org/)), following the exact *Experiment Pattern* structure of referenced artifacts (e.g., [`a1af42d2-b517-4fd3-8044-661c2f2c1992`](https://trovi.chameleoncloud.org/dashboard/artifacts/a1af42d2-b517-4fd3-8044-661c2f2c1992)).

---

## 1. Directory Structure

```
trovi_artifact/
├── FAST26_LATTE_Chameleon_Reproduction.ipynb  <-- Master Self-Contained Notebook
├── trovi_metadata.json                        <-- Trovi publication metadata
├── README.md                                  <-- This guide
├── scripts/
│   ├── setup_spdk_csal.sh                     <-- Bare-metal environment setup
│   ├── setup_ebs_nvmeof.sh                    <-- NVMe-oF target EBS emulation
│   ├── run_all_benchmarks.sh                  <-- Automated benchmark runner
│   └── fio_workloads.fio                      <-- Standardized FIO workloads
└── src/
    ├── ml_dispatcher.py                       <-- Linear-SVM & Two-Tier Dispatcher
    └── t_bfac_qos.py                          <-- Multi-Tenant Token-Bucket QoS
```

---

## 2. Authentication & Credentials on Chameleon Cloud

> **SECURITY NOTE:**  
> **You do NOT need to share your Chameleon Cloud credentials, private keys, or passwords.**

Chameleon Cloud features native, integrated session authentication:
1. **Running on Chameleon JupyterHub ([jupyter.chameleoncloud.org](https://jupyter.chameleoncloud.org/)):**
   - Logging in to JupyterHub automatically authenticates your session.
   - The `python-chi` library inherits your pre-authenticated session.
   - Simply configure your Chameleon project allocation name (e.g., `CHI-240123`) in the notebook:
     ```python
     CHAMELEON_PROJECT_NAME = "YOUR_PROJECT_NAME"
     ```
2. **Flexible Execution Modes:**
   - **Standalone Emulation Mode (Default):** `ENABLE_BAREMETAL_PROVISIONING = False`. Runs directly on JupyterHub without leasing a physical node, consuming zero allocation hours.
   - **Full Bare-Metal Mode:** `ENABLE_BAREMETAL_PROVISIONING = True`. Automatically provisions an NVMe-equipped physical node (`compute_cascadelake` at CHI@UC) via `python-chi`.

---

## 3. How to Run on Chameleon Cloud JupyterHub

1. Open [jupyter.chameleoncloud.org](https://jupyter.chameleoncloud.org/) and log in.
2. Upload the single file `FAST26_LATTE_Chameleon_Reproduction.ipynb`.
3. Open the notebook and select **Kernel** $\rightarrow$ **Restart Kernel and Run All Cells**.
4. The notebook will sequentially execute the microbenchmarks, ML dispatcher tests, cache hit-rate evaluations, and multi-tenant QoS simulations.

---

## 4. How to Publish on Trovi

To make your artifact permanently available with an interactive **Launch on Chameleon** button:
1. Push your repository to GitHub.
2. Go to [trovi.chameleoncloud.org](https://trovi.chameleoncloud.org/).
3. Click **Import Artifact** $\rightarrow$ select **Git Repository**.
4. Paste your GitHub repository URL.
5. Trovi will parse `trovi_metadata.json` automatically and generate your public artifact page!
