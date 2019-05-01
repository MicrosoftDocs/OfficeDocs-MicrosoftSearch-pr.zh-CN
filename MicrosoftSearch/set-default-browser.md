---
title: 设置默认浏览器
ms.author: dawholl
author: dawholl
manager: kellis
ms.date: 12/20/2018
ms.audience: Admin
ms.topic: article
ms.service: mssearch
localization_priority: Priority
search.appverid:
- BFB160
- MET150
- MOE150
ms.assetid: 53e2b71a-348b-4dfe-a504-6e97d573effe
description: 了解如何使用 Microsoft 搜索为公司配置默认浏览器。
ms.openlocfilehash: 160dbbef9981127b74c51f54f86428667ecd4471
ms.sourcegitcommit: a5fd9d4f46bbb7c539630735ac16e0c786939e5d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2019
ms.locfileid: "33508987"
---
# <a name="set-default-browser"></a><span data-ttu-id="aa0e0-103">设置默认浏览器</span><span class="sxs-lookup"><span data-stu-id="aa0e0-103">Set default browser</span></span>

<span data-ttu-id="aa0e0-104">配置默认浏览器、默认搜索引擎和默认主页将帮助用户发现 Microsoft 搜索功能、鼓励更多用户使用，并提供更流畅的体验。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-104">Configuring the default browser, default search engine, and default homepage will help your users discover Microsoft Search capabilities, encourage more usage, and provide a smoother experience.</span></span>
  
<span data-ttu-id="aa0e0-105">若要为组织设置默认浏览器，请按照下面步骤操作。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-105">To set the default browser for your organization, follow the steps below.</span></span>
  
## <a name="windows-8-and-above"></a><span data-ttu-id="aa0e0-106">Windows 8 及更高版本</span><span class="sxs-lookup"><span data-stu-id="aa0e0-106">Windows 8 and above</span></span>

<span data-ttu-id="aa0e0-107">要将 Internet Explorer 或 Microsoft Edge 设置为默认浏览器，请按以下步骤操作：</span><span class="sxs-lookup"><span data-stu-id="aa0e0-107">To set Internet Explorer or Microsoft Edge as the default browser, follow these steps:</span></span>
  
### <a name="create-default-associations-file"></a><span data-ttu-id="aa0e0-108">创建默认关联文件</span><span class="sxs-lookup"><span data-stu-id="aa0e0-108">Create default associations file</span></span>

1. <span data-ttu-id="aa0e0-109">打开 PowerShell 管理控制台。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-109">Open an administrative PowerShell console.</span></span>
    
2.  `New-Item -Path "\\$env:USERDOMAIN\SYSVOL\$env:USERDNSDOMAIN" -Type Directory -Name "Settings"`
    
3.  `$SettingsPath="\\$env:USERDOMAIN\SYSVOL\$env:USERDNSDOMAIN\Settings"`
    
4.  `Start-Process Dism.exe -PassThru "/Online /Export-DefaultAppAssociations:$SettingsPath\AppAssoc.xml"`
    
<span data-ttu-id="aa0e0-110">这些步骤尝试在域控制器的 SYSVOL 文件夹中创建默认关联文件。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-110">These steps try and create the default associations file in the SYSVOL folder of the domain controller.</span></span>
  
### <a name="add-or-edit-the-default-associations-file"></a><span data-ttu-id="aa0e0-111">添加或编辑默认关联文件</span><span class="sxs-lookup"><span data-stu-id="aa0e0-111">Add or edit the default associations file</span></span>

1. `Notepad "$SettingsPath\AppAssoc.xml"`
    
2. <span data-ttu-id="aa0e0-112">编辑以下条目（.htm、.html、http、https），如果不需要，则删除其他条目。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-112">Edit the following entries (.htm, .html, http, https), and remove other entries if they're not needed.</span></span>
    
  - <span data-ttu-id="aa0e0-113">**Microsoft Edge**</span><span class="sxs-lookup"><span data-stu-id="aa0e0-113">**Microsoft Edge**</span></span>
    
     `<Association Identifier=".htm" ProgId="AppX4hxtad77fbk3jkkeerkrm0ze94wjf3s9" ApplicationName="Microsoft Edge" />`
  
     `<Association Identifier=".html" ProgId="AppX4hxtad77fbk3jkkeerkrm0ze94wjf3s9" ApplicationName="Microsoft Edge" />`
  
     `<Association Identifier="http" ProgId="AppXq0fevzme2pys62n3e0fbqa7peapykr8v" ApplicationName="Microsoft Edge" />`
    
  - <span data-ttu-id="aa0e0-114">**Internet Explorer**</span><span class="sxs-lookup"><span data-stu-id="aa0e0-114">**Internet Explorer**</span></span>
    
     `<Association Identifier=".htm" ProgId="htmlfile" ApplicationName="Internet Explorer" />`
  
     `<Association Identifier=".html" ProgId="htmlfile" ApplicationName="Internet Explorer" />`
  
     `<Association Identifier="http" ProgId="IE.HTTP" ApplicationName="Internet Explorer" />`
  
     `<Association Identifier="https" ProgId="IE.HTTPS" ApplicationName="Internet Explorer" />`
    
