---
title: 自定义搜索结果布局
ms.author: anfowler
author: adefowler
manager: shohara
ms.audience: Admin
ms.topic: article
ms.service: mssearch
localization_priority: Normal
search.appverid:
- BFB160
- MET150
- MOE150
description: 使用自适应卡片，创建布局以查看自定义搜索结果
ms.openlocfilehash: 2ca53f2e2dc207acdf48542f39ee4f448bdeb90e
ms.sourcegitcommit: bfcab9d42e93addccd1e3875b41bc9cc1b6986cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "37949601"
---
# <a name="create-a-layout-to-customize-search-results"></a><span data-ttu-id="9bbb1-103">创建布局以自定义搜索结果</span><span class="sxs-lookup"><span data-stu-id="9bbb1-103">Create a layout to customize search results</span></span>

<span data-ttu-id="9bbb1-104">您可以使用搜索布局设计器来设计自定义垂直布局的结果布局。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-104">You can design the result layout for a custom vertical using the search layout designer.</span></span> <span data-ttu-id="9bbb1-105">您可以通过选择布局设计器中提供的模板来开始设计布局，并在它们满足您的要求时使用它们。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-105">You can start designing the layout by choosing templates offered in the layout designer and using them if they fit your requirements.</span></span> <span data-ttu-id="9bbb1-106">或者，您可以选择以多种方式编辑这些模板以满足您的要求。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-106">Or you can choose to edit these templates in various ways to fit your requirements.</span></span> <span data-ttu-id="9bbb1-107">例如，"添加/删除图像"、"添加/删除文本"、"修改文本"。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-107">For example, add/remove images, add/remove text, modify text.</span></span> <span data-ttu-id="9bbb1-108">如果所有模板都无法满足您的要求，则可以选择使用空白模板开始设计布局。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-108">If none of the templates meet your requirement, you can choose to start designing your layout using a blank template.</span></span>  

 

