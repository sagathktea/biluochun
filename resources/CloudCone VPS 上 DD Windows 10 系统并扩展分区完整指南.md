# CloudCone VPS 上 DD Windows 10 系统并扩展分区完整指南

## 前言
本文将详细介绍如何在 CloudCone VPS 上通过 DD 方式安装 Windows 10 系统，包括分区扩展和系统激活等完整流程。适用于需要 Windows 环境的开发者和管理员。

👉 [【点击查看】2025年最新CloudCone优惠码及特价云服务器方案汇总](https://bit.ly/Cloudcone)

## 准备工作
### 系统要求
- CloudCone VPS 实例
- 至少 2GB 内存
- 推荐使用 Debian 9.9 作为初始系统

## DD Windows 10 详细步骤

### 1. 进入救援模式
1. 在 CloudCone 控制面板启用救援模式(Recovery Mode)
2. 记录救援模式密码
3. 通过 VNC 连接到救援模式

### 2. 执行 DD 命令
bash
wget -O- https://go.520.be/win10 | gunzip | dd of=/dev/vda

等待命令执行完成，直到看到成功提示。

### 3. 替代 DD 方法（无需救援模式）
bash
bash <(wget --no-check-certificate -qO- 'https://moeclub.org/attachment/LinuxShell/InstallNET.sh') -dd "系统镜像地址"

可用镜像地址：
- Windows 10 LTSC 64位中文版：
  `https://image.moeclub.org/GoogleDrive/1OVA3t-ZI2arkM4E4gKvofcBN9aoVdneh`

## Windows 10 初始设置

### 1. 首次登录
- 用户名：Administrator
- 初始密码：ievo.top
- 如遇 Grub 界面，按 C 键输入 `exit` 继续启动

### 2. 修改密码
cmd
net user Administrator YourNewPassword

### 3. 网络配置
cmd
netsh ipv4 set address name="Ethernet" static <IP> <Netmask> <Gateway>
netsh int ipv4 set dns name="Ethernet" static 1.1.1.1

## 远程桌面配置

### 1. 启用远程桌面
1. 通过注册表修改端口
2. 配置防火墙允许远程桌面连接
3. Mac 用户可使用 Microsoft Remote Desktop 客户端连接

### 2. 解决中文显示问题
确保系统区域设置正确，安装必要的中文字体包。

## 分区扩展教程

### 方法一：使用系统自带工具
1. 打开"磁盘管理"
2. 右键点击 C 盘选择"扩展卷"
3. 按照向导完成分区扩展

### 方法二：使用分区助手
1. 下载安装分区助手
2. 选择 C 盘并点击"调整/移动分区"
3. 拖动滑块扩展分区大小
4. 提交操作并等待完成

## Windows 激活指南

### KMS 激活步骤
1. 访问 kms 激活网站获取脚本
2. 以管理员身份运行 CMD
3. 执行激活命令：
   cmd
   slmgr /skms kms.ievo.top
   slmgr /ato
   

### 验证激活状态
cmd
slmgr /xpr

### 取消激活
cmd
slmgr /upk
slmgr /ckms
slmgr /rearm

## 其他 Windows 镜像资源
- Windows 10 LTSC 精简版镜像
- Windows Server 2019 镜像
- 各版本 MD5 校验值

## 常见问题解答
Q: DD 过程中断怎么办？
A: 重新启动救援模式并再次执行 DD 命令

Q: 分区无法扩展？
A: 确保没有未分配空间，或使用专业分区工具

Q: 激活失败如何解决？
A: 尝试更换 KMS 服务器或检查网络连接

---

👉 [立即获取 CloudCone 最新优惠，享受高性能云服务器](https://bit.ly/Cloudcone)