---
title: "Azure Storage에서 보안 전송 필요 | Microsoft Docs"
description: "Azure Storage에 대한 \"보안 전송 필요\" 기능과 이 기능을 사용하도록 설정하는 방법에 대해 알아봅니다."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: bc5b7fc79869c632db96958f17aaf953a5fd3b19
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="68fe2-103">보안 전송 필요</span><span class="sxs-lookup"><span data-stu-id="68fe2-103">Require secure transfer</span></span>

<span data-ttu-id="68fe2-104">"보안 전송 필요" 옵션으로 안전한 연결에서 저장소 계정으로만 요청을 허용하여 저장소 계정의 보안을 강화합니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-104">The "Secure transfer required" option enhances the security of your storage account by only allowing requests to the storage account from secure connections.</span></span> <span data-ttu-id="68fe2-105">예를 들어 저장소 계정에 액세스하는 데 REST API를 호출하는 경우 HTTPS를 사용하여 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-105">For example, when calling REST APIs to access your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="68fe2-106">"보안 전송 필요"가 설정된 경우 HTTP를 사용한 모든 요청이 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="68fe2-107">Azure 파일 서비스를 사용하는 경우 "보안 전송 필요"가 설정된 경우 암호화되지 않은 모든 연결이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-107">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="68fe2-108">여기에는 암호화되지 않은 SMB 2.1, SMB 3.0을 사용하는 시나리오와 Linux SMB 클라이언트의 일부 유형이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span> 

<span data-ttu-id="68fe2-109">기본적으로 "보안 전송 필요" 옵션은 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-109">By default, the "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="68fe2-110">Azure Storage에서 사용자 지정 도메인 이름에 대해 HTTPS를 지원하지 않으므로 사용자 지정 도메인 이름을 사용할 때 이 옵션이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a><span data-ttu-id="68fe2-111">Azure Portal에서 "보안 전송 필요"를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="68fe2-111">Enable "Secure transfer required" in the Azure portal</span></span>

<span data-ttu-id="68fe2-112">[Azure Portal](https://portal.azure.com)에서 저장소 계정을 만들 경우 및 기존 저장소 계정 모두에 "보안 전송 필요" 설정을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-112">You can enable the "Secure transfer required" setting both when you create a storage account in the [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="68fe2-113">저장소 계정을 만들 때 보안 전송 필요</span><span class="sxs-lookup"><span data-stu-id="68fe2-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="68fe2-114">Azure Portal에서 **저장소 계정 만들기** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-114">Open the **Create storage account** blade in the Azure portal.</span></span>
1. <span data-ttu-id="68fe2-115">**보안 전송 필요** 아래에서 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![스크린샷](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="68fe2-117">기존 저장소 계정에 대해 보안 전송 필요</span><span class="sxs-lookup"><span data-stu-id="68fe2-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="68fe2-118">Azure Portal에서 기존 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-118">Select an existing storage account in the Azure portal.</span></span>
1. <span data-ttu-id="68fe2-119">저장소 계정 메뉴 블레이드의 **설정** 아래에서 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-119">Select **Configuration** under **SETTINGS** in the storage account menu blade.</span></span>
1. <span data-ttu-id="68fe2-120">**보안 전송 필요** 아래에서 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![스크린샷](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="68fe2-122">프로그래밍 방식으로 "보안 전송 필요" 사용</span><span class="sxs-lookup"><span data-stu-id="68fe2-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="68fe2-123">설정 이름은 저장소 계정 속성에서 _supportsHttpsTrafficOnly_입니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-123">The setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="68fe2-124">REST API, 도구 또는 라이브러리를 사용하여 "보안 전송 필요" 설정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="68fe2-125">**REST API**(버전: 2016-12-01): [릴리스 패키지](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="68fe2-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="68fe2-126">**PowerShell**(버전: 4.1.0): [릴리스 패키지](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="68fe2-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="68fe2-127">**CLI**(버전: 2.0.11): [릴리스 패키지](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="68fe2-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="68fe2-128">**NodeJS**(버전: 1.1.0): [릴리스 패키지](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="68fe2-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="68fe2-129">**.NET SDK**(버전: 6.3.0): [릴리스 패키지](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="68fe2-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="68fe2-130">**Python SDK**(버전: 1.1.0): [릴리스 패키지](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="68fe2-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="68fe2-131">**Ruby SDK**(버전: 0.11.0): [릴리스 패키지](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="68fe2-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="68fe2-132">REST API를 사용하여 "보안 전송 필요" 설정 사용</span><span class="sxs-lookup"><span data-stu-id="68fe2-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="68fe2-133">REST API를 사용하여 테스트를 단순화하기 위해 [ArmClient](https://github.com/projectkudu/ARMClient)를 사용하여 명령줄에서 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-133">To simplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) to call from command line.</span></span>

 <span data-ttu-id="68fe2-134">아래 명령줄을 사용하여 REST API로 설정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-134">You can use below command line to check the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="68fe2-135">응답에서 _supportsHttpsTrafficOnly_ 설정을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-135">In the response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="68fe2-136">샘플:</span><span class="sxs-lookup"><span data-stu-id="68fe2-136">Sample:</span></span>

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

<span data-ttu-id="68fe2-137">아래 명령줄을 사용하여 REST API로 설정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-137">You can use below command line to enable the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="68fe2-138">Input.json의 샘플:</span><span class="sxs-lookup"><span data-stu-id="68fe2-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="68fe2-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68fe2-139">Next steps</span></span>
<span data-ttu-id="68fe2-140">Azure Storage는 여러 개발자가 보안 응용 프로그램을 함께 빌드할 수 있도록 하는 포괄적인 보안 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="68fe2-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers to build secure applications.</span></span> <span data-ttu-id="68fe2-141">자세한 내용은 [저장소 보안 가이드](storage-security-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68fe2-141">For more details, visit the [Storage Security Guide](storage-security-guide.md).</span></span>
