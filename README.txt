v1.6.3 自动更新源（GitHub Pages）

当前版本：v1.6.3 (versionCode 153)，2026-11-06 构建。
上一版本：v1.6.2 (152)，回退包保存在 ../v1.6.2/。

清单地址：
  APK 更新：https://chengyuzi20-sudo.github.io/taobao-coin-updates/update.json
  活动配置：https://chengyuzi20-sudo.github.io/taobao-coin-updates/profiles.json

本目录文件：
  app-1.6.3-<abi>-release.apk  v1.6.3 四个 ABI 的 release 签名包
  update.json                  APK 更新清单（当前仅指向 v1.6.3）
  profiles.json                活动配置清单（version 10，schemaVersion 1）
  profiles/taobao.json         活动配置正文（含赛场 race 区域与新锚点）
  SHA256SUMS.txt               本目录 APK 的校验值（当前 4 个 v1.6.3 包）

清理说明：
  为控制仓库体积，本目录只保留当前版本 APK；v1.5.7 ~ v1.5.13 的旧包已从工作区
  删除，但仍保留在 dist/pages-upload/.git 历史中。v1.5.14 ~ v1.6.2 没有提交到本
  仓库（Pages 只需要 update.json 指向的当前版本），回退包保存在同级 dist/v<版本>/。
  发布说明与旧校验值已归档到 archive/legacy-dist/notes/。

签名说明：
  v1.5.5 起使用固定 release 证书（SHA-256: 6f86a2e10a6906b19a77e6c2c08c8da642a378c81c0833a12fb43c366c9fe46b）。
  此前安装过 debug 签名版本的用户无法覆盖安装，需要卸载后重新安装一次；
  此后所有版本继续使用同一张证书，OTA 可正常覆盖升级。
  签名文件与口令应保存在本机安全位置/CI Secret 中，不要随项目目录打包分发。

以后发新版：
  1. 在 source_taobao_coin_assistant 执行：
       powershell -ExecutionPolicy Bypass -File tools/publish_release.ps1 -Version 1.6.4 -VersionCode 154 -Notes "..."
  2. 确认本目录生成 app-<版本>-<abi>-release.apk，且 update.json 指向版本化 URL；
  3. 校验 SHA256SUMS.txt 与 update.json 中的 sha256 一致；
  4. git add . && git commit -m "Release v1.6.4" && git push。
  Pages 通常 1–2 分钟生效。

说明：
  - 仓库必须是 Public；GitHub Pages 免费版不支持私有仓库。
  - 清单和 APK 必须是 HTTPS，GitHub Pages 默认满足。
  - 如果手机访问 github.io 不稳定，可以把同一目录上传到 Gitee Pages /
    OSS / 自有 Nginx，只改 update.json 里的 4 个 URL。
  - App 内“更新设置”留空时使用内置清单；填写其他地址时优先使用自定义清单。
