---
title: "Azure 저장소에 안전 하 게 전송 aaaRequire | Microsoft Docs"
description: "Azure 저장소에 대 한 hello \"보안 전송 필요\" 기능에 대 한 자세한 내용은 방법과 tooenable 것입니다."
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
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="1c983-103">보안 전송 필요</span><span class="sxs-lookup"><span data-stu-id="1c983-103">Require secure transfer</span></span>

<span data-ttu-id="1c983-104">hello "보안 전송 필요" 옵션만 toohello 저장소 계정에서 보안 연결 요청을 허용 하 여 저장소 계정의 hello 보안이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-104">hello "Secure transfer required" option enhances hello security of your storage account by only allowing requests toohello storage account from secure connections.</span></span> <span data-ttu-id="1c983-105">예를 들어, REST Api tooaccess 저장소 계정의 호출할 때 HTTPS를 사용 하 여 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-105">For example, when calling REST APIs tooaccess your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="1c983-106">"보안 전송 필요"가 설정된 경우 HTTP를 사용한 모든 요청이 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="1c983-107">Hello Azure 파일 서비스를 사용 하는 암호화 되지 않은 모든 연결 실패 "보안 전송 필요"를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-107">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="1c983-108">SMB 2.1, SMB 3.0 암호화 없이 및 일부 버전의 Linux SMB 클라이언트 hello 사용 하는 시나리오를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span> 

<span data-ttu-id="1c983-109">기본적으로 hello "보안 전송 필요" 옵션이 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-109">By default, hello "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="1c983-110">Azure Storage에서 사용자 지정 도메인 이름에 대해 HTTPS를 지원하지 않으므로 사용자 지정 도메인 이름을 사용할 때 이 옵션이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a><span data-ttu-id="1c983-111">"보안 전송 필요" hello Azure 포털에서에서 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="1c983-111">Enable "Secure transfer required" in hello Azure portal</span></span>

<span data-ttu-id="1c983-112">Hello "보안 전송 필요" hello에서 저장소 계정을 만들 때 모두 설정 되지 않는 것이 가능 [Azure 포털](https://portal.azure.com), 및 기존 저장소 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-112">You can enable hello "Secure transfer required" setting both when you create a storage account in hello [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="1c983-113">저장소 계정을 만들 때 보안 전송 필요</span><span class="sxs-lookup"><span data-stu-id="1c983-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="1c983-114">열기 hello **저장소 계정 만들기** 블레이드 hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="1c983-114">Open hello **Create storage account** blade in hello Azure portal.</span></span>
1. <span data-ttu-id="1c983-115">**보안 전송 필요** 아래에서 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![스크린샷](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="1c983-117">기존 저장소 계정에 대해 보안 전송 필요</span><span class="sxs-lookup"><span data-stu-id="1c983-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="1c983-118">Hello Azure 포털에서에서 기존 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-118">Select an existing storage account in hello Azure portal.</span></span>
1. <span data-ttu-id="1c983-119">선택 **구성** 아래 **설정을** hello 저장소 계정 메뉴 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-119">Select **Configuration** under **SETTINGS** in hello storage account menu blade.</span></span>
1. <span data-ttu-id="1c983-120">**보안 전송 필요** 아래에서 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![스크린샷](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="1c983-122">프로그래밍 방식으로 "보안 전송 필요" 사용</span><span class="sxs-lookup"><span data-stu-id="1c983-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="1c983-123">hello 설정 이름은 _supportsHttpsTrafficOnly_ 저장소 계정 속성에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-123">hello setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="1c983-124">REST API, 도구 또는 라이브러리를 사용하여 "보안 전송 필요" 설정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="1c983-125">**REST API**(버전: 2016-12-01): [릴리스 패키지](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="1c983-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="1c983-126">**PowerShell**(버전: 4.1.0): [릴리스 패키지](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="1c983-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="1c983-127">**CLI**(버전: 2.0.11): [릴리스 패키지](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="1c983-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="1c983-128">**NodeJS**(버전: 1.1.0): [릴리스 패키지](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="1c983-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="1c983-129">**.NET SDK**(버전: 6.3.0): [릴리스 패키지](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="1c983-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="1c983-130">**Python SDK**(버전: 1.1.0): [릴리스 패키지](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="1c983-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="1c983-131">**Ruby SDK**(버전: 0.11.0): [릴리스 패키지](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="1c983-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="1c983-132">REST API를 사용하여 "보안 전송 필요" 설정 사용</span><span class="sxs-lookup"><span data-stu-id="1c983-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="1c983-133">REST API를 사용 하 여 테스트 toosimplify 사용할 수 있습니다 [ArmClient](https://github.com/projectkudu/ARMClient) toocall 명령줄에서.</span><span class="sxs-lookup"><span data-stu-id="1c983-133">toosimplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) toocall from command line.</span></span>

 <span data-ttu-id="1c983-134">아래 명령줄 hello REST API를 사용 하는 toocheck hello 설정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-134">You can use below command line toocheck hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="1c983-135">Hello에 대 한 응답을 찾을 수 있습니다 _supportsHttpsTrafficOnly_ 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-135">In hello response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="1c983-136">샘플:</span><span class="sxs-lookup"><span data-stu-id="1c983-136">Sample:</span></span>

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

<span data-ttu-id="1c983-137">아래 명령줄 hello REST API를 사용 하는 tooenable hello 설정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-137">You can use below command line tooenable hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="1c983-138">Input.json의 샘플:</span><span class="sxs-lookup"><span data-stu-id="1c983-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="1c983-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1c983-139">Next steps</span></span>
<span data-ttu-id="1c983-140">Azure 저장소는 다양 한 개발자를 함께 사용 하는 보안 기능을 toobuild 보안 응용 프로그램을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="1c983-141">자세한 내용은 방문 hello [저장소 보안 가이드](storage-security-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1c983-141">For more details, visit hello [Storage Security Guide](storage-security-guide.md).</span></span>
