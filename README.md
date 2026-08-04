<div align="center">

# 你好，我是渠超胜 | Quchaosheng

**机器人系统软件开发者 | Robot Systems Software Developer**

ROS 2 · C++ · Linux · RISC-V · deterministic runtimes · evidence-driven debugging

<p>
  <a href="https://github.com/Quchaosheng/embodied-agent-runtime/actions/workflows/ros2-ci.yml"><img src="https://github.com/Quchaosheng/embodied-agent-runtime/actions/workflows/ros2-ci.yml/badge.svg" alt="Embodied Agent Runtime CI"></a>
  <a href="https://github.com/Quchaosheng/ros2-control-vcan-motor-demo/actions/workflows/ci.yml"><img src="https://github.com/Quchaosheng/ros2-control-vcan-motor-demo/actions/workflows/ci.yml/badge.svg" alt="ros2 control vcan demo CI"></a>
  <a href="https://github.com/Quchaosheng/quard-star-riscv64-net/actions/workflows/m8-smoke.yml"><img src="https://github.com/Quchaosheng/quard-star-riscv64-net/actions/workflows/m8-smoke.yml/badge.svg" alt="RISC-V QEMU M8 smoke CI"></a>
</p>

<p>
  <a href="https://github.com/Quchaosheng/ros2-control-vcan-motor-demo"><img src="https://raw.githubusercontent.com/Quchaosheng/ros2-control-vcan-motor-demo/master/docs/demo/vcan_diffbot_demo.gif" width="49%" alt="ROS 2 ros2_control and SocketCAN virtual motor demo"></a>
  <a href="https://github.com/Quchaosheng/quard-star-riscv64-net"><img src="https://raw.githubusercontent.com/Quchaosheng/quard-star-riscv64-net/main/docs/assets/qemu-m8-demo.gif" width="49%" alt="RISC-V64 QEMU system evidence replay"></a>
</p>

</div>

---

## 我在解决什么问题

我关注机器人软件中最不应该模糊的三件事：**任务如何确定地执行、异常如何被证据定位、系统边界如何被验证**。

我的工作方式是先定义终态和证据，再运行实验：保留环境、命令、时间线、原始输出和结论边界，让仓库回答“实现了什么、测到了什么、还没有证明什么”。

## 证据摘要

