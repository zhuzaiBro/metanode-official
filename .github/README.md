# GitHub Actions 部署到七牛云配置说明

本项目提供了两种部署方案，你可以选择其中一种使用：

## 方案一：使用 qshell（推荐，功能更强大）

使用文件：`.github/workflows/deploy-to-qiniu.yml`

### 配置步骤

1. **在 GitHub 仓库中设置 Secrets**
   
   在 GitHub 仓库设置 → Secrets and variables → Actions 中添加：
   - `QINIU_ACCESS_KEY`: 七牛云的 Access Key
   - `QINIU_SECRET_KEY`: 七牛云的 Secret Key
   - `QINIU_CDN_URL` (可选): CDN 刷新 URL，格式如：`https://your-domain.com/*`

2. **修改配置文件**
   
   编辑 `.github/qiniu-config.json` 文件：
   - `bucket`: 你的七牛云存储空间名称
   - `key_prefix`: 文件上传的前缀路径（如果需要上传到子目录）
   - `ignore_dir`: 需要忽略的目录列表

3. **触发部署**
   - 自动触发：推送到 `main` 分支时自动部署
   - 手动触发：在 GitHub Actions 页面手动触发

---

## 方案二：使用现成的 Action（更简单）

使用文件：`.github/workflows/deploy-to-qiniu-simple.yml`

### 配置步骤

1. **在 GitHub 仓库中设置 Secrets**
   
   - `QINIU_ACCESS_KEY`: 七牛云的 Access Key
   - `QINIU_SECRET_KEY`: 七牛云的 Secret Key
   - `QINIU_BUCKET`: 七牛云存储空间名称

2. **修改 workflow 文件（可选）**
   
   编辑 `deploy-to-qiniu-simple.yml` 中的 `ignore` 部分，添加需要忽略的文件

3. **触发部署**
   - 自动触发：推送到 `main` 分支时自动部署
   - 手动触发：在 GitHub Actions 页面手动触发

---

## 注意事项

1. 确保七牛云存储空间已创建并配置好
2. 确保 Access Key 和 Secret Key 有足够的权限
3. 如果使用 CDN，需要配置 CDN 刷新 URL
4. 首次运行时可能需要调整忽略文件列表

## 选择建议

- **方案一**：适合需要更精细控制、需要 CDN 刷新等高级功能的场景
- **方案二**：适合快速部署、配置简单的场景

**注意**：两个方案只需要启用其中一个，如果都启用可能会重复部署。建议删除不需要的那个 workflow 文件。

