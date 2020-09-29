---
title: Suporte a Objective-C
description: Este documento fornece uma descrição do suporte para Objective-C na inserção do .NET. Ele aborda a contagem de referência automática, NSString, protocolos, protocolo NSObject, exceções e muito mais.
ms.prod: xamarin
ms.assetid: 3367A4A4-EC88-4B75-96D0-51B1FCBCE614
author: davidortinau
ms.author: daortin
ms.date: 11/14/2017
ms.openlocfilehash: c172208b77728423617d17b3f4c5b5a516a0b932
ms.sourcegitcommit: 4e399f6fa72993b9580d41b93050be935544ffaa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91457348"
---
# <a name="objective-c-support"></a>Suporte a Objective-C

## <a name="specific-features"></a>Recursos específicos

A geração de Objective-C tem alguns recursos especiais que valem a pena observar.

### <a name="automatic-reference-counting"></a>Contagem de referência automática

O uso da contagem de referência automática (ARC) é **necessário** para chamar as associações geradas. O projeto que usa uma biblioteca baseada em incorporação .NET deve ser compilado com `-fobjc-arc` .

### <a name="nsstring-support"></a>Suporte do NSString

As APIs que expõem `System.String` tipos são convertidas em `NSString` . Isso facilita o gerenciamento de memória do que ao lidar com o `char*` .

### <a name="protocols-support"></a>Suporte a protocolos

As interfaces gerenciadas são convertidas em protocolos Objective-C, onde todos os membros são `@required` .

### <a name="nsobject-protocol-support"></a>Suporte do protocolo NSObject

Por padrão, o hash padrão e a igualdade de tempo de execução do .NET e do Objective-C são considerados intercambiáveis, pois compartilham semânticas semelhantes.

Quando um tipo gerenciado `Equals(Object)` é substituído ou `GetHashCode` , em geral, significa que o comportamento padrão (.net) não era suficiente; isso implica que o comportamento padrão de Objective-C provavelmente não é suficiente.

