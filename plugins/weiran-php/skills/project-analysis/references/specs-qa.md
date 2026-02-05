# 项目质量规范 (Quality Assurance)

## 1. 框架基础定义

| 关键项 | 定义 |
|:---|:---|
| **框架版本** | Laravel 10.x + PHP 8.2 |
| **根目录** | `/weiran` (Core) 或 `/modules` (Modules) |
| **Strict Mode** | **必须开启** `declare(strict_types = 1);` |
| **PSR** | 遵循 PSR-12 编码规范 |

## 2. 目录结构规范

### 2.1 标准模块结构
所有模块（`modules/{module}`）必须包含以下核心目录：
- `src/` (源码)
- `tests/` (测试)
- `configurations/` (配置)
- `resources/` (资源)

### 2.2 命名空间映射
- `modules/user/src` -> `namespace User;`
- `modules/user/tests` -> `namespace User\Tests;`

## 3. 编码规范 (Coding Standards)

### 3.1 命名约定
- **Class**: `PascalCase` (e.g., `UserController`)
- **Method**: `camelCase` (e.g., `getUserInfo`)
- **Variable**: `camelCase` (e.g., `isAvailable`)
- **Constant**: `UPPER_CASE` (e.g., `MAX_RETRY`)
- **Interface**: 以 `Interface` 结尾 (e.g., `UserInterface`)
- **Trait**: 以 `Trait` 结尾 (e.g., `LogTrait`)

### 3.2 特殊文件命名
- **Event**: `*Event.php`
- **Listener**: `*Listener.php`
- **Job**: `*Job.php`
- **Policy**: `*Policy.php`
- **Resource**: `*Resource.php`

### 3.3 路由与控制器
- **Controller**: 必须以 `Controller` 结尾。
- **Routes**:
    - 位置: `src/Http/Routes/*.php`
    - 禁止: 路由文件中**禁止**使用 `namespace` 参数。
    - 命名: `{module}:{type}.{group}.{action}` (e.g., `sys:api.auth.login`)

### 3.4 国际化 (i18n)
- **Validation**: `resources/lang/zh/validation.php` 必须存在且与 `en` 目录同步。
- **Keys**: 必须使用 snake_case (e.g., `user_not_found`)。

## 4. 🚫 禁止项 (Forbidden)

以下模式在生产代码中严格禁止：

1.  **Debug Functions**:
    - `dd(...)`
    - `dump(...)`
    - `var_dump(...)`
    - `print_r(...)`
    - `console.log(...)` (JS中)
2.  **Unsafe Code**:
    - `eval(...)`
    - `exec(...)` (除特定系统命令封装外)
3.  **Legacy**:
    - 使用 `@deprecated` 标记的方法/类。

## 5. 🤖 AI Analysis Rules (Regex Patterns)

AI 在执行代码扫描时，应使用以下正则模式进行快速验证：

| 检查项 | 推荐 Regex 模式 | 说明 |
|:---|:---|:---|
| **Strict Types** | `^declare\s*\(\s*strict_types\s*=\s*1\s*\);` | 必须出现在文件头部 (除 view/config 外) |
| **Forbidden Debug** | `(dd|dump|var_dump|print_r)\s*\(` | 扫描所有 .php 文件 |
| **Namespace** | `namespace\s+[A-Z][a-zA-Z0-9\\]*;` | 验证命名空间格式 |
| **Route Prefix** | `['"]prefix['"]\s*=>\s*['"][a-z0-9\-\/]+['"]` | 提取路由前缀 |
| **Class Name** | `class\s+[A-Z][a-zA-Z0-9]*` | 验证类名 PascalCase |

## 6. 🔍 快速检查清单 (Checklist)

- [ ] **Strict Types**: `src/` 下的所有 PHP 文件第一行是否开启严格模式？
- [ ] **No Debug**: 是否残留了 `dd()` 或 `dump()`？
- [ ] **Config Depth**: `configurations/` 下的数组深度是否超过 2 层？(禁止深层嵌套)
- [ ] **I18n**: `resources/lang/zh` 和 `en` 文件数量是否一致？
- [ ] **Naming**: 是否存在下划线命名的类文件 (e.g., `user_controller.php`)？(必须改为 `UserController.php`)
