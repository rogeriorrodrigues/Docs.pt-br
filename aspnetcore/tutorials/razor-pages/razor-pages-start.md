---
title: "Introdução a Páginas do Razor no ASP.NET Core"
author: rick-anderson
description: "Introdução a Páginas do Razor no ASP.NET Core"
keywords: "ASP.NET Core, Páginas do Razor, Razor, MVC"
ms.author: riande
manager: wpickett
ms.date: 08/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: 9d647657f21dd7e952808e5fe020f7a9e8767cd8
ms.sourcegitcommit: 3ba32b2b6425ed94604cb0f681db0d5bb5f8ad58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2017
---
# <a name="getting-started-with-razor-pages-in-aspnet-core"></a>Introdução a Páginas do Razor no ASP.NET Core

Por [Rick Anderson](https://twitter.com/RickAndMSFT)

Este tutorial ensina as noções básicas de criação de um aplicativo Web de Páginas do Razor do ASP.NET Core. Recomendamos que você conclua a [Introdução a Páginas do Razor](xref:mvc/razor-pages/index) antes de iniciar este tutorial. Páginas do Razor é a maneira recomendada para criar a interface do usuário para aplicativos Web no ASP.NET Core.

## <a name="prerequisites"></a>Pré-requisitos

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

## <a name="create-a-razor-web-app"></a>Criar um aplicativo Web do Razor

* No menu **Arquivo** do Visual Studio, selecione **Novo** > **Projeto**.
* Crie um novo Aplicativo Web ASP.NET Core. Nomeie o projeto **RazorPagesMovie**. É importante nomear o projeto *RazorPagesMovie* de modo que os namespaces façam a correspondência quando você copiar/colar código.
  ![novo aplicativo Web ASP.NET Core](../../mvc/razor-pages/index/_static/np.png)
* Selecione **ASP.NET Core 2.0** na lista suspensa e selecione **Aplicativo Web**.
  ![Aplicativo Web (Páginas do Razor)](../../mvc/razor-pages/index/_static/np2.png)

O modelo do Visual Studio cria um projeto inicial:

![Gerenciador de Soluções](razor-pages-start/_static/se.png)

Pressione **F5** para executar o aplicativo no modo de depuração ou **Ctrl-F5** para executar sem anexar o depurador

![Página Inicial ou de Índice](razor-pages-start/_static/home.png)

* O Visual Studio inicia o [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview) e executa o aplicativo. A barra de endereços mostra `localhost:port#` e não algo como `example.com`. Isso ocorre porque `localhost` é o nome do host padrão do computador local. Localhost serve somente solicitações da Web do computador local. Quando o Visual Studio cria um projeto Web, uma porta aleatória é usada para o servidor Web. Na imagem anterior, o número da porta é 5000. Quando você executar o aplicativo, você verá um número da porta diferente.
* Iniciar o aplicativo com **Ctrl+F5** (modo de não depuração) permite que você faça alterações de código, salve o arquivo, atualize o navegador e veja as alterações de código. Muitos desenvolvedores preferem usar modo de não depuração para iniciar o aplicativo e exibir alterações rapidamente.

[!INCLUDE[razor-pages-start](../../includes/RP/razor-pages-start.md)]

>[!div class="step-by-step"]
[Próximo: adicionando um modelo](xref:tutorials/razor-pages/model)
