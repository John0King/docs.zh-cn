---
title: "base（C# 参考）"
description: "base 关键字 (C#)"
keywords: "base (C#)、base 关键字 (C#)、base 关键字（C# 参考）、base 关键字（C# 语言参考）"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- base
- BaseClass.BaseClass
- base_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- base keyword [C#]
ms.assetid: 8b645dbe-1a33-49b8-8716-1c401f9a5ea5
caps.latest.revision: 14
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c875ca834fc66e0bf6cd596f376773badca757e3
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="base-c-reference"></a>base（C# 参考）
`base` 关键字用于从派生类中访问基类的成员：  
  
-   调用基类上已被其他方法重写的方法。  
  
-   指定创建派生类实例时应调用的基类构造函数。  
  
 仅允许基类访问在构造函数、实例方法或实例属性访问器中进行。  
  
 从静态方法中使用 `base` 关键字是错误的。  
  
 所访问的基类是类声明中指定的基类。 例如，如果指定 `class ClassB : ClassA`，则从 ClassB 访问 ClassA 的成员，而不考虑 ClassA 的基类。  
  
## <a name="example"></a>示例  
 在本例中，基类 `Person` 和派生类 `Employee` 都有一个名为 `Getinfo` 的方法。 通过使用 `base` 关键字，可以从派生类中调用基类的 `Getinfo` 方法。  
  
 [!code-cs[csrefKeywordsAccess#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/base_1.cs)]  
  
 有关其他示例，请参阅 [new](../../../csharp/language-reference/keywords/new.md)、[virtual](../../../csharp/language-reference/keywords/virtual.md) 和 [override](../../../csharp/language-reference/keywords/override.md)。  
  
## <a name="example"></a>示例  
 本示例显示如何指定在创建派生类实例时调用的基类构造函数。  
  
 [!code-cs[csrefKeywordsAccess#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/base_2.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [this](../../../csharp/language-reference/keywords/this.md)

