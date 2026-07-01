# 🌧️ 雨云自动签到 (GitHub Actions 版) v2.5



雨云（Rainyun）每日自动签到工具，支持 **GitHub Actions 一键部署**，无需服务器即可实现每日自动签到、积分累计。

## ✨ 功能特性

| 功能 | 状态 | 说明 |
|------|------|------|
| [X] 每日自动签到 | 🟢 支持 | 全自动登录 + 验证码识别 |
| [X] 验证码识别 | 🟢 支持 | 使用 ddddocr 自动识别滑块验证码 |
| [X] 多平台通知 | 🟢 支持 | Server酱、Bark 等通知渠道 |
| [X] GitHub Actions 部署 | 🟢 支持 | 无需服务器，完全免费 |
| [X] Docker 支持 | 🟢 支持 | 可选 Docker 容器化部署 |
| [X] 随机延迟 | 🟢 支持 | 避免请求模式被识别 |
| [X] 仓库自动保功能 | 🟢 支持 | 防止60天不动被关 |
| 📊 积分查询 | 🟢 支持 | 显示当前积分和人民币价值 |

## 🚀 快速开始

### 1. Fork 仓库
[https://img.shields.io/badge/Fork-本仓库-4285F4?style=for-the-badge&logo=github](https://github.com/0x6768/Rainyun-Checkin/fork)

点击上方按钮或访问 https://github.com/0x6768/Rainyun-Checkin/fork

### 2. 配置环境变量
1. 进入你 Fork 的仓库
2. 点击 **Settings** → **Secrets and variables** → **Actions**
3. 点击 **New repository secret** 添加以下必需环境变量：

| 变量名 | 说明 | 获取方式 |
|--------|------|----------|
| `RAINYUN_USER` | 雨云登录邮箱 | 你的雨云账号邮箱 |
| `RAINYUN_PWD` | 雨云登录密码 | 你的雨云账号密码 |

### 3. 测试运行
1. 点击 **Actions** 标签页
2. 在左侧选择 **雨云自动签到** 工作流
3. 点击 **Run workflow** 手动执行
4. 等待约 1-2 分钟完成首次测试

### 4. 查看结果
[X] 成功后，每天 **UTC 0:00**（北京时间 8:00）会自动执行

## ⚙️ 环境变量配置

### 📋 必需环境变量
| 变量名 | 说明 | 示例值 | 是否保密 |
|--------|------|--------|----------|
| `RAINYUN_USER` | 雨云登录用户名 | `your_email@example.com` | [X] 是 |
| `RAINYUN_PWD` | 雨云登录密码 | `your_password_123` | [X] 是 |

### 🔧 可选环境变量
| 变量名 | 说明 | 默认值 | 建议设置 |
|--------|------|--------|----------|
| `TIMEOUT` | 页面加载超时（秒） | `20` | 网络差可设为 `30` |
> 如果需要设置`TIMEOUT`请前往checkin.yml文件取消对应的注释, 并在**Repository Secret**中添加`TIMEOUT`

### 🔧 高级配置（通常无需修改）
| 变量名 | 说明 | 默认值 | 适用场景 |
|--------|------|--------|----------|
| `CHROME_BIN` | Chrome 路径 | 自动检测 | 自定义 Chrome 路径 |
| `CHROMEDRIVER_PATH` | ChromeDriver 路径 | `/usr/local/share/chromedriver-linux64/chromedriver` | ChromeDriver 路径问题 |

## 📁 项目结构
```
Rainyun-Checkin/
├── .github/workflows/          # GitHub Actions 工作流
│   └── checkin.yml      # 自动签到工作流       
├─ api_client.py      
├─ config.py          
├─ cookies.json       
├─ notify.py          
├─ rainyun.py         
├─ README.md          
├─ requirements.txt   
├─ server_manager.py  
└─ stealth.min.js     
```

## 🔍 故障排除

### 常见问题
| 问题 | 解决方案 |
|------|----------|
| ❌ 登录失败 | 检查账号密码是否正确，网络是否正常 |
| ❌ 验证码识别失败 | 增加 `TIMEOUT` 到 30 秒，网络问题可能导致图片下载失败 |
| ❌ ChromeDriver 错误 | 确保 `CHROMEDRIVER_PATH` 正确，或使用默认值 |

### 查看日志
1. GitHub Actions 执行页面的 **Run Workflow** 步骤
2. 展开每个步骤查看详细输出
3. 如有错误，截图 Issue 方便排查

## ⏰ 执行时间
- **默认**：每天 UTC 8:00（北京时间 14:00）
- **修改**：编辑 `.github/workflows/checkin.yml` 中的 `cron` 表达式
- **时区**：GitHub Actions 使用 UTC 时间

```yaml
# 示例：每天北京时间 8:00 执行
schedule:
  - cron: '0 0 * * *'  # UTC 0:00 = 北京时间 8:00
```

## 🔄 更新脚本
```bash
# 同步上游更新
git remote add upstream https://github.com/0x6768/Rainyun-Checkin.git
git fetch upstream
git merge upstream/main
```

## 🤝 贡献指南
欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建功能分支：`git checkout -b feature/your-feature`
3. 提交更改：`git commit -m 'Add some feature'`
4. 推送到分支：`git push origin feature/your-feature`
5. 提交 Pull Request

## 📄 许可证
本项目采用 MIT 许可证 - 查看 LICENSE 文件了解详情

## 🙏 致谢
本项目基于以下优秀项目二次开发：

| 版本 | 作者 | 仓库 | 主要贡献 |
|------|------|------|----------|
| 原版 | SerendipityR | https://github.com/SerendipityR-2022/Rainyun-Qiandao | 初始 Python 实现 |
| 二改 | fatekey | https://github.com/fatekey/Rainyun-Qiandao | Docker 化改造 |
| 三改 | Jielumoon | https://github.com/Jielumoon/Rainyun-Qiandao | 稳定性优化 |
| 四改 | 0x6768 | https://github.com/0x6768/Rainyun-Checkin | GitHub Actions 集成 移除了服务器端管理功能 |

## ⭐ 支持项目
如果这个项目对你有帮助，请点个 Star ⭐ 支持一下！

---

**免责声明**：本项目仅供学习交流使用，请遵守雨云服务条款，合理使用自动签到功能。
