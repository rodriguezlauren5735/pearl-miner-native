# Pearl Miner Native

Linux x86-64 原生 Pearlhash 程序，支持 NVIDIA H100、H200、B200。默认使用全部可见 GPU，整个程序共用一个 Worker、一条外部矿池连接。

## 下载

在 [Releases](https://github.com/rodriguezlauren5735/pearl-miner-native/releases) 下载 `pearl-miner-native`、`pearl-miner-native.sha256` 和使用说明。当前版本：`0.8.3-preview5`（预发布版）。

此仓库用于分发二进制与文档；GitHub 自动生成的 Source code ZIP/TAR 不包含完整程序源码。

## 环境要求

- Linux x86-64；不是 Windows EXE。
- NVIDIA H100 / H200 / B200，以及兼容 CUDA 13 的驱动和常规 Linux 系统库。
- 无需 Python、PyTorch 或 CUDA Toolkit。

## 运行

```bash
sha256sum -c pearl-miner-native.sha256
chmod +x pearl-miner-native
./pearl-miner-native --pool global.pearlfortune.org:8888 --wallet YOUR_PRL_WALLET.UNIQUE_WORKER
```

Kryptex 示例：

```bash
./pearl-miner-native --pool prl.kryptex.network:7048 --wallet YOUR_PRL_WALLET.UNIQUE_WORKER
```

每台主机使用不同的 Worker。不传 `--device` 默认使用全部可见 GPU；可选 `--device 0` 或 `CUDA_VISIBLE_DEVICES`。

- `--diagnose`：列出设备。
- `--self-test --self-test-full`：全部可见 GPU 的生产尺寸离线证明测试。
- `--seconds 3600`：有界一小时运行，另有初始化和有限回执等待。
- Ctrl-C / SIGTERM：停止全部 GPU。
- 8888 / 7048 默认明文 TCP，8048 默认校验证书的 TLS；也可显式使用 `stratum+tcp://` / `stratum+ssl://`。

## 版本说明

修复合法任务长时间未更新时错误重连的问题。Pearl Fortune 若拒绝独立算力统计，会在同一连接回退 `mining.ping`；真实份额仍正常提交，页面在首份额前可能显示 0。GPU 子进程使用私有 IPC，不直接连接矿池。

本地计算速率和网页 Client Hashrate 不等于矿池接受份额的难度加权算力或收益；短测及一小时测试不构成 24 小时稳定性或超过其他程序的证明。

仅在有权限的设备上运行，自行承担运行费用。

## SHA256

```text
3d9a98e45d4365e6438a73526307dbe490d99948524cfa46a9e6e44a9c2f44b9  pearl-miner-native
```
