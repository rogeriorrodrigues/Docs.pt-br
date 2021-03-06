---
title: "Atualizando as páginas geradas"
author: rick-anderson
description: "Atualizando as páginas geradas com melhor exibição."
keywords: "ASP.NET Core, Páginas Razor"
ms.author: riande
manager: wpickett
ms.date: 08/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/razor-pages/da1
ms.openlocfilehash: 290d752ea5f177348ff3e749cc125e946ae6e763
ms.sourcegitcommit: 6e83c55eb0450a3073ef2b95fa5f5bcb20dbbf89
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2017
---
# <a name="updating-the-generated-pages"></a>Atualizando as páginas geradas

Por [Rick Anderson](https://twitter.com/RickAndMSFT)

Temos um bom começo para o aplicativo de filme, mas a apresentação não é ideal. Você não deseja ver a hora (12:00:00 AM na imagem abaixo) e **ReleaseDate** deve ser **Release Date** (duas palavras).

![Aplicativo de filme aberto no Chrome mostrando os dados do filme](sql/_static/m55.png)

## <a name="update-the-generated-code"></a>Atualize o código gerado

Abra o arquivo *Models/Movie.cs* e adicione as linhas realçadas mostradas no seguinte código:

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/MovieDate.cs?name=snippet_1&highlight=10-11)]

Clique com o botão direito do mouse em uma linha curvada vermelha > ** Ações Rápidas e Refatorações**.

  ![Menu contextual mostra **> Ações Rápidas e Refatorações**.](da1/qa.png)

Selecione `using System.ComponentModel.DataAnnotations;`

  ![usando System.ComponentModel.DataAnnotations na parte superior da lista](da1/da.png)

  O Visual Studio adiciona `using System.ComponentModel.DataAnnotations;`.

Abordaremos [DataAnnotations](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) no próximo tutorial. O atributo [Display](https://docs.microsoft.com//aspnet/core/api/microsoft.aspnetcore.mvc.modelbinding.metadata.displaymetadata) especifica o que deve ser exibido no nome de um campo (neste caso, “Release Date” em vez de “ReleaseDate”). O atributo [DataType](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) especifica o tipo de dados (Data) e, portanto, as informações de hora armazenadas no campo não são exibidas.

Procure Pages/Movies e focalize um link **Editar** para ver a URL de destino.

![Janela do navegador com o mouse sobre o link Editar e a URL de link http://localhost:1234/Movies/Edit/5 é mostrada](da1/edit7.png)

Os links **Editar**, **Detalhes** e **Excluir** são gerados pelo [Auxiliar de Marcação de Âncora](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) no arquivo *Pages/Movies/Index.cshtml*.

[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml?highlight=16-18&range=32-)]

Os [Auxiliares de Marcação](xref:mvc/views/tag-helpers/intro) permitem que o código do servidor participe da criação e renderização de elementos HTML em arquivos do Razor. No código anterior, o `AnchorTagHelper` gera dinamicamente o valor do atributo `href` HTML da página Razor (a rota é relativa), o `asp-page` e a ID da rota (`asp-route-id`). Consulte [Geração de URL para Páginas](xref:mvc/razor-pages/index#url-generation-for-pages) para obter mais informações.

Use **Exibir Código-fonte** em seu navegador favorito para examinar a marcação gerada. Uma parte do HTML gerado é mostrada abaixo:

```html
<td>
  <a href="/Movies/Edit?id=1">Edit</a> |
  <a href="/Movies/Details?id=1">Details</a> |
  <a href="/Movies/Delete?id=1">Delete</a>
</td>
```

Os links gerados dinamicamente passam a ID de filme com uma cadeia de consulta (por exemplo, `http://localhost:5000/Movies/Details?id=2`). 

Atualize as Páginas Editar, Detalhes e Excluir do Razor para que elas usem o modelo de rota “{id:int}”. Altere a diretiva de página de cada uma dessas páginas para `@page "{id:int}"`. Execute o aplicativo e, em seguida, exiba o código-fonte. O HTML gerado adiciona a ID à parte do caminho da URL:

```html
<td>
  <a href="/Movies/Edit/1">Edit</a> |
  <a href="/Movies/Details/1">Details</a> |
  <a href="/Movies/Delete/1">Delete</a>
</td>
```

Uma solicitação para a página com o modelo de rota “{id:int}” que **não** inclui o inteiro retornará um erro HTTP 404 (não encontrado). Por exemplo, `http://localhost:5000/Movies/Details` retornará um erro 404. Para tornar a ID opcional, acrescente `?` à restrição de rota:

 ```cshtml
@page "{id:int?}"
```

### <a name="update-concurrency-exception-handling"></a>Atualizar o tratamento de exceção de simultaneidade

Atualize o método `OnPostAsync` no arquivo *Pages/Movies/Edit.cshtml.cs*. O seguinte código realçado mostra as alterações:

[!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Edit.cshtml.cs?name=snippet1&highlight=16-23)]

O código anterior apenas detecta as exceções de simultaneidade quando o primeiro cliente simultâneo exclui o filme e o segundo cliente simultâneo posta alterações no filme.

Para testar o bloco `catch`:

* Definir um ponto de interrupção em `catch (DbUpdateConcurrencyException)`
* Edite um filme.
* Em outra janela do navegador, selecione o link **Excluir** do mesmo filme e, em seguida, exclua o filme.
* Na janela do navegador anterior, poste as alterações no filme.

O código de produção geralmente detectará conflitos de simultaneidade quando dois ou mais clientes atualizarem um registro ao mesmo tempo. Consulte [Tratando conflitos de simultaneidade](xref:data/ef-mvc/concurrency) para obter mais informações.

### <a name="posting-and-binding-review"></a>Análise de postagem e associação

Examine o arquivo *Pages/Movies/Edit.cshtml.cs*: [!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Edit.cshtml.cs?name=snippet2)]

Quando uma solicitação HTTP GET é feita para a página Movies/Edit (por exemplo, `http://localhost:5000/Movies/Edit/2`):

* O método `OnGetAsync` busca o filme do banco de dados e retorna o método `Page`. 
* O método `Page` renderiza a página Razor *Pages/Movies/Edit.cshtml*. O arquivo *Pages/Movies/Edit.cshtml* contém a diretiva de modelo (`@model RazorPagesMovie.Pages.Movies.EditModel`), que torna o modelo de filme disponível na página.
* O formulário Editar é exibido com os valores do filme.

Quando a página Movies/Edit é postada:

* Os valores de formulário na página são associados à propriedade `Movie`. O atributo `[BindProperty]` habilita a [Associação de modelos](xref:mvc/models/model-binding).

  ```csharp
  [BindProperty]
  public Movie Movie { get; set; }
  ```

* Se houver erros no estado do modelo (por exemplo, `ReleaseDate` não pode ser convertida em uma data), o formulário será postado novamente com os valores enviados.
* Se não houver erros do modelo, o filme será salvo.

Os métodos HTTP GET nas páginas Índice, Criar e Excluir do Razor seguem um padrão semelhante. O método `OnPostAsync` HTTP POST na página Criar do Razor segue um padrão semelhante ao método `OnPostAsync` na página Editar do Razor.

A pesquisa é adicionada no próximo tutorial.

>[!div class="step-by-step"]
[Anterior: Trabalhando com o SQL Server LocalDB](xref:tutorials/razor-pages/sql)
[Adicionando uma pesquisa](xref:tutorials/razor-pages/search)
