<div align="center">

<p>
  <a href="https://github.com/Quchaosheng/quard-star-riscv64-net"><img src="https://raw.githubusercontent.com/Quchaosheng/quard-star-riscv64-net/main/docs/assets/qemu-m8-demo.gif" width="49%" alt="RISC-V64 QEMU system demonstration"></a>
  <a href="https://github.com/Quchaosheng/embodied-agent-runtime"><img src="https://raw.githubusercontent.com/Quchaosheng/embodied-agent-runtime/main/docs/assets/x5-aruco-live-demo.jpg" width="49%" alt="Embodied Agent Runtime on a real X5 camera input"></a>
</p>

# 你好，我是渠超胜 | Quchaosheng

**Robot Systems Developer**

Deterministic task runtimes · Cross-layer observability · RISC-V systems

<p>
  <a href="https://github.com/Quchaosheng/embodied-agent-runtime"><img src="https://img.shields.io/badge/Runtime-Embodied_Agent_Runtime-3558A8?style=flat-square" alt="Embodied Agent Runtime"></a>
  <a href="https://github.com/Quchaosheng/RoboTraceOpt"><img src="https://img.shields.io/badge/Tracing-RoboTraceOpt-6F42C1?style=flat-square" alt="RoboTraceOpt"></a>
  <a href="https://quchaosheng.github.io/"><img src="https://img.shields.io/badge/Notes-技术笔记-2F6F68?style=flat-square" alt="Technical notes"></a>
</p>

<p>
  <a href="#能力重点">能力重点</a> ·
  <a href="#核心项目">核心项目</a> ·
  <a href="#其他公开项目">其他公开项目</a> ·
  <a href="#工具与技术">工具与技术</a> ·
  <a href="#工程记录">工程记录</a>
</p>

</div>

---

我做机器人系统软件，关注三件最不应该模糊的事：**任务如何确定地执行、异常如何被证据定位、系统边界如何被验证**。

## 能力重点

- **确定性任务运行时：** 用固定工作流、截止时间、取消/恢复语义和设备确认约束任务执行。
- **跨层可观测性：** 关联 ROS 2、Linux/eBPF 与 CAN 证据；证据不足时拒绝给出诊断结论。
- **系统边界验证：** 从 RISC-V 多 hart 隔离到故障探针，区分配置声明、软件证据与硬件证据。
- **工程栈：** C、C++、ROS 2、Linux、SocketCAN、eBPF、RISC-V；Python 主要用于编排、验证与工程工具。重视可复现测试和明确的验证边界。

## 核心项目

### [Embodied Agent Runtime](https://github.com/Quchaosheng/embodied-agent-runtime)

面向 ROS 2 的确定性任务运行时：使用固定工作流、嵌套 Action、截止时间、取消与恢复语义承接 AI 和感知输入，并提供设备桥接、任务历史与受限模型适配。<br>
`ROS 2 Jazzy` · `C++17` · `BehaviorTree.CPP` · `SocketCAN` · `gRPC` · `SQLite`

### [RoboTraceOpt](https://github.com/Quchaosheng/RoboTraceOpt)

关联 RuntimeEvent、ROS 2 tracing 与 Linux 运行时证据，构建可审计的跨层诊断和受约束配置优化流程。<br>
`ROS 2` · `Linux tracing` · `eBPF` · `evidence graph` · `Python`

### [quard-star-riscv64-net](https://github.com/Quchaosheng/quard-star-riscv64-net)

个人项目：面向 QEMU quard-star 的 RISC-V64 系统，包含 7-hart SMP 内核、独立 FreeRTOS trusted hart、Sv39、VirtIO、文件系统与自研 TCP/IP 链路；我编写 OpenSBI domain DTS 声明资源边界，并用自建 fault probe 验证 PMP 双向访问拒绝。<br>
`C` · `RISC-V` · `OpenSBI` · `FreeRTOS` · `QEMU`

### [workbench-desk-robot](https://github.com/Quchaosheng/workbench-desk-robot)

