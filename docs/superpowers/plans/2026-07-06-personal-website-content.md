# Personal Website Content Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Put the user's real personal website content into the existing Academic Pages/Jekyll site while preserving the current visual style.

**Architecture:** This is a content-only change. The implementation updates site metadata in `_config.yml`, replaces the homepage body in `_pages/about.md`, and fills `_pages/cv.md` with detailed CV content extracted and condensed from `D:\我的文档\简历\个人经历基础资料.md`.

**Tech Stack:** Jekyll, Academic Pages, Markdown, YAML, GitHub Pages.

---

## File Structure

- Modify `_config.yml`: public site title, description, author sidebar profile, contact links, and removal of unsuitable public sidebar fields.
- Modify `_pages/about.md`: concise Chinese-first homepage with English technical terms preserved.
- Modify `_pages/cv.md`: detailed CV page using existing `layout: archive` front matter.
- No CSS, layout, collection, image, or navigation redesign in this implementation.

## Task 1: Update Site Metadata

**Files:**
- Modify: `_config.yml`

- [ ] **Step 1: Inspect current metadata**

Run:

```powershell
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8
Select-String -Path '_config.yml' -Pattern '^(title|name|description|  avatar|  name|  bio|  location|  employer|  email|  github|  steam)' | ForEach-Object { $_.Line }
```

Expected: current title is `Xuran Lu / Personal Homepage`, author name is `Xuran Lu（卢叙燃）`, bio is a placeholder quote, and `steam` has unsuitable public text.

- [ ] **Step 2: Update metadata**

Change `_config.yml` to these public values:

```yaml
title                    : "卢叙燃 / Xuran Lu"
name                     : &name "卢叙燃 / Xuran Lu"
description              : &description "深圳大学控制科学与工程硕士在读，聚焦机器人导航、ROS 2、足式机器人运动控制与具身系统集成。"
author:
  avatar           : "me.png"
  name             : "卢叙燃 / Xuran Lu"
  bio              : "深圳大学控制科学与工程硕士在读，研究与工程兴趣包括机器人导航、ROS 2、足式机器人运动控制、强化学习控制与具身系统集成。"
  location         : "Shenzhen, China"
  employer         : "Shenzhen University"
  email            : "qiurechard72@gmail.com"
  github           : "Rechardluxry"
  steam            :
```

Keep other unrelated `_config.yml` keys unchanged.

- [ ] **Step 3: Verify YAML-relevant lines**

Run:

```powershell
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8
Select-String -Path '_config.yml' -Pattern '^(title|name|description|  avatar|  name|  bio|  location|  employer|  email|  github|  steam)' | ForEach-Object { $_.Line }
```

Expected: updated Chinese-first metadata appears, `github` is `Rechardluxry`, and `steam` is blank.

- [ ] **Step 4: Commit metadata update**

Run:

```powershell
git add _config.yml
git commit -m "Update personal site metadata"
```

Expected: commit succeeds with one modified file.

## Task 2: Replace Homepage Content

**Files:**
- Modify: `_pages/about.md`

- [ ] **Step 1: Inspect current homepage**

Run:

```powershell
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8
Get-Content -Raw -Encoding UTF8 '_pages/about.md'
```

Expected: current content contains template text about a third-year undergraduate student and placeholder sections.

- [ ] **Step 2: Replace homepage body**

Keep the existing front matter shape and replace the Markdown body with this content:

