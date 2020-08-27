---
title: Introdução aos comportamentos
description: Comportamentos permitem adicionar funcionalidade a controles de interface do usuário sem precisar dividi-los em subclasses. Em vez disso, a funcionalidade é implementada em uma classe de comportamento e anexada ao controle como se fizesse parte do próprio controle. Este artigo fornece uma introdução a comportamentos.
ms.prod: xamarin
ms.assetid: 0DF1EF8C-A212-4142-A3C6-DF760A82A757
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/06/2016
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 37c76a5f325c363a92c2a2c1e597dab28f064cd9
ms.sourcegitcommit: a003b036f6fb83818e2ecc9c72a641e3aeb373bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88964604"
---
# <a name="introduction-to-behaviors"></a>Introdução aos comportamentos

_Os comportamentos permitem que você adicione funcionalidade aos controles da interface do usuário sem precisar subclasseá-los. Em vez disso, a funcionalidade é implementada em uma classe de comportamento e anexada ao controle como se fosse parte do próprio controle. Este artigo fornece uma introdução aos comportamentos._

Os comportamentos permitem que você implemente código que normalmente precisaria escrever como code-behind, porque interagem diretamente com a API do controle, de forma que podem ser anexados de forma concisa ao controle e empacotados para reutilização em mais de um aplicativo. Eles podem ser usados para fornecer uma ampla gama de funcionalidade para controles, como:

- Adicionando um validador de email a um [`Entry`](xref:Xamarin.Forms.Entry) .
- Criar um controle de classificação usando um reconhecedor de gesto de toque.
- Controlar uma animação.
- Adicionar um efeito a um controle.

Os comportamentos também permitem cenários mais avançados. No contexto dos *comandos*, os comportamentos são uma abordagem útil para conectar um controle a um comando. Além disso, eles podem ser usados para associar comandos a controles que não foram projetados para interagir com comandos. Por exemplo, podem ser usados para invocar um comando em resposta ao acionamento de um evento.

Xamarin.Forms dá suporte a dois estilos diferentes de comportamentos:

- ** Xamarin.Forms comportamentos** – classes que derivam da [`Behavior`](xref:Xamarin.Forms.Behavior) [`Behavior<T>`](xref:Xamarin.Forms.Behavior`1) classe ou, em que `T` é o tipo do controle ao qual o comportamento deve ser aplicado. Para obter mais informações sobre Xamarin.Forms comportamentos, consulte [ Xamarin.Forms comportamentos](~/xamarin-forms/app-fundamentals/behaviors/creating.md).
- **Comportamentos anexados** – `static` classes com uma ou mais propriedades anexadas. Para obter mais informações sobre comportamentos anexados, confira [Comportamentos anexados](~/xamarin-forms/app-fundamentals/behaviors/attached.md).

Este guia concentra-se em Xamarin.Forms comportamentos porque eles são a abordagem preferida para a construção de comportamento.

## <a name="related-links"></a>Links Relacionados

- [Comportamento](xref:Xamarin.Forms.Behavior)
- [Comportamento &lt; T&gt;](xref:Xamarin.Forms.Behavior`1)
