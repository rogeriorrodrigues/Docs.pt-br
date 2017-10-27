---
title: Novidades do ASP.NET Core 2.0
author: rick-anderson
description: Novidades do ASP.NET Core 2.0
keywords: "ASP.NET Core, notas de versão, novidades"
ms.author: riande
manager: wpickett
ms.date: 07/10/2017
ms.topic: article
ms.assetid: 08c9f457-9c24-40f9-a08b-47dc251e4cec
ms.technology: aspnet
ms.prod: aspnet-core
uid: aspnetcore-2.0
ms.openlocfilehash: c572315d7a801b9b87d5f4cd14b82c5ed27e7a85
ms.sourcegitcommit: 6e83c55eb0450a3073ef2b95fa5f5bcb20dbbf89
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2017
---
# <a name="whats-new-in-aspnet-core-20"></a>Novidades do ASP.NET Core 2.0

Este artigo destaca as alterações mais significativas no ASP.NET Core 2.0, com links para a documentação relevante.

## <a name="razor-pages"></a>Páginas do Razor

Páginas do Razor é um novo recurso do ASP.NET Core MVC que torna a codificação de cenários focados em página mais fácil e produtiva.

Para obter mais informações, consulte a introdução e o tutorial:

* [Introdução a Páginas do Razor](xref:mvc/razor-pages/index)
* [Iniciando com Páginas do Razor](xref:tutorials/razor-pages/razor-pages-start)

## <a name="aspnet-core-metapackage"></a>Metapacote do ASP.NET Core

Um novo metapacote do ASP.NET Core inclui todos os pacotes feitos e com suporte pelas equipes do ASP.NET Core e do Entity Framework Core, juntamente com as respectivas dependências internas e de terceiros. Você não precisa mais escolher recursos individuais do ASP.NET Core por pacote. Todos os recursos estão incluídos no pacote [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All). Os modelos padrão usam este pacote.

Para obter mais informações, consulte [Metapacote do Microsoft.AspNetCore.All para ASP.NET Core 2.0](xref:fundamentals/metapackage).

## <a name="runtime-store"></a>Repositório de tempo de execução

Aplicativos que usam o metapacote `Microsoft.AspNetCore.All` aproveitam automaticamente o novo repositório de tempo de execução do .NET Core. O repositório contém todos os ativos de tempo de execução necessários para executar aplicativos ASP.NET Core 2.0. Quando você usa o metapacote `Microsoft.AspNetCore.All`, nenhum ativo dos pacotes NuGet do ASP.NET Core referenciados são implantados com o aplicativo porque eles já estão no sistema de destino. Os ativos no repositório de tempo de execução também são pré-compilados para melhorar o tempo de inicialização do aplicativo.

