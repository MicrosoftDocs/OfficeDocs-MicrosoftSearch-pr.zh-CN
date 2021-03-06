---
title: 在 SharePoint 网站中管理搜索框
ms.author: keremy
author: jeffkizn
manager: parulm
ms.audience: Admin
ms.topic: article
ms.service: mssearch
localization_priority: Normal
search.appverid:
- BFB160
- MET150
- MOE150
description: 如何自定义 SharePoint 网站的搜索框体验
ms.openlocfilehash: c58e7cf0a47d22fa9c6fd3abd93cc97087625690
ms.sourcegitcommit: 5df252e6d0bd67bb1b4c59418aceca8369f5fe42
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2021
ms.locfileid: "51031356"
---
# <a name="search-box-settings-on-sharepoint-sites"></a>SharePoint 网站的搜索框设置

在 SharePoint 网站上自定义 Microsoft 搜索的几种方法之一是定制套件导航栏中的搜索框在 SharePoint 网站中的工作方式，以最好地满足您的需求。

有关其他自定义选项，请参阅 Changing [the Microsoft Search results page to add custom verticals， result types and layouts](customize-search-page.md)和 Creating a custom search results [page](create-search-results-pages.md)。

> [!NOTE]
> 套件导航栏搜索框目前并非可供所有客户使用，但这些选项仍可立即设置，并且将在可用时生效。

对于下面列出的任务，你将 PowerShell 与 SharePoint PnP PowerShell 扩展一同使用。 可以在此处安装并了解有关如何开始使用 [的更多信息](/powershell/sharepoint/sharepoint-pnp/sharepoint-pnp-cmdlets?view=sharepoint-ps)。 您将使用此命令登录到您的网站或网站集：

```powershell
Connect-PnPOnline -Url <yoursiteurl> -UseWebLogin
# this will prompt you to sign into your site. Use the site owner credentials 
```

## <a name="changing-the-scope-of-search"></a>更改搜索范围

今天在 SharePoint Online 中创建新网站并键入搜索框中时，你将进入 Microsoft 搜索结果页面。 此页面默认显示来自当前网站的结果，并允许您将搜索范围扩展到当前网站与 (（如果有一个) ）关联的中心，或扩展到整个组织。

默认情况下，搜索框使用的范围取决于网站类型。

* 常规网站搜索当前网站。
* 中心网站搜索中心内的所有网站。
* 主网站搜索所有内容。

在某些情况下，您可能需要更改这些默认值以始终在整个组织或网站关联的中心进行搜索，而无需额外单击。

作为网站所有者，您可以使用以下命令更改这些默认值：

```powershell
Set-PnPSearchSettings -SearchScope Tenant
# DefaultScope | Hub | Site | Tenant
```

运行此命令后，之前默认显示当前网站的结果的网站将开始显示来自整个组织的结果。

若要返回到默认设置，请再次运行命令，值为"DefaultScope"。 若要在 Hub 中搜索，请使用"Hub"作为 SearchScope 值。

此设置适用于单个网站级别。 网站集没有等效设置。

## <a name="show-or-hide-the-search-box"></a>显示或隐藏搜索框

如果你想要阻止用户搜索或使用自定义搜索框实现，你可以选择隐藏套件导航栏搜索框。

若要更改给定网站的此设置，请使用此命令：

```powershell
Set-PnPSearchSettings -Scope Web -SearchBoxInNavBar Hidden
# Hidden | Inherit
```

或者，如果要为网站集中的所有网站设置它，可以使用此命令：

```powershell
Set-PnPSearchSettings -Scope Site -SearchBoxInNavBar Hidden
# Hidden | Inherit
```

运行这些命令后，搜索框将不再显示在页面顶部的导航栏中。 若要返回显示搜索框，请再次运行命令，将提供给"SearchBoxInNavBar"参数的值返回到"Inherit"。

有几个点需要考虑：

* 此设置仅适用于套件导航栏中的搜索框。 它不适用于页面中的搜索框或经典页面上的搜索框。

* 在导航栏中禁用搜索框后，如果您希望网站具有搜索功能，您必须使用自定义 Web 部件或 SharePoint 框架扩展自己提供搜索框。

* 此解决方案还将从网站的列表和库中删除搜索框。 除了网站范围的搜索之外，自定义搜索解决方案还需要考虑 SharePoint 列表和库的上下文搜索。

* 如果将设置应用到域的根网站，SharePoint 起始页也将停止显示搜索框。

## <a name="changing-the-hint-displayed-in-the-search-box"></a>更改搜索框中显示的提示

您可以更改针对给定站点或网站集的搜索框显示的提示。 这是在搜索框中开始键入之前显示的文本。 如果你以其他方式配置了自定义结果页面或更改了搜索行为，这可以帮助指导用户了解搜索预期内容。

> [!NOTE]
> 为了能够进行此更改，需要允许以租户管理员角色在有关网站上运行自定义脚本，这默认情况下是不允许的。 有关详细信息 https://docs.microsoft.com/sharepoint/allow-or-prevent-custom-script ，请参阅 。 您可以允许运行自定义脚本，进行更改，然后在必要时还原为禁止网站的脚本。

若要更改给定网站的此设置，请运行以下命令：

```powershell
Set-PnPSearchSettings -Scope Web -SearchBoxPlaceholderText "my placeholder" 
```

或者，如果要为网站集中的所有网站设置它，可以使用此命令：

```powershell
Set-PnPSearchSettings -Scope Site -SearchBoxPlaceholderText "my placeholder" 
```

若要返回到默认占位符文本，将该值设置为空白 ("") 。