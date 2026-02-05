# Weiran Framework 单元测试规范

## 1. 核心配置要求

### 1.1 基础环境
- **测试框架**: PHPUnit 10.x
- **配置文件**: `phpunit.xml`
- **关键配置项**:
  - `processIsolation="true"` (必须开启进程隔离)
  - `failOnRisky="true"`
  - `failOnWarning="true"`
  - `<env name="CACHE_DRIVER" value="array"/>` (或 redis)

### 1.2 目录结构规范
测试目录 `tests/` 必须严格镜像 `src/` 结构：

```text
modules/{module}/
├── src/Action/UserCreateAction.php
└── tests/Action/UserCreateActionTest.php  <-- 对应测试文件
```

## 2. 命名规范 (Strict)

| 对象类型 | 源码规则 | 测试类命名规则 | 示例 |
|:---|:---|:---|:---|
| **Class** | `UserAction` | `{Class}Test` | `UserActionTest` |
| **Command** | `ClearCacheCommand` | `{Command}Test` | `ClearCacheCommandTest` |
| **Model** | `User` | `{Model}Test` | `UserTest` |
| **Method** | `handle()` | `test{Method}[Condition]` | `testHandle`, `testHandleWithInvalidData` |

**规则**:
1. 测试类必须以 `Test` 结尾。
2. 测试方法必须以 `test` 开头。
3. 辅助方法（非测试入口）**禁止**以 `test` 开头。

## 3. 覆盖率标准

| 阶段 | 目标覆盖率 | 关键路径要求 |
|:---|:---|:---|
| **Phase 1** | 50% | 核心 Action 类必须覆盖 |
| **Phase 2** | 65% | 所有 Service/Support 类必须覆盖 |
| **Phase 3** | 80%+ | 全面覆盖，包括异常处理 |

**覆盖率排除项** (不计入统计):
- `src/Http/Routes/*`
- `src/Http/RouteServiceProvider.php`
- `configurations/*`
- `resources/*`

## 4. 代码质量规范

### 4.1 AAA 模式
所有测试方法必须遵循 **Arrange-Act-Assert** 结构：

```php
public function testExample(): void
{
    // Arrange: 准备数据
    $data = ['name' => 'test'];

    // Act: 执行动作
    $result = $action->run($data);

    // Assert: 验证结果 (必须至少包含一个断言)
    $this->assertTrue($result);
}
```

### 4.2 禁止项 (Forbidden)
1. **禁止**在测试中使用 `dd()`, `dump()`, `var_dump()`。
2. **禁止**在测试中进行硬编码的 `sleep()` 等待。
3. **禁止**测试方法之间存在依赖 (`@depends` 慎用)。
4. **禁止**直接操作生产数据库，必须使用 `RefreshDatabase` 或事务。

### 4.3 最佳实践
- 使用 `Faker` 生成随机数据，严禁大量硬编码字符串。
- 优先使用 `$this->mock()` 隔离外部服务依赖。
- 每个测试方法应专注于一个单一的断言场景。

## 5. 🔍 AI 分析检查清单 (Checklist)

在分析测试代码时，请依次检查以下项目：

- [ ] **Config**: `phpunit.xml` 是否存在且配置了 `processIsolation="true"`？
- [ ] **Structure**: `tests/` 目录下的文件结构是否与 `src/` 一致？
- [ ] **Naming**: 所有测试文件名是否以 `Test.php` 结尾？
- [ ] **Inheritance**: 测试类是否继承自 `Weiran\Framework\Application\TestCase` 或模块基类？
- [ ] **Content**: 测试方法中是否包含 `$this->assert*` 调用？(无断言的测试是无效的)
- [ ] **Quality**: 是否存在被注释掉的测试代码 (`// public function test...`)？