Para obter mais informações, consulte [Repositório de tempo de execução](https://docs.microsoft.com/dotnet/core/deploying/runtime-store)

## <a name="net-standard-20"></a>.NET Standard 2.0

Os pacotes do ASP.NET Core 2.0 são direcionados ao .NET Standard 2.0. Os pacotes podem ser referenciados por outras bibliotecas do .NET Standard 2.0 e podem ser executados em implementações em conformidade com o .NET Standard 2.0, incluindo o .NET Core 2.0 e o .NET Framework 4.6.1. 

O metapacote `Microsoft.AspNetCore.All` tem como destino apenas o .NET Core 2.0, porque ele se destina a ser usado com o repositório de tempo de execução do .NET Core 2.0.

## <a name="configuration-update"></a>Atualização da configuração

Uma instância de `IConfiguration` é adicionada ao contêiner de serviços por padrão no ASP.NET Core 2.0. `IConfiguration` no contêiner de serviços torna mais fácil para aplicativos recuperarem valores de configuração do contêiner.

Para obter informações sobre o status da documentação planejada, consulte o [problema do GitHub](https://github.com/aspnet/Docs/issues/3387).

## <a name="logging-update"></a>Atualização de registro em log

No ASP.NET Core 2.0, o log será incorporado no sistema de DI (injeção de dependência) por padrão. Você adiciona provedores e configura a filtragem no arquivo *Program.cs* em vez de usar o arquivo *Startup.cs*. E o `ILoggerFactory` padrão dá suporte à filtragem de forma que lhe permite usar uma abordagem flexível para filtragem entre provedores e filtragem específica do provedor.

Para obter mais informações, consulte [Introdução ao registro em log](xref:fundamentals/logging).

## <a name="authentication-update"></a>Atualização de autenticação

Um novo modelo de autenticação torna mais fácil configurar a autenticação para um aplicativo usando a DI.

Novos modelos estão disponíveis para configurar a autenticação para aplicativos Web e APIs Web usando [Azure AD B2C] (https://azure.microsoft.com/services/active-directory-b2c/).

Para obter informações sobre o status da documentação planejada, consulte o [problema do GitHub](https://github.com/aspnet/Docs/issues/3054).

## <a name="identity-update"></a>Atualização de identidade

Tornamos mais fácil criar APIs Web seguras usando a identidade do ASP.NET Core 2.0. Você pode adquirir tokens de acesso para acessar suas APIs Web usando a [MSAL (Biblioteca de Autenticação da Microsoft)](https://www.nuget.org/packages/Microsoft.Identity.Client).

Para obter mais informações sobre alterações de autenticação no 2.0, consulte os seguintes recursos:

* [Confirmação de conta e de recuperação de senha no ASP.NET Core](xref:security/authentication/accconfirm)
* [Habilitar a geração de código QR para aplicativos de autenticador no ASP.NET Core](xref:security/authentication/identity-enable-qrcodes)
* [Migrando Autenticação e Identidade para o ASP.NET Core 2.0](xref:migration/1x-to-2x/identity-2x)

## <a name="spa-templates"></a>Modelos do SPA

Modelos de projeto de SPA (aplicativo de página único) para Angular, Aurelia, Knockout.js, React.js e React.js com Redux estão disponíveis. O modelo Angular foi atualizado para Angular 4. Os modelos Angular e React estão disponíveis por padrão. Para obter informações sobre como obter os outros modelos, consulte [Criar um novo projeto de SPA](xref:client-side/spa-services#creating-a-new-project). Para obter informações sobre como criar um SPA no ASP.NET Core, consulte [Usando JavaScriptServices para criar aplicativos de página única](xref:client-side/spa-services).

## <a name="kestrel-improvements"></a>Melhorias do Kestrel

O servidor Web Kestrel tem novos recursos que o tornam mais adequado como um servidor voltado para a Internet. Adicionamos um número de opções de configuração de restrição de servidor na nova propriedade `Limits` da classe `KestrelServerOptions`. Agora você pode adicionar limites para o seguinte:

- Número máximo de conexões de cliente
- Tamanho máximo do corpo da solicitação
- Taxa de dados mínima do corpo da solicitação

Para obter mais informações, consulte [Implementação do servidor Web Kestrel no ASP.NET Core](xref:fundamentals/servers/kestrel).

## <a name="weblistener-renamed-to-httpsys"></a>WebListener renomeado para HTTP.sys

Os pacotes `Microsoft.AspNetCore.Server.WebListener` e `Microsoft.Net.Http.Server` foram mesclados em um novo pacote `Microsoft.AspNetCore.Server.HttpSys`. Os namespaces foram atualizados para corresponderem.

Para obter mais informações, consulte [Implementação do servidor Web HTTP.sys no ASP.NET Core](xref:fundamentals/servers/httpsys).

## <a name="enhanced-http-header-support"></a>Suporte aprimorado a cabeçalho HTTP

Ao usar o MVC para transmitir um `FileStreamResult` ou um `FileContentResult`, agora você tem a opção de definir uma `ETag` ou uma data `LastModified` no conteúdo que você transmitir. Você pode definir esses valores no conteúdo retornado com código semelhante ao seguinte:

```csharp
var data = Encoding.UTF8.GetBytes("This is a sample text from a binary array");
var entityTag = new EntityTagHeaderValue("\"MyCalculatedEtagValue\"");
return File(data, "text/plain", "downloadName.txt", lastModified: DateTime.UtcNow.AddSeconds(-5), entityTag: entityTag);
```

O arquivo retornado para os visitantes será decorado com os cabeçalhos HTTP apropriados para os valores `ETag` e `LastModified`.

Se um visitante de aplicativo solicita o conteúdo com um cabeçalho de solicitação de intervalo, o ASP.NET reconhece isso e manipula esse cabeçalho. Se o conteúdo solicitado puder ser parcialmente entregue, o ASP.NET ignorará adequadamente e retornará apenas o conjunto de bytes solicitado.  Você não precisa escrever nenhum manipulador especial em seus métodos para adaptar ou manipular esse recurso; ele é manipulado automaticamente para você.

## <a name="hosting-startup-and-application-insights"></a>Inicialização de hospedagem e o Application Insights

Ambientes de hospedagem podem injetar dependências de pacote extras e executar código durante a inicialização do aplicativo, sem que o aplicativo precise tomar uma dependência explicitamente ou chamar algum método. Esse recurso pode ser usado para habilitar determinados ambientes para recursos de "esclarecimento" exclusivos para esse ambiente sem que o aplicativo precise saber antecipadamente. 

No ASP.NET Core 2.0, esse recurso é usado para habilitar o diagnóstico do Application Insights automaticamente durante a depuração no Visual Studio e (depois de optar por isto) quando em execução nos Serviços de Aplicativos do Azure. Como resultado, os modelos de projeto não adicionam mais código e pacotes do Application Insights por padrão.

Para obter informações sobre o status da documentação planejada, consulte o [problema do GitHub](https://github.com/aspnet/Docs/issues/3389).

## <a name="automatic-use-of-anti-forgery-tokens"></a>Uso automático de tokens antifalsificação

O ASP.NET Core sempre ajudou a fazer a codificação HTML de seu conteúdo por padrão, mas com a nova versão, estamos dando uma passo adicional para ajudar a impedir ataques de XSRF (falsificação de solicitação entre sites). O ASP.NET Core agora emitirá tokens antifalsificação por padrão e os validará em ações de POST de formulário e em páginas sem configuração adicional.

Para obter mais informações, consulte [Impedindo ataques de falsificação de solicitação entre sites (CSRF/XSRF) no ASP.NET Core](xref:security/anti-request-forgery).

## <a name="automatic-precompilation"></a>Pré-compilação automática

A pré-compilação da exibição do Razor é habilitada durante a publicação por padrão, reduzindo o tamanho da saída de publicação e o tempo de inicialização do aplicativo.

## <a name="razor-support-for-c-71"></a>Suporte ao Razor para C# 7.1

O mecanismo de exibição Razor foi atualizado para funcionar com o novo compilador Roslyn. Isso inclui suporte para recursos do C# 7.1 como expressões padrão, nomes de tupla inferidos e correspondência de padrões com genéricos. Para usar o C# 7.1 em seu projeto, adicione a seguinte propriedade no arquivo de projeto e, em seguida, recarregue a solução:

```xml
<LangVersion>latest</LangVersion>
```

Para obter informações sobre o status dos recursos do C# 7.1, consulte [o repositório GitHub do Roslyn](https://github.com/dotnet/roslyn/blob/master/docs/Language%20Feature%20Status.md).

## <a name="other-documentation-updates-for-20"></a>Outras atualizações de documentação para 2.0

* [Criar perfis de publicação para o Visual Studio e o MSBuild para implantar aplicativos ASP.NET Core](xref:publishing/web-publishing-vs)
* [Gerenciamento de chaves](xref:security/data-protection/implementation/key-management)
* [Configurando a autenticação do Facebook](xref:security/authentication/facebook-logins)
* [Configurando a autenticação do Twitter](xref:security/authentication/twitter-logins)
* [Configurando a autenticação do Google](xref:security/authentication/google-logins)
* [Configurando a autenticação da Conta da Microsoft](xref:security/authentication/microsoft-logins)

## <a name="migration-guidance"></a>Diretrizes de migração

Para obter diretrizes sobre como migrar aplicativos ASP.NET Core 1.x para o ASP.NET Core 2.0, consulte os seguintes recursos:

* [Migrando do ASP.NET Core 1.x para o ASP.NET Core 2.0](xref:migration/1x-to-2x/index)
* [Migrando Autenticação e Identidade para o ASP.NET Core 2.0](xref:migration/1x-to-2x/identity-2x)

## <a name="additional-information"></a>Informações adicionais

Para obter uma lista de alterações, consulte as [Notas de versão do ASP.NET Core 2.0](https://github.com/aspnet/Home/releases/tag/2.0.0).

Se você deseja ficar conectado com o progresso e os planos da equipe de desenvolvimento do ASP.NET Core, prepare-se para a [palestra semanal da comunidade do ASP.NET](https://live.asp.net/).
