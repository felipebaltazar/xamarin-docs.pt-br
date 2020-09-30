---
title: Cor do plano de fundo da célula no iOS
description: As especificações de plataforma permitem que você consuma a funcionalidade que só está disponível em uma plataforma específica, sem implementar renderizadores ou efeitos personalizados. Este artigo explica como consumir a plataforma específica do iOS que define a cor de plano de fundo padrão de células no iOS.
ms.prod: xamarin
ms.assetid: 2A3FDACF-5AE2-40DE-8488-6FE41733712F
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/24/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: a9ab12b5aabee03d84c58580ec200de4b63d5106
ms.sourcegitcommit: 122b8ba3dcf4bc59368a16c44e71846b11c136c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91562425"
---
# <a name="cell-background-color-on-ios"></a>Cor do plano de fundo da célula no iOS

[![Baixar Exemplo](~/media/shared/download.png) Baixar o exemplo](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

Essa plataforma do iOS específica define a cor de plano de fundo padrão das [`Cell`](xref:Xamarin.Forms.Cell) instâncias. Ele é consumido em XAML definindo a `Cell.DefaultBackgroundColor` propriedade vinculável como a [`Color`](xref:Xamarin.Forms.Color) :

```xaml
<ContentPage ...
             xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core">
    <StackLayout Margin="20">
        <ListView ItemsSource="{Binding GroupedEmployees}"
                  IsGroupingEnabled="true">
            <ListView.GroupHeaderTemplate>
                <DataTemplate>
                    <ViewCell ios:Cell.DefaultBackgroundColor="Teal">
                        <Label Margin="10,10"
                               Text="{Binding Key}"
                               FontAttributes="Bold" />
                    </ViewCell>
                </DataTemplate>
            </ListView.GroupHeaderTemplate>
            ...
        </ListView>
    </StackLayout>
</ContentPage>
```

Como alternativa, ele pode ser consumido em C# usando a API fluente:

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;
...

var viewCell = new ViewCell { View = ... };
viewCell.On<iOS>().SetDefaultBackgroundColor(Color.Teal);
```

O `ListView.On<iOS>` método especifica que essa plataforma específica será executada somente no Ios. O `Cell.SetDefaultBackgroundColor` método, no [`Xamarin.Forms.PlatformConfiguration.iOSSpecific`](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific) namespace, define a cor do plano de fundo da célula como um especificado [`Color`](xref:Xamarin.Forms.Color) . Além disso, o `Cell.DefaultBackgroundColor` método pode ser usado para recuperar a cor de plano de fundo da célula atual.

O resultado é que a cor do plano de fundo em um [`Cell`](xref:Xamarin.Forms.Cell) pode ser definida como um específico [`Color`](xref:Xamarin.Forms.Color) :

[![Captura de tela das células do cabeçalho do grupo azul-petróleo, no iOS](cell-background-color-images/group-header-cell-color.png "ListView com células de cabeçalho de grupo azul-petróleo")](cell-background-color-images/group-header-cell-color-large.png#lightbox "ListView com células de cabeçalho de grupo azul-petróleo")

## <a name="related-links"></a>Links relacionados

- [PlatformSpecifics (exemplo)](/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [Criação de itens específicos à plataforma](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [API iOSSpecific](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)