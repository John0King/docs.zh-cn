---
title: "泛型代码中的默认关键字（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- generics [C#], default keyword
- default keyword [C#], generic programming
ms.assetid: b9daf449-4e64-496e-8592-6ed2c8875a98
caps.latest.revision: 22
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
ms.openlocfilehash: b5f5995b720d377717a5fff8a5e7e6e2196c612c
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="default-keyword-in-generic-code-c-programming-guide"></a>泛型代码中的默认关键字（C# 编程指南）
在泛型类和方法中，产生的一个问题是如何在无法提前知道以下内容的情况下将默认值赋值给参数化类型 T：  
  
-   T 是引用类型还是值类型。  
  
-   如果 T 是值类型，它是数值还是结构。  
  
 已知参数化类型 T 的变量 t，仅当 T 是引用类型时，语句 t = NULL 才有效；t = 0 仅对数值类型有效，对结构无效。 解决方案是使用 `default` 关键字，这样将对引用类型返回 NULL，对于数值类型返回零。 对于结构，将根据它们是值类型还是引用类型，返回初始化为零或 NULL 的结构的每个成员。 对于可为 NULL 的值类型，默认返回像任何结构一样初始化的 <xref:System.Nullable%601?displayProperty=fullName>。  
  
 `GenericList<T>` 类的以下示例演示如何使用 `default` 关键字。 有关详细信息，请参阅[泛型概述](../../../csharp/programming-guide/generics/introduction-to-generics.md)。  
  
 [!code-cs[csProgGuideGenerics#41](../../../csharp/programming-guide/generics/codesnippet/CSharp/default-keyword-in-generic-code_1.cs)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Collections.Generic>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型](../../../csharp/programming-guide/generics/index.md)   
 [泛型方法](../../../csharp/programming-guide/generics/generic-methods.md)   
 [泛型](~/docs/standard/generics/index.md)

