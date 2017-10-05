---
title: "HDInsight 응용 프로그램 게시 - Azure | Microsoft Docs"
description: "HDInsight 응용 프로그램을 만들고 게시하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 14aef891-7a37-4cf1-8f7d-ca923565c783
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 6aa66cac35bc317fc87003e6c3d824544c53de88
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-hdinsight-applications-into-the-azure-marketplace"></a><span data-ttu-id="8b434-103">Azure 마켓플레이스에 HDInsight 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="8b434-103">Publish HDInsight applications into the Azure Marketplace</span></span>
<span data-ttu-id="8b434-104">HDInsight 응용 프로그램은 Linux 기반 HDInsight 클러스터에 사용자가 설치할 수 있는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-104">An HDInsight application is an application that users can install on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="8b434-105">Microsoft, ISV(독립 소프트웨어 공급 업체) 또는 사용자가 직접 이러한 응용 프로그램을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-105">These applications can be developed by Microsoft, independent software vendors (ISV) or by yourself.</span></span> <span data-ttu-id="8b434-106">이 문서에서는 HDInsight 응용 프로그램을 Azure Marketplace에 게시하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-106">In this article, you learn how to publish an HDInsight application into the Azure Marketplace.</span></span>  <span data-ttu-id="8b434-107">Azure 마켓플레이스에 게시하는 방법에 대한 일반 정보는 [Azure 마켓플레이스에 제품 게시](../marketplace-publishing/marketplace-publishing-getting-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b434-107">For general information about publishing into the Azure Marketplace, see [publish an offer to the Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="8b434-108">HDInsight 응용 프로그램은 *BYOL(사용자 라이선스 필요)* 을 사용하며 여기서 응용 프로그램 공급자는 최종 사용자에게 응용 프로그램을 라이선싱하는 작업을 담당하고 Azure에서 최종 사용자에게 HDInsight 클러스터와 해당 VM/노드 등 만들 리소스에 대한 요금을 청구합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-108">HDInsight applications use the *Bring Your Own License (BYOL)* model, where application provider is responsible for licensing the application to end-users, and end-users are only charged by Azure for the resources they create, such as the HDInsight cluster and its VMs/nodes.</span></span> <span data-ttu-id="8b434-109">지금은 응용 프로그램 자체에 대한 청구가 Azure를 통해 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-109">Currently, billing for the application itself is not done through Azure.</span></span>

<span data-ttu-id="8b434-110">다른 HDInsight 응용 프로그램 관련 문서:</span><span class="sxs-lookup"><span data-stu-id="8b434-110">Other HDInsight application-related article:</span></span>

* <span data-ttu-id="8b434-111">[HDInsight 응용 프로그램 설치](hdinsight-apps-install-applications.md): HDInsight 응용 프로그램을 클러스터에 설치하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-111">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="8b434-112">[사용자 지정 HDInsight 응용 프로그램 설치](hdinsight-apps-install-custom-applications.md): 사용자 지정 HDInsight 응용 프로그램을 설치하고 테스트하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-112">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to install and test custom HDInsight applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b434-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8b434-113">Prerequisites</span></span>
<span data-ttu-id="8b434-114">마켓플레이스에 사용자 지정 응용 프로그램을 제출하기 위해 사용자 지정 응용 프로그램을 만들고 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-114">To submit your custom application to the marketplace, you must have created and tested your custom application.</span></span> <span data-ttu-id="8b434-115">다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b434-115">See the following articles:</span></span>

* <span data-ttu-id="8b434-116">[사용자 지정 HDInsight 응용 프로그램 설치](hdinsight-apps-install-custom-applications.md): 사용자 지정 HDInsight 응용 프로그램을 설치하고 테스트하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-116">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to install and test custom HDInsight applications.</span></span>

<span data-ttu-id="8b434-117">또한 개발자 계정을 등록했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-117">You must also have registered your developer account.</span></span> <span data-ttu-id="8b434-118">[Azure Marketplace에 제품 게시](../marketplace-publishing/marketplace-publishing-getting-started.md) 및 [Microsoft 개발자 계정 만들기](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b434-118">See [publish an offer to the Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) and [Create a Microsoft Developer account](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).</span></span>

## <a name="define-application"></a><span data-ttu-id="8b434-119">응용 프로그램 정의</span><span class="sxs-lookup"><span data-stu-id="8b434-119">Define application</span></span>
<span data-ttu-id="8b434-120">Azure 마켓플레이스에 응용 프로그램을 게시하기 위해 두 가지 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-120">There are two steps involved for publishing applications to the Azure Marketplace.</span></span>  <span data-ttu-id="8b434-121">먼저 **createUiDef.json** 파일을 정의하여 응용 프로그램과 호환되고 클러스터를 나타낸 다음 Azure 포털에서 템플릿을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-121">First you define a **createUiDef.json** file to indicate which clusters your application is compatible with; and then you publish the template from the Azure portal.</span></span> <span data-ttu-id="8b434-122">다음은 섹션은 예제 createUiDef.json 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-122">The following section is a sample createUiDef.json file.</span></span>

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| <span data-ttu-id="8b434-123">필드</span><span class="sxs-lookup"><span data-stu-id="8b434-123">Field</span></span> | <span data-ttu-id="8b434-124">설명</span><span class="sxs-lookup"><span data-stu-id="8b434-124">Description</span></span> | <span data-ttu-id="8b434-125">가능한 값</span><span class="sxs-lookup"><span data-stu-id="8b434-125">Possible values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b434-126">types</span><span class="sxs-lookup"><span data-stu-id="8b434-126">types</span></span> |<span data-ttu-id="8b434-127">응용 프로그램과 호환되는 클러스터 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-127">The cluster types that the application is compatible with.</span></span> |<span data-ttu-id="8b434-128">Hadoop, HBase, Storm, Spark(또는 이들의 조합)</span><span class="sxs-lookup"><span data-stu-id="8b434-128">Hadoop, HBase, Storm, Spark, (or any combination of these)</span></span> |
| <span data-ttu-id="8b434-129">tiers</span><span class="sxs-lookup"><span data-stu-id="8b434-129">tiers</span></span> |<span data-ttu-id="8b434-130">응용 프로그램과 호환되는 클러스터 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-130">The cluster tiers that the application is compatible with.</span></span> |<span data-ttu-id="8b434-131">Standard, Premium(또는 둘 다)</span><span class="sxs-lookup"><span data-stu-id="8b434-131">Standard, Premium, (or both)</span></span> |
| <span data-ttu-id="8b434-132">versions</span><span class="sxs-lookup"><span data-stu-id="8b434-132">versions</span></span> |<span data-ttu-id="8b434-133">응용 프로그램과 호환되는 HDInsight 클러스터 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-133">The HDInsight cluster types that the application is compatible with.</span></span> |<span data-ttu-id="8b434-134">3.4</span><span class="sxs-lookup"><span data-stu-id="8b434-134">3.4</span></span> |

## <a name="application-install-script"></a><span data-ttu-id="8b434-135">응용 프로그램 설치 스크립트</span><span class="sxs-lookup"><span data-stu-id="8b434-135">Application install script</span></span>
<span data-ttu-id="8b434-136">응용 프로그램이 클러스터(기존 클러스터 또는 새 클러스터)에서 설치될 때마다 Edge 노드가 생성되고 응용 프로그램 설치 스크립트가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-136">Whenever an application is installed on a cluster (either an existing one or a new one), an edge node is created and the application install script is run on it.</span></span>
  > [!IMPORTANT]
  > <span data-ttu-id="8b434-137">아래 형식을 사용하는 응용 프로그램 설치 스크립트의 이름은 특정 클러스터에 대해 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-137">The name of the application install script names must be unique for a particular cluster with the following format.</span></span>
  > 
  > <span data-ttu-id="8b434-138">name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"</span><span class="sxs-lookup"><span data-stu-id="8b434-138">name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"</span></span>
  > 
  > <span data-ttu-id="8b434-139">스크립트 이름은 세 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-139">Note there are three parts to the script name:</span></span>
  > 
  > 1. <span data-ttu-id="8b434-140">응용 프로그램 이름 또는 응용 프로그램에 관련된 이름을 포함하는 스크립트 이름 접두사.</span><span class="sxs-lookup"><span data-stu-id="8b434-140">A script name prefix, which shall include either the application name or a name relevant to the application.</span></span>
  > 2. <span data-ttu-id="8b434-141">가독성을 위한 "-".</span><span class="sxs-lookup"><span data-stu-id="8b434-141">A "-" for readability.</span></span>
  > 3. <span data-ttu-id="8b434-142">매개 변수로 응용 프로그램 이름이 사용된 고유 문자열 함수.</span><span class="sxs-lookup"><span data-stu-id="8b434-142">A unique string function with the application name as the parameter.</span></span>
  > 
  > <span data-ttu-id="8b434-143">한 가지 예로서, 위 스크립트는 지속형 스크립트 작업 목록의 hue-install-v0-4wkahss55hlas가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-143">An example is the above ends up becoming: hue-install-v0-4wkahss55hlas in the persisted script action list.</span></span> <span data-ttu-id="8b434-144">샘플 JSON 페이로드는 [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b434-144">For a sample JSON payload, see [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).</span></span>
  > 
<span data-ttu-id="8b434-145">설치 스크립트는 다음 특성을 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-145">The installation script must have the following characteristics:</span></span>
1. <span data-ttu-id="8b434-146">스크립트가 idempotent여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-146">Ensure that the script is idempotent.</span></span> <span data-ttu-id="8b434-147">스크립트를 여러 번 호출하면 같은 결과가 생성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-147">Multiple calls to the script should produce the same result.</span></span>
2. <span data-ttu-id="8b434-148">스크립트 버전이 적절히 관리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-148">The script should be properly versioned.</span></span> <span data-ttu-id="8b434-149">응용 프로그램을 설치하려는 고객이 영향을 받지 않도록 업그레이드하거나 변경 내용을 테스트하는 경우 스크립트에 대해 다른 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-149">Use a different location for the script when you are upgrading or testing out changes so that customers that are trying to install the application are not affected.</span></span> 
3. <span data-ttu-id="8b434-150">스크립트의 각 지점에 적절한 로깅을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-150">Add adequate logging to the scripts at each point.</span></span> <span data-ttu-id="8b434-151">일반적으로 스크립트 로그는 응용 프로그램 설치 문제를 디버그하는 유일한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-151">Usually the script logs are the only way to debug application installation issues.</span></span>
4. <span data-ttu-id="8b434-152">일시적인 네트워크 문제로 인해 설치가 영향을 받지 않도록 외부 서비스 또는 리소스에 대한 호출이 적절히 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-152">Ensure that calls to external services or resources have adequate retries so that the installation is not affected by transient network issues.</span></span>
5. <span data-ttu-id="8b434-153">스크립트가 노드에서 서비스를 시작하는 경우 서비스를 모니터링하고 노드 재부팅 시 자동으로 시작되도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-153">If your script is starting services on the nodes, ensure that the services are monitored and configured to start automatically in case of node reboots.</span></span>

## <a name="package-application"></a><span data-ttu-id="8b434-154">패키지 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8b434-154">Package application</span></span>
<span data-ttu-id="8b434-155">HDInsight 응용 프로그램을 설치하는 데 필요한 모든 파일을 포함하는 zip 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-155">Create a zip file that contains all required files for installing your HDInsight applications.</span></span> <span data-ttu-id="8b434-156">[응용 프로그램 게시](#publish-application)에 zip 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-156">You need the zip file in [Publish application](#publish-application).</span></span>

* <span data-ttu-id="8b434-157">[createUiDefinition.json](#define-application).</span><span class="sxs-lookup"><span data-stu-id="8b434-157">[createUiDefinition.json](#define-application).</span></span>
* <span data-ttu-id="8b434-158">mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="8b434-158">mainTemplate.json.</span></span> <span data-ttu-id="8b434-159">[사용자 지정 HDInsight 응용 프로그램 설치](hdinsight-apps-install-custom-applications.md)의 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b434-159">See a sample at [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>
* <span data-ttu-id="8b434-160">모든 필수 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-160">All required scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="8b434-161">응용 프로그램 파일(있는 경우 웹 응용 프로그램 파일 포함)은 공개적으로 액세스할 수 있는 끝점에 위치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-161">The application files (including web application files if there is any) can be located on any publicly accessible endpoint.</span></span>
> 

## <a name="publish-application"></a><span data-ttu-id="8b434-162">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="8b434-162">Publish application</span></span>
<span data-ttu-id="8b434-163">다음 단계를 수행하여 HDInsight 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-163">Follow the following steps to publish an HDInsight application:</span></span>

1. <span data-ttu-id="8b434-164">[Azure 게시 포털](https://publish.windowsazure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-164">Sign on to the [Azure Publishing portal](https://publish.windowsazure.com/).</span></span>
2. <span data-ttu-id="8b434-165">왼쪽에서 **솔루션 템플릿** 을 클릭하여 새 솔루션 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-165">Click **Solution templates** from the left to create a new solution template.</span></span>
3. <span data-ttu-id="8b434-166">제목을 입력한 다음 **새 솔루션 템플릿 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-166">Enter a title, and then click **Create a new solution template**.</span></span>
4. <span data-ttu-id="8b434-167">**Dev Center 계정 만들기 및 Azure 프로그램 조인** 을 클릭하여 아직 수행하지 않은 경우 회사를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-167">Click **Create Dev Center account and join the Azure program** to register your company if you haven't done so.</span></span>  <span data-ttu-id="8b434-168">[Microsoft 개발자 계정 만들기](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b434-168">See [Create a Microsoft Developer account](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).</span></span>
5. <span data-ttu-id="8b434-169">**시작할 몇 가지 토폴로지 정의**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-169">Click **Define some Topologies to get Started**.</span></span> <span data-ttu-id="8b434-170">솔루션 템플릿은 해당하는 모든 토폴로지의 "부모"입니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-170">A solution template is a "parent" to all its topologies.</span></span> <span data-ttu-id="8b434-171">하나의 제품/솔루션 템플릿에서 여러 토폴로지를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-171">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="8b434-172">제품이 스테이징으로 푸시될 때 해당 토폴로지도 모두 함께 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-172">When an offer is pushed to staging, it is pushed with all its topologies.</span></span> 
6. <span data-ttu-id="8b434-173">토폴로지 이름을 입력하고 더하기 기호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-173">Enter a topology name, and then click the plus sign.</span></span>
7. <span data-ttu-id="8b434-174">새 버전을 입력하고 더하기 기호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-174">Enter a new version, and then click the Plus sign.</span></span>
8. <span data-ttu-id="8b434-175">[패키지 응용 프로그램](#package-application)에서 준비한 zip 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-175">Upload the zip file prepared in [Package application](#package-application).</span></span>  
9. <span data-ttu-id="8b434-176">**인증 요청**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-176">Click **Request Certification**.</span></span> <span data-ttu-id="8b434-177">Microsoft 인증 팀이 파일을 검토하고 토폴로지를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-177">The Microsoft certification team will review the files and certify the topology.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b434-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b434-178">Next steps</span></span>
* <span data-ttu-id="8b434-179">[HDInsight 응용 프로그램 설치](hdinsight-apps-install-applications.md): HDInsight 응용 프로그램을 클러스터에 설치하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-179">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="8b434-180">[사용자 지정 HDInsight 응용 프로그램 설치](hdinsight-apps-install-custom-applications.md): HDInsight로 게시 취소된 HDInsight 응용 프로그램을 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-180">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="8b434-181">[스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md): 스크립트 작업을 사용하여 추가 응용 프로그램을 설치하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-181">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="8b434-182">[Azure Resource Manager 템플릿을 사용하여 HDInsight의 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Azure Resource Manager 템플릿을 호출하여 HDInsight 클러스터를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-182">[Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how to call Resource Manager templates to create HDInsight clusters.</span></span>
* <span data-ttu-id="8b434-183">[HDInsight에서 비어 있는 에지 노드 사용](hdinsight-apps-use-edge-node.md): HDInsight 클러스터에 액세스, HDInsight 응용 프로그램 테스트 및 HDInsight 응용 프로그램 호스팅하는 데 비어 있는 에지 노드를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8b434-183">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): learn how to use an empty edge node for accessing HDInsight cluster, testing HDInsight applications, and hosting HDInsight applications.</span></span>

