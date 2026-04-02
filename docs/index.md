# Incident AI 事故分析引擎 - 计算巢部署文档

**项目名称**：Incident AI 事故分析引擎  
**部署平台**：阿里云计算巢（推荐企业用户使用）  
**更新日期**：2026年4月

### 一、产品简介

Incident AI 是一款轻量级 AI 事故分析引擎，能够自动从 Loki / Prometheus 拉取异常日志，使用 Qwen、DeepSeek 等大模型进行智能根因分析，快速生成结构化事故报告，并支持推送至企业微信（同时兼容钉钉、飞书、邮箱、短信）。

核心价值：帮助 SRE 将故障定位和事故复盘时间从 1-2 小时缩短至 10-20 分钟。

### 二、计算巢一键私有化部署

**一键部署地址**：  
[https://computenest.console.aliyun.com/service/instance/create/cn-hangzhou?type=user&ServiceId=service-a98eb17b44db48c3a7b4](https://computenest.console.aliyun.com/service/instance/create/cn-hangzhou?type=user&ServiceId=service-a98eb17b44db48c3a7b4)

#### 部署步骤（3-5分钟完成）

1. 点击上方链接进入计算巢部署页面
2. 在「参数配置」区域填写以下关键参数：

   **必填 / 核心参数**：

   | 参数类别       | 参数名称                    | 说明说明                                      | 示例 / 建议 |
            |----------------|-----------------------------|-----------------------------------------------|-------------|
   | 数据库        | `POSTGRES_PASSWORD`        | PostgreSQL 密码（必须修改为强密码）          | YourStrongPasswordHere123! |
   | 监控服务      | `LOKI_URL`                 | Loki 服务地址（**必填**）                    | http://192.168.1.100:3100 |
   | 通知渠道      | `WECOM_WEBHOOK`            | 企业微信机器人 Webhook（**强烈推荐**）      | https://qyapi.weixin.qq.com/... |
   | AI 模型       | `AI_PROVIDER`              | AI 提供商                                     | `qwen` 或 `deepseek` |
   | AI 模型       | `AI_API_KEY_QWEN`          | 通义千问 API Key（当选择 qwen 时必填）      | sk-xxxxxxxx |
   | AI 模型       | `AI_API_KEY_DEEPSEEK`      | DeepSeek API Key（当选择 deepseek 时必填）  | sk-xxxxxxxx |

   **常用可选参数**：

    - `PROMETHEUS_URL`：Prometheus 服务地址
    - `INCIDENT_SERVICES`：需要监控的服务列表（逗号分隔，例如 `oa-server,admin-server`）
    - `DINGTALK_WEBHOOK`、`FEISHU_WEBHOOK`：钉钉 / 飞书 Webhook
    - `EMAIL_ENABLED`、`EMAIL_FROM`、`EMAIL_TO`：邮件通知配置
    - `SMS_ENABLED`、`SMS_ACCESS_KEY`、`SMS_SECRET_KEY`：阿里云短信配置

3. 参数填写完成后，点击「部署」
4. 等待实例创建和初始化完成（通常 2-5 分钟）
5. 部署成功后，在实例详情页可查看访问地址，打开 Web 界面进行测试

### 三、使用流程

1. 部署完成后，通过 Web 界面手动上传日志或配置定时任务
2. 系统自动从 Loki 拉取异常日志 → AI 智能分析 → 生成结构化报告
3. 报告自动推送至企业微信（或其他配置的渠道）

### 四、注意事项

- 本服务采用**完全私有化部署**，所有数据、日志均运行在您自己的阿里云账号内
- `LOKI_URL` 和 `WECOM_WEBHOOK` 是最核心的两个参数，请确保填写正确且服务可达
- AI 分析质量取决于所选模型 API Key 的有效性和额度
- 首次启动时 PostgreSQL 会自动执行初始化脚本
- 如需自动定时拉取、License 激活、高级定制功能等，请联系获取商业授权

### 五、开源地址

https://gitee.com/Luke-xuedong/incident-community

---

有任何部署问题或需要技术支持，欢迎在 Gitee Issue 留言，或联系我。

**感谢使用 Incident AI！**