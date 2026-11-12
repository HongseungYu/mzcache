# mzCache

Artifact for the MobiCom 2026 paper *mzCache: On-Device LLM Memory Management
under Multitasking*.

mzCache manages the memory of an on-device LLM while the user switches between
apps. When memory runs low, it evicts the KV cache in compressed chunks and
unloads weight layers. On the next request, it restores them while the GPU runs
prefill, which gives 2.1–5.5× lower time-to-first-token than a storage-backed
partial-offload baseline.

This repository contains the mzCache engine (a fork of
[llama.cpp](https://github.com/ggml-org/llama.cpp) at `fa4a9f2a`), the two
baselines, and the scripts that reproduce the paper's main figures.

## Demo video

The mzCache app and the OS-paging baseline run the same app-switching workload
(30× speed). mzCache frees memory each time it goes to the background and
responds quickly when it comes back. The baseline is killed by Android's
low-memory killer and has to reload from scratch.

https://github.com/user-attachments/assets/3925f5db-1e82-4838-b98f-e9cf8accd564

## Start here

See [EVALUATION.md](EVALUATION.md) for hardware requirements, setup, and
step-by-step instructions for each experiment.

## License

MIT, following llama.cpp. Vendored Khronos OpenCL headers under
`examples/llama.android/.../CL/` are Apache-2.0.
