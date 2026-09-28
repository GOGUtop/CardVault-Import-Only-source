# CardVault · SillyTavern 只读角色卡导入版

这是根据原 CardVault Standalone 源码裁出的 **Import-Only / 只读导入版**。

## 保留

- 云端角色卡浏览、搜索、封面展示
- AI 标签分类与筛选（分类配置/结果仍保存在 SillyTavern 扩展设置中）
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

- Import-Only: `1.2.0`
- 基于用户提供的 `card-main (1).zip` 修改
