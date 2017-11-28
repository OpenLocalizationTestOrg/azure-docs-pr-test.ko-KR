---
title: "aaaPublish HDInsight 응용 프로그램-Azure | Microsoft Docs"
description: "자세한 내용은 방법 toocreate HDInsight 응용 프로그램을 게시 합니다."
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
ms.openlocfilehash: 7da0aa53828563e50ef372df901e1ba541fb40be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-hdinsight-applications-into-hello-azure-marketplace"></a><span data-ttu-id="47c44-103">Azure 마켓플레이스 hello에 HDInsight 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="47c44-103">Publish HDInsight applications into hello Azure Marketplace</span></span>
<span data-ttu-id="47c44-104">HDInsight 응용 프로그램은 Linux 기반 HDInsight 클러스터에 사용자가 설치할 수 있는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-104">An HDInsight application is an application that users can install on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="47c44-105">Microsoft, ISV(독립 소프트웨어 공급 업체) 또는 사용자가 직접 이러한 응용 프로그램을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-105">These applications can be developed by Microsoft, independent software vendors (ISV) or by yourself.</span></span> <span data-ttu-id="47c44-106">이 문서에서는 설명 어떻게 toopublish hello Azure 마켓플레이스로 HDInsight 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-106">In this article, you learn how toopublish an HDInsight application into hello Azure Marketplace.</span></span>  <span data-ttu-id="47c44-107">Hello Azure 마켓플레이스에서 게시에 대 한 일반 정보를 참조 하십시오. [제공 toohello Azure 마켓플레이스에서 게시](../marketplace-publishing/marketplace-publishing-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-107">For general information about publishing into hello Azure Marketplace, see [publish an offer toohello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="47c44-108">HDInsight 응용 프로그램 사용 hello *Bring Your 자체 라이선스 (BYOL)* 여기서 응용 프로그램 공급자는 hello 응용 프로그램 tooend-사용자, 라이선스 해야 하 고 최종 사용자만 Azure에서에 부과 hello 리소스는 모델에서 hello HDInsight 클러스터와 해당 Vm/노드가 같은 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-108">HDInsight applications use hello *Bring Your Own License (BYOL)* model, where application provider is responsible for licensing hello application tooend-users, and end-users are only charged by Azure for hello resources they create, such as hello HDInsight cluster and its VMs/nodes.</span></span> <span data-ttu-id="47c44-109">현재, 자체 hello 응용 프로그램에 대 한 청구 Azure를 통해 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-109">Currently, billing for hello application itself is not done through Azure.</span></span>

<span data-ttu-id="47c44-110">다른 HDInsight 응용 프로그램 관련 문서:</span><span class="sxs-lookup"><span data-stu-id="47c44-110">Other HDInsight application-related article:</span></span>

* <span data-ttu-id="47c44-111">[HDInsight 응용 프로그램을 설치](hdinsight-apps-install-applications.md): tooinstall HDInsight 응용 프로그램 tooyour 클러스터 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-111">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how tooinstall an HDInsight application tooyour clusters.</span></span>
* <span data-ttu-id="47c44-112">[사용자 지정 HDInsight 응용 프로그램을 설치](hdinsight-apps-install-custom-applications.md): 자세한 방법을 tooinstall 및 테스트 사용자 지정 HDInsight 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-112">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how tooinstall and test custom HDInsight applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47c44-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="47c44-113">Prerequisites</span></span>
<span data-ttu-id="47c44-114">toosubmit 사용자 지정 응용 프로그램 toohello 마켓플레이스를 만들고를 사용자 지정 응용 프로그램을 테스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-114">toosubmit your custom application toohello marketplace, you must have created and tested your custom application.</span></span> <span data-ttu-id="47c44-115">Hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="47c44-115">See hello following articles:</span></span>

* <span data-ttu-id="47c44-116">[사용자 지정 HDInsight 응용 프로그램을 설치](hdinsight-apps-install-custom-applications.md): 자세한 방법을 tooinstall 및 테스트 사용자 지정 HDInsight 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-116">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how tooinstall and test custom HDInsight applications.</span></span>

<span data-ttu-id="47c44-117">또한 개발자 계정을 등록했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-117">You must also have registered your developer account.</span></span> <span data-ttu-id="47c44-118">참조 [제공 toohello Azure 마켓플레이스에서 게시](../marketplace-publishing/marketplace-publishing-getting-started.md) 및 [Microsoft 개발자 계정을 만들려면](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-118">See [publish an offer toohello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) and [Create a Microsoft Developer account](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).</span></span>

## <a name="define-application"></a><span data-ttu-id="47c44-119">응용 프로그램 정의</span><span class="sxs-lookup"><span data-stu-id="47c44-119">Define application</span></span>
<span data-ttu-id="47c44-120">응용 프로그램 toohello Azure 마켓플레이스에서 게시 하기 위한 관련 된 두 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-120">There are two steps involved for publishing applications toohello Azure Marketplace.</span></span>  <span data-ttu-id="47c44-121">먼저 정의 **createUiDef.json** 응용 프로그램 클러스터는 파일 tooindicate;와 호환 되 고 hello Azure 포털에서에서 hello 서식 파일을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-121">First you define a **createUiDef.json** file tooindicate which clusters your application is compatible with; and then you publish hello template from hello Azure portal.</span></span> <span data-ttu-id="47c44-122">다음 섹션 hello 샘플 createUiDef.json 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-122">hello following section is a sample createUiDef.json file.</span></span>

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| <span data-ttu-id="47c44-123">필드</span><span class="sxs-lookup"><span data-stu-id="47c44-123">Field</span></span> | <span data-ttu-id="47c44-124">설명</span><span class="sxs-lookup"><span data-stu-id="47c44-124">Description</span></span> | <span data-ttu-id="47c44-125">가능한 값</span><span class="sxs-lookup"><span data-stu-id="47c44-125">Possible values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47c44-126">types</span><span class="sxs-lookup"><span data-stu-id="47c44-126">types</span></span> |<span data-ttu-id="47c44-127">hello 응용 프로그램와 호환 되는 hello 클러스터 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-127">hello cluster types that hello application is compatible with.</span></span> |<span data-ttu-id="47c44-128">Hadoop, HBase, Storm, Spark(또는 이들의 조합)</span><span class="sxs-lookup"><span data-stu-id="47c44-128">Hadoop, HBase, Storm, Spark, (or any combination of these)</span></span> |
| <span data-ttu-id="47c44-129">tiers</span><span class="sxs-lookup"><span data-stu-id="47c44-129">tiers</span></span> |<span data-ttu-id="47c44-130">hello 응용 프로그램와 호환 되는 hello 클러스터 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-130">hello cluster tiers that hello application is compatible with.</span></span> |<span data-ttu-id="47c44-131">Standard, Premium(또는 둘 다)</span><span class="sxs-lookup"><span data-stu-id="47c44-131">Standard, Premium, (or both)</span></span> |
| <span data-ttu-id="47c44-132">versions</span><span class="sxs-lookup"><span data-stu-id="47c44-132">versions</span></span> |<span data-ttu-id="47c44-133">hello 응용 프로그램와 호환 되는 hello HDInsight 클러스터 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-133">hello HDInsight cluster types that hello application is compatible with.</span></span> |<span data-ttu-id="47c44-134">3.4</span><span class="sxs-lookup"><span data-stu-id="47c44-134">3.4</span></span> |

## <a name="application-install-script"></a><span data-ttu-id="47c44-135">응용 프로그램 설치 스크립트</span><span class="sxs-lookup"><span data-stu-id="47c44-135">Application install script</span></span>
<span data-ttu-id="47c44-136">응용 프로그램이 설치 될 때마다 (기존 또는 새) 클러스터에서 가장자리 노드 만들어지고 hello 응용 프로그램 설치 스크립트에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-136">Whenever an application is installed on a cluster (either an existing one or a new one), an edge node is created and hello application install script is run on it.</span></span>
  > [!IMPORTANT]
  > <span data-ttu-id="47c44-137">hello 응용 프로그램 설치 스크립트 이름이의 hello 이름 형식에 따라 hello로 특정 클러스터에 대 한 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-137">hello name of hello application install script names must be unique for a particular cluster with hello following format.</span></span>
  > 
  > <span data-ttu-id="47c44-138">name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"</span><span class="sxs-lookup"><span data-stu-id="47c44-138">name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"</span></span>
  > 
  > <span data-ttu-id="47c44-139">여기에 메모는 세 부분 toohello 스크립트 이름:</span><span class="sxs-lookup"><span data-stu-id="47c44-139">Note there are three parts toohello script name:</span></span>
  > 
  > 1. <span data-ttu-id="47c44-140">스크립트 이름 접두사-hello 응용 프로그램 이름 또는 이름 toohello 관련 응용 프로그램을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-140">A script name prefix, which shall include either hello application name or a name relevant toohello application.</span></span>
  > 2. <span data-ttu-id="47c44-141">가독성을 위한 "-".</span><span class="sxs-lookup"><span data-stu-id="47c44-141">A "-" for readability.</span></span>
  > 3. <span data-ttu-id="47c44-142">매개 변수를 hello hello 응용 프로그램 이름 사용 하는 고유 문자열 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-142">A unique string function with hello application name as hello parameter.</span></span>
  > 
  > <span data-ttu-id="47c44-143">예로 위의 hello 결국 되 고: 색상-설치-v0-4wkahss55hlas hello에 지속형 스크립트 동작 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-143">An example is hello above ends up becoming: hue-install-v0-4wkahss55hlas in hello persisted script action list.</span></span> <span data-ttu-id="47c44-144">샘플 JSON 페이로드는 [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47c44-144">For a sample JSON payload, see [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).</span></span>
  > 
<span data-ttu-id="47c44-145">hello 설치 스크립트에 다음 특징 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-145">hello installation script must have hello following characteristics:</span></span>
1. <span data-ttu-id="47c44-146">Hello 스크립트 idempotent 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-146">Ensure that hello script is idempotent.</span></span> <span data-ttu-id="47c44-147">동일한 결과 hello toohello 스크립트 생성 해야 하는 여러 번 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-147">Multiple calls toohello script should produce hello same result.</span></span>
2. <span data-ttu-id="47c44-148">hello 스크립트는 제대로 버전 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-148">hello script should be properly versioned.</span></span> <span data-ttu-id="47c44-149">업그레이드 하거나 tooinstall hello 응용 프로그램을 시도 하 고 있는 고객에 영향을 받지 않는 있도록 변경 내용을 테스트 하는 경우에 hello 스크립트에 대 한 다른 위치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-149">Use a different location for hello script when you are upgrading or testing out changes so that customers that are trying tooinstall hello application are not affected.</span></span> 
3. <span data-ttu-id="47c44-150">각 지점에서 적절 한 로깅 toohello 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-150">Add adequate logging toohello scripts at each point.</span></span> <span data-ttu-id="47c44-151">일반적으로 스크립트 로그 hello는 유일한 방법은 toodebug hello 응용 프로그램 설치 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-151">Usually hello script logs are hello only way toodebug application installation issues.</span></span>
4. <span data-ttu-id="47c44-152">있어야 호출 tooexternal 서비스 또는 리소스 적절 한 재시도 hello 설치는 일시적인 네트워크 문제로 인해 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-152">Ensure that calls tooexternal services or resources have adequate retries so that hello installation is not affected by transient network issues.</span></span>
5. <span data-ttu-id="47c44-153">스크립트 hello 노드에서 서비스의 시작 하는 경우 확인 hello 서비스를 모니터링 하 고 toostart 노드 재부팅 시 자동으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-153">If your script is starting services on hello nodes, ensure that hello services are monitored and configured toostart automatically in case of node reboots.</span></span>

## <a name="package-application"></a><span data-ttu-id="47c44-154">패키지 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="47c44-154">Package application</span></span>
<span data-ttu-id="47c44-155">HDInsight 응용 프로그램을 설치하는 데 필요한 모든 파일을 포함하는 zip 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-155">Create a zip file that contains all required files for installing your HDInsight applications.</span></span> <span data-ttu-id="47c44-156">Zip 파일의 hello 필요 [응용 프로그램 게시](#publish-application)합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-156">You need hello zip file in [Publish application](#publish-application).</span></span>

* <span data-ttu-id="47c44-157">[createUiDefinition.json](#define-application).</span><span class="sxs-lookup"><span data-stu-id="47c44-157">[createUiDefinition.json](#define-application).</span></span>
* <span data-ttu-id="47c44-158">mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="47c44-158">mainTemplate.json.</span></span> <span data-ttu-id="47c44-159">[사용자 지정 HDInsight 응용 프로그램 설치](hdinsight-apps-install-custom-applications.md)의 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47c44-159">See a sample at [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>
* <span data-ttu-id="47c44-160">모든 필수 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-160">All required scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="47c44-161">응용 프로그램 파일 (있는 경우 웹 응용 프로그램 파일 포함) hello 공개적으로 액세스할 수 있는 모든 끝점에 위치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-161">hello application files (including web application files if there is any) can be located on any publicly accessible endpoint.</span></span>
> 

## <a name="publish-application"></a><span data-ttu-id="47c44-162">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="47c44-162">Publish application</span></span>
<span data-ttu-id="47c44-163">Hello 단계 toopublish HDInsight 응용 프로그램에 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-163">Follow hello following steps toopublish an HDInsight application:</span></span>

1. <span data-ttu-id="47c44-164">Toohello 로그온 [Azure 게시 포털](https://publish.windowsazure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-164">Sign on toohello [Azure Publishing portal](https://publish.windowsazure.com/).</span></span>
2. <span data-ttu-id="47c44-165">클릭 **솔루션 템플릿을** hello 왼쪽된 toocreate 새 솔루션 템플릿에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-165">Click **Solution templates** from hello left toocreate a new solution template.</span></span>
3. <span data-ttu-id="47c44-166">제목을 입력한 다음 **새 솔루션 템플릿 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-166">Enter a title, and then click **Create a new solution template**.</span></span>
4. <span data-ttu-id="47c44-167">클릭 **만들기 개발 센터 계정 및 조인 hello Azure 프로그램** tooregister 그렇게 하지 않은 경우 회사입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-167">Click **Create Dev Center account and join hello Azure program** tooregister your company if you haven't done so.</span></span>  <span data-ttu-id="47c44-168">[Microsoft 개발자 계정 만들기](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47c44-168">See [Create a Microsoft Developer account](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).</span></span>
5. <span data-ttu-id="47c44-169">클릭 **일부 토폴로지 tooget Started 정의**합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-169">Click **Define some Topologies tooget Started**.</span></span> <span data-ttu-id="47c44-170">솔루션 템플릿을 "부모" tooall 해당 토폴로지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-170">A solution template is a "parent" tooall its topologies.</span></span> <span data-ttu-id="47c44-171">하나의 제품/솔루션 템플릿에서 여러 토폴로지를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-171">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="47c44-172">제안을 toostaging 푸시됩니다, 모든 토폴로지에서 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-172">When an offer is pushed toostaging, it is pushed with all its topologies.</span></span> 
6. <span data-ttu-id="47c44-173">토폴로지 이름을 입력 하 고 hello 더하기 기호를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-173">Enter a topology name, and then click hello plus sign.</span></span>
7. <span data-ttu-id="47c44-174">새 버전을 입력 하 고 hello 더하기 기호를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-174">Enter a new version, and then click hello Plus sign.</span></span>
8. <span data-ttu-id="47c44-175">업로드 hello zip 파일에서 준비한 [응용 프로그램 패키지](#package-application)합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-175">Upload hello zip file prepared in [Package application](#package-application).</span></span>  
9. <span data-ttu-id="47c44-176">**인증 요청**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-176">Click **Request Certification**.</span></span> <span data-ttu-id="47c44-177">Microsoft 인증 팀 hello hello 파일을 검토 하 고 hello 토폴로지를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-177">hello Microsoft certification team will review hello files and certify hello topology.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47c44-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="47c44-178">Next steps</span></span>
* <span data-ttu-id="47c44-179">[HDInsight 응용 프로그램을 설치](hdinsight-apps-install-applications.md): tooinstall HDInsight 응용 프로그램 tooyour 클러스터 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-179">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how tooinstall an HDInsight application tooyour clusters.</span></span>
* <span data-ttu-id="47c44-180">[사용자 지정 HDInsight 응용 프로그램을 설치](hdinsight-apps-install-custom-applications.md): 자세한 방법을 toodeploy 게시 되지 않은 HDInsight 응용 프로그램 tooHDInsight 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-180">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how toodeploy an unpublished HDInsight application tooHDInsight.</span></span>
* <span data-ttu-id="47c44-181">[스크립트 동작을 사용 하 여 Linux 기반 HDInsight 클러스터를 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md): 자세한 방법을 toouse 스크립트 동작 tooinstall 추가 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-181">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how toouse Script Action tooinstall additional applications.</span></span>
* <span data-ttu-id="47c44-182">[Azure 리소스 관리자 템플릿을 사용 하 여 HDInsight의 Linux 기반 Hadoop 클러스터를 만들어](hdinsight-hadoop-create-linux-clusters-arm-templates.md): 방법을 toocall 리소스 관리자 템플릿 toocreate HDInsight 클러스터에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-182">[Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how toocall Resource Manager templates toocreate HDInsight clusters.</span></span>
* <span data-ttu-id="47c44-183">[빈 가장자리 노드를 사용 하 여 HDInsight의](hdinsight-apps-use-edge-node.md): 방법을 toouse 빈 가장자리 노드 HDInsight 클러스터에 액세스, HDInsight 응용 프로그램 테스트 및 호스팅에 대 한 자세한 내용은 HDInsight 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="47c44-183">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): learn how toouse an empty edge node for accessing HDInsight cluster, testing HDInsight applications, and hosting HDInsight applications.</span></span>

