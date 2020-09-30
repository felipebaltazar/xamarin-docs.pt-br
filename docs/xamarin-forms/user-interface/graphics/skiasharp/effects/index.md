---
title: Efeitos de SkiaSharp
description: Saiba como alterar a exibição normal de elementos gráficos com gradientes, bitmap em blocos gráficos, modos de mesclagem, Desfoque e outros efeitos.
ms.prod: xamarin
ms.technology: xamarin-skiasharp
ms.assetid: B3E06572-8E2A-49FA-90D1-444C394CD516
author: davidbritch
ms.author: dabritch
ms.date: 08/22/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: e63d92cde5925561dae4217c3c46af2c2c59f795
ms.sourcegitcommit: 122b8ba3dcf4bc59368a16c44e71846b11c136c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91563985"
---
# <a name="skiasharp-effects"></a>Efeitos de SkiaSharp

[![Baixar Exemplo](~/media/shared/download.png) Baixar o exemplo](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/skiasharpforms-demos)

A [`SKPaint`](xref:SkiaSharp.SKPaint) classe SkiaSharp define seis propriedades que podem ser classificadas sob o termo geral de _efeitos_. Essas são propriedades que alteram a exibição normal de elementos gráficos de alguma forma. Os efeitos SkiaSharp se enquadram em seis categorias:

## <a name="path-effects"></a>[Efeitos de caminho](../curves/effects.md)

Defina a [`PathEffect`](xref:SkiaSharp.SKPaint.PathEffect) propriedade de `SKPaint` como um objeto do tipo [`SKPathEffect`](xref:SkiaSharp.SKPathEffect) para exibir linhas tracejadas ou para traçar ou preencher uma área com um padrão criado a partir de caminhos. O efeito de caminho foi abordado anteriormente nesta série no artigo [**efeitos de caminho em SkiaSharp**](../curves/effects.md).

## <a name="shaders"></a>[Sombreadores](shaders/index.md)

Defina a [`Shader`](xref:SkiaSharp.SKPaint.Shader) propriedade de `SKPaint` como um objeto do tipo [`SKShader`](xref:SkiaSharp.SKShader) para exibir gradientes lineares ou circulares, bitmaps ao lado do ladrilho e padrões de ruído de perlm.

## <a name="blend-modes"></a>[Modos do Blend](blend-modes/index.md)

Defina a [`BlendMode`](xref:SkiaSharp.SKPaint.BlendMode) propriedade de `SKPaint` como um membro da [`SKBlendMode`](xref:SkiaSharp.SKBlendMode) enumeração para controlar o que acontece quando um gráfico de origem é exibido em um destino. O SkiaSharp dá suporte a todos os modos de composição e mesclagem CSS, incluindo os modos carregador-Duff, separáveis Blend e modos de mesclagem não separáveis.

## <a name="mask-filters"></a>[Filtros de máscara](mask-filters.md)

Defina a [`MaskFilter`](xref:SkiaSharp.SKPaint.MaskFilter) propriedade de `SKPaint` como um objeto do tipo [`SKMaskFilter`](xref:SkiaSharp.SKMaskFilter) para desfoques e outros efeitos alfa.

## <a name="image-filters"></a>[Filtros de imagem](image-filters.md)

Defina a [`ImageFilter`](xref:SkiaSharp.SKPaint.ImageFilter) propriedade de `SKPaint` como um objeto do tipo [`SKImageFilter`](xref:SkiaSharp.SKImageFilter) para esfocar bitmaps e criar sombras de soltar, relevo ou efeitos de engraving.

## <a name="color-filters"></a>[Filtros de cores](color-filters.md)

Defina a [`ColorFilter`](xref:SkiaSharp.SKPaint.ColorFilter) propriedade de `SKPaint` como um objeto do tipo [`SKColorFilter`](xref:SkiaSharp.SKColorFilter) para alterar as cores usando tabelas ou transformações de matriz.

Todos os códigos de exemplo para esses artigos estão no [**SkiaSharpFormsDemos**](/samples/xamarin/xamarin-forms-samples/skiasharpforms-demos). No home page, selecione **efeitos de SkiaSharp**.

## <a name="related-links"></a>Links relacionados

- [APIs do SkiaSharp](/dotnet/api/skiasharp)
- [SkiaSharpFormsDemos (exemplo)](/samples/xamarin/xamarin-forms-samples/skiasharpforms-demos)