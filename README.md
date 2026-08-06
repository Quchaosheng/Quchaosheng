<div align="center">

<p>
  <a href="https://github.com/Quchaosheng/quard-star-riscv64-net"><img src="https://raw.githubusercontent.com/Quchaosheng/quard-star-riscv64-net/main/docs/assets/qemu-m8-demo.gif" width="49%" alt="RISC-V64 QEMU system demonstration"></a>
  <a href="https://github.com/Quchaosheng/ros2-apriltag-docking-demo"><img src="https://raw.githubusercontent.com/Quchaosheng/ros2-apriltag-docking-demo/main/docs/demo/apriltag_docking_demo.gif" width="49%" alt="ROS 2 AprilTag docking demonstration"></a>
</p>

# 你好，我是渠超胜 | Quchaosheng

**Robot Systems Developer**

Deterministic task runtimes · Cross-layer observability · RISC-V systems

<p>
  <a href="https://github.com/Quchaosheng/embodied-agent-runtime"><img src="https://img.shields.io/badge/Runtime-Embodied_Agent_Runtime-3558A8?style=flat-square" alt="Embodied Agent Runtime"></a>
  <a href="https://github.com/Quchaosheng/RoboTraceOpt"><img src="https://img.shields.io/badge/Tracing-RoboTraceOpt-6F42C1?style=flat-square" alt="RoboTraceOpt"></a>
  <a href="https://quchaosheng.github.io/"><img src="https://img.shields.io/badge/Notes-技术笔记-2F6F68?style=flat-square" alt="Technical notes"></a>
</p>

</div>

---

我做机器人系统软件，重点是让“任务是否真的执行了”这件事有证据支撑。
三个方向：确定性任务运行时（取消与设备确认不可绕过）、跨层证据准入
（ROS 2 / eBPF / CAN 关联，证据不足时拒绝下结论）、RISC-V 系统
（7+1 hart 双域隔离，访问拒绝经故障探针实测）。

核心项目仓库都有独立的验证边界章节，明确区分软件证据与硬件证据。

## 关于我

我关注机器人软件中最不应该模糊的三件事：**任务如何确定地执行、异常如何被证据定位、系统边界如何被验证**。

- 个人项目覆盖 ROS 2 任务运行时、跨层追踪优化工具和 RISC-V64 系统。
- 主要使用 C++、Python、ROS 2 与 Linux，工作范围覆盖任务编排、设备桥接、运行时追踪、内核与网络协议栈。
- 重视可复现测试、失败终态、取消语义与验证边界；实现了什么、验证到哪里，尽量让仓库本身可以回答。

## 核心项目

### [Embodied Agent Runtime](https://github.com/Quchaosheng/embodied-agent-runtime)

面向 ROS 2 的确定性任务运行时：使用固定工作流、嵌套 Action、截止时间、取消与恢复语义承接 AI 和感知输入，并提供设备桥接、任务历史与受限模型适配。  
`ROS 2 Jazzy` · `C++17` · `BehaviorTree.CPP` · `SocketCAN` · `gRPC` · `SQLite`

### [RoboTraceOpt](https://github.com/Quchaosheng/RoboTraceOpt)

关联 RuntimeEvent、ROS 2 tracing 与 Linux 运行时证据，构建可审计的跨层诊断和受约束配置优化流程。  
`Python` · `ROS 2` · `tracing` · `eBPF` · `evidence graph`

### [quard-star-riscv64-net](https://github.com/Quchaosheng/quard-star-riscv64-net)

个人项目：面向 QEMU quard-star 的 RISC-V64 系统，包含 7-hart SMP 内核、独立 FreeRTOS trusted hart、Sv39、VirtIO、文件系统与自研 TCP/IP 链路；我编写 OpenSBI domain DTS 声明资源边界，并用自建 fault probe 验证 PMP 双向访问拒绝。<br>
`C` · `RISC-V` · `OpenSBI` · `FreeRTOS` · `QEMU`

### [ros2-control-vcan-motor-demo](https://github.com/Quchaosheng/ros2-control-vcan-motor-demo)

实现 `ros2_control` 硬件接口与 SocketCAN 双虚拟电机链路，覆盖 ACK、编码器反馈、看门狗、故障注入和确定性失败终态。  
`ROS 2 Humble` · `C++17` · `ros2_control` · `SocketCAN`

## 其他公开项目

> 以下列表由 GitHub Actions 自动同步；新建公开仓库后会自动加入。

<!-- ALL_PROJECTS:START -->
- [workbench-desk-robot](https://github.com/Quchaosheng/workbench-desk-robot) · `Python`  
  A reproducible desktop robot arm simulation where task completion must be verified, not assumed. Language → constrained TaskGraph → grasp/place → WorldState verification. Refuses to report success without evidence. ROS 2 Jazzy · Gazebo Harmonic · MoveIt 2.
- [Quchaosheng.github.io](https://github.com/Quchaosheng/Quchaosheng.github.io) · `HTML`  
  Technical notes and project documentation on Linux kernel, ROS 2, embedded systems, and robotics.
- [ros2-apriltag-docking-demo](https://github.com/Quchaosheng/ros2-apriltag-docking-demo) · `Python`  
  AprilTag docking with 6 admission guards (including pose-jump with angle wrapping); Guard is re-evaluated during the active task, not just at start.
<!-- ALL_PROJECTS:END -->

## 工具与技术

<p>
  <img src="https://img.shields.io/badge/C++-17-00599C?style=flat-square&logo=cplusplus&logoColor=white" alt="C++17">
  <img src="https://img.shields.io/badge/Python-3-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python 3">
  <img src="https://img.shields.io/badge/ROS_2-Jazzy_%7C_Humble-22314E?style=flat-square&logo=ros&logoColor=white" alt="ROS 2 Jazzy and Humble">
  <img src="https://img.shields.io/badge/Linux-Systems-FCC624?style=flat-square&logo=linux&logoColor=111111" alt="Linux systems">
  <img src="https://img.shields.io/badge/CMake-Build-064F8C?style=flat-square&logo=cmake&logoColor=white" alt="CMake">
  <img src="https://img.shields.io/badge/SocketCAN-CAN-3C873A?style=flat-square" alt="SocketCAN">
  <img src="https://img.shields.io/badge/SQLite-History-003B57?style=flat-square&logo=sqlite&logoColor=white" alt="SQLite">
</p>

## 工程记录

- [技术笔记与项目记录](https://quchaosheng.github.io/)
- [ROS 2 task runtime architecture](https://github.com/Quchaosheng/embodied-agent-runtime#runtime-architecture)
- [RISC-V64 system architecture and QEMU evidence](https://github.com/Quchaosheng/quard-star-riscv64-net#system-architecture)

<div align="center">
  <sub>Build the boundary. Trace the failure. Keep the evidence.</sub>
</div>