面向桌面机器人任务验证的可复现工程：将语言请求约束为 TaskGraph，以追加式事件存储、确定性重放与三值验证区分“动作已发送”和“任务已完成”；证据不足时拒绝报告成功。当前提供脚本化运行时、SocketCAN 内核模块与 RISC-V 安全 MCU 脚手架，Gazebo / MoveIt 集成仍在推进。<br>
`ROS 2 Jazzy` · `C` · `SocketCAN` · `RISC-V` · `JSON Schema` · `Python 3.12`

## 其他公开项目

> 以下列表由 GitHub Actions 自动同步；新建的原创公开仓库会自动加入，并展示项目级技术栈或主要语言。

<!-- ALL_PROJECTS:START -->
<details>
<summary><a href="https://github.com/Quchaosheng/job-search-automation-patches"><strong>job-search-automation-patches</strong></a></summary>
<br>求职自动化工具的兼容性修复与实验补丁归档。<br>
<code>Rust</code> · <code>TypeScript</code> · <code>HTML</code> · <code>CSS</code>
</details>

<details>
<summary><a href="https://github.com/Quchaosheng/Quchaosheng.github.io"><strong>Quchaosheng.github.io</strong></a></summary>
<br>Technical notes and project documentation on Linux kernel, ROS 2, embedded systems, and robotics.<br>
<code>HTML</code> · <code>CSS</code> · <code>JavaScript</code> · <code>GitHub Pages</code>
</details>

<details>
<summary><a href="https://github.com/Quchaosheng/ros2-control-vcan-motor-demo"><strong>ros2-control-vcan-motor-demo</strong></a></summary>
<br>ros2_control hardware interface over SocketCAN with 7 deterministic fault injectors; launch tests assert the safe-stop frame count upper bound at the CAN byte level.<br>
<code>C++17</code> · <code>ROS 2 Humble</code> · <code>ros2_control</code> · <code>SocketCAN</code> · <code>launch_testing</code>
</details>

<details>
<summary><a href="https://github.com/Quchaosheng/ros2-apriltag-docking-demo"><strong>ros2-apriltag-docking-demo</strong></a></summary>
<br>AprilTag docking with 6 admission guards (including pose-jump with angle wrapping); Guard is re-evaluated during the active task, not just at start.<br>
<code>ROS 2 Jazzy</code> · <code>Nav2 Docking</code> · <code>AprilTag</code> · <code>Gazebo Harmonic</code> · <code>Python 3</code>
</details>
<!-- ALL_PROJECTS:END -->

## 工具与技术

<p>
  <img src="https://img.shields.io/badge/C-Systems-A8B9CC?style=flat-square&logo=c&logoColor=111111" alt="C systems programming">
  <img src="https://img.shields.io/badge/C++-17-00599C?style=flat-square&logo=cplusplus&logoColor=white" alt="C++17">
  <img src="https://img.shields.io/badge/ROS_2-Jazzy_%7C_Humble-22314E?style=flat-square&logo=ros&logoColor=white" alt="ROS 2 Jazzy and Humble">
  <img src="https://img.shields.io/badge/Linux-Systems-FCC624?style=flat-square&logo=linux&logoColor=111111" alt="Linux systems">
  <img src="https://img.shields.io/badge/CMake-Build-064F8C?style=flat-square&logo=cmake&logoColor=white" alt="CMake">
  <img src="https://img.shields.io/badge/SocketCAN-CAN-3C873A?style=flat-square" alt="SocketCAN">
  <img src="https://img.shields.io/badge/eBPF-Observability-E34F26?style=flat-square" alt="eBPF observability">
  <img src="https://img.shields.io/badge/RISC--V-Systems-283272?style=flat-square&logo=riscv&logoColor=white" alt="RISC-V systems">
  <img src="https://img.shields.io/badge/Python-Tooling-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python tooling">
</p>

## 工程记录

- [技术笔记与项目记录](https://quchaosheng.github.io/)
- [ROS 2 task runtime architecture](https://github.com/Quchaosheng/embodied-agent-runtime#runtime-architecture)
- [RISC-V64 system architecture and QEMU evidence](https://github.com/Quchaosheng/quard-star-riscv64-net#system-architecture)
- [Workbench task verification and replay](https://github.com/Quchaosheng/workbench-desk-robot#core-contributions-kernel-engineering)

<div align="center">
  <sub>Build the boundary. Trace the failure. Keep the evidence.</sub>
</div>
