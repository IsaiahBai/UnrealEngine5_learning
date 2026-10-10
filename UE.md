# UE 蓝图常用节点介绍

> 适用于 Unreal Engine 4/5 蓝图（Blueprint）。节点名称可能因引擎版本、项目类型和插件而略有差异。

## 1. 事件与流程控制

| 节点                        | 作用                         | 常见用法                                       |
| --------------------------- | ---------------------------- | ---------------------------------------------- |
| **Event BeginPlay**         | Actor/组件开始运行时触发一次 | 初始化变量、绑定输入、创建 UI                  |
| **Event Tick**              | 每帧执行                     | 持续检测、插值、跟随；应避免在其中执行昂贵逻辑 |
| **Event ActorBeginOverlap** | 其他碰撞体进入触发区域       | 拾取物、触发器、伤害区域                       |
| **Event ActorEndOverlap**   | 其他碰撞体离开区域           | 结束提示、停止伤害、清理状态                   |
| **InputAction / InputAxis** | 响应项目输入映射             | 移动、跳跃、交互、镜头控制                     |
| **Branch**                  | 布尔条件分支                 | True/False 两条执行路径                        |
| **Sequence**                | 按顺序执行多个输出           | 初始化多组逻辑、分阶段处理                     |
| **DoOnce**                  | 只允许执行一次               | 一次性提示、开门、触发剧情                     |
| **Do N**                    | 最多执行 N 次                | 限制技能次数、循环触发                         |
| **FlipFlop**                | 在 A、B 两个输出之间交替     | 开关、切换状态                                 |
| **Gate**                    | 控制执行流是否通过           | 开启/关闭输入响应                              |
| **MultiGate**               | 按顺序或随机分发执行流       | 随机事件、轮流播放效果                         |
| **ForLoop**                 | 整数范围循环                 | 批量生成、遍历索引                             |
| **ForEachLoop**             | 遍历数组元素                 | 处理数组中的 Actor、数据或组件                 |
| **WhileLoop**               | 条件满足时持续循环           | 谨慎使用，避免死循环阻塞游戏线程               |
| **Retriggerable Delay**     | 可重新触发的延迟             | 计时、冷却、连续输入防抖                       |

## 2. 变量与数据

| 节点                                     | 作用                       | 使用要点                         |
| ---------------------------------------- | -------------------------- | -------------------------------- |
| **Get/Set Variable**                     | 读取/写入变量              | 将状态、数值集中管理             |
| **Make Struct / Break Struct**           | 组装/拆分结构体            | Transform、Vector、命中结果等    |
| **Select**                               | 根据条件选择一个值         | 比 Branch 更适合给变量赋值       |
| **Is Valid**                             | 判断对象引用是否有效       | 防止访问已销毁或为空的对象       |
| **Set Timer by Event**                   | 按时间调用事件             | 周期逻辑、技能冷却、延迟回调     |
| **Clear and Invalidate Timer by Handle** | 清除定时器并使句柄失效     | Actor 销毁或状态结束时清理       |
| **Random Integer / Random Float**        | 生成随机数                 | 随机伤害、掉落、位置和动画选择   |
| **Clamp (Float/Int)**                    | 将值限制在最小和最大范围   | 限制血量、速度、角度、进度       |
| **Map Range Clamped**                    | 将一个范围映射到另一个范围 | 进度条、距离驱动效果、输入归一化 |
| **Lerp (Float/Vector/Rotator)**          | 线性插值                   | 平滑移动、颜色变化、镜头过渡     |

## 3. 数学与向量

