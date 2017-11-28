---
title: "관리 되는 응용 프로그램 파일 업로드 UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Common.FileUpload UI 요소를 설명합니다."
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
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="e702e-103">Microsoft.Common.FileUpload UI 요소</span><span class="sxs-lookup"><span data-stu-id="e702e-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="e702e-104">하나 이상의 사용자 toospecify를 허용 하는 컨트롤 tooupload 파일.</span><span class="sxs-lookup"><span data-stu-id="e702e-104">A control that allows a user toospecify one or more files tooupload.</span></span> <span data-ttu-id="e702e-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="e702e-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="e702e-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="e702e-108">스키마</span><span class="sxs-lookup"><span data-stu-id="e702e-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="e702e-109">설명</span><span class="sxs-lookup"><span data-stu-id="e702e-109">Remarks</span></span>
- <span data-ttu-id="e702e-110">`constraints.accept`hello 형식의 hello 브라우저의 파일 대화 상자에 표시 되는 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-110">`constraints.accept` specifies hello types of files that are shown in hello browser's file dialog.</span></span> <span data-ttu-id="e702e-111">Hello 참조 [HTML5 사양](http://www.w3.org/TR/html5/forms.html#attr-input-accept) 에 대 한 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-111">See hello [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="e702e-112">hello 기본값은 **null**합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-112">hello default value is **null**.</span></span>
- <span data-ttu-id="e702e-113">경우 `options.multiple` 너무 설정**true**, hello 사용자가 tooselect 이상의 hello 브라우저의 파일 대화 상자에서 파일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-113">If `options.multiple` is set too**true**, hello user is allowed tooselect more than one file in hello browser's file dialog.</span></span> <span data-ttu-id="e702e-114">hello 기본값은 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-114">hello default value is **false**.</span></span>
- <span data-ttu-id="e702e-115">이 요소에서의 hello 값에 따라 두 가지 모드에서 업로드 파일 지원 `options.uploadMode`합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-115">This element supports uploading files in two modes based on hello value of `options.uploadMode`.</span></span> <span data-ttu-id="e702e-116">경우 **파일** 지정 hello 출력 blob로 hello 파일의 hello 내용을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-116">If **file** is specified, hello output contains hello contents of hello file as a blob.</span></span> <span data-ttu-id="e702e-117">경우 **url** 지정 되지 않으면 hello 파일이 업로드 된 tooa 임시 위치가 고 hello 출력 hello blob의 hello URL을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-117">If **url** is specified, then hello file is uploaded tooa temporary location, and hello output contains hello URL of hello blob.</span></span> <span data-ttu-id="e702e-118">임시 Blob은 24시간 후에 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="e702e-119">hello 기본값은 **파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-119">hello default value is **file**.</span></span>
- <span data-ttu-id="e702e-120">값을 hello `options.openMode` hello 파일을 읽는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-120">hello value of `options.openMode` determines how hello file is read.</span></span> <span data-ttu-id="e702e-121">예상된 toobe 일반 텍스트 hello 파일을 사용 하는 경우 지정 **텍스트**, 그렇지 않으면, 지정 **이진**합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-121">If hello file is expected toobe plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="e702e-122">hello 기본값은 **텍스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-122">hello default value is **text**.</span></span>
- <span data-ttu-id="e702e-123">경우 `options.uploadMode` 너무 설정**파일** 및 `options.openMode` 너무 설정**이진**, hello 출력은 base64 인코딩된 합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-123">If `options.uploadMode` is set too**file** and `options.openMode` is set too**binary**, hello output is base64-encoded.</span></span>
- <span data-ttu-id="e702e-124">`options.encoding`hello 파일을 읽을 때 인코딩 toouse hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-124">`options.encoding` specifies hello encoding toouse when reading hello file.</span></span> <span data-ttu-id="e702e-125">hello 기본값은 **u t F-8**, 사용 되 고 경우에만 `options.openMode` 너무 설정**텍스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-125">hello default value is **UTF-8**, and is used only when `options.openMode` is set too**text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="e702e-126">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="e702e-126">Sample output</span></span>
<span data-ttu-id="e702e-127">Options.multiple가 false이 고 options.uploadMode은 파일을 하는 경우 JSON 문자열로 hello 파일의 내용을 hello 포함 출력:</span><span class="sxs-lookup"><span data-stu-id="e702e-127">If options.multiple is false and options.uploadMode is file, then the output contains hello contents of hello file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="e702e-128">Options.multiple 참인 and'options.uploadMode 파일인 경우 출력 JSON 배열로 hello hello 파일 내용에 포함 된:</span><span class="sxs-lookup"><span data-stu-id="e702e-128">If options.multiple is true and\`options.uploadMode is file, then the output contains hello contents of hello files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="e702e-129">options.multiple이 false이고 options.uploadMode가 url이면 출력에 URL이 JSON 문자열로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="e702e-130">options.multiple이 true이고 options.uploadMode가 url이면 출력에 URL 목록이 JSON 배열로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="e702e-131">CreateUiDefinition을 테스트할 때 일부 브라우저 (예: Google Chrome) hello 브라우저 콘솔에서 hello Microsoft.Common.FileUpload 요소에 의해 생성 된 Url을 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by hello Microsoft.Common.FileUpload element in hello browser console.</span></span> <span data-ttu-id="e702e-132">Tooright 클릭 개별 링크 toocopy hello 전체 Url을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-132">You may need tooright-click individual links toocopy hello full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e702e-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e702e-133">Next steps</span></span>
* <span data-ttu-id="e702e-134">소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-134">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="e702e-135">소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e702e-135">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="e702e-136">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e702e-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
