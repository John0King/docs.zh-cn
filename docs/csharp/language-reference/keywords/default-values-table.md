---
title: "默认值表（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- constructors [C#], return values
- keywords [C#], new
- default constructor [C#]
- defaults [C#]
- value types [C#], initializing
- variables [C#], value types
- constructors [C#], default constructor
- types [C#], default constructor return values
ms.assetid: 4af2c1df-9e3a-48c1-83ac-b192986fc5bc
caps.latest.revision: 12
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d609403269a5cbfe6715647a240c44b254a4d8f9
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="default-values-table-c-reference"></a>默认值表（C# 参考）
下表显示默认构造函数返回的值类型的默认值。 默认构造函数使用 `new` 运算符进行调用，如下所示：  
  
```  
int myInt = new int();  
```  
  
 上一语句与如下语句效果相同：  
  
```  
int myInt = 0;  
```  
  
 请记住：不允许在 C# 中使用未初始化的变量。  
  
|值类型|默认值|  
|----------------|-------------------|  
|[bool](../../../csharp/language-reference/keywords/bool.md)|`false`|  
|[byte](../../../csharp/language-reference/keywords/byte.md)|0|  
|[char](../../../csharp/language-reference/keywords/char.md)|'\0'|  
|[小数](../../../csharp/language-reference/keywords/decimal.md)|0.0M|  
|[double](../../../csharp/language-reference/keywords/double.md)|0.0D|  
|[enum](../../../csharp/language-reference/keywords/enum.md)|表达式 (E)0 生成的值，其中 E 是枚举标识符。|  
|[float](../../../csharp/language-reference/keywords/float.md)|0.0F|  
|[int](../../../csharp/language-reference/keywords/int.md)|0|  
|[long](../../../csharp/language-reference/keywords/long.md)|0L|  
|[sbyte](../../../csharp/language-reference/keywords/sbyte.md)|0|  
|[short](../../../csharp/language-reference/keywords/short.md)|0|  
|[struct](../../../csharp/language-reference/keywords/struct.md)|通过如下设置生成的值：将所有值类型的字段设置为其默认值，将所有引用类型的字段设置为 `null`。|  
|[uint](../../../csharp/language-reference/keywords/uint.md)|0|  
|[ulong](../../../csharp/language-reference/keywords/ulong.md)|0|  
|[ushort](../../../csharp/language-reference/keywords/ushort.md)|0|  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [值类型表](../../../csharp/language-reference/keywords/value-types-table.md)   
 [值类型](../../../csharp/language-reference/keywords/value-types.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [类型参考表](../../../csharp/language-reference/keywords/reference-tables-for-types.md)