| 节点                                   | 作用                         | 常见场景                        |
| -------------------------------------- | ---------------------------- | ------------------------------- |
| **Add / Subtract / Multiply / Divide** | 基本四则运算                 | 伤害计算、坐标偏移、属性计算    |
| **Abs / Sign / Min / Max**             | 绝对值、符号、最小值、最大值 | 数值判断和归一化                |
| **Vector Length**                      | 获取向量长度                 | 距离、速度大小、范围判断        |
| **Normalize**                          | 将向量转换为单位方向向量     | 移动方向、瞄准方向              |
| **Dot Product**                        | 计算两个向量的点积           | 判断前后关系、视野夹角          |
| **Cross Product**                      | 计算叉积                     | 求垂直方向、判断左右侧          |
| **Get Forward/Right/Up Vector**        | 获取旋转对应的前/右/上方向   | 基于角色朝向移动或发射          |
| **Make Rot from X/Y/Z**                | 根据方向向量生成旋转         | 让物体朝向目标                  |
| **Find Look at Rotation**              | 计算从起点看向目标的旋转     | AI 瞄准、炮塔、摄像机朝向       |
| **Break Hit Result**                   | 拆分射线/碰撞命中信息        | 获取命中位置、法线、Actor、材质 |

## 4. Actor、组件与对象

| 节点                             | 作用                         | 常见用法                       |
| -------------------------------- | ---------------------------- | ------------------------------ |
| **Spawn Actor from Class**       | 生成 Actor                   | 子弹、特效、敌人、道具         |
| **Destroy Actor**                | 销毁 Actor                   | 敌人死亡、临时物体清理         |
| **Get Actor Location/Rotation**  | 获取 Actor 的位置/旋转       | 计算距离、生成物体、同步位置   |
| **Set Actor Location/Rotation**  | 设置 Actor 的位置/旋转       | 传送、移动、朝向调整           |
| **Add Actor World Offset**       | 按世界坐标位移               | 简单移动或位移效果             |
| **Add Actor Local Offset**       | 按自身局部坐标位移           | 沿自身前方/侧方移动            |
| **Set Actor Transform**          | 同时设置位置、旋转和缩放     | 完整变换同步                   |
| **Get Component by Class**       | 获取指定类型组件             | 获取碰撞、网格、运动组件       |
| **Attach Actor to Component**    | 将 Actor 附着到组件          | 武器挂接、道具跟随             |
| **Set Collision Enabled**        | 开启/关闭碰撞                | 无敌、拾取后禁用碰撞           |
| **Line Trace by Channel**        | 发射单条射线检测             | 交互、枪械命中、地面检测       |
| **Sphere Trace by Channel**      | 球形扫掠检测                 | 近战攻击、范围检测             |
| **Box/Capsule Trace by Channel** | 盒体/胶囊体扫掠检测          | 更符合武器或角色形状的检测     |
| **Get All Actors of Class**      | 获取场景中指定类的所有 Actor | 管理器查找对象；数量大时需谨慎 |
| **Get All Actors with Tag**      | 按标签获取 Actor             | 查找任务目标、特定交互物       |

## 5. 角色、移动与动画

| 节点                                   | 作用                       | 使用要点                          |
| -------------------------------------- | -------------------------- | --------------------------------- |
| **Add Movement Input**                 | 向角色移动组件输入方向     | 第三人称/第一人称角色移动核心节点 |
| **Jump**                               | 让角色跳跃                 | 通常绑定 InputAction              |
| **Crouch / UnCrouch**                  | 蹲下/站起                  | 需要角色移动组件支持              |
| **Launch Character**                   | 给角色施加发射速度         | 击退、跳台、爆炸冲击              |
| **Set Movement Mode**                  | 设置行走、下落、飞行等模式 | 空中控制、攀爬和特殊移动          |
| **Play Animation / Play Anim Montage** | 播放动画或动画蒙太奇       | 攻击、受击、交互动作              |
| **Montage Play / Stop**                | 播放/停止蒙太奇            | 配合 AnimBP 管理动作动画          |
| **Set Simulate Physics**               | 开启/关闭物理模拟          | 布娃娃、可推动物体、死亡效果      |

## 6. UI、音频与特效

