---
title: Criando interfaces do usuário com o designer do iOS
description: Este documento descreve como usar o Xamarin Designer para iOS para criar a interface do usuário de um aplicativo com storyboards e arquivos. xib. Ele é vinculado a documentos que discutem a disponibilidade da ferramenta, sua funcionalidade básica, controles designáveis e fornecem orientações sobre seu uso.
ms.prod: xamarin
ms.assetid: E35EFB69-EBBA-40E3-ADBE-CB8016F17127
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 05/31/2018
ms.openlocfilehash: 3a58fc58b429a8a16437773289cd4d7286bbff81
ms.sourcegitcommit: d2aa3a8bf9a60b6708db55b10b0c6893c06d3256
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2020
ms.locfileid: "93331473"
---
# <a name="building-user-interfaces-with-the-ios-designer"></a>Criando interfaces do usuário com o designer do iOS

_O Xamarin Designer para iOS é um designer visual para os formatos de storyboard e Interface Builder do iOS que é totalmente integrado ao Visual Studio para Mac e ao Visual Studio. O designer do iOS mantém a compatibilidade total com os formatos storyboard e. xib, para que os arquivos possam ser editados no Visual Studio para Mac ou no Visual Studio, além do Interface Builder do Xcode. Além disso, o Xamarin Designer para iOS dá suporte a recursos avançados, como controles personalizados que são renderizados em tempo de design no editor._

> [!WARNING]
> A maneira recomendada de criar interfaces de usuário do iOS agora está diretamente em um Mac que executa o Xcode. Mais informações podem ser [encontradas aqui](~/ios/user-interface/ios-use-xcode.md).

# <a name="visual-studio-for-mac"></a>[Visual Studio para Mac](#tab/macos)

[![Designer do iOS no Visual Studio para Mac](images/designer-vsmac-sml.png "O Designer de iOS")](images/designer-vsmac.png#lightbox)

# <a name="visual-studio"></a>[Visual Studio](#tab/windows)

[![Designer do iOS no Visual Studio](images/designer-vs.png "O Designer de iOS")](images/designer-vs.png#lightbox)

-----

## <a name="availability"></a>Disponibilidade

O Xamarin Designer para iOS está disponível em Visual Studio para Mac e no Visual Studio 2017 no Windows.

Esses guias pressupõem familiaridade com o conteúdo abordado nos [guias introdução do Xamarin. Ios](~/ios/get-started/index.md).

## <a name="ios-designer-basics"></a>[Noções básicas do Designer do iOS](introduction.md)

Este guia aborda os recursos do Xamarin iOS designer. Ele aborda noções básicas de designer, mostrando como usar o designer para dispor controles visualmente e como editar propriedades.

## <a name="designable-controls-overview"></a>[Visão geral de controles designáveis](ios-designable-controls-overview.md)

Este guia analisa em detalhes os controles personalizados, como eles são criados e quais requisitos eles devem atender para serem renderizados na superfície de design. Além disso, ele mostra como depurar problemas comuns que podem ocorrer ao usar controles designáveis.

## <a name="walkthrough---using-custom-controls-with-ios-designer"></a>[Walkthrough – usando controles personalizados com o iOS designer](ios-designable-controls-walkthrough.md)

Este artigo fornece uma explicação passo a passo mostrando como criar um controle personalizado e usá-lo no designer do iOS. Ele mostra como tornar um controle disponível na caixa de ferramentas do designer para que ele possa ser arrastado/Descartado para uma exibição. Além disso, ele mostra como implementar um controle para que ele seja renderizado corretamente no tempo de design e no runtime, além de como criar propriedades que podem ser definidas em tempo de design.

## <a name="auto-layout-with-the-xamarin-ios-designer"></a>[Layout automático com o Xamarin iOS designer](designer-auto-layout.md)

Este guia apresenta o layout automático do iOS e o fluxo de trabalho de novas restrições disponíveis no designer do iOS.
