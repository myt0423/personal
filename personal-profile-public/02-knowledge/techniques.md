# 02 · 方法论与踩坑记录

> 只写**我自己验证过**的。格式：问题 → 做法 → 坑。

---

## Windows 上没有 node 怎么跑 JS 工具

**问题**：系统没装 node/npm，但很多 CLI 工具是 `bin/xxx.js`。

**做法（按优先级）**：

1. `bun`（本机已有）：`& "$env:USERPROFILE\.dsh\tools\bun-portable\package\bin\bun.exe" script.js`
2. Electron 当 node：
   ```powershell
   $env:ELECTRON_RUN_AS_NODE="1"
   & "I:\Deepseek\DeepSeek Harness.exe" script.js
   ```
   好处：`process.versions.electron` 存在，能读写 `app.asar` 内部（普通 node 不能）。
3. 桌面版自带的 `resources\runtime\bin\node.cmd`（依赖 `DSH_DESKTOP_NODE_EXECUTABLE`）

**坑**：
- `Harness.exe -e "..."` 不输出内容，必须写成 `.js` 文件再跑。
- 从 bun/独立脚本跑插件 CLI 时，插件往往认不出「当前宿主」，要显式给 `DSH_BASE`。

---

## 定位「DSH 插件到底装在哪」

```powershell
$env:DSH_HOME            # %USERPROFILE%\.dsh
$env:DSH_PROFILE         # desktop
Get-Content "$env:DSH_HOME\profiles\$env:DSH_PROFILE\package.json"
```

- 插件在 `profiles\<profile>\node_modules\<包名>`
- 要在界面里出现，包名还必须写进 `package.json` 的 `dsh.profile.bundles`
- 只装依赖、不加 bundles = 装了但不加载

---

## 没有 sqlite3 命令行怎么读 SQLite

`C:\Windows\System32\winsqlite3.dll` 是系统自带的 SQLite，可以 P/Invoke：

```powershell
Add-Type -Name W -Namespace S -MemberDefinition @'
[DllImport("winsqlite3.dll")] public static extern int sqlite3_open_v2(byte[] f, out IntPtr db, int flags, IntPtr vfs);
'@
```

或者直接用分发里的 Python（自带 `sqlite3` 模块），别去装命令行工具。

---

## 微信 4.x 数据库是 SQLCipher4

- `contact.db` 文件头不是 `SQLite format 3\0`（实测 `06 25 42 76 8b 5a 66 da ...`）= 加密
- 参数：page 4096、PBKDF2-HMAC-SHA512 / 256000 迭代、HMAC-SHA512
- key 是 32 字节 raw key，存在 `Weixin.exe` 进程内存里；用 db 前 16 字节 salt 作锚点在内存中定位，再用「解第一页能否还原 `SQLite format 3`」验证
- 定位不到 key 时，先确认微信真的在跑（只有 `WeChatAppEx.exe` 不算）

---

## 插件「装好了但不生效」的通用排查顺序

```text
1. 装上了吗      → profiles/<p>/node_modules/<包>
2. 会被加载吗    → package.json 的 dsh.profile.bundles 里有吗
3. 落地了吗      → 插件自己的 status / selfcheck
4. 重启了吗      → 宿主补丁类改动必须退出重开
5. 证据是什么    → 有没有真实命令输出，还是"应该生效了"
```

第 5 条最重要：**没有输出 = 没有证据 = 不算完成**。

---

## 判断一个「一段话搞定」的教程值不值得跟

看它有没有回答这三个问题：

1. 东西存在哪（路径 / 仓库 / 账号）
2. 怎么验证它真的生效（可观测的证据）
3. 出问题了怎么退回

三个都答不上的，基本是演示视频。
