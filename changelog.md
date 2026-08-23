## 220260823

## 修复
- 修复 1Pondo 官方 JSON 接口将 UCNAME 标签数组误写入制作商和发行商字段的问题；缺少制作商信息时回退为 1Pondo。

## 验证
- 通过 `tests/crawlers/test_official.py`（21 项）。

## 220260728

## 新增
- 在下载主配置中增加图片压缩开关：启用后在所有图片处理步骤完成后统一压缩，质量为 80，最长边限制为 1100。
- 该选项为个人使用环境添加的自用功能，默认关闭。

## 修复
- 避免水印、Poster 裁剪等前置处理使用高质量写回后再次触发中间压缩，确保图片只在最终步骤处理一次。

## 220260722

## 新增
- 新增独立的封面补图工具：可通过 `scripts/cover_backfill.py` 命令行或 `scripts/cover_backfill_gui.bat` 图形界面，按番号或文件名下载并补齐封面、缩略图。
- 补图工具复用当前 MDCx 配置、站点优先级、命名、裁切和水印规则，并支持批量输入与覆盖已有图片。

## 修复
- `official` 新增 `JIMMY` 前缀路由，`JIMMY-003` 等番号会从 FALENO 官网获取资料。
- 自动最佳海报不再将横向海报作为最终 Poster；存在缩略图时会按原规则从缩略图右侧裁切，修复 `ABF-371` 一类封面未裁剪的问题。
- 所有刮削来源均失败时，日志会列出各站点的具体失败原因，便于定位超时或搜索未匹配。
- 改进 Madouqu 页面请求指纹和页面解析，提升手动指定 Madouqu 时的刮削稳定性。

## 验证
- 已通过 `tests/core/test_web_amazon.py`、`tests/crawlers/test_official.py`、`tests/test_file_crawler_runtime.py`。
