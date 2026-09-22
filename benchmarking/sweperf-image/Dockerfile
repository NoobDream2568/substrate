# Task image for the substrate sweperf workload (template swebench-astropy-7336).
# Base: official SWE-bench eval image for instance astropy__astropy-7336 (multi-GB,
# Docker Hub). replay.py + astropy_trace.json are vendored from
# https://github.com/gke-labs/sweperf (generate-images/) plus the trajectory of run
# 20251120_livesweagent_gemini-3-pro-preview (dataset
# livesweagent/gemini_3_pro_swebench_verified_traj on Hugging Face), reduced to its
# 21 bash commands by generate.py's extract_commands. replay.py serves
# /status + /execute on :80, which is what the boomer sweperf client drives.
FROM swebench/sweb.eval.x86_64.astropy_1776_astropy-7336:latest
RUN if command -v pip >/dev/null 2>&1; then pip install pexpect; else apt-get update && apt-get install -y python3-pexpect; fi
RUN mkdir -p /opt/swebench
COPY replay.py /opt/swebench/replay.py
COPY astropy_trace.json /opt/swebench/astropy_trace.json
ENTRYPOINT ["python3", "/opt/swebench/replay.py", "/opt/swebench/astropy_trace.json"]
