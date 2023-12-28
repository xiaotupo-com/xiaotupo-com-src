- `npm -v` 查看 `npm` 版本
- `npm install -g npm` 升级 `npm` 版本
- `npm install <Module Name>` 安装模块
- `npm install express` 本地安装
- `npm install express -g` 全局安装
- `npm config set proxy null` 情况代理
- `npm list -g` 查看全局安装的模块
- `npm list grunt` 查看某个模块
- `npm uninstall express` 卸载模块
- `npm update express` 更新模块
- `npm search express` 更新模块
- `npm init` 创建模块
- `npm help <command>` 查看命令帮帮
- `npm cache clear` 可以情况 `NPM`本地缓存
- `npm config list` 查看基本配置
- `npm config get prefix` 获取全局安装的默认路径
- `npm config set prefix "directory"` 设置全局安装的默认路径

## npm config list

查看基本配置：

```powershell
PS E:\tmp> npm config list
; "builtin" config from E:\bin\nodejs\node_global\node_modules\npm\npmrc

; prefix = "C:\\Users\\freer\\AppData\\Roaming\\npm" ; overridden by user

; "user" config from C:\Users\freer\.npmrc

cache = "e:\\bin\\nodejs\\node_cache"
prefix = "e:\\bin\\nodejs\\node_global"

; node bin location = E:\Program Files\nodejs\node.exe
; node version = v20.9.0
; npm local prefix = E:\tmp
; npm version = 9.6.4
; cwd = E:\tmp
; HOME = C:\Users\freer
; Run `npm config ls -l` to show all defaults.
```

## npm config list -l

查看所有配置：

```powershell
PS E:\tmp> npm config list -l
; "default" config from default values

_auth = (protected)
access = null
all = false
allow-same-version = false
also = null
audit = true
audit-level = null
auth-type = "web"
before = null
bin-links = true
browser = null
ca = null
; cache = "C:\\Users\\freer\\AppData\\Local\\npm-cache" ; overridden by user
cache-max = null
cache-min = 0
cafile = null
call = ""
cert = null
ci-name = null
cidr = null
color = true
commit-hooks = true
depth = null
description = true
dev = false
diff = []
diff-dst-prefix = "b/"
diff-ignore-all-space = false
diff-name-only = false
diff-no-prefix = false
diff-src-prefix = "a/"
diff-text = false
diff-unified = 3
dry-run = false
editor = "C:\\Windows\\notepad.exe"
engine-strict = false
fetch-retries = 2
fetch-retry-factor = 10
fetch-retry-maxtimeout = 60000
fetch-retry-mintimeout = 10000
fetch-timeout = 300000
force = false
foreground-scripts = false
format-package-lock = true
fund = true
git = "git"
git-tag-version = true
global = false
global-style = false
globalconfig = "e:\\bin\\nodejs\\node_global\\etc\\npmrc"
heading = "npm"
https-proxy = null
if-present = false
ignore-scripts = false
include = []
include-staged = false
include-workspace-root = false
init-author-email = ""
init-author-name = ""
init-author-url = ""
init-license = "ISC"
init-module = "C:\\Users\\freer\\.npm-init.js"
init-version = "1.0.0"
init.author.email = ""
init.author.name = ""
init.author.url = ""
init.license = "ISC"
init.module = "C:\\Users\\freer\\.npm-init.js"
init.version = "1.0.0"
install-links = false
install-strategy = "hoisted"
json = false
key = null
legacy-bundling = false
legacy-peer-deps = false
link = false
local-address = null
location = "user"
lockfile-version = null
loglevel = "notice"
logs-dir = null
logs-max = 10
; long = false ; overridden by cli
maxsockets = 15
message = "%s"
metrics-registry = "https://registry.npmjs.org/"
node-options = null
noproxy = [""]
offline = false
omit = []
omit-lockfile-registry-resolved = false
only = null
optional = null
otp = null
pack-destination = "."
package = []
package-lock = true
package-lock-only = false
parseable = false
prefer-offline = false
prefer-online = false
; prefix = "E:\\Program Files\\nodejs" ; overridden by user
preid = ""
production = null
progress = true
provenance = false
proxy = null
read-only = false
rebuild-bundle = true
registry = "https://registry.npmjs.org/"
replace-registry-host = "npmjs"
save = true
save-bundle = false
save-dev = false
save-exact = false
save-optional = false
save-peer = false
save-prefix = "^"
save-prod = false
scope = ""
script-shell = null
searchexclude = ""
searchlimit = 20
searchopts = ""
searchstaleness = 900
shell = "C:\\Windows\\system32\\cmd.exe"
shrinkwrap = true
sign-git-commit = false
sign-git-tag = false
strict-peer-deps = false
strict-ssl = true
tag = "latest"
tag-version-prefix = "v"
timing = false
tmp = "C:\\Users\\freer\\AppData\\Local\\Temp"
umask = 0
unicode = false
update-notifier = true
usage = false
user-agent = "npm/{npm-version} node/{node-version} {platform} {arch} workspaces/{workspaces} {ci}"
userconfig = "C:\\Users\\freer\\.npmrc"
version = false
versions = false
viewer = "browser"
which = null
workspace = []
workspaces = null
workspaces-update = true
yes = null

; "builtin" config from E:\bin\nodejs\node_global\node_modules\npm\npmrc

; prefix = "C:\\Users\\freer\\AppData\\Roaming\\npm" ; overridden by user

; "user" config from C:\Users\freer\.npmrc

cache = "e:\\bin\\nodejs\\node_cache"
prefix = "e:\\bin\\nodejs\\node_global"

; "cli" config from command line options

long = true
```

## 查看全局安装路径

```bash
PS E:\tmp> npm config get prefix
e:\bin\nodejs\node_global
```

