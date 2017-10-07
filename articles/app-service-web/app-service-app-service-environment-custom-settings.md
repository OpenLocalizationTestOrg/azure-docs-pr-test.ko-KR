---
title: "앱 서비스 환경에 대 한 aaaCustom 설정"
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
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="bbeb5-103">앱 서비스 환경에 대한 사용자 지정 구성 설정</span><span class="sxs-lookup"><span data-stu-id="bbeb5-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="bbeb5-104">개요</span><span class="sxs-lookup"><span data-stu-id="bbeb5-104">Overview</span></span>
<span data-ttu-id="bbeb5-105">없기 때문에 앱 서비스 환경 격리 tooa 단일 고객 인 특정 일 수 있는 구성 설정이 적용 독점적으로 tooApp 서비스 환경.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-105">Because App Service Environments are isolated tooa single customer, there are certain configuration settings that can be applied exclusively tooApp Service Environments.</span></span> <span data-ttu-id="bbeb5-106">이 문서 hello 앱 서비스 환경에 사용할 수 있는 다양 한 특정 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-106">This article documents hello various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="bbeb5-107">앱 서비스 환경이 참조 [어떻게 tooCreate 앱 서비스 환경](app-service-web-how-to-create-an-app-service-environment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-107">If you do not have an App Service Environment, see [How tooCreate an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="bbeb5-108">Hello에 새 배열을 사용 하 여 앱 서비스 환경 사용자 지정을 저장할 수 있습니다 **clusterSettings** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-108">You can store App Service Environment customizations by using an array in hello new **clusterSettings** attribute.</span></span> <span data-ttu-id="bbeb5-109">이 특성이 hello hello "속성" 사전에 있으면 *hostingEnvironments* Azure 리소스 관리자 엔터티.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-109">This attribute is found in hello "Properties" dictionary of hello *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="bbeb5-110">hello 다음 축약형된 리소스 관리자 템플릿 코드 조각 표시 hello **clusterSettings** 특성:</span><span class="sxs-lookup"><span data-stu-id="bbeb5-110">hello following abbreviated Resource Manager template snippet shows hello **clusterSettings** attribute:</span></span>

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

<span data-ttu-id="bbeb5-111">hello **clusterSettings** 리소스 관리자 템플릿 tooupdate hello 앱 서비스 환경에에서 특성을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-111">hello **clusterSettings** attribute can be included in a Resource Manager template tooupdate hello App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a><span data-ttu-id="bbeb5-112">Azure 리소스 탐색기 tooupdate 앱 서비스 환경 사용</span><span class="sxs-lookup"><span data-stu-id="bbeb5-112">Use Azure Resource Explorer tooupdate an App Service Environment</span></span>
<span data-ttu-id="bbeb5-113">앱 서비스 환경 hello를 사용 하 여 업데이트할 수 있습니다 또는 [Azure 리소스 탐색기](https://resources.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-113">Alternatively, you can update hello App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="bbeb5-114">리소스 탐색기에서 hello 앱 서비스 환경에 대 한 toohello 노드를 이동 (**구독** > **resourceGroups** > **공급자**  >  **Microsoft.Web** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="bbeb5-114">In Resource Explorer, go toohello node for hello App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="bbeb5-115">클릭 한 다음 원하는 tooupdate 특정 앱 서비스 환경 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-115">Then click hello specific App Service Environment that you want tooupdate.</span></span>
2. <span data-ttu-id="bbeb5-116">Hello 오른쪽 창에서 클릭 **읽기/쓰기** 에 hello 위쪽 도구 모음 tooallow 대화형 리소스 탐색기에서 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-116">In hello right pane, click **Read/Write** in hello upper toolbar tooallow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="bbeb5-117">파란색 hello 클릭 **편집** 단추 toomake hello 리소스 관리자 템플릿을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-117">Click hello blue **Edit** button toomake hello Resource Manager template editable.</span></span>
4. <span data-ttu-id="bbeb5-118">Hello 오른쪽 창의 맨을 toohello 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-118">Scroll toohello bottom of hello right pane.</span></span> <span data-ttu-id="bbeb5-119">hello **clusterSettings** 특성은 hello 매우 맨 아래에 입력 하거나 해당 값을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-119">hello **clusterSettings** attribute is at hello very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="bbeb5-120">Hello에 원하는 구성 값의 형식 (또는 복사 및 붙여넣기) hello 배열 **clusterSettings** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-120">Type (or copy and paste) hello array of configuration values you want in hello **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="bbeb5-121">녹색 hello 클릭 **배치** 단추의 hello 위쪽 hello 오른쪽 창 toocommit hello 변경 toohello 앱 서비스 환경에 찾았으며 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-121">Click hello green **PUT** button that's located at hello top of hello right pane toocommit hello change toohello App Service Environment.</span></span>

<span data-ttu-id="bbeb5-122">Hello 변경을 제출 하면 되지만 약 30 분 프런트 엔드 tootake 효과 변경 하는 hello에 대 한 앱 서비스 환경 hello에 hello 수를 곱한 걸리는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-122">However you submit hello change, it takes roughly 30 minutes multiplied by hello number of front ends in hello App Service Environment for hello change tootake effect.</span></span>
<span data-ttu-id="bbeb5-123">예를 들어, 앱 서비스 환경에 있는 4 개의 프런트 엔드 경우 대략 2 시간 hello 구성 업데이트 toofinish 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for hello configuration update toofinish.</span></span> <span data-ttu-id="bbeb5-124">Hello 구성 변경 롤아웃하는, 다른 크기 조정 작업 또는 구성 변경 작업 hello 앱 서비스 환경에서 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-124">While hello configuration change is being rolled out, no other scaling operations or configuration change operations can take place in hello App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="bbeb5-125">TLS 1.0 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="bbeb5-125">Disable TLS 1.0</span></span>
<span data-ttu-id="bbeb5-126">고객의 질문을 되풀이 특히 고객에 게 PCI 준수 처리 하는 감사를 tooexplicitly가 앱에 대 한 TLS 1.0을 해제 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how tooexplicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="bbeb5-127">Hello 다음을 통해 사용 하지 않도록 설정 TLS 1.0 **clusterSettings** 항목:</span><span class="sxs-lookup"><span data-stu-id="bbeb5-127">TLS 1.0 can be disabled through hello following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="bbeb5-128">TLS 암호화 그룹 순서 변경</span><span class="sxs-lookup"><span data-stu-id="bbeb5-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="bbeb5-129">고객 으로부터 다른 질문은 hello 목록이 해당 서버에서 협상 된 암호를 수정 하 고 hello를 수정 하 여 이렇게 할 경우 **clusterSettings** 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-129">Another question from customers is if they can modify hello list of ciphers negotiated by their server and this can be achieved by modifying hello **clusterSettings** as shown below.</span></span> <span data-ttu-id="bbeb5-130">암호 그룹 사용 가능한 hello 목록에서 검색할 수 [이 MSDN 문서](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-130">hello list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="bbeb5-131">SChannel 이해할 수 없습니다 hello 암호 그룹의 잘못 된 값을 설정 하는 모든 TLS 통신 tooyour 서버 작동을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-131">If incorrect values are set for hello cipher suite that SChannel cannot understand, all TLS communication tooyour server might stop functioning.</span></span> <span data-ttu-id="bbeb5-132">이 경우 tooremove hello 필요 합니다 *FrontEndSSLCipherSuiteOrder* 에서 항목 **clusterSettings** hello 업데이트 리소스 관리자 템플릿 toorevert 백 toohello 기본 암호화 제출 도구 모음 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-132">In such a case, you will need tooremove hello *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit hello updated Resource Manager template toorevert back toohello default cipher suite settings.</span></span>  <span data-ttu-id="bbeb5-133">이 기능을 주의하여 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="bbeb5-134">시작</span><span class="sxs-lookup"><span data-stu-id="bbeb5-134">Get started</span></span>
<span data-ttu-id="bbeb5-135">hello Azure 빠른 시작 리소스 관리자 템플릿 사이트 포함 hello에 대 한 기본 정의 된 템플릿이 [앱 서비스 환경 만들기](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbeb5-135">hello Azure Quickstart Resource Manager template site includes a template with hello base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
