---
title: Instalação e requisitos do Inspetor
description: Este documento descreve como instalar o Xamarin Inspector e discute o sistema operacional, IDEs e plataformas de aplicativos com suporte.
ms.prod: xamarin
ms.assetid: 81174493-02D3-4FF5-AD57-04F3288A7F94
author: davidortinau
ms.author: daortin
ms.date: 06/19/2018
ms.openlocfilehash: 70bc0f90b2802587dba8e2da19430164fccfe861
ms.sourcegitcommit: 4e399f6fa72993b9580d41b93050be935544ffaa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91457335"
---
# <a name="inspector-installation-and-requirements"></a>Instalação e requisitos do Inspetor

## <a name="download-and-installation"></a>Download e instalação

# <a name="windows"></a>[Windows](#tab/windows)

1. Baixe e instale o [Visual Studio Enterprise](https://visualstudio.microsoft.com/vs/) e selecione o **desenvolvimento móvel com** carga de trabalho do .net.
1. [Entre](/visualstudio/ide/signing-in-to-visual-studio) para habilitar sua assinatura do Enterprise.
1. [Inspecione](~/tools/inspector/inspect.md) seu próprio aplicativo!

# <a name="macos"></a>[macOS](#tab/macos)

1. Baixe e instale o [Visual Studio para Mac](https://visualstudio.microsoft.com/vs/mac/).
1. [Entre](/visualstudio/mac/activation) para habilitar sua assinatura do Enterprise.
1. [Inspecione](~/tools/inspector/inspect.md) seu próprio aplicativo!

-----

## <a name="requirements"></a>Requisitos

### <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

- **Mac** -OS X 10,11 ou superior
- **Windows** -Windows 7 ou superior (com o Internet Explorer 11 ou superior e o .NET 4.6.1 ou superior)

### <a name="supported-ides"></a>IDEs com suporte

- Visual Studio para Mac
- Visual Studio 2017 com **desenvolvimento móvel com carga de** trabalho do .net

A inspeção do aplicativo ao vivo está disponível para clientes empresariais.

<a name="supported-platforms"></a>

### <a name="supported-app-platforms"></a>Plataformas de aplicativos com suporte

|Plataforma de aplicativo|Suporte a IDE|Observações|
|--- |--- |--- |
|Mac|Somente com suporte no Visual Studio para Mac|
|iOS|Com suporte no Visual Studio 2017 e Visual Studio para Mac| O comportamento do vinculador deve ser definido como [**não vincular**](~/ios/deploy-test/linker.md) (em opções do projeto de **compilação do IOS** ) |
|Android|Com suporte no Visual Studio 2017 e Visual Studio para Mac|É necessário direcionar o Android >= 4.0.3, com **fastdev** habilitado.<br />Deve usar os emuladores do Google, Visual Studio ou Xamarin Android. Os emuladores do Android 7 podem não permitir a inspeção no momento.|
|WPF|Somente com suporte no Visual Studio 2017|

<a name="reporting-bugs"></a>

## <a name="reporting-bugs"></a>Relatar bugs

Os bugs devem ser relatados diretamente por meio do Visual Studio:

- **Ajuda > enviar comentários > relatar um problema**

Inclua todas as seguintes informações:

### <a name="platform-version-information"></a>Informações de versão da plataforma

Essas informações são vitais.

Visual Studio para Mac

- **O Visual Studio > sobre o Visual Studio > mostrar detalhes > copiar informações**
- Colar no relatório de bugs

Visual Studio

- **Ajuda > sobre o Visual Studio > copiar informações**
- Informe-nos a sua versão do sistema operacional e se você está executando o Windows de 32 bits ou 64 bits.

### <a name="log-files"></a>Arquivos de log

Sempre Anexe os arquivos de log de cliente IDE e Inspector.

Cliente do Inspetor

- Mac: `~/Library/Logs/Xamarin/Inspector/Xamarin Inspector {date}.log`
- Windows: `%LOCALAPPDATA%\Xamarin\Inspector\logs\Xamarin Inspector {date}.log`

o 1.4. x também apresenta a capacidade de selecionar o arquivo de log no Finder (Mac) ou Explorer (Windows) diretamente no menu principal:

- **Ajuda > revelar arquivo de log**

Visual Studio para Mac

- `~/Library/Logs/VisualStudio/7.0/Ide.log`

Visual Studio

- `%LOCALAPPDATA%\Xamarin\Logs\{VS version}\Inspector {date}.log`
- O conteúdo do painel de **saída** do Visual Studio também pode ser informativo.

### <a name="project-settings"></a>Configurações do projeto

Se você puder anexar o **. csproj** para o projeto que está tentando inspecionar, ele seria extremamente útil. Isso é mais fácil do que perguntar sobre configurações individuais.

Além disso, confirme se você está na configuração de depuração.

### <a name="selected-devices"></a>Dispositivos selecionados

Para Android e iOS, é vital que saibamos em qual dispositivo você está depurando quando quiser inspecionar. Precisamos saber:

- Nome do dispositivo, conforme mostrado no seu IDE
- Versão do sistema operacional do seu dispositivo
- Android: Verifique se você está usando um emulador x86
- Android: qual plataforma de emulador você está usando? O Google Emulator? Android Emulator do Visual Studio? Xamarin Android Player?
- O aplicativo que você está depurando aparece corretamente e funciona no dispositivo?
- O dispositivo tem conectividade de rede (verifique via navegador da Web)?

[client-bugs]: https://github.com/Microsoft/workbooks/issues/new