- **端到端运行时**：[`Embodied Agent Runtime` 的验证记录](https://github.com/Quchaosheng/embodied-agent-runtime#verified-software-evidence) 在 Windows + WSL2/Jazzy 完成 **11 个包、393 个测试、0 错误、0 失败、72 跳过**；X5/Ubuntu 22.04/Humble 的 ARM smoke 通过 **311 个测试、0 错误、0 失败、72 跳过**。实体 UVC 相机在 30/30 帧中识别出 ArUco ID 10，双 CANable 台架完成双向帧收发。
- **跨层诊断**：[`RoboTraceOpt native F3/F4 evidence`](https://github.com/Quchaosheng/RoboTraceOpt/blob/main/docs/evidence/native-f3f4-formal-v3/README.md) 在 Ubuntu 24.04/Jazzy 完成 **40/40 次**正式分区运行；F3 完整生命周期恢复率为 **95.30% → 67.56%**，F4 请求-响应中位数为 **0.875 ms → 101.212 ms**，配对中位数增量 **100.337 ms**。结论限定为完整路径恢复和应用层阻塞效应，不外推为调度器或 syscall 因果归因。
- **实体 CAN 台架**：[`X5 physical-CAN smoke evidence`](https://github.com/Quchaosheng/RoboTraceOpt/blob/main/docs/evidence/x5-physical-can-smoke-20260727/README.md) 保留一段 arm64 PREEMPT_RT 正常 ACK 捕获：**34 次发送、34 次匹配 ACK、100% payload matching**，send-to-ACK P50/P95 为 **6.039/6.238 ms**。这是正常 ACK transport smoke，不是 ECU HIL，也没有 drop/timeout 对照。
- **RISC-V 系统**：[`quard-star-riscv64-net M8 验收与性能基线`](https://github.com/Quchaosheng/quard-star-riscv64-net/blob/main/docs/performance-baseline.md) 覆盖 7 个普通 hart、1 个 FreeRTOS trusted hart、1 MiB TFTP、SMP、存储、网络和双向 PMP 拒绝。3 次 fresh-disk 基线的 M8 host elapsed 中位数为 **29.602 s**，相对离散度为 **11.496%**；这是同一 WSL2 主机上的基线观察，不是优化结论。

## 核心项目

### [Embodied Agent Runtime](https://github.com/Quchaosheng/embodied-agent-runtime)

面向 ROS 2 的确定性任务运行时：用固定的 BehaviorTree.CPP 工作流、嵌套 Action、截止时间、取消与恢复语义承接 AI 和感知输入，再通过 SocketCAN 设备桥接和 SQLite 历史记录保留运行证据。软件路径和 X5 输入/通信台架已验证；电机运动与硬件急停回路明确不在当前证据范围内。

`ROS 2 Jazzy/Humble` · `C++17` · `BehaviorTree.CPP` · `SocketCAN` · `gRPC` · `SQLite`

### [ros2-control-vcan-motor-demo](https://github.com/Quchaosheng/ros2-control-vcan-motor-demo)

用 `ros2_control` 硬件接口驱动两个虚拟电机，沿 SocketCAN 链路验证 ACK、编码器反馈、看门狗、反馈超时、故障注入和安全停车。它是可运行的 `vcan0` 协议与控制回路 demo，不宣称真实执行器或闭环机器人性能。

`ROS 2 Humble` · `C++17` · `ros2_control` · `SocketCAN` · `vcan`

### [RoboTraceOpt](https://github.com/Quchaosheng/RoboTraceOpt)

把 RuntimeEvent、ROS 2 tracing、eBPF 调度记录和 SocketCAN/vcan ACK 生命周期关联成可审计的证据图，做带不确定性报告的根因诊断与受约束配置优化。开发结果会标注 proxy、formal 和 physical evidence 的边界，不把 WSL 或 mock 结果冒充正式硬件结论。

`Python` · `ROS 2` · `ros2_tracing` · `eBPF` · `evidence graph`

[公开证据索引](https://github.com/Quchaosheng/RoboTraceOpt/tree/main/docs/evidence) · [项目记录](https://quchaosheng.github.io/projects/robotraceopt/)

### [quard-star-riscv64-net](https://github.com/Quchaosheng/quard-star-riscv64-net)

面向 QEMU quard-star 的 RISC-V64 系统：7-hart SMP 内核、独立 FreeRTOS trusted hart、OpenSBI domain、Sv39、PMP、VirtIO、FatFs 和自研 TCP/IP 链路。PMP 与性能结果均明确标为 QEMU/WSL 证据，不外推为物理板安全性或性能。

`C` · `RISC-V64` · `OpenSBI` · `FreeRTOS` · `QEMU`

## 工程记录

我在把“现象 → 时间线/帧/trace → 根因 → 修复 → 回归验证”写成可复查的工程记录。当前可直接阅读：

- [cyclictest：怎样测量 Linux 实时调度延迟](https://quchaosheng.github.io/2026/07/30/cyclictest-latency/)
- [实时回归测试：把一次调优变成可持续的延迟基线](https://quchaosheng.github.io/2026/07/30/realtime-regression-baseline/)
- [TCP 丢包追踪：用 kprobe 和 tracepoint 串起证据链](https://quchaosheng.github.io/2026/07/29/tcp-drop-tracing/)
- [QEMU gdbstub 调试：从启动第一条指令定位系统问题](https://quchaosheng.github.io/2026/07/29/qemu-gdbstub-debugging/)
- [全部技术笔记与项目记录](https://quchaosheng.github.io/)

## 其他入口

- [ros2-apriltag-docking-demo](https://github.com/Quchaosheng/ros2-apriltag-docking-demo)：ROS 2 AprilTag 感知与对接流程。
- [GitHub Actions 与运行入口](https://github.com/Quchaosheng)：每个核心项目的 README 都包含构建、测试、证据边界和可复现实验入口。

<div align="center">
  <sub>Build the boundary. Trace the failure. Keep the evidence.</sub>
</div>
