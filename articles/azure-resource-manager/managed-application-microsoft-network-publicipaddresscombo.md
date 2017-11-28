---
title: "관리 되는 응용 프로그램 PublicIpAddressCombo UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Network.PublicIpAddressCombo UI 요소를 설명합니다."
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="82486-103">Microsoft.Network.PublicIpAddressCombo UI 요소</span><span class="sxs-lookup"><span data-stu-id="82486-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="82486-104">새 또는 기존 공용 IP 주소를 선택하는 컨트롤 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="82486-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="82486-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="82486-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="82486-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="82486-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="82486-108">Hello 사용자가 공용 IP 주소에 대 한 ' 없음'를 선택 하는 경우 hello 도메인 이름 레이블 입력란은 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="82486-108">If hello user selects 'None' for public IP address, hello domain name label text box is hidden.</span></span>
- <span data-ttu-id="82486-109">Hello 사용자가 기존 공용 IP 주소를 선택 하는 경우 hello 도메인 이름 레이블 텍스트 상자가 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82486-109">If hello user selects an existing public IP address, hello domain name label text box is disabled.</span></span> <span data-ttu-id="82486-110">해당 값은 hello 도메인 이름 레이블이 hello 선택한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="82486-110">Its value is hello domain name label of hello selected IP address.</span></span>
- <span data-ttu-id="82486-111">hello hello 선택한 위치에 따라 자동으로 도메인 이름 접미사 (예를 들어 westus.cloudapp.azure.com) 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="82486-111">hello domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on hello selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="82486-112">스키마</span><span class="sxs-lookup"><span data-stu-id="82486-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="82486-113">설명</span><span class="sxs-lookup"><span data-stu-id="82486-113">Remarks</span></span>
- <span data-ttu-id="82486-114">경우 `constraints.required.domainNameLabel` 너무 설정**true**, hello 사용자가 새 공용 IP 주소를 만들 때 도메인 이름 레이블을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82486-114">If `constraints.required.domainNameLabel` is set too**true**, hello user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="82486-115">레이블이 없는 기존의 공용 IP 주소는 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="82486-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="82486-116">경우 `options.hideNone` 너무 설정**true**, 다음 옵션 tooselect hello **None** hello 공용 IP 주소는 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="82486-116">If `options.hideNone` is set too**true**, then hello option tooselect **None** for hello public IP address is hidden.</span></span> <span data-ttu-id="82486-117">hello 기본값은 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="82486-117">hello default value is **false**.</span></span>
- <span data-ttu-id="82486-118">경우 `options.hideDomainNameLabel` 너무 설정 되어**true**, 다음 hello 텍스트 상자에 도메인 이름 레이블이 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="82486-118">If `options.hideDomainNameLabel` is set too**true**, then hello text box for domain name label is hidden.</span></span> <span data-ttu-id="82486-119">hello 기본값은 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="82486-119">hello default value is **false**.</span></span>
- <span data-ttu-id="82486-120">경우 `options.hideExisting` 가 true 이면 hello 사용자가 기존 공용 IP 주소 수 toochoose가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="82486-120">If `options.hideExisting` is true, then hello user is not able toochoose an existing public IP address.</span></span> <span data-ttu-id="82486-121">hello 기본값은 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="82486-121">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="82486-122">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="82486-122">Sample output</span></span>
<span data-ttu-id="82486-123">Hello 사용자가 공용 IP 주소를 선택 하는 경우 hello 다음 예상 출력은:</span><span class="sxs-lookup"><span data-stu-id="82486-123">If hello user selects no public IP address, hello following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="82486-124">Hello 사용자가 기존 또는 새 IP 주소를 선택 하는 경우 hello 다음 예상 출력은:</span><span class="sxs-lookup"><span data-stu-id="82486-124">If hello user selects a new or existing IP address, hello following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="82486-125">`options.hideNone`을 지정하면 `newOrExistingOrNone`은 항상 **none**을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="82486-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="82486-126">`options.hideDomainNameLabel`을 지정하면 `domainNameLabel`이 선언되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82486-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82486-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="82486-127">Next steps</span></span>
* <span data-ttu-id="82486-128">소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82486-128">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="82486-129">소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82486-129">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="82486-130">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82486-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