<span data-ttu-id="9bbb1-109">在布局准备就绪后，可以使用[自适应卡片模板语言](https://docs.microsoft.com/adaptive-cards/templating/language)创建 thea 结果布局 JSON，该格式用于定义结果类型。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-109">Once the layout is ready, you use the [Adaptive Cards Template language](https://docs.microsoft.com/adaptive-cards/templating/language)  to create thea result layout JSON which is used to define a result type.</span></span> <span data-ttu-id="9bbb1-110">您可以使用布局设计器中的映射步骤将结果属性映射到布局。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-110">You map the result properties to the layout using the Mapping step in the layout designer.</span></span>  

## <a name="create-a-layout-on-your-own"></a><span data-ttu-id="9bbb1-111">自己创建布局</span><span class="sxs-lookup"><span data-stu-id="9bbb1-111">Create a layout on your own</span></span>
<span data-ttu-id="9bbb1-112">您自己创建布局需要了解[自适应卡片](https://docs.microsoft.com/adaptive-cards/authoring-cards/getting-started)及其[架构](https://adaptivecards.io/explorer/)。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-112">Creating a layout on your own requires knowledge of [adaptive cards](https://docs.microsoft.com/adaptive-cards/authoring-cards/getting-started) and their [schema](https://adaptivecards.io/explorer/).</span></span> <span data-ttu-id="9bbb1-113">搜索结果布局使用自适应卡片提供的部分元素，您可以使用布局设计器了解支持的一组元素。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-113">Search result layout uses a subset of the elements offered by adaptive cards and you can use the layout designer to learn about the supported set of elements.</span></span>  

<span data-ttu-id="9bbb1-114">创建自己的布局时，请使用来自您的数据创建自适应卡片布局，然后再完成布局。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-114">While creating your own layout, create the adaptive card layout using data from your , and then finalize the layout.</span></span>
<span data-ttu-id="9bbb1-115">创建自己的布局有两个主要步骤</span><span class="sxs-lookup"><span data-stu-id="9bbb1-115">There are two main steps in creating your own layout</span></span>
- <span data-ttu-id="9bbb1-116">设计布局</span><span class="sxs-lookup"><span data-stu-id="9bbb1-116">Designing the layout</span></span>
- <span data-ttu-id="9bbb1-117">将数据与模板分离</span><span class="sxs-lookup"><span data-stu-id="9bbb1-117">Separating the data from the template</span></span>

#### <a name="designing-the-layout"></a><span data-ttu-id="9bbb1-118">设计布局</span><span class="sxs-lookup"><span data-stu-id="9bbb1-118">Designing the layout</span></span>

<span data-ttu-id="9bbb1-119">在此示例中，我们将显示一个包含标题、链接和说明性文本的布局。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-119">In this example, we're showing a layout with a header, link, and descriptive text.</span></span>

![包含标头、链接和说明的布局的示例。](media/Verts-ExampleLayout.png)

<span data-ttu-id="9bbb1-121">以下是布局的关联 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="9bbb1-121">And here's the layout's associated JSON file:</span></span>


```json
{ 
    "type": "AdaptiveCard", 
    "version": "1.0", 
     "body": [ 
{ 

            "type": "ColumnSet", 
             "columns": [ 
                 { 
                     "type": "Column", 
                     "width": 8, 
                     "items": [ 
                         { 
                             "type": "TextBlock", 
                             "text": "Contoso Marketing Analysis - Q3 FY18", 
                             "color": "Accent", 
                             "size": "Medium", 
                             "spacing": "None", 
                             "$when": "{title != \"\"}", 
                             "weight": "Bolder" 
                        }, 
                        { 
                        "type": "TextBlock",  
                        "text": "https://contoso.com/hr/link", 
                        "spacing": "None",  
                        "color": "Dark", 
                        "weight": "Bolder" 

                        }, 

                        {  
                        "type": "TextBlock", 
                        "text": "Marketing team at Contoso.., and looking at the Contoso Marketing documents on the team site. This contains the data from FY20 and will taken over to FY21...Marketing Planning is ongoing for FY20..",  
                        "wrap": true, 
                        "maxLines": 2, 
                        "spacing": "Medium" 
                        } 
                        ], 

                    "horizontalAlignment": "Center", 
                    "spacing": "None" 

                } 

            ] 

        } 
        ], 

    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json" 
}
```

#### <a name="separating-the-data-from-the-layout"></a><span data-ttu-id="9bbb1-122">将数据与布局分离</span><span class="sxs-lookup"><span data-stu-id="9bbb1-122">Separating the data from the layout</span></span>

<span data-ttu-id="9bbb1-123">您可以将数据与布局分开，并绑定数据。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-123">You can separate the data from the layout and bind the data.</span></span> 

<span data-ttu-id="9bbb1-124">下面是绑定数据后的布局 JSON：</span><span class="sxs-lookup"><span data-stu-id="9bbb1-124">Here's Layout JSON after binding the data:</span></span>


```json
{ 

    "type": "AdaptiveCard", 
    "version": "1.0", 
    "body": [ 
    { 
    "type": "ColumnSet", 
"columns": [ 

                { 
                "type": "Column", 
                "width": 8, 
                "items": [ 
                { 
                "type": "TextBlock", 
                "text": "[{title}]({titleUrl})", 
                "color": "Accent", 
                "size": "Medium",
                "spacing": "None", 
                "weight": "Bolder" 

                 }, 
                 { 
                 "type": "TextBlock", 
                 "text": "{link}",
                 "spacing": "None", 
                 "color": "Dark",
                 "weight": "Bolder" 
                 }, 
                 { 
                 "type": "TextBlock",
                 "text": "{description}",
                 "wrap": true,
                 "maxLines": 2, 
                 "spacing": "Medium" 
                 } 
                 ], 
                 "horizontalAlignment": "Center", 
                 "spacing": "None" 
                 } 
                 ] 

        } 

    ], 

    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json" 
}
```

<span data-ttu-id="9bbb1-125">示例数据：在 "预览模式" 中，在**示例数据编辑器**中指定示例数据以查看数据绑定卡。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-125">Sample data: Specify sample data in the **Sample Data Editor** to view the data-bound card when in "Preview Mode".</span></span>

```json
{ 

    "title": "Contoso Marketing Analysis - Q3 FY18", 
    "titleUrl": "https://contoso.com/hr/link", 
    "link": "https://contoso.com/hr/link", 
    "description": "Marketing team, and looking at the Contoso Marketing documents on the team site. Yo can't see right...Marketing Planning presentation?" 

} 
```

## <a name="map-the-layout-to-the-result-properties"></a><span data-ttu-id="9bbb1-126">将布局映射到结果属性</span><span class="sxs-lookup"><span data-stu-id="9bbb1-126">Map the layout to the result properties</span></span>

<span data-ttu-id="9bbb1-127">您必须将布局的每个字段映射到一个 result 属性或一个连接器属性，以生成结果布局 JSON。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-127">You must map each field of the layout to a result property or a connector property to generate the result layout JSON.</span></span>

![Verts-SearchLayoutDesigner](media/Verts-SearchLayoutDesigner.png)

<span data-ttu-id="9bbb1-129">在布局中选择一个字段，以突出显示需要映射的变量。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-129">Select a field in the layout to highlight the variables that need to be mapped.</span></span> <span data-ttu-id="9bbb1-130">您可以将多个变量用于单个字段，并且所有字段都必须映射到 result 属性。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-130">You can use multiple variables for a single field and all fields must be mapped to the result properties.</span></span>

## <a name="things-to-consider"></a><span data-ttu-id="9bbb1-131">要考虑的事项 .。。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-131">Things to consider...</span></span>

<span data-ttu-id="9bbb1-132">在开始之前，应执行一些操作，并应避免使用以下操作，以确保布局将会成功。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-132">Before you get started, there are a few things that you should do and a few things you should avoid to ensure that your layouts will be successful.</span></span>

### <a name="do"></a><span data-ttu-id="9bbb1-133">允许事项</span><span class="sxs-lookup"><span data-stu-id="9bbb1-133">Do</span></span>

- <span data-ttu-id="9bbb1-134">编辑模板以在布局中提供徽标链接（如果要对徽标使用静态链接，而不是结果属性）。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-134">Edit a template to provide the logo link in the layout if you are using static links for logos and not result properties.</span></span>   
- <span data-ttu-id="9bbb1-135">在结果 JSON 中使用的 result 属性未返回任何数据的情况下，验证结果布局。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-135">Validate the result layout for scenarios where no data is returned for a result property used in the result JSON.</span></span> <span data-ttu-id="9bbb1-136">如果`$when`属性不包含数据，则使用条件来隐藏元素。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-136">Use `$when` condition to hide an element if the property doesn't contain data.</span></span>  
- <span data-ttu-id="9bbb1-137">请确保`$when` condition 和 result 属性的数据类型匹配。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-137">Make sure that data types of the `$when` condition and the result property match.</span></span> <span data-ttu-id="9bbb1-138">例如，不能`Number` `Text`在条件中`$when`进行比较。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-138">For example, don't compare `Number` with `Text` in `$when` condition.</span></span>  
- <span data-ttu-id="9bbb1-139">设计结果布局时，请考虑主题要求。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-139">Think of theme requirements when designing a result layout.</span></span>  
- <span data-ttu-id="9bbb1-140">请确保该`Textblock`  元素可以处理动态内容。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-140">Make sure that `Textblock` element can handle dynamic content.</span></span> <span data-ttu-id="9bbb1-141">您可以使用`wrap`和`maxLines`元素属性来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-141">You can use the `wrap` and `maxLines` element properties for this purpose.</span></span> 
- <span data-ttu-id="9bbb1-142">在 markdown 中使用`{DATE()}`时正确设置日期格式。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-142">Properly format the date when using `{DATE()}` in markdown.</span></span>  

### <a name="dont"></a><span data-ttu-id="9bbb1-143">禁止事项</span><span class="sxs-lookup"><span data-stu-id="9bbb1-143">Don't</span></span>

- <span data-ttu-id="9bbb1-144">绑定值时，请勿定义无效的数据类型。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-144">Don't define invalid data types when binding values.</span></span> <span data-ttu-id="9bbb1-145">有关数据类型的详细信息，请参阅[管理搜索架构](https://docs.microsoft.com/sharepoint/search/manage-the-search-schema )。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-145">For more information about the data types, see [Manage the Search schema](https://docs.microsoft.com/sharepoint/search/manage-the-search-schema ).</span></span>
- <span data-ttu-id="9bbb1-146">避免通过遵循结果布局 JSON 的最大高度来裁剪结果页上的结果。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-146">Avoid cropping the result on the result page by following the maximum height of the result layout JSON.</span></span> <span data-ttu-id="9bbb1-147">如果超出结果布局的最大高度，则结果页上的结果将被裁剪。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-147">If you exceed the maximum height of the result layout the result will be cropped on the result page.</span></span>
- <span data-ttu-id="9bbb1-148">不要在`px`元素的属性中使用值。</span><span class="sxs-lookup"><span data-stu-id="9bbb1-148">Don't use `px` values in properties of element.</span></span>


## <a name="resources"></a><span data-ttu-id="9bbb1-149">资源</span><span class="sxs-lookup"><span data-stu-id="9bbb1-149">Resources</span></span>
[<span data-ttu-id="9bbb1-150">自定义搜索结果页面</span><span class="sxs-lookup"><span data-stu-id="9bbb1-150">Customize search result page</span></span>](customize-search-page.md)

[<span data-ttu-id="9bbb1-151">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="9bbb1-151">Adaptive cards</span></span>](https://docs.microsoft.com/adaptive-cards/authoring-cards/getting-started)

[<span data-ttu-id="9bbb1-152">自适应卡片模板语言</span><span class="sxs-lookup"><span data-stu-id="9bbb1-152">Adaptive Cards Template language</span></span>](https://docs.microsoft.com/adaptive-cards/templating/language)

[<span data-ttu-id="9bbb1-153">自适应卡片架构</span><span class="sxs-lookup"><span data-stu-id="9bbb1-153">Adaptive card schema</span></span>](https://adaptivecards.io/explorer/)