```markdown
---
permalink: /
title: "About me"
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

我是卢叙燃，深圳大学控制科学与工程专业 2025 级硕士研究生，本科就读于深圳大学机器人工程专业。我的研究与工程兴趣聚焦机器人导航、ROS/ROS 2 系统、足式机器人运动控制、强化学习控制和具身智能平台集成。

我希望把算法、系统和实机调试串起来：从 `Nav2`、`Fast-LIO2`、`SLAM`、代价地图与路径规划，到 `AMP`、`PPO`、`Sim2Sim` 和足式机器人运动控制，再到 `Unitree B2`、`Go2`、`Jetson AGX Orin`、`Livox MID360`、`RealSense D435`、`Piper` 机械臂等平台上的部署与联调。

[Email](mailto:qiurechard72@gmail.com) / [Github](https://github.com/Rechardluxry) / [Wechat](../images/wechat.png) / [CSDN](https://blog.csdn.net/m0_66461274?spm=1010.2135.3001.5343)

---

### 研究与工程方向

- 机器人导航与定位：`ROS 2`、`Nav2`、`Fast-LIO2`、`SLAM`、代价地图、全局/局部规划、点云桥接与实机导航调试。
- 足式机器人运动控制：`VMC`、`MPC`、`WBC`、`QP`、状态估计、步态轨迹规划和实机控制接口。
- 强化学习与模仿学习控制：`PPO`、`AMP`、`Actor-Critic`、`RSL-RL`、`Legged Gym`、`Isaac Gym`、`MuJoCo`、`Sim2Sim/Sim2Real`。
- 机器人系统集成：传感器 bringup、`Jetson` 部署、`Unitree SDK2` 通信、`/cmd_vel` 控制桥接、安全急停和具身智能任务调用。

### 精选经历

- **Unitree B2 导航与 OpenClaw 具身控制系统集成**：参与 `Unitree B2 + Jetson AGX Orin + Piper` 机械臂平台集成，完成 `ROS 2` 通信、IMU 与 `/cmd_vel` 桥接、`MID360/D435` 驱动部署、`Fast-LIO2` 建图定位、`Nav2` 目标点导航和 `3D-BBS` 自动重定位调试。
- **小 Pi 双足机器人 AMP 与 Sim2Sim 验证**：在高擎机电实习期间，基于 `AMP_for_hardware`、`Legged Gym` 与 `RSL-RL` 适配双足机器人强化学习任务，完成观测构造、关节映射、运动数据格式对齐和 `Isaac Gym` 到 `MuJoCo` 的 `Sim2Sim` 验证。
- **语义安全余量收紧 MPC-SECBF 动态避障研究**：参与上下文相关动态避障研究，将语义安全度量嵌入全局运动基元碰撞检测和局部 `MPC-SECBF` 安全约束。
- **ROS 智慧物流小车与无人智能小车项目**：负责自主多点导航、二维码任务解析、投递顺序优化、`SLAM` 建图、`Navigation` 参数调试和实车验证。

### 荣誉与证书

- 深圳大学 2025 级硕士研究生学业奖学金特等奖。
- 深蓝学院《足式机器人运动控制》第一期优秀学员与结业证书。
- 第 18 届全国大学生智能汽车竞赛讯飞智慧农业组分赛区三等奖。
- 第 14 届蓝桥杯广东赛区单片机设计与开发大学组三等奖。
- 全国大学生数学建模竞赛广东省分赛三等奖。
- NVIDIA 深度学习基础证书，Datawhale AI 夏令营 NLP 方向优秀学习者。
```

- [ ] **Step 3: Verify homepage file**

Run:

```powershell
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8
Select-String -Path '_pages/about.md' -Pattern '卢叙燃|ROS 2|AMP|Unitree B2|MPC-SECBF|mailto'
```

Expected: each pattern appears at least once.

- [ ] **Step 4: Commit homepage update**

Run:

```powershell
git add _pages/about.md
git commit -m "Update homepage content"
```

Expected: commit succeeds with one modified file.

## Task 3: Fill CV Page

**Files:**
- Modify: `_pages/cv.md`

- [ ] **Step 1: Inspect current CV**

Run:

```powershell
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8
Get-Content -Raw -Encoding UTF8 '_pages/cv.md'
```

Expected: current CV body is almost entirely commented-out template content.

- [ ] **Step 2: Replace CV body**

Keep front matter and replace the body with detailed sections:

