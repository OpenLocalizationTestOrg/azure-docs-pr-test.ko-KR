---
title: "Azure Managed Application PublicIpAddressCombo UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Network.PublicIpAddressCombo UI 요소에 대해 설명합니다."
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
ms.openlocfilehash: 2eb773f5f0cf389fc39bc3a0f5fbf9ac726d1949
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="e54a2-103">Microsoft.Network.PublicIpAddressCombo UI 요소</span><span class="sxs-lookup"><span data-stu-id="e54a2-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="e54a2-104">새 또는 기존 공용 IP 주소를 선택하는 컨트롤 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="e54a2-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="e54a2-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="e54a2-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="e54a2-108">사용자가 공용 IP 주소에 대해 '없음'을 선택하면 도메인 이름 레이블 텍스트 상자가 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-108">If the user selects 'None' for public IP address, the domain name label text box is hidden.</span></span>
- <span data-ttu-id="e54a2-109">사용자가 기존 공용 IP 주소를 선택하면 도메인 이름 레이블 텍스트 상자가 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-109">If the user selects an existing public IP address, the domain name label text box is disabled.</span></span> <span data-ttu-id="e54a2-110">이 값은 선택한 IP 주소의 도메인 이름 레이블입니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-110">Its value is the domain name label of the selected IP address.</span></span>
- <span data-ttu-id="e54a2-111">도메인 이름 접미사(예: westus.cloudapp.azure.com)는 선택한 위치에 따라 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-111">The domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on the selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="e54a2-112">스키마</span><span class="sxs-lookup"><span data-stu-id="e54a2-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="e54a2-113">설명</span><span class="sxs-lookup"><span data-stu-id="e54a2-113">Remarks</span></span>
- <span data-ttu-id="e54a2-114">`constraints.required.domainNameLabel`을 **true**로 설정하면 사용자가 새 공용 IP 주소를 만들 때 도메인 이름 레이블을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-114">If `constraints.required.domainNameLabel` is set to **true**, the user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="e54a2-115">레이블이 없는 기존의 공용 IP 주소는 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="e54a2-116">`options.hideNone`을 **true**로 설정하면 공용 IP 주소에 대해 **없음**을 선택하는 옵션이 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-116">If `options.hideNone` is set to **true**, then the option to select **None** for the public IP address is hidden.</span></span> <span data-ttu-id="e54a2-117">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-117">The default value is **false**.</span></span>
- <span data-ttu-id="e54a2-118">`options.hideDomainNameLabel`이 **true**로 설정하면 도메인 이름 레이블의 텍스트 상자가 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-118">If `options.hideDomainNameLabel` is set to **true**, then the text box for domain name label is hidden.</span></span> <span data-ttu-id="e54a2-119">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-119">The default value is **false**.</span></span>
- <span data-ttu-id="e54a2-120">`options.hideExisting`이 true이면 사용자가 기존 공용 IP 주소를 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-120">If `options.hideExisting` is true, then the user is not able to choose an existing public IP address.</span></span> <span data-ttu-id="e54a2-121">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-121">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="e54a2-122">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="e54a2-122">Sample output</span></span>
<span data-ttu-id="e54a2-123">사용자가 공용 IP 주소를 선택하지 않는 경우 예상되는 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-123">If the user selects no public IP address, the following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="e54a2-124">사용자가 새 또는 기존 IP 주소를 선택하는 경우 예상되는 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-124">If the user selects a new or existing IP address, the following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="e54a2-125">`options.hideNone`을 지정하면 `newOrExistingOrNone`은 항상 **none**을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="e54a2-126">`options.hideDomainNameLabel`을 지정하면 `domainNameLabel`이 선언되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e54a2-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e54a2-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e54a2-127">Next steps</span></span>
* <span data-ttu-id="e54a2-128">관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e54a2-128">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="e54a2-129">UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e54a2-129">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="e54a2-130">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e54a2-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