3. <span data-ttu-id="aa0e0-115">打开组策略管理控制台 (gpmc.msc) 并切换到编辑任何现有策略或新建一个策略。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-115">Open Group Policy Management Console (gpmc.msc) and switch to editing any existing policy or creating a new one.</span></span>
    
1. <span data-ttu-id="aa0e0-116">导航到**计算机配置\管理模板\Windows 组件\文件资源管理器**</span><span class="sxs-lookup"><span data-stu-id="aa0e0-116">Navigate to **Computer Configuration\Administrative Templates\Windows Components\File Explorer**</span></span>
    
2. <span data-ttu-id="aa0e0-117">双击“设置默认关联配置文件”\*\*\*\*，将其设置为“已启用”\*\*\*\*，并输入访问 AppAssoc.xml 的路径（例如 %USERDOMAIN%\SYSVOL\%USERDNSDOMAIN%\Settings\AppAssoc.xml）</span><span class="sxs-lookup"><span data-stu-id="aa0e0-117">Double-click **Set a default associations configuration file**, set it to **Enabled**, and enter the path to AppAssoc.xml (for example %USERDOMAIN%\SYSVOL\%USERDNSDOMAIN%\Settings\AppAssoc.xml)</span></span>
    
4. <span data-ttu-id="aa0e0-118">通过将生成的 GPO 链接到适当的域来强制执行。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-118">Enforce the resultant GPO by linking it to the appropriate domain.</span></span>
    
<span data-ttu-id="aa0e0-119">用户将能够在设置此策略后更改浏览器。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-119">Users will be able to change the browser after this policy is set.</span></span>
  
## <a name="windows-7"></a><span data-ttu-id="aa0e0-120">Windows 7</span><span class="sxs-lookup"><span data-stu-id="aa0e0-120">Windows 7</span></span>

1. <span data-ttu-id="aa0e0-121">配置将用于设置 GPO 的本地计算机。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-121">Configure the local machine that will be used to set the GPO.</span></span>
    
1. <span data-ttu-id="aa0e0-122">打开“控制面板\程序\默认程序\设置默认程序”\*\*\*\* 并将 Internet Explorer 设置为默认程序。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-122">Open **Control Panel\Programs\Default Programs\Set Default Programs** and set Internet Explorer as the default.</span></span> 
    
2. <span data-ttu-id="aa0e0-123">打开组策略管理控制台 (gpmc.msc) 并切换到编辑任何现有策略或新建一个策略。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-123">Open Group Policy Management Console (gpmc.msc) and switch to editing any existing policy or creating a new one.</span></span>
    
1. <span data-ttu-id="aa0e0-124">导航到**\<计算机/用户\>配置\策略\偏好设置\Windows 设置**。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-124">Navigate to **\<Computer/User\> Configuration\Policies\Preferences\Windows Settings**.</span></span>
    
2. <span data-ttu-id="aa0e0-125">右键单击“注册表\新建”\*\*\*\* 然后选择“注册表向导”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-125">Right-click on **Registry\New** and select **Registry Wizard**.</span></span>
    
3. <span data-ttu-id="aa0e0-126">从注册表浏览器窗口中，选择“本地计算机”\*\*\*\*，然后单击“下一步”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-126">From the Registry Browser window, select **Local Computer** and click **Next**.</span></span>
    
4. <span data-ttu-id="aa0e0-p101">导航到 **HKEY_CURRENT_USER\Software\Microsoft\Windows\Shell\Associations\UrlAssociations\https** 并选择 ProgId 值。请确保值如下所示：</span><span class="sxs-lookup"><span data-stu-id="aa0e0-p101">Navigate to **HKEY_CURRENT_USER\Software\Microsoft\Windows\Shell\Associations\UrlAssociations\https** and select the ProgId value. Make sure the value looks like the one below:</span></span> 
    
    ![在编辑字符串中选择 ProgID 值](media/f6173dcc-b898-4967-8c40-4b0fe411a92b.png)
  
5. <span data-ttu-id="aa0e0-p102">导航到 **HKEY_CURRENT_USER\Software\Microsoft\Windows\Shell\Associations\UrlAssociations\https** 并选择 ProgId 值。请确保值如下所示：</span><span class="sxs-lookup"><span data-stu-id="aa0e0-p102">Navigate to **HKEY_CURRENT_USER\Software\Microsoft\Windows\Shell\Associations\UrlAssociations\https** and select the ProgId value. Make sure that the value looks like the one below:</span></span> 
    
    ![在编辑字符串中选择 HTTPS 的 ProgId](media/3519e13b-4fe7-4d15-946c-82fd50fc49bb.png)
  
3. <span data-ttu-id="aa0e0-133">通过将生成的 GPO 链接到适当的域来强制执行。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-133">Enforce the resultant GPO by linking it to the appropriate domain.</span></span>
    
<span data-ttu-id="aa0e0-134">用户将能够在设置此策略后更改浏览器。</span><span class="sxs-lookup"><span data-stu-id="aa0e0-134">Users will be able to change the browser after this policy is set.</span></span>