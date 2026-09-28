# CardVault · 只读角色卡导入版

> v1.2.4：界面只保留角色卡浏览、服务器共享标签筛选和“自动导入酒馆”。AI 分类、失败重试、手动刷新以及扩展配置面板均已隐藏/移除。

这是根据原 CardVault Standalone 源码裁出的 **Import-Only / 只读导入版**。

## 保留

- 云端角色卡浏览、搜索、封面展示
- AI 标签筛选；启动/刷新卡库时读取 Full + Anima 写入 CardVault 云端内部数据卡的分类
- 角色详情查看
- **自动导入酒馆**：读取 CardVault 角色文件，导入 SillyTavern，并补齐卡内世界书与 Scoped Regex
- 导入守护：已导入角色的卡内世界书/Scoped Regex 缺失时可自动补回
- CardVault 固定账号自动登录、令牌失效自动重连

## 已删除/禁用

- 角色卡上传
- 本地角色备份、批量备份
- 批量删除云端角色卡
- 游玩备份 / 冷库存档及其恢复、归档、同步归还
- 世界书/正则/附件/角色卡的本地下载按钮
- Anima 世界书入口（原上传的这份源码本身没有该入口，本构建也不新增）

另外，`apiFetch()` 在本构建中只允许对 CardVault 发出 `GET/HEAD` 请求；任何 POST/PUT/PATCH/DELETE 都会直接报错。登录请求是独立的 `/api/login`，不属于卡库数据写操作。

## 安装

把本目录放在 GitHub 仓库根目录，或直接放入 SillyTavern 的第三方扩展目录。至少保留：

```text
manifest.json
index.js
style.css
settings.html
```

## 版本

### 1.2.3：读取 CardVault 云端分类 + 悬浮球半隐藏吸边

- 只读版会从 CardVault 卡库中的内部分类数据库卡读取 Full+Anima 已完成的 AI 分类，不再依赖两个插件必须处于同一个浏览器 localStorage。
- 内部分类数据库卡不会显示在插件角色卡列表中；只读版仍严格禁止 POST/PUT/PATCH/DELETE。
- 悬浮球松手后吸进屏幕边缘约 50%，只露出半个球，减少遮挡。


- Import-Only: `1.2.3`
- 基于用户提供的 `card-main (1).zip` 修改

### 1.2.2：修复读取 Full+Anima 永久分类

- 本版本**不负责写入永久 AI 分类**；现在会同时读取 Full + Anima 写入的 SillyTavern 共享设置 `cardvault-ai-classifications-shared-v1` 与 localStorage 镜像，并在每次读取设置时重新合并，修复切换版本后看不到已分类结果的问题。
- 悬浮球改为 0px 真正贴边，并加入移动端窗口级 `pointerup` 兜底；拖动松手后强制吸附到最近的左 / 右屏幕边缘。
