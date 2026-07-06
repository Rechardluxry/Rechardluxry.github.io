# Personal Website Content Design

Date: 2026-07-06
Site: `D:\我的文档\简历\个人网站`
Source material: `D:\我的文档\简历\个人经历基础资料.md`

## Goal

Keep the current Academic Pages/Jekyll visual style and put real personal website content online first. The first pass focuses on content placement rather than redesign.

## Language

The site content will use Chinese as the primary language. Key technical terms stay in English where they are normally written that way, including `ROS 2`, `Nav2`, `Fast-LIO2`, `AMP`, `PPO`, `Sim2Sim`, `MuJoCo`, `Isaac Gym`, `Unitree B2`, `OpenClaw`, `PointCloud2`, `Jetson AGX Orin`, and similar names.

## Files To Update

- `_config.yml`: update public site metadata and sidebar author profile.
- `_pages/about.md`: replace template homepage text with a concise personal homepage.
- `_pages/cv.md`: add the detailed CV-style content.

No CSS, layout, navigation structure, collections, or visual assets will be redesigned in this pass.

## Homepage Content

The homepage will be a concise overview:

- short personal introduction;
- research and engineering interests;
- selected projects and research experience;
- selected honors and certificates;
- public contact links.

The homepage should highlight robotics navigation, `ROS 2`, legged robot motion control, reinforcement learning control, and embodied robotics system integration.

## CV Content

The CV page will be the detailed content page with these sections:

- Education;
- Internship;
- Research;
- Projects;
- Skills;
- Honors and Certificates;
- Leadership and Service.

Project descriptions will be condensed from the source material into website-readable bullets. The most prominent projects are:

- `Unitree B2` navigation and `OpenClaw` embodied control system integration;
- small Pi biped robot `AMP` reinforcement learning and `Sim2Sim` validation;
- semantic margin-tightened `MPC-SECBF` dynamic obstacle avoidance research;
- `Go2`, `Lite3`, ROS logistics vehicle, smart agriculture robot, and ROS unmanned vehicle projects.

## Conservative Claims

The source material marks several facts as needing confirmation. The website will use conservative wording:

- avoid publishing conflicting undergraduate rank numbers until confirmed;
- describe the computer design competition award without overstating national-level status unless a national certificate is available;
- describe the society role conservatively if president/vice president records conflict;
- describe the `SEESM/MPC-SECBF` paper as research or in-progress work unless submission/publication status is confirmed.

## Verification

After implementation:

- inspect `git diff` for unintended style or unrelated changes;
- run a local Jekyll build if dependencies are available;
- if local build is unavailable, report that explicitly and still verify Markdown/YAML structure by inspection.
