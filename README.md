<p align="center">
  <img src="./assets/brand-avatar.png" width="220" height="220" alt="牛牛做梦">
</p>

<h1 align="center">牛牛做梦 pallas-plugin-dream</h1>

<p align="center">提供群内梦话漂流、历史梦与醉酒联动能力。</p>

<p align="center">
  <img alt="官方插件" src="https://img.shields.io/badge/%E5%AE%98%E6%96%B9%E6%8F%92%E4%BB%B6-FE7D37">
  <img alt="控制台插件商店" src="https://img.shields.io/badge/%E6%8E%A7%E5%88%B6%E5%8F%B0-%E6%8F%92%E4%BB%B6%E5%95%86%E5%BA%97-4EA94B">
  <img alt="安装命令" src="https://img.shields.io/badge/uv%20run%20pallas%20ext%20install%20pallas--plugin--dream-586069">
  <img alt="PyPI 版本" src="https://img.shields.io/pypi/v/pallas-plugin-dream?label=%E7%89%88%E6%9C%AC&color=2563EB">
</p>

## 安装方式

需已安装 [Pallas-Bot](https://github.com/PallasBot/Pallas-Bot) **≥ 4.0**。

推荐直接在控制台插件商店安装，或在本体项目中执行：

```bash
uv run pallas ext install pallas-plugin-dream
```

也可单独安装本包：

```bash
uv pip install pallas-plugin-dream
```

开发联调：clone 本仓库后 `uv pip install -e .`。

## 多进程分片

- **hub 与每个 worker 须安装相同版本**；共享 **`data/`** 与 Redis 协调层。
- 梦话漂流经本体 **`plugin_coord.dream`**；未安装扩展时不影响 core。

详见：[多进程分片](https://PallasBot.github.io/Pallas-Bot-Docs/architecture/bot-process-sharding)

## 怎么使用

做梦期间推送梦话：跨群漂流、历史梦、画画归档图、复读已学句；醉酒时更密且可联动夺舍。

### 用户命令

| 口令 / 触发 | 场景 | 说明 |
| --- | --- | --- |
| `牛牛做梦` | 群内 | 进入做梦约 5～15 分钟 |
| `牛牛醒梦` / `牛牛别做梦` | 群内 | 结束做梦 |
| `牛牛醒一醒` | 群内 | 醒酒时亦会醒梦（见 `plugins-party`） |

### 命令权限

| 命令 ID | 默认等级 |
| --- | --- |
| `dream.ban_cleanup` | 群管或号主 |

（与复读共用「不可以」清理梦库，权限见帮助详情。）

> 详细用法、限制条件和可用范围以帮助为主。

## 配置项

WebUI **插件 → dream**，或本仓库 [`config.py`](src/pallas_plugin_dream/config.py)：`dream_worker_sleep_*`、`dream_drift_queue_tick_probability`、`dream_message_retention_days` 等。

## 排障

| 现象 | 处理 |
| --- | --- |
| 无梦话 | 确认已做梦、冷却未挡；他群无做梦则无漂流 |
| 梦库过大 | 运维可调用库清理逻辑 |

## 实现

源码位置：[`src/pallas_plugin_dream/`](src/pallas_plugin_dream/)

实现要点：

- 做梦后会按配置周期推送梦话，并可跨群漂流。
- 分片模式下依赖共享 `data/` 与协调层保持行为一致。
- 醉酒等其他玩法会影响梦话频率与联动表现。

## 相关链接

| 说明 | 链接 |
| --- | --- |
| 牛牛做梦 · 用户文档 | [文档站 · dream](https://PallasBot.github.io/Pallas-Bot-Docs/plugins/dream) |
| 插件开发入门 | [develop/plugin/getting-started](https://PallasBot.github.io/Pallas-Bot-Docs/develop/plugin/getting-started) |
