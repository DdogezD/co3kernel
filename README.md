<div align = center>
<h1>CO³Kernel</h1>

***C**ustom **O**nePlus **O**pen **O**ptimized **K**ernel*

这是为 Hedwig/Xueying (OnePlus Open) 编译的客制化内核
<h1></h1>
</div>

#### 👾 内核级 root impl. 
- KernelSU Next: v1.1.0 (Manual Hooks)
- KernelSU Scope Minimized Hooks: v1.5
- Mountify 支持: tmpfs: 支持拓展属性

#### ⚡ CPU 优化
- cpuidle: 去除 menu 的 iowait
- fair: PELT 半衰期 32ms 减少到 16ms
- fair: 减少任务迁移开销

#### 📦 内存优化
- lz4: v1.10.0
- 优化的 mem* (~25%+ faster)
  - memcpy
  - memmove
  - memset
- vmalloc: 支持大块虚拟内存
- mm: 不为 user/admin 登录而保留内存 (~136m)
- arm64: clear_page 对齐 16b
- 小幅 zram 优化

#### 📀 存储优化
- fs: 减少缓存以发挥大内存的作用
- fs: 对齐 8b

#### 🖨️ 妥协调试效率换取的性能提升
- 禁用 KFENCE & UBSAN
- BLK/BLKdev 不收集 io stat
- 去除 drm 中的 debug
- 去除 psi 中的 debug
- arm64: 关闭 self-hosted debug
- selinux: 去除对 audit 的依赖以提升性能

#### 🔓 妥协安全性换取的性能提升

- 禁用软件模拟的 PAN 以提升性能
- 禁用 Meltdown 缓解措施 (在 EL0 上作 unmap 处理) 以提升性能
- 禁用 Spectre 缓解措施 (禁用基于历史的分支预测) 以提升性能

#### 🦄 编译器优化
  - 启用 o3 优化编译
  - 启用 llvm Polly 优化器
  - 对 freezer_trap 作 LTO noinline 处理

#### 🔨 小幅调整
- 使用 TCP_NODELAY
- 通过禁用所有 I/O 调速器, 将 I/O 调速器配置为 "none"
- 额外的省电工作队列配置
- RCU: 修复省电工作队列造成的性能损失
- 更快的整数平方根算法
- arm64: 默认使用 LSE 原子指令集
- 相对宽容的 alarmtimer, 避免阻止 suspend
- selinux: 避免动态内存分配
- sched idle loop 中省略多余的获取内存屏障
- ttwu 流程中省略多余的获取内存屏障

## 🍀 特别感谢

[OnePlus OSS/sm8550](https://github.com/OnePlusOSS/android_kernel_common_oneplus_sm8550/tree/oneplus/sm8550_v_15.0.0_oneplus_open)

此内核合并了来自 **Sultan, arter97, Pzqqt, brokestar233, ztc1997, hfdem** 等内核开发者的提交。

感谢 **Pzqqt, brokestar233, Cloud_Yun** 提供了开发指导。

内核开发者们的排名不分先后。