```markdown
---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

## 基本信息

卢叙燃，深圳大学控制科学与工程专业 2025 级硕士研究生，本科为深圳大学机器人工程专业。研究与工程方向包括机器人导航、ROS/ROS 2 系统、足式机器人运动控制、强化学习控制、移动机器人路径规划、SLAM 与具身智能平台集成。

- 邮箱：qiurechard72@gmail.com；1147975692@qq.com
- GitHub：[Rechardluxry](https://github.com/Rechardluxry)
- 所在地：深圳

## 教育经历

### 深圳大学｜控制科学与工程｜硕士

2025.09 至今，机电与控制工程学院。

- 研究方向聚焦机器人导航、运动控制、足式机器人强化学习与具身系统集成。
- 获得深圳大学 2025 级硕士研究生学业奖学金特等奖。

### 深圳大学｜机器人工程｜本科

2021.09 - 2025.06，机电与控制工程学院。

- 本科推免至深圳大学控制科学与工程专业。
- 系统学习机器人工程、控制理论、运动规划、机器视觉、嵌入式开发与智能机器人系统课程。
- 具备控制、算法、软硬件联调和机器人系统开发综合背景。

## 实习经历

### 高擎机电｜运动控制算法实习生｜电控部-运控组

2025.03 - 2025.07

方向：双足机器人强化学习运动控制、`AMP` 模仿学习、`Sim2Sim` 验证、执行器数据采集。

- 编写 `ROS` 数据采集脚本，订阅 12 自由度双足机器人关节状态 topic，采集关节位置、速度、目标位置与力矩，并完成 `rosbag` 录制、时间戳对齐和 CSV 转换，为执行器网络建模提供实机数据。
- 基于 `AMP_for_hardware`、`Legged Gym` 与 `RSL-RL` 完成小 Pi 双足机器人 `AMP` 模仿学习任务适配，新增机器人环境、配置文件与运动数据加载器，统一 12 自由度关节映射和 `AMP` 观测格式。
- 排查并修正观测索引、坐标轴转换、左右腿关节顺序、姿态偏置、`NaN` 训练发散等问题，使 `AMP` 训练链路成功跑通并获得前进、后退、静止策略效果。
- 搭建 `Isaac Gym` 到 `MuJoCo` 的 `Sim2Sim` 验证链路，系统排查 obs/action/tau、关节顺序、动作缩放、控制频率、URDF/XML 映射和 PD 参数差异，保证策略跨仿真器行为一致。

## 科研经历

### Semantic Margin-Tightened MPC-SECBF for Context-Dependent Dynamic Obstacle Avoidance

方向：自主移动机器人、动态障碍物避障、语义安全边界、`MPC`、控制屏障函数、路径规划。

- 参与语义安全余量收紧 `MPC-SECBF` 动态避障方法研究，在 EESM 动态几何安全距离基础上叠加类别与交互风险驱动的有界语义安全余量，用于上下文相关动态障碍物避障。
- 构建 `SEESM` 分层规划框架，将语义安全度量用于全局运动基元碰撞检测和局部 `MPC-SECBF` 安全约束。
- 当前作为在研工作展示，后续可根据投稿或发表状态补充会议、期刊和个人贡献细节。

## 项目经历

### Unitree B2 四足机器人导航与 OpenClaw 具身控制系统集成

2026.03 至今

技术栈：`Unitree B2`、`Jetson AGX Orin`、`Piper` 机械臂、`Livox MID360`、`Intel RealSense D435`、`ROS 2 Humble`、`Fast-LIO2`、`Nav2`、`OpenClaw`。

- 参与 `Unitree B2 + Jetson AGX Orin + Piper` 机械臂具身平台集成，完成 Orin 系统配置、`Unitree ROS 2/SDK2` 通信、IMU 与 `/cmd_vel` 桥接、急停控制和多传感器驱动部署。
- 基于 `Livox MID360`、`RealSense D435`、`Fast-LIO2` 和 `Nav2` 搭建自主导航链路，完成建图、地图保存、定位、全局/局部规划、代价地图、RViz 目标点导航和 `3D-BBS` 自动重定位调试。
- 开发或接入 `Livox CustomMsg` 至 `PointCloud2` 点云桥接节点，解决导航与重定位链路中的消息类型兼容问题，并通过坐标偏差标定实现 `3D-BBS` 位姿到 `Nav2 initialpose` 的转换。
- 接入 `OpenClaw` 智能体控制框架，实现 B2 四足机器人运动控制、目标点下发和二维导航任务调用，为狗臂协同具身实验提供系统基础。

### 小 Pi 双足机器人 AMP 强化学习与 Sim2Sim 验证

2025.03 - 2025.07

技术栈：`AMP`、`PPO`、`RSL-RL`、`Legged Gym`、`Isaac Gym`、`MuJoCo`、`ROS`、`PyTorch`、`Python`。

- 完成 `AMP_for_hardware` 框架到小 Pi 双足平台的环境适配，包括数据加载器、环境控制类、配置文件、观测构造和 runner 调用逻辑。
- 将小 Pi 运动数据与 `AMP` 所需数据格式对齐，处理 root pose、关节顺序、左右腿映射、观测维度和动作缩放等问题。
- 通过 action 置零、obs 置零、固定动作注入和 play 数据回放等方法定位策略部署问题，修正左右腿 action 映射和 `MuJoCo` 观测构造错误。

### Unitree Go2 强化学习步态策略真机部署

技术栈：`Unitree Go2`、强化学习步态策略、状态观测、关节指令映射、底层控制接口。

- 完成强化学习步态策略向 `Unitree Go2` 的真机部署，打通状态观测、关节指令映射和底层控制接口。
- 积累四足机器人实机调试、控制接口对接和策略部署经验。

### DeepRobotics Lite3 足式机器人运动控制学习与仿真

技术栈：`Lite3`、`PyBullet`、`VMC`、`QP`、Kalman Filter、正逆运动学。

- 基于 `Lite3` 仿真平台实现正逆运动学、摆动腿轨迹插值、Kalman 状态估计和 `VMC/QP` 站立控制。
- 验证足端雅可比、虚拟力求解和站立控制流程，获得深蓝学院《足式机器人运动控制》第一期优秀学员。

### 邮件分拣投递物流小车

2024.07 - 2024.09

技术栈：`C++`、`Python`、`ROS`、`SLAM`、二维码识别、路径规划、`DWA`、`TEB`、`PID`、`Magician` 机械臂。

- 基于 `ROS` 构建自主多点导航、二维码任务解析、投递顺序优化和机械臂夹取控制流程。
- 负责自主导航与路径规划模块，结合二维码信息生成目标点序列，控制小车与 `Magician` 机械臂完成邮件分拣、夹取和投递。
- 项目获得中国大学生计算机设计大赛智慧物流赛道相关奖项；当前公开表述采用保守写法，避免在证书未补全前夸大奖项级别。

### 智慧农业巡检机器人

2023.09 - 2023.12

技术栈：`ROS`、`A*`、`DWA`、`TEB`、`OpenCV`、`YOLO`、移动机器人导航。

- 负责智慧农业巡检机器人自主多点导航与路径规划参数调试，使用 `A*`、`DWA`、`TEB` 完成任务点导航。
- 配合 `YOLO/OpenCV` 模块完成农作物识别、分类和数量统计。
- 获第 18 届全国大学生智能汽车竞赛讯飞智慧农业组分赛区三等奖。

### 自主搭建基于 ROS 的无人智能小车

2023.05 - 2024.05

项目类型：广东省大学生创新训练计划项目。

- 负责 `SLAM` 与 `Navigation` 导航模块，完成激光雷达建图、代价地图配置、全局/局部规划参数调试和自主导航实车验证。
- 参与从底盘结构、`ROS` 驱动板、树莓派上位机、`STM32` 下位机到视觉识别和自主导航的完整机器人系统搭建。
- 解决话题匹配、地图构建和导航参数调试问题，项目成功结题。

### 基于 LabVIEW 的智能车状态检测系统

2023.04 - 2023.07

- 使用 `LabVIEW` 开发智能车上位机调试系统，实现状态监控、串口/I2C 通信和 `PID` 参数调试界面。

### Dubins 路径规划曲线

- 使用 `MATLAB` 实现 `Dubins` 路径规划曲线，覆盖 LSL、LSR、RSL、RSR、RLR、LRL 等路径类型，用于理解车辆非完整约束下的最短路径规划。

### STM32 平衡小车与软硬件联调

- 自制 `STM32` 平衡小车，独立完成 `PID` 控制、电机控制和基础硬件调试，具备原理图阅读、芯片手册查阅和软硬件联调经验。

## 专业技能

### 编程与开发

- 语言与工具：`C`、`C++`、`Python`、`MATLAB`、`LabVIEW`、`Linux`、`Ubuntu`、`Git`、`CMake`、`Conda`、`colcon`。
- 工程能力：代码仓库阅读、实验复现、运行错误定位、技术文档整理和调试记录沉淀。

### ROS 与机器人系统

- `ROS 1`：topic、node、`rosbag`、`navigation`、`SLAM`、costmap、`DWA`、`TEB`、rqt 调参。
- `ROS 2`：Humble、`Nav2`、map_server、RViz2、launch、`PointCloud2`、`LaserScan`、`TF/TF2`、`CycloneDDS`、`Fast-LIO2`、传感器驱动 bringup。
- 实机平台：`Unitree B2`、`Unitree Go2`、`DeepRobotics Lite3`、小 Pi 双足机器人、ROS 智能小车。

### 导航、定位与路径规划

- 使用或调试过：`A*`、`DWA`、`TEB`、`Nav2`、`Fast-LIO2`、`SLAM`、`Navigation`、`3D-BBS`、`Dubins` 曲线。
- 熟悉地图加载、定位、全局规划、局部规划、代价地图、膨胀层、障碍物层、目标点导航、初始定位和点云桥接。

### 足式机器人运动控制

- 控制与运动学：四足机器人正逆运动学、坐标变换、雅可比矩阵、`PID`、`VMC`、`MPC`、`WBC`、`QP` 力分配、`ZMP`、`LIPM`。
- 强化学习：`PPO`、`AMP`、`Actor-Critic`、`RSL-RL`、`Legged Gym`、`AMP_for_hardware`、镜像对称损失、奖励函数设计。
- 仿真与部署：`Isaac Gym`、`Isaac Sim`、`MuJoCo`、`Gazebo`、`PyBullet`、`Sim2Sim`、`Sim2Real`。

### 视觉、感知与硬件

- 视觉与感知：`OpenCV`、`YOLO`、`Lanenet`、`Face_recognition`、`RealSense D435`、`Livox MID360`、`RPLIDAR A1M8`、Astra 深度相机。
- 嵌入式与硬件：`STM32`、Arduino、树莓派、`Jetson Nano`、`Jetson AGX Orin`、GPIO、UART、I2C、中断、串口通信、PWM、电机控制、PCB 设计、焊接、原理图阅读和软硬件联调。

## 荣誉奖项与证书

- 深圳大学 2025 级硕士研究生学业奖学金特等奖，2025-2026 学年。
- 本科推免至深圳大学控制科学与工程专业。
- 第 18 届全国大学生智能汽车竞赛讯飞智慧农业组分赛区三等奖，2023。
- 第 14 届蓝桥杯全国软件和信息技术专业人才大赛广东赛区单片机设计与开发大学组三等奖，2023。
- 全国大学生数学建模竞赛广东省分赛三等奖，2024。
- 中国大学生计算机设计大赛智慧物流赛道相关奖项，2024。
- 深蓝学院《足式机器人运动控制》第一期优秀学员与结业证书，2025。
- NVIDIA 深度学习基础证书。
- Datawhale AI 夏令营 NLP 方向优秀学习者，2024。
- CET-4：532；CET-6：426。

## 组织与服务

- 深圳大学机电与控制工程学院具身智能社团成员，参与机器人相关学习、实践与组织工作。
- 本科期间担任班级干部和学习委员相关职务。
- 深圳市志愿者服务记录累计 243.40 小时。
```

