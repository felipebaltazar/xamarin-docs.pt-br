---
title: Sombra do MasterDetailPage no iOS
description: As especificações de plataforma permitem que você consuma a funcionalidade que só está disponível em uma plataforma específica, sem implementar renderizadores ou efeitos personalizados. Este artigo explica como consumir a plataforma do iOS específica que controla se a página de detalhes de um MasterDetailPage tem sombra aplicada a ele, ao revelar a página mestra.
ms.prod: xamarin
ms.assetid: FB907EA2-C00A-43A5-84B1-A43584C867A5
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 03/05/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 0b3f7a28452d8507c4cb4a42d75b5edb5d62d8e4
ms.sourcegitcommit: 122b8ba3dcf4bc59368a16c44e71846b11c136c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91563673"
---
# <a name="masterdetailpage-shadow-on-ios"></a>Sombra do MasterDetailPage no iOS

[![Baixar Exemplo](~/media/shared/download.png) Baixar o exemplo](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

Essa plataforma determina se a página de detalhes de um [`MasterDetailPage`](xref:Xamarin.Forms.MasterDetailPage) tem sombra aplicada a ele, ao revelar a página mestra. Ele é consumido em XAML definindo a `MasterDetailPage.ApplyShadow` propriedade vinculável como `true` :

```xaml
<MasterDetailPage ...
                  xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core"
                  ios:MasterDetailPage.ApplyShadow="true">
    ...
</MasterDetailPage>
```

Como alternativa, ele pode ser consumido em C# usando a API fluente:

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;
...

public class iOSMasterDetailPageCS : MasterDetailPage
{
    public iOSMasterDetailPageCS(ICommand restore)
    {
        On<iOS>().SetApplyShadow(true);
        // ...
    }
}
```

O `MasterDetailPage.On<iOS>` método especifica que essa plataforma específica será executada somente no Ios. O `MasterDetailPage.SetApplyShadow` método, no [`Xamarin.Forms.PlatformConfiguration.iOSSpecific`](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific) namespace, é usado para controlar se a página de detalhes de um [`MasterDetailPage`](xref:Xamarin.Forms.MasterDetailPage) tem sombra aplicada a ele, ao revelar a página mestra. Além disso, o `GetApplyShadow` método pode ser usado para determinar se a sombra é aplicada à página de detalhes de um `MasterDetailPage` .

O resultado é que a página de detalhes de um [`MasterDetailPage`](xref:Xamarin.Forms.MasterDetailPage) pode ter sombra aplicada a ele, ao revelar a página mestra:

[![Captura de tela de um MasterDetailPage com e sem sombra](masterdetailpage-shadow-images/shadow.png "MasterDetailPage com e sem sombra")](masterdetailpage-shadow-images/shadow-large.png#lightbox "MasterDetailPage com e sem sombra")

## <a name="related-links"></a>Links relacionados

- [PlatformSpecifics (exemplo)](/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [Criação de itens específicos à plataforma](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [API iOSSpecific](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)