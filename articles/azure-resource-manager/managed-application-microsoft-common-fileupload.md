---
title: "Azure Managed Application FileUpload UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Common.FileUpload UI 요소에 대해 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 217e9e63eb7cd198f70cee42b418867df9f1f993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="7b978-103">Microsoft.Common.FileUpload UI 요소</span><span class="sxs-lookup"><span data-stu-id="7b978-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="7b978-104">사용자가 업로드할 파일을 하나 이상 지정할 수 있게 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-104">A control that allows a user to specify one or more files to upload.</span></span> <span data-ttu-id="7b978-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="7b978-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="7b978-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="7b978-108">스키마</span><span class="sxs-lookup"><span data-stu-id="7b978-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="7b978-109">설명</span><span class="sxs-lookup"><span data-stu-id="7b978-109">Remarks</span></span>
- <span data-ttu-id="7b978-110">`constraints.accept`는 브라우저의 파일 대화 상자에 표시되는 파일 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-110">`constraints.accept` specifies the types of files that are shown in the browser's file dialog.</span></span> <span data-ttu-id="7b978-111">허용되는 값은 [HTML5 사양](http://www.w3.org/TR/html5/forms.html#attr-input-accept)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b978-111">See the [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="7b978-112">기본값은 **null**입니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-112">The default value is **null**.</span></span>
- <span data-ttu-id="7b978-113">`options.multiple`이 **true**로 설정되면 사용자가 브라우저의 파일 대화 상자에서 둘 이상의 파일을 선택할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-113">If `options.multiple` is set to **true**, the user is allowed to select more than one file in the browser's file dialog.</span></span> <span data-ttu-id="7b978-114">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-114">The default value is **false**.</span></span>
- <span data-ttu-id="7b978-115">이 요소는 `options.uploadMode` 값에 따라 두 가지 모드로 파일 업로드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-115">This element supports uploading files in two modes based on the value of `options.uploadMode`.</span></span> <span data-ttu-id="7b978-116">**file**을 지정하면 출력에 파일의 내용이 Blob으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-116">If **file** is specified, the output contains the contents of the file as a blob.</span></span> <span data-ttu-id="7b978-117">**url**을 지정하면 파일은 임시 위치에 업로드되고 출력에 Blob의 URL이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-117">If **url** is specified, then the file is uploaded to a temporary location, and the output contains the URL of the blob.</span></span> <span data-ttu-id="7b978-118">임시 Blob은 24시간 후에 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="7b978-119">기본값은 **file**입니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-119">The default value is **file**.</span></span>
- <span data-ttu-id="7b978-120">`options.openMode` 값은 파일을 읽는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-120">The value of `options.openMode` determines how the file is read.</span></span> <span data-ttu-id="7b978-121">파일이 일반 텍스트여야 하면 **text**를 지정합니다. 그렇지 않으면 **binary**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-121">If the file is expected to be plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="7b978-122">기본값은 **text**입니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-122">The default value is **text**.</span></span>
- <span data-ttu-id="7b978-123">`options.uploadMode`를 **file**로 설정하고 `options.openMode`를 **binary**로 설정하면 출력이 base64로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-123">If `options.uploadMode` is set to **file** and `options.openMode` is set to **binary**, the output is base64-encoded.</span></span>
- <span data-ttu-id="7b978-124">`options.encoding`은 파일을 읽을 때 사용할 인코딩을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-124">`options.encoding` specifies the encoding to use when reading the file.</span></span> <span data-ttu-id="7b978-125">기본값은 **UTF-8**이며, `options.openMode`를 **text**로 설정한 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-125">The default value is **UTF-8**, and is used only when `options.openMode` is set to **text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="7b978-126">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="7b978-126">Sample output</span></span>
<span data-ttu-id="7b978-127">options.multiple이 false이고 options.uploadMode가 file이면 출력에 파일의 내용이 JSON 문자열로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-127">If options.multiple is false and options.uploadMode is file, then the output contains the contents of the file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="7b978-128">options.multiple이 true이고 options.uploadMode가 file이면 출력에 파일의 내용이 JSON 배열로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-128">If options.multiple is true and\`options.uploadMode is file, then the output contains the contents of the files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="7b978-129">options.multiple이 false이고 options.uploadMode가 url이면 출력에 URL이 JSON 문자열로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="7b978-130">options.multiple이 true이고 options.uploadMode가 url이면 출력에 URL 목록이 JSON 배열로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="7b978-131">CreateUiDefinition을 테스트할 때 일부 브라우저(예: Chrome)에서는 브라우저 콘솔의 Microsoft.Common.FileUpload 요소로 생성된 URL을 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by the Microsoft.Common.FileUpload element in the browser console.</span></span> <span data-ttu-id="7b978-132">개별 링크를 마우스 오른쪽 단추로 클릭하여 전체 URL을 복사해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b978-132">You may need to right-click individual links to copy the full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7b978-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b978-133">Next steps</span></span>
* <span data-ttu-id="7b978-134">관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b978-134">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="7b978-135">UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b978-135">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="7b978-136">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b978-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
