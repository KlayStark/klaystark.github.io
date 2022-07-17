---
title: UE4类命名规则
date: 2022-2-27 23:25:18
categories: UE4
tags:
---

## 命名规范

- **A** 派生自 Actor，比如 AController。

- **U** 派生自 Object，比如 UComponent。

- **S** 派生自 SWidget（Slate UI），比如 SButton。

- **H** HitResult相关类。

- **E** Enums ，比如 EFortificationType。

- **I** Interface 类的前缀，比如 IAbilitySystemInterface。

- **T** Template 类的前缀，比如 TArray。

- **F** 纯C++类，比如 FVector。

虚幻引擎头文件工具 Unreal Header Tool 会在编译前检查类命名。如果类命名出现错误，那么它会提出警告并终止编译。