| 节点                                 | 作用                    | 常见用法                       |
| ------------------------------------ | ----------------------- | ------------------------------ |
| **Create Widget**                    | 创建 UMG 控件实例       | HUD、菜单、提示框              |
| **Add to Viewport**                  | 将控件添加到屏幕        | 显示 UI                        |
| **Remove from Parent**               | 移除控件                | 关闭菜单、清理提示             |
| **Set Visibility**                   | 设置控件或组件可见性    | 显示/隐藏面板、模型和特效      |
| **Set Text / Set Progress**          | 更新文本或进度条        | 血量、弹药、任务进度           |
| **Print String**                     | 在屏幕上打印调试文字    | 快速检查变量和执行路径         |
| **Play Sound 2D**                    | 播放不随距离衰减的声音  | UI 音效、提示音                |
| **Spawn Sound at Location**          | 在世界位置播放声音      | 爆炸、枪声、环境音             |
| **Spawn Emitter at Location**        | 在位置生成粒子特效      | 爆炸、命中、魔法效果           |
| **Niagara Spawn System at Location** | 在位置生成 Niagara 特效 | UE5 推荐的特效生成方式         |
| **Set Niagara Variable**             | 设置 Niagara 参数       | 动态颜色、大小、方向和材质参数 |

## 7. 函数、事件与通信

| 节点                                | 作用                   | 适用场景                                   |
| ----------------------------------- | ---------------------- | ------------------------------------------ |
| **Custom Event**                    | 创建可执行的自定义事件 | 封装流程、网络多播入口                     |
| **Function Call**                   | 调用函数               | 复用逻辑并返回结果                         |
| **Macro**                           | 封装一段可复用节点图   | 通用流程模板；复杂逻辑建议使用函数         |
| **Event Dispatcher**                | 声明并广播事件         | UI 与角色、系统间的松耦合通信              |
| **Bind Event to Dispatcher**        | 绑定事件分发器         | 监听血量变化、任务完成等事件               |
| **Call/Assign Event Dispatcher**    | 广播或绑定分发器       | 发送状态变化通知                           |
| **Cast To**                         | 将对象转换为指定类型   | 访问特定类变量或函数；频繁 Cast 时考虑接口 |
| **Blueprint Interface Message**     | 通过接口调用行为       | 交互系统、跨类通信，减少类型依赖           |
| **Get Player Character/Controller** | 获取玩家角色或控制器   | 玩家输入、相机和角色控制                   |
| **Get Game Mode/Game State**        | 获取游戏规则或共享状态 | 回合、比分、全局游戏状态                   |

## 8. 常用调试节点

- **Print String**：打印文本、数字和布尔值，可设置颜色与持续时间。
- **Draw Debug Line**：绘制调试射线，检查 Trace 起点、终点和方向。
- **Draw Debug Sphere/Box/Capsule**：可视化范围检测和碰撞体。
- **Breakpoints**：在蓝图节点上设置断点，逐步查看执行过程。
- **Watch This Value**：监视变量或引脚值，适合定位状态异常。
- **Execution Flow**：使用节点连线和注释框整理执行路径，减少调试成本。

## 9. 使用建议

1. 将初始化逻辑放在 **BeginPlay**，持续逻辑优先考虑定时器或事件驱动，谨慎使用 Tick。
2. 对可能为空的对象先使用 **Is Valid**，尤其是异步回调、延迟节点和 Actor 引用。
3. 尽量用 **接口、事件分发器** 进行通信，减少层层 Cast 带来的耦合。
4. 对 Trace、Overlap 和定时器及时清理，避免重复绑定和无效引用。
5. 复杂蓝图应拆分为函数、宏或组件，并用注释框标记输入、处理和输出。
6. 网络游戏中注意执行端：服务器负责权威状态，客户端负责表现和本地输入。

## 10. 节点选择速查

- **需要条件判断**：`Branch`
- **需要多路顺序执行**：`Sequence`
- **只执行一次**：`DoOnce`
- **需要延迟或冷却**：`Delay` / `Set Timer by Event`
- **需要平滑变化**：`Lerp` / `Timeline`
- **需要检测前方物体**：`Line Trace by Channel`
- **需要范围攻击**：`Sphere Trace by Channel` 或 `Apply Radial Damage`
- **需要生成对象**：`Spawn Actor from Class`
- **需要销毁对象**：`Destroy Actor`
- **需要更新界面**：`Create Widget`、`Add to Viewport`、`Set Text`
- **需要跨类交互**：优先考虑 `Blueprint Interface`
