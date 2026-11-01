v1.5.8 自动更新源（GitHub Pages）

当前版本：v1.5.8 (versionCode 133)，2026-11-01 构建。
已发布版本：v1.3.2 (110) → v1.3.3 (111) → v1.4.0 (115) → v1.5.5 (130) → v1.5.6 (131) → v1.5.7 (132) → v1.5.8 (133)。

清单地址：
  APK 更新：https://chengyuzi20-sudo.github.io/taobao-coin-updates/update.json
  活动配置：https://chengyuzi20-sudo.github.io/taobao-coin-updates/profiles.json

本目录文件：
  app-1.5.8-<abi>-release.apk  v1.5.8 四个 ABI 的 release 签名包（版本化文件名，避免 CDN 旧包配新清单）
  app-1.5.7-<abi>-release.apk  v1.5.7 旧包，保留用于回退
  app-<abi>-release.apk        v1.5.6 旧文件名，保留用于过渡；旧清单仍可下载
  update.json             APK 更新清单
  profiles.json           活动配置清单
  profiles/taobao.json    活动配置正文
  SHA256SUMS.txt          校验值

签名说明：
  v1.5.5 起使用固定 release 证书（SHA-256: 6f86a2e10a6906b19a77e6c2c08c8da642a378c81c0833a12fb43c366c9fe46b）。
  此前安装过 debug 签名版本的用户无法覆盖安装，需要卸载后重新安装一次；
  此后所有版本继续使用同一张证书，OTA 可正常覆盖升级。
  证书文件保存在项目外层的 keys/ 目录，keystore.properties 已被 gitignore。

以后发新版：
  1. 在 source_taobao_coin_assistant 执行 tools/publish_release.ps1（会构建 release 包并更新本地 Pages 暂存）；
  2. 确认本目录生成 app-<版本>-<abi>-release.apk，且 update.json 指向版本化 URL；
  3. 校验 SHA256SUMS.txt 与 update.json 中的 sha256 一致；
  4. git add . && git commit -m "Release vX.Y.Z" && git push。
  Pages 通常 1–2 分钟生效。

说明：
  - 仓库必须是 Public；GitHub Pages 免费版不支持私有仓库。
  - 清单和 APK 必须是 HTTPS，GitHub Pages 默认满足。
  - 如果手机访问 github.io 不稳定，可以把同一目录上传到 Gitee Pages /
    OSS / 自有 Nginx，只改 update.json 里的 4 个 URL。
  - App 内“更新设置”留空时使用内置清单；填写其他地址时优先使用自定义清单。
