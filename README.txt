v1.5.6 自动更新源（GitHub Pages）

当前版本：v1.5.6 (versionCode 131)，2026-10-31 构建。
已发布版本：v1.3.2 (110) → v1.3.3 (111) → v1.4.0 (115) → v1.5.5 (130) → v1.5.6 (131)。

清单地址：
  APK 更新：https://chengyuzi20-sudo.github.io/taobao-coin-updates/update.json
  活动配置：https://chengyuzi20-sudo.github.io/taobao-coin-updates/profiles.json

本目录文件：
  app-<abi>-release.apk   四个 ABI 的 release 签名包（v1.5.5 起）
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
  1. 在 source_taobao_coin_assistant 执行 tools/publish_release.ps1（会构建 release 包）；
  2. 把 app/build/outputs/apk/release 下的 4 个 app-<abi>-release.apk 复制到本目录；
  3. 更新 update.json（版本号、URL、SHA-256、notes）与 SHA256SUMS.txt；
  4. git add . && git commit -m "Release vX.Y.Z" && git push。
  Pages 通常 1–2 分钟生效。

说明：
  - 仓库必须是 Public；GitHub Pages 免费版不支持私有仓库。
  - 清单和 APK 必须是 HTTPS，GitHub Pages 默认满足。
  - 如果手机访问 github.io 不稳定，可以把同一目录上传到 Gitee Pages /
    OSS / 自有 Nginx，只改 update.json 里的 4 个 URL。
  - App 内“更新设置”留空时使用内置清单；填写其他地址时优先使用自定义清单。
