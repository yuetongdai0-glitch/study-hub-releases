# 备考复习 · 发布仓库

移动端安装包与版本清单。文件由主仓库 `pnpm release:build` 自动生成并推送，**不要手改**。

## 目录

| 路径 | 说明 |
|---|---|
| `index.html` | 下载页（Pages 首页） |
| `app-version.json` | 应用内更新清单，安卓 App 启动时读取 |
| `releases/android/*.apk` | 安卓安装包（release，已签名） |
| `releases/ios/*.ipa` | iOS 安装包（未签名，需自行重签） |

## 链接

- 下载页：https://yuetongdai0-glitch.github.io/study-hub-releases/
- 版本清单：https://yuetongdai0-glitch.github.io/study-hub-releases/app-version.json
- 网页版：https://yuetongdai0-glitch.github.io/study-review-hub/

## 应用内更新怎么工作

1. App 启动或点击左上角刷新按钮 → `GET app-version.json`（带 `Cache-Control: no-cache`）。
2. 清单里的 `android.versionCode` 大于已装版本 → 显示「发现新版本」。
3. 下载 `android.apkUrl` → 校验整包 `sha256` → 校验新包签名与已装包一致 → 调系统安装器。

因此**发布新版本必须递增主仓库根 `package.json` 的版本号**，`versionCode` 由它推导（主×10000 + 次×100 + 修订），签名 keystore 必须保持同一份。

## 旧版本

每次发布会新增当次文件；不再需要时可手动删除旧文件，同时注意 `app-version.json` 只指向最新版本，删旧文件不影响更新。

## iOS

iOS 不允许侧载未签名应用。下载页提供未签名 IPA，需用 AltStore / Sideloadly / Xcode 以个人 Apple ID 重签后安装。
