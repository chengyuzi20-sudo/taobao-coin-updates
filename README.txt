v1.3.2 自定义 HTTPS 更新源（不切换 GitHub 账号）

已执行完成（2026-10-27）：
  仓库：https://github.com/chengyuzi20-sudo/taobao-coin-updates
  清单：https://chengyuzi20-sudo.github.io/taobao-coin-updates/update.json
  Pages 状态：built（HTTPS 已启用）

手机 App → 应用更新 → 更新设置 → 填上面的清单地址 → 保存 → 检查更新。
v1.3.1 (109) 会看到 v1.3.2 (110)。

以后发新版：
  1. 把新的 4 个 APK 复制到本目录（文件名保持 app-<abi>-debug.apk）；
  2. 更新 update.json 的 versionCode/versionName/notes/sha256；
  3. git add . && git commit -m "Release vX.Y.Z" && git push
  Pages 会自动重建，通常 1–2 分钟生效。

以下为首次创建步骤（已完成，留作参考）
------------------------------------------------------------------
一、用当前账号创建公开仓库并上传（PowerShell）
------------------------------------------------------------------
cd "D:\淘宝双十一自动化项目\dist\pages-upload"

git init
git branch -M main
git config user.name "chengyuzi20-sudo"
git config user.email "chengyuzi20-sudo@users.noreply.github.com"
git add .
git commit -m "Add TaobaoCoinAssistant v1.3.2 update manifest"

$gh = "D:\Temp\ghex\bin\gh.exe"
& $gh repo create taobao-coin-updates --public --source=. --remote=origin --push

# 开启 GitHub Pages（main 分支根目录）
Set-Content -Path pages.json -Value '{"source":{"branch":"main","path":"/"}}' -Encoding ASCII
& $gh api -X POST repos/chengyuzi20-sudo/taobao-coin-updates/pages --input pages.json

# 查看 Pages 地址，通常是：
# https://chengyuzi20-sudo.github.io/taobao-coin-updates/
& $gh api repos/chengyuzi20-sudo/taobao-coin-updates/pages --jq ".html_url"

二、等 1–2 分钟，浏览器确认清单可访问
------------------------------------------------------------------
https://chengyuzi20-sudo.github.io/taobao-coin-updates/update.json

能看到 versionCode 110 / versionName 1.3.2 就说明 Pages 已生效。

三、手机上切换更新源
------------------------------------------------------------------
App → 应用更新 → 更新设置 → 填：
https://chengyuzi20-sudo.github.io/taobao-coin-updates/update.json
→ 保存 → 检查更新。

v1.3.1 (109) 会看到 v1.3.2 (110)，下载后校验 SHA-256、包名、versionCode
和签名，再由系统安装器覆盖安装。

说明：
- 仓库必须是 Public；GitHub Pages 免费版不支持私有仓库。
- 清单和 APK 必须是 HTTPS，GitHub Pages 默认满足。
- 如果手机访问 github.io 不稳定，可以把同一目录上传到 Gitee Pages /
  OSS / 自有 Nginx，只改 update.json 里的 4 个 URL。
- 以后发新版本：替换本目录的 APK 和 update.json，commit + push 即可。
- 想恢复默认的 Doplars GitHub Releases：在 App 的更新设置里清空清单地址。
