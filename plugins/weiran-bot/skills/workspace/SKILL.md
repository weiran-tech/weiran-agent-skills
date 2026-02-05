---
name: workspace
description: 管理 Weiran 工作空间 - 成员管理、权限配置、团队组织
---

# Weiran 工作空间管理

管理 Weiran 工作空间和团队成员。

用户输入: $ARGUMENTS

## 职责范围

- 管理工作空间
- 添加/移除团队成员
- 配置成员角色和权限

## 核心知识

### 工作空间概念

工作空间是 Weiran 中的资源隔离单元，用于：
- 组织团队的测试资源
- 控制访问权限
- 隔离不同项目/团队

### 角色权限

| 角色 | 权限 |
|------|------|
| **Admin** | 管理成员，编辑所有资源 |
| **Member** | 创建和编辑自己的资源 |

## 常用操作

### 查看我的工作空间
```
weiran_get_my_workspaces
weiran_get_my_workspaces_with_roles  # 包含角色信息
```

### 添加成员
```
weiran_list_users → 查找用户
weiran_assign_user_to_workspace → 添加单个用户
weiran_assign_users_to_workspace → 批量添加
```

### 修改成员角色
```
weiran_find_workspace_users → 查找工作空间下所有用户
weiran_assign_user_to_workspace → 修改单个用户
```

### 获取工作空间成员列表
```
weiran_find_workspace_users → 查找工作空间下现有成员
```

### 移除成员
```
weiran_remove_user_from_workspace → 从工作空间移除用户
```

### 申请新工作空间
```
weiran_check_workspace_key → 检查 workspace key 是否可用
weiran_request_workspace → 提交申请
```
注意：申请前需先调用 weiran_check_workspace_key 检查 key 是否已被占用。

## 工作流程

1. **确认目标**：操作哪个工作空间？
2. **获取当前状态**：`weiran_get_my_workspaces_with_roles`
3. **执行操作**：添加成员、修改角色等
4. **确认结果**：返回操作状态

## 返回格式

任务完成后，向用户汇报：
- 操作结果
- 受影响的成员/工作空间
- 当前权限状态

## 参考文档

详细概念请参考：
- [核心概念](../weiran-guide/references/concepts.md)
