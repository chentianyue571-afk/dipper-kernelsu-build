# dipper-kernelsu-build

小米 8（dipper）NGK 内核 + 最新官方 KernelSU 云编译仓库，全自动打包 AnyKernel3 刷机包。

## 用法

1. 进入 **Actions → Build dipper kernel with latest official KernelSU → Run workflow**
2. 可选参数：
   - `kernel_ref`：内核源码分支，默认 `susfs`（已含 SUSFS 补丁 + KSU 挂钩）
   - `ksu_ref`：KernelSU 版本，默认 `main`（最新官方），可填具体 tag
   - `create_release`：构建成功后自动发 Release
3. 构建产物在 Artifacts 和 Releases 里，zip 直接用 TWRP / 管理器刷入

## 内核信息

- 基底源码：`mansiaer/NGK_android_kernel_xiaomi_sdm845`（NoGravityKernel dipper，susfs 分支）
- defconfig：`nh-dipper_defconfig`（CONFIG_KSU=y + CONFIG_KSU_SUSFS=y）
- 工具链：AOSP clang r584948b，LLVM=1 LLVM_IAS=1
- KernelSU：官方 `tiann/KernelSU`，manual hooks 方式集成
- 刷机包配置：supported.versions=13-16（Android 13-16 ROM/GSI），boot 分区直刷

## 注意

- 刷前务必备份原厂 boot.img
- 如果 Actions 构建报 undefined symbol（KSU 版本与源码挂钩 API 不匹配），把 `ksu_ref` 换成与源码同期版本重试