Nesses casos, o gerador substitui o [`isEqual:`](https://developer.apple.com/reference/objectivec/1418956-nsobject/1418795-isequal?language=objc) método e a [`hash`](https://developer.apple.com/reference/objectivec/1418956-nsobject/1418859-hash?language=objc) propriedade definidos no [ `NSObject` protocolo](https://developer.apple.com/reference/objectivec/1418956-nsobject?language=objc). Isso permite que a implementação gerenciada personalizada seja usada do código Objective-C de forma transparente.

### <a name="exceptions-support"></a>Suporte a exceções

Passar `--nativeexception` como um argumento para `objcgen` converterá exceções gerenciadas em exceções de Objective-C que podem ser capturadas e processadas. 

### <a name="comparison"></a>Comparação

Os tipos gerenciados que implementam `IComparable` (ou sua versão genérica `IComparable<T>` ) produzirão métodos amigáveis de Objective-C que retornam `NSComparisonResult` e aceitam um `nil` argumento. Isso torna a API gerada mais amigável para os desenvolvedores de Objective-C. Por exemplo:

```objc
- (NSComparisonResult)compare:(XAMComparableType * _Nullable)other;
```

### <a name="categories"></a>Categorias

Os métodos de extensões gerenciadas são convertidos em categorias. Por exemplo, os seguintes métodos de extensão em `Collection` :

```csharp
public static class SomeExtensions {
    public static int CountNonNull (this Collection collection) { ... }
    public static int CountNull (this Collection collection) { ... }
}
```

criaria uma categoria Objective-C como esta:

```objc
@interface Collection (SomeExtensions)

- (int)countNonNull;
- (int)countNull;

@end
```

Quando um único tipo gerenciado estende vários tipos, várias categorias de Objective-C são geradas.

### <a name="subscripting"></a>Subscrito

As propriedades indexadas gerenciadas são convertidas em assinatura de objeto. Por exemplo:

```csharp
public bool this[int index] {
    get { return c[index]; }
    set { c[index] = value; }
}
```

criaria Objective-C semelhante a:

```objc
- (id)objectAtIndexedSubscript:(int)idx;
- (void)setObject:(id)obj atIndexedSubscript:(int)idx;
```

que pode ser usado por meio da sintaxe de assinatura Objective-C:

```objc
if ([intCollection [0] isEqual:@42])
    intCollection[0] = @13;
```

Dependendo do tipo de indexador, a assinatura indexada ou com chave será gerada quando apropriado.

Este [artigo](https://nshipster.com/object-subscripting/) é uma ótima introdução à assinatura.

## <a name="main-differences-with-net"></a>Principais diferenças com o .NET

### <a name="constructors-vs-initializers"></a>Construtores vs inicializadores

Em Objective-C, você pode chamar qualquer um dos protótipos de inicializador de qualquer uma das classes pai na cadeia de herança, a menos que esteja marcado como indisponível ( `NS_UNAVAILABLE` ).

Em C#, você deve declarar explicitamente um membro de Construtor dentro de uma classe, o que significa que os construtores não são herdados.

Para expor a representação correta da API do C# para Objective-C, `NS_UNAVAILABLE` é adicionada a qualquer inicializador que não está presente na classe filho da classe pai.

API DO C#:

```csharp
public class Unique {
    public Unique () : this (1)
    {
    }

    public Unique (int id)
    {
    }
}

public class SuperUnique : Unique {
    public SuperUnique () : base (911)
    {
    }
}
```

API Surface-C de Objective:

```objc
@interface SuperUnique : Unique

- (instancetype)initWithId:(int)id NS_UNAVAILABLE;
- (instancetype)init;

@end
```

Aqui, foi `initWithId:` marcado como não disponível.

### <a name="operator"></a>Operador

O Objective-C não dá suporte à sobrecarga de operador, pois o C# faz, de modo que os operadores sejam convertidos em seletores de classe:

```csharp
public static AllOperators operator + (AllOperators c1, AllOperators c2)
{
    return new AllOperators (c1.Value + c2.Value);
}
```

como

```objc
+ (instancetype)add:(Overloads_AllOperators *)anObjectC1 c2:(Overloads_AllOperators *)anObjectC2;
```

No entanto, algumas linguagens .NET não oferecem suporte à sobrecarga de operador, portanto, é comum também incluir um método nomeado ["amigável"](/dotnet/standard/design-guidelines/operator-overloads) além da sobrecarga de operador.

Se a versão do operador e a versão "amigável" forem encontradas, somente a versão amigável será gerada, pois elas serão geradas para o mesmo nome de Objective-C.

```csharp
public static AllOperatorsWithFriendly operator + (AllOperatorsWithFriendly c1, AllOperatorsWithFriendly c2)
{
    return new AllOperatorsWithFriendly (c1.Value + c2.Value);
}

public static AllOperatorsWithFriendly Add (AllOperatorsWithFriendly c1, AllOperatorsWithFriendly c2)
{
    return new AllOperatorsWithFriendly (c1.Value + c2.Value);
}
```

 torna-se:

```objc
+ (instancetype)add:(Overloads_AllOperatorsWithFriendly *)anObjectC1 c2:(Overloads_AllOperatorsWithFriendly *)anObjectC2;
```

### <a name="equality-operator"></a>Operador de igualdade

Em geral `==` , o em C# é tratado como um operador geral, conforme mencionado acima.

No entanto, se o operador "friendly" Equals for encontrado, ambos operador `==` e operador `!=` serão ignorados na geração.

### <a name="datetime-vs-nsdate"></a>DateTime vs NSDate

Na [`NSDate`](https://developer.apple.com/reference/foundation/nsdate?language=objc) documentação:

> `NSDate` os objetos encapsulam um único ponto no tempo, independentemente de qualquer sistema calendrical ou fuso horário específico. Os objetos Date são imutáveis, representando um intervalo de tempo invariável relativo a uma data de referência absoluta (00:00:00 UTC em 1 de janeiro de 2001).

Devido à `NSDate` data de referência, todas as conversões entre ela e `DateTime` devem ser feitas em UTC.

#### <a name="datetime-to-nsdate"></a>DateTime para NSDate

Ao converter de `DateTime` para `NSDate` , a `Kind` propriedade `DateTime` é levada em conta:

|Tipo|Resultados|
|---|---|
|`Utc`|A conversão é executada usando o `DateTime` objeto fornecido como está.|
|`Local`|O resultado da chamada `ToUniversalTime()` no objeto fornecido `DateTime` é usado para conversão.|
|`Unspecified`|O `DateTime` objeto fornecido é considerado como UTC, portanto, mesmo comportamento quando `Kind` é `Utc` .|

A conversão usa a seguinte fórmula:

```
TimeInterval = DateTimeObjectTicks - NSDateReferenceDateTicks / TicksPerSecond
```

Nesta fórmula: 

- `NSDateReferenceDateTicks` é calculado com base na `NSDate` data de referência de 00:00:00 UTC em 1 de janeiro de 2001: 

    ```csharp
    new DateTime (year:2001, month:1, day:1, hour:0, minute:0, second:0, kind:DateTimeKind.Utc).Ticks;
    ```

- [`TicksPerSecond`](/dotnet/api/system.timespan.tickspersecond) é definido em [`TimeSpan`](/dotnet/api/system.timespan)

Para criar o `NSDate` objeto, o `TimeInterval` é usado com o `NSDate` seletor [dateWithTimeIntervalSinceReferenceDate:](https://developer.apple.com/reference/foundation/nsdate/1591577-datewithtimeintervalsincereferen?language=objc) .

#### <a name="nsdate-to-datetime"></a>NSDate para DateTime

A conversão de `NSDate` para `DateTime` usa a seguinte fórmula:

```
DateTimeTicks = NSDateTimeIntervalSinceReferenceDate * TicksPerSecond + NSDateReferenceDateTicks
```

Nesta fórmula: 

- `NSDateReferenceDateTicks` é calculado com base na `NSDate` data de referência de 00:00:00 UTC em 1 de janeiro de 2001: 

    ```csharp
    new DateTime (year:2001, month:1, day:1, hour:0, minute:0, second:0, kind:DateTimeKind.Utc).Ticks;
    ```

- [`TicksPerSecond`](/dotnet/api/system.timespan.tickspersecond) é definido em [`TimeSpan`](/dotnet/api/system.timespan)

Depois `DateTimeTicks` de calcular, o `DateTime` [Construtor](/dotnet/api/system.datetime.-ctor#System_DateTime__ctor_System_Int64_System_DateTimeKind_) é invocado, definindo seu `kind` como `DateTimeKind.Utc` .

> [!NOTE]
> `NSDate` pode ser `nil` , mas uma `DateTime` é uma struct no .net, que por definição não pode ser `null` . Se você fornecer um `nil` `NSDate` , ele será convertido para o valor padrão `DateTime` , que é mapeado para `DateTime.MinValue` .

`NSDate` dá suporte a um valor máximo mais alto e menor que `DateTime` . Ao converter de `NSDate` para `DateTime` , esses valores superiores e inferiores são alterados para `DateTime` [MaxValue](/dotnet/api/system.datetime.maxvalue) ou [MinValue](/dotnet/api/system.datetime.minvalue), respectivamente.