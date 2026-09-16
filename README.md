# CSCE-765-HW1
This README documents the setup used for the OpenClaw agent security experiments.

---

## 1. Virtual Machine Setup

The homework was performed inside an Ubuntu 24.04 LTS x86-64 virtual machine using VirtualBox.

VM configuration:

- OS: Ubuntu 24.04 LTS
- Architecture: x86-64
- CPU: 4 vCPUs
- RAM: 4 GB
- Network: NAT

Check the architecture:
- uname -m

check the network:
- ip -brief address
- ip route

## 2. Openclaw installation

- npm install -g openclaw@2026.7.1-2 
- openclaw --version 

## 3. run local proxy for openclaw to call tamuAPI

- export TAMU_API_KEY="<YOUR_TAMU_API_KEY>"
- node tamu-shim.mjs
- The shim runs locally at: http://127.0.0.1:8899

## 4. Start openclaw gateway

- openclaw daemon install
- openclaw daemon start
- openclaw gateway status ----this should show as running

## 5. configure Openclaw 
- openclaw onboard --non-interactive \
  --accept-risk \
  --auth-choice custom-api-key \
  --custom-provider-id tamus \
  --custom-compatibility openai \
  --custom-base-url "http://127.0.0.1:8899/openai" \
  --custom-api-key via-shim \
  --custom-model-id "protected.gpt-4o" \
  --skip-channels

- openclaw config set models.providers.tamus.request.allowPrivateNetwork true
- openclaw config set agents.defaults.timeoutSeconds 600
- openclaw config set agents.defaults.memorySearch.enabled false
- openclaw config validate
- openclaw models set tamus/protected.gpt-4o

- check model status using 

openclaw models status --probe(this should show tamus/protected.gpt-4o as success)

## 6. Prompt openclaw
- openclaw agent --agent main -m "message"






