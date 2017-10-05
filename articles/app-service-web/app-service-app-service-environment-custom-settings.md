---
title: "앱 서비스 환경에 대한 사용자 지정 설정"
description: "앱 서비스 환경에 대한 사용자 지정 구성 설정"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 687475fae0c90713c15e8abbb92b71059eae81c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="9f54f-103">앱 서비스 환경에 대한 사용자 지정 구성 설정</span><span class="sxs-lookup"><span data-stu-id="9f54f-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="9f54f-104">개요</span><span class="sxs-lookup"><span data-stu-id="9f54f-104">Overview</span></span>
<span data-ttu-id="9f54f-105">앱 서비스 환경은 단일 고객에게 격리되므로 앱 서비스 환경에만 적용할 수 있는 특정 구성 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-105">Because App Service Environments are isolated to a single customer, there are certain configuration settings that can be applied exclusively to App Service Environments.</span></span> <span data-ttu-id="9f54f-106">이 문서에서는 앱 서비스 환경에 사용 가능한 다양한 앱 서비스 환경 관련 사용자 지정 항목을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-106">This article documents the various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="9f54f-107">앱 서비스 환경이 없는 경우 [앱 서비스 환경을 만드는 방법](app-service-web-how-to-create-an-app-service-environment.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f54f-107">If you do not have an App Service Environment, see [How to Create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="9f54f-108">새 **clusterSettings** 특성의 배열을 사용하여 앱 서비스 환경 사용자 지정을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-108">You can store App Service Environment customizations by using an array in the new **clusterSettings** attribute.</span></span> <span data-ttu-id="9f54f-109">이 특성은 *hostingEnvironments* Azure Resource Manager 엔터티의 "속성" 사전에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-109">This attribute is found in the "Properties" dictionary of the *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="9f54f-110">다음 약식 리소스 관리자 템플릿 코드 조각에는 **clusterSettings** 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-110">The following abbreviated Resource Manager template snippet shows the **clusterSettings** attribute:</span></span>

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

<span data-ttu-id="9f54f-111">**clusterSettings** 특성을 리소스 관리자 템플릿에 포함하여 앱 서비스 환경을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-111">The **clusterSettings** attribute can be included in a Resource Manager template to update the App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-to-update-an-app-service-environment"></a><span data-ttu-id="9f54f-112">Azure 리소스 탐색기를 사용하여 앱 서비스 환경 업데이트</span><span class="sxs-lookup"><span data-stu-id="9f54f-112">Use Azure Resource Explorer to update an App Service Environment</span></span>
<span data-ttu-id="9f54f-113">또는 [Azure 리소스 탐색기](https://resources.azure.com)를 사용하여 앱 서비스 환경을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-113">Alternatively, you can update the App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="9f54f-114">리소스 탐색기에서 App Service Environment 노드(**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-114">In Resource Explorer, go to the node for the App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="9f54f-115">그런 다음 업데이트하려는 특정 앱 서비스 환경을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-115">Then click the specific App Service Environment that you want to update.</span></span>
2. <span data-ttu-id="9f54f-116">오른쪽 창의 위쪽 도구 모음에서 **읽기/쓰기** 를 클릭하여 리소스 탐색기에서 대화형 편집을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-116">In the right pane, click **Read/Write** in the upper toolbar to allow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="9f54f-117">파란색 **편집** 단추를 클릭하여 리소스 관리자 템플릿을 편집 가능하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-117">Click the blue **Edit** button to make the Resource Manager template editable.</span></span>
4. <span data-ttu-id="9f54f-118">오른쪽 창의 아래쪽으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-118">Scroll to the bottom of the right pane.</span></span> <span data-ttu-id="9f54f-119">**clusterSettings** 특성은 거의 맨 아래쪽에 있습니다. 여기에서 해당 값을 입력하거나 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-119">The **clusterSettings** attribute is at the very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="9f54f-120">**clusterSettings** 특성에서 원하는 구성 값 배열을 입력하거나 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-120">Type (or copy and paste) the array of configuration values you want in the **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="9f54f-121">오른쪽 창의 위쪽에 있는 녹색 **PUT** 단추를 클릭하여 앱 서비스 환경에 대한 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-121">Click the green **PUT** button that's located at the top of the right pane to commit the change to the App Service Environment.</span></span>

<span data-ttu-id="9f54f-122">변경 내용을 제출한 후 변경 내용이 적용되려면 앱 서비스 환경의 프런트 엔드 수에 약 30 분을 곱한 만큼의 시간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-122">However you submit the change, it takes roughly 30 minutes multiplied by the number of front ends in the App Service Environment for the change to take effect.</span></span>
<span data-ttu-id="9f54f-123">예를 들어 앱 서비스 환경에 4개의 프런트 엔드가 있는 경우 구성 업데이트를 완료하는 데 약 2시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for the configuration update to finish.</span></span> <span data-ttu-id="9f54f-124">구성 변경이 롤아웃되는 동안 앱 서비스 환경에서 다른 크기 조정 작업 또는 구성 변경 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-124">While the configuration change is being rolled out, no other scaling operations or configuration change operations can take place in the App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="9f54f-125">TLS 1.0 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="9f54f-125">Disable TLS 1.0</span></span>
<span data-ttu-id="9f54f-126">고객, 특히 PCI 규정 준수 감사를 다루는 고객으로부터의 되풀이되는 질문은 자신의 앱에 TLS 1.0을 명시적으로 사용하지 않도록 설정하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how to explicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="9f54f-127">다음 **clusterSettings** 항목을 통해 TLS 1.0을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-127">TLS 1.0 can be disabled through the following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="9f54f-128">TLS 암호화 그룹 순서 변경</span><span class="sxs-lookup"><span data-stu-id="9f54f-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="9f54f-129">고객의 또 다른 질문은 고객이 자신의 서버와 협의한 암호화 목록을 수정할 수 있는지에 대한 것으로 아래 표시된 것처럼 **clusterSettings** 를 수정하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-129">Another question from customers is if they can modify the list of ciphers negotiated by their server and this can be achieved by modifying the **clusterSettings** as shown below.</span></span> <span data-ttu-id="9f54f-130">사용 가능한 암호화 그룹 목록은 [이 MSDN 문서](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx)에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-130">The list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="9f54f-131">암호화 그룹에 대해 SChannel에서 이해할 수 없는 잘못된 값이 설정된 경우 서버에 대한 모든 TLS 통신의 작동이 중지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-131">If incorrect values are set for the cipher suite that SChannel cannot understand, all TLS communication to your server might stop functioning.</span></span> <span data-ttu-id="9f54f-132">이러한 경우 *clusterSettings* 에서 **FrontEndSSLCipherSuiteOrder** 항목을 제거하고 업데이트된 Resource Manager 템플릿을 제출하여 기본 암호화 제품군 설정으로 되돌려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-132">In such a case, you will need to remove the *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit the updated Resource Manager template to revert back to the default cipher suite settings.</span></span>  <span data-ttu-id="9f54f-133">이 기능을 주의하여 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9f54f-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="9f54f-134">시작</span><span class="sxs-lookup"><span data-stu-id="9f54f-134">Get started</span></span>
<span data-ttu-id="9f54f-135">Azure 빠른 시작 Resource Manager 템플릿 사이트에는 [앱 서비스 환경 만들기](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/)에 대한 기본 정의에 템플릿이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f54f-135">The Azure Quickstart Resource Manager template site includes a template with the base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