- [ ] **Step 3: Verify CV file**

Run:

```powershell
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8
Select-String -Path '_pages/cv.md' -Pattern '教育经历|高擎机电|MPC-SECBF|Unitree B2|专业技能|荣誉奖项'
```

Expected: each major CV section appears.

- [ ] **Step 4: Commit CV update**

Run:

```powershell
git add _pages/cv.md
git commit -m "Add detailed CV content"
```

Expected: commit succeeds with one modified file.

## Task 4: Verify Site Content

**Files:**
- Inspect: `_config.yml`
- Inspect: `_pages/about.md`
- Inspect: `_pages/cv.md`

- [ ] **Step 1: Inspect final diff**

Run:

```powershell
git diff HEAD~3..HEAD -- _config.yml _pages/about.md _pages/cv.md
```

Expected: diff only changes public metadata, homepage content, and CV content. There are no CSS, layout, collection, or navigation changes.

- [ ] **Step 2: Check repository status**

Run:

```powershell
git status --short --branch
```

Expected: branch is clean except for this plan file if it has not yet been committed.

- [ ] **Step 3: Try local Jekyll build**

Run:

```powershell
bundle exec jekyll build
```

Expected if dependencies are installed: build succeeds and writes `_site`.

Expected if dependencies are not installed: command fails with a clear Ruby/Bundler dependency error. In that case, report the failure and continue with Markdown/YAML inspection results.

- [ ] **Step 4: Commit plan file if still uncommitted**

Run:

```powershell
git add docs/superpowers/plans/2026-07-06-personal-website-content.md
git commit -m "Add personal website content implementation plan"
```

Expected: commit succeeds with the plan file if it was not already committed.
