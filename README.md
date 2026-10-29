# 中国综合日历 ICS 订阅部署包

这个小项目会定期下载并合并 ChinaCalendar 项目的日历源，生成一个 `public/china-calendar.ics`，可通过 GitHub Pages 作为单一订阅地址使用。

## 合并内容

- 中国法定节假日、国务院调休补班（上游数据有更新时同步）
- 中国传统节日及部分纪念日
- 二十四节气（来自上游日历源）
- 农历日期及按年份生成的农历相关事件（来自上游日历源）
- 主日历中的其他公历节日

## 重要说明

这是一个**上游数据合并器**，不是自己实现农历/节气天文算法。农历节日和节气的年份覆盖范围、节假日的准确性取决于上游 ICS 数据；法定放假安排应以国务院当年通知为准。合并时按“开始时间 + 标题”去重，但仍建议首次订阅后检查是否有重复或缺项。

## 部署到 GitHub，获得一个可自动更新的订阅 URL

1. 登录 GitHub，创建一个新的 **Public** 仓库，例如 `china-calendar-ics`。
2. 将本压缩包内的全部文件上传到仓库根目录，保持 `.github/workflows/build.yml` 路径不变。
3. 打开仓库 **Settings → Actions → General**，确认允许 Actions 运行；如首次运行未自动启动，在 **Actions** 页面手动运行 `Build combined China calendar`。
4. 打开 **Settings → Pages**，在 **Build and deployment** 中选择 **Deploy from a branch**；分支选 `main`，目录选 `/public`，保存。
5. 等待 Pages 部署完成。订阅地址通常为：

   `https://你的GitHub用户名.github.io/china-calendar-ics/china-calendar.ics`

   将 `你的GitHub用户名` 和 `china-calendar-ics` 换成自己的用户名、仓库名。此 URL 只有在仓库创建并成功部署后才有效。

6. GitHub Actions 每周一自动重建并提交更新；也可在 **Actions → Build combined China calendar → Run workflow** 手动更新。

## 首次运行和排错

- 打开 Actions，确认任务绿色成功。
- 仓库的 `public/china-calendar.ics` 应存在且非空。
- 在浏览器打开 Pages 订阅 URL，应该显示以 `BEGIN:VCALENDAR` 开头的 ICS 文本。
- 如果上游源临时不可用，日志会显示 WARNING；如果所有源均不可用，任务会失败而不会生成空日历。
- 如果 Actions 无法推送，检查仓库 `Settings → Actions → General → Workflow permissions` 是否允许读写仓库内容。

## 三星日历订阅提醒

三星日历不同版本不一定提供“通过 URL 订阅 ICS”的入口。若有“添加日历 / URL 导入”，粘贴上面的订阅 URL。若只有“导入 .ics 文件”，那通常是一次性导入，不会自动同步更新；可改用支持 URL 订阅的日历服务，再同步到三星日历。

## 上游来源

- https://github.com/YangH9/ChinaCalendar
