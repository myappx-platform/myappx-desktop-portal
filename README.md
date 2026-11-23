# MyAppx Desktop Portal

iDempiere OSGi 插件，在 MyAppx Server 上提供 MyAppx Desktop 的下载页和自动更新源。

上下文路径：`/desktop`（默认 `https://localhost:18443/desktop/`）。

## 提供的内容

| 路径 | 用途 |
| --- | --- |
| `/desktop/` | 下载页（`index.html`） |
| `help.html`、`academy.html`、`upgrade.html`、`changelog.html`、`problem.html` | 客户端菜单里的帮助、说明、升级、更新日志、问题反馈 |
| `linux-desktop-install.html` | Linux 安装说明（当前只发布 Windows x64） |
| `latest.yml` | electron-updater 通用源清单（版本、安装包名、sha512、大小） |
| `latest.txt` | 纯文本版本号，供版本检查 |
| `myappx-desktop-setup-*.exe` 与同名 `.blockmap` | Windows 安装包及增量更新块图 |
| `ping` | 连通性探测，返回 `{"status":"OK"}` |

客户端基址在 `myappx-desktop` 的 `MYAPPX_DESKTOP_BASE_URL`（`src/common/constants.ts`），须与 `electron-builder.ts` 里的 `publish.url` 一致。

## 发布新版本

1. 在 `myappx-desktop` 打出 Windows NSIS 安装包，拿到 `latest.yml`、`*.exe`、`*.blockmap`。
2. 把这三个文件放到本插件根目录。`*.exe` 和 `*.blockmap` 不进 Git，打包前必须在本地放好。
3. 把 `latest.yml` 里的版本、文件名、日期同步到 `latest.txt` 和 `index.html`（下载链接、版本徽标、更新日志）。
4. 重新构建本插件，并更新扩展仓库 `myappx-extension-repository`。

`build.properties` 会把页面、清单和安装包打进 bundle。目录列表已关闭，只提供这些静态文件。
