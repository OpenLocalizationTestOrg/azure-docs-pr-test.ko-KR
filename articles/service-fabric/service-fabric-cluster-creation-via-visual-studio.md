---
title: "Visual Studio를 사용 하 여 서비스 패브릭 클러스터를 aaaSetting | Microsoft Docs"
description: "Visual Studio에서 Azure 리소스 그룹 프로젝트에서 만든 Azure 리소스 관리자 템플릿을 사용 하 여 서비스 패브릭을 tooset 클러스터링 하는 방법을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="b28da-103">Visual Studio를 사용하여 서비스 패브릭 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="b28da-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="b28da-104">이 문서에서는 Visual Studio 및 Azure 리소스 관리자 템플릿을 사용 하 여 Azure 서비스 패브릭을 tooset 클러스터링 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-104">This article describes how tooset up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="b28da-105">Visual Studio Azure 리소스 그룹 프로젝트 toocreate hello 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-105">We will use a Visual Studio Azure resource group project toocreate hello template.</span></span> <span data-ttu-id="b28da-106">배포할 수 hello 서식 파일을 만든 후 Visual Studio에서 직접 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-106">After hello template has been created, it can be deployed directly tooAzure from Visual Studio.</span></span> <span data-ttu-id="b28da-107">스크립트에서 또는 CI(연속 통합) 기능의 일부로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="b28da-108">Azure 리소스 그룹 프로젝트를 사용하여 서비스 패브릭 클러스터 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="b28da-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="b28da-109">tooget 시작, Visual Studio를 열고 Azure 리소스 그룹 프로젝트를 만듭니다 (hello에서 사용할 수 **클라우드** 폴더):</span><span class="sxs-lookup"><span data-stu-id="b28da-109">tooget started, open Visual Studio and create an Azure resource group project (it is available in hello **Cloud** folder):</span></span>

![선택한 Azure 리소스 그룹 프로젝트를 사용하는 새 프로젝트 대화 상자][1]

<span data-ttu-id="b28da-111">이 프로젝트에 대 한 새 Visual Studio 솔루션을 만들거나 tooan 기존 솔루션에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-111">You can create a new Visual Studio solution for this project or add it tooan existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="b28da-112">Hello Azure 리소스 그룹 프로젝트 hello 클라우드 노드 아래에 표시 되지 않으면, 않아도 hello Azure SDK가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-112">If you do not see hello Azure resource group project under hello Cloud node, you do not have hello Azure SDK installed.</span></span> <span data-ttu-id="b28da-113">웹 플랫폼 설치 관리자를 시작 ([지금 설치](http://www.microsoft.com/web/downloads/platform.aspx) 설치 하지 않은 경우), "Azure SDK에 대 한.NET" 및 Visual Studio 버전에 호환 되는 hello 버전 설치에 대 한 다음 검색 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install hello version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="b28da-114">Hello 확인 단추를 맞추면 Visual Studio에서 묻는 tooselect hello 리소스 관리자 템플릿을 toocreate:</span><span class="sxs-lookup"><span data-stu-id="b28da-114">After you hit hello OK button, Visual Studio will ask you tooselect hello Resource Manager template you want toocreate:</span></span>

![선택한 서비스 패브릭 클러스터 템플릿을 사용하여 Azure 템플릿 대화 상자를 선택합니다.][2]

<span data-ttu-id="b28da-116">Hello 서비스 패브릭 클러스터 템플릿과 적중된 hello 확인 단추를 다시 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-116">Select hello Service Fabric Cluster template and hit hello OK button again.</span></span> <span data-ttu-id="b28da-117">hello 프로젝트 및 hello 리소스 관리자 템플릿 이제 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-117">hello project and hello Resource Manager template have now been created.</span></span>

## <a name="prepare-hello-template-for-deployment"></a><span data-ttu-id="b28da-118">배포에 대 한 hello 템플릿 준비</span><span class="sxs-lookup"><span data-stu-id="b28da-118">Prepare hello template for deployment</span></span>
<span data-ttu-id="b28da-119">Hello 템플릿이 있으면 배포 toocreate hello 클러스터 전에 hello 필요한 템플릿 매개 변수 값을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-119">Before hello template is deployed toocreate hello cluster, you must provide values for hello required template parameters.</span></span> <span data-ttu-id="b28da-120">이러한 매개 변수 값 hello에서 읽혀집니다 `ServiceFabricCluster.parameters.json` hello에 있는 파일 `Templates` hello 리소스 그룹 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-120">These parameter values are read from hello `ServiceFabricCluster.parameters.json` file, which is in hello `Templates` folder of hello resource group project.</span></span> <span data-ttu-id="b28da-121">Hello 파일을 열고 hello 다음 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-121">Open hello file and provide hello following values:</span></span>

| <span data-ttu-id="b28da-122">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="b28da-122">Parameter name</span></span> | <span data-ttu-id="b28da-123">설명</span><span class="sxs-lookup"><span data-stu-id="b28da-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b28da-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="b28da-124">adminUserName</span></span> |<span data-ttu-id="b28da-125">서비스 패브릭 컴퓨터 (노드)에 대 한 hello 관리자 계정의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-125">hello name of hello administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="b28da-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="b28da-126">certificateThumbprint</span></span> |<span data-ttu-id="b28da-127">hello 클러스터를 보호 하는 hello 인증서의 지문 안녕하세요입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-127">hello thumbprint of hello certificate that secures hello cluster.</span></span> |
| <span data-ttu-id="b28da-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="b28da-128">sourceVaultResourceId</span></span> |<span data-ttu-id="b28da-129">hello *리소스 ID* hello 키 자격 증명 모음의 hello 클러스터를 보호 하는 hello 인증서 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-129">hello *resource ID* of hello key vault where hello certificate that secures hello cluster is stored.</span></span> |
| <span data-ttu-id="b28da-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="b28da-130">certificateUrlValue</span></span> |<span data-ttu-id="b28da-131">hello 클러스터 보안 인증서의 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-131">hello URL of hello cluster security certificate.</span></span> |

<span data-ttu-id="b28da-132">Visual Studio 서비스 패브릭 리소스 관리자 템플릿 hello 인증서로 보호 되는 보안 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-132">hello Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="b28da-133">이 인증서는 hello로 식별 되 마지막 세 개의 템플릿 매개 변수 (`certificateThumbprint`, `sourceVaultValue`, 및 `certificateUrlValue`)에 있어야 하 고는 **Azure 키 자격 증명 모음**합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-133">This certificate is identified by hello last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="b28da-134">어떻게 toocreate hello 클러스터 보안 인증서에 대 한 자세한 내용은 참조 하십시오. [서비스 패브릭 클러스터 보안 시나리오](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) 문서.</span><span class="sxs-lookup"><span data-stu-id="b28da-134">For more information on how toocreate hello cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-hello-cluster-name"></a><span data-ttu-id="b28da-135">선택 사항: hello 클러스터 이름 변경</span><span class="sxs-lookup"><span data-stu-id="b28da-135">Optional: change hello cluster name</span></span>
<span data-ttu-id="b28da-136">모든 서비스 패브릭 클러스터에는 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="b28da-137">클러스터 이름 ("hello Azure 지역) 함께 개인 Azure에서 패브릭 클러스터를 만들면 hello 클러스터에 대 한 hello 도메인 이름 (DNS System) 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-137">When a Fabric cluster is created in Azure, cluster name determines (together with hello Azure region) hello Domain Name System (DNS) name for hello cluster.</span></span> <span data-ttu-id="b28da-138">예를 들어, 클러스터 이름을 `myBigCluster`, hello 새 클러스터를 호스트 하는 hello 리소스 그룹의 hello 위치 (Azure 지역)는 미국 동부를 hello 클러스터의 DNS 이름을 hello 됩니다 `myBigCluster.eastus.cloudapp.azure.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-138">For example, if you name your cluster `myBigCluster`, and hello location (Azure region) of hello resource group that will host hello new cluster is East US, hello DNS name of hello cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="b28da-139">기본적으로 hello 클러스터 이름은 자동으로 생성 이며 임의 접미사 tooa "클러스터" 접두사를 연결 하 여 고유 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-139">By default hello cluster name is generated automatically and made unique by attaching a random suffix tooa "cluster" prefix.</span></span> <span data-ttu-id="b28da-140">이렇게 하면 매우 쉽게 toouse hello 서식 파일의 일부로 **연속 통합** (CI) 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-140">This makes it very easy toouse hello template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="b28da-141">Toouse 의미 있는 tooyou 있는 클러스터에 대해 특정 이름을 설정의 hello hello 값 `clusterName` hello 리소스 관리자 템플릿 파일에 변수 (`ServiceFabricCluster.json`) tooyour 선택한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-141">If you want toouse a specific name for your cluster, one that is meaningful tooyou, set hello value of hello `clusterName` variable in hello Resource Manager template file (`ServiceFabricCluster.json`) tooyour chosen name.</span></span> <span data-ttu-id="b28da-142">변수는 해당 파일에 정의 된 hello 첫 번째 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-142">It is hello first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="b28da-143">옵션: 공용 응용 프로그램 포트 추가</span><span class="sxs-lookup"><span data-stu-id="b28da-143">Optional: add public application ports</span></span>
<span data-ttu-id="b28da-144">배포 하기 전에 hello 클러스터에 대 한 toochange hello 공용 응용 프로그램이 포트를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-144">You may also want toochange hello public application ports for hello cluster before you deploy it.</span></span> <span data-ttu-id="b28da-145">기본적으로 두 개의 공용 TCP 포트 (80 및 8081) hello 템플릿을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-145">By default, hello template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="b28da-146">응용 프로그램에 대 한 추가 해야 할 경우 hello 템플릿에서 hello Azure 부하 분산 장치 정의 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-146">If you need more for your applications, modify hello Azure Load Balancer definition in hello template.</span></span> <span data-ttu-id="b28da-147">hello 정의 hello 주 템플릿 파일에 저장 됩니다 (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="b28da-147">hello definition is stored in hello main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="b28da-148">해당 파일을 열고 `loadBalancedAppPort`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="b28da-149">각 포트는 세 개의 아티팩트에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="b28da-150">Hello 포트에 대 한 hello TCP 포트 값을 정의 하는 템플릿 변수:</span><span class="sxs-lookup"><span data-stu-id="b28da-150">A template variable that defines hello TCP port value for hello port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="b28da-151">A *프로브* Azure 부하 분산 장치가 하나 tooanother 통해 toouse 실패 하기 전에 특정 서비스 패브릭 노드 하려고 시도 빈도 및 기간 hello에 대 한 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-151">A *probe* that defines how frequently and for how long hello Azure load balancer attempts toouse a specific Service Fabric node before failing over tooanother one.</span></span> <span data-ttu-id="b28da-152">hello 프로브는 hello 부하 분산 장치 리소스의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-152">hello probes are part of hello Load Balancer resource.</span></span> <span data-ttu-id="b28da-153">첫 번째 기본 응용 프로그램 포트 hello에 대 한 hello 프로브 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-153">Here is hello probe definition for hello first default application port:</span></span>
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. <span data-ttu-id="b28da-154">A *부하 분산 규칙* hello 포트 및 부하 분산 서비스 패브릭 클러스터 노드 집합을 사용 하는 hello 프로브 함께 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-154">A *load-balancing rule* that ties together hello port and hello probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   <span data-ttu-id="b28da-155">Toodeploy toohello 클러스터를 계획 하는 hello 응용 프로그램에서 더 많은 포트를 필요 만드는 추가 검색 및 부하 분산 규칙 정의 하 여 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-155">If hello applications that you plan toodeploy toohello cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="b28da-156">방법에 대 한 자세한 내용은 Azure 부하 분산 장치를 리소스 관리자 템플릿을 통해 toowork 참조 [템플릿을 사용 하는 내부 부하 분산 장치를 만들기 전에](../load-balancer/load-balancer-get-started-ilb-arm-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-156">For more information on how toowork with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-hello-template-by-using-visual-studio"></a><span data-ttu-id="b28da-157">Visual Studio를 사용 하 여 hello 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-157">Deploy hello template by using Visual Studio</span></span>
<span data-ttu-id="b28da-158">모든 hello에 필요한 매개 변수 값 저장 한 후의`ServiceFabricCluster.param.dev.json` 파일을 준비 toodeploy hello 템플릿을 있고 서비스 패브릭 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-158">After you have saved all hello required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready toodeploy hello template and create your Service Fabric cluster.</span></span> <span data-ttu-id="b28da-159">Visual Studio 솔루션 탐색기에서 hello 리소스 그룹 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **배포 | 새 배포...** . 필요한 경우 Visual Studio hello 표시 됩니다 **tooResource 그룹 배포** tooauthenticate tooAzure 묻는 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="b28da-159">Right-click hello resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**. If necessary, Visual Studio will show hello **Deploy tooResource Group** dialog box, asking you tooauthenticate tooAzure:</span></span>

![배포 tooResource 그룹 대화 상자][3]

<span data-ttu-id="b28da-161">hello 대화 상자에는 hello 클러스터와 새 옵션 toocreate을 hello 제공에 대 한 기존 리소스 관리자 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-161">hello dialog box lets you choose an existing Resource Manager resource group for hello cluster and gives you hello option toocreate a new one.</span></span> <span data-ttu-id="b28da-162">일반적으로 이렇게 하면 의미 toouse 서비스 패브릭 클러스터에 대 한 별도 리소스 그룹 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-162">It normally makes sense toouse a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="b28da-163">Hello 배포 단추 맞추면 tooconfirm hello 템플릿 매개 변수 값 Visual Studio에 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-163">After you hit hello Deploy button, Visual Studio will prompt you tooconfirm hello template parameter values.</span></span> <span data-ttu-id="b28da-164">적중된 hello **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-164">Hit hello **Save** button.</span></span> <span data-ttu-id="b28da-165">매개 변수가 하나 지속형된 값이 없는: hello 클러스터에 대 한 hello 관리 계정 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-165">One parameter does not have a persisted value: hello administrative account password for hello cluster.</span></span> <span data-ttu-id="b28da-166">Visual Studio 하나에 대 한 메시지에 따라 tooprovide 암호 값을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-166">You need tooprovide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="b28da-167">Azure SDK 2.9부터는 Visual Studio에서 배포 중에 **Azure 주요 자격 증명 모음**에서 암호를 읽도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-167">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="b28da-168">Hello 템플릿 매개 변수 대화 상자에서 해당 hello 확인 `adminPassword` 매개 변수 입력란 오른쪽 hello에 대 한 작은 "키" 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-168">In hello template parameters dialog notice that hello `adminPassword` parameter text box has a little "key" icon on hello right.</span></span> <span data-ttu-id="b28da-169">이 아이콘으로 hello hello 클러스터에 대 한 관리자 암호는 기존 키 자격 증명 모음 암호 tooselect이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-169">This icon allows you tooselect an existing key vault secret as hello administrative password for hello cluster.</span></span> <span data-ttu-id="b28da-170">단지 있는지 toofirst을 주요 자격 증명 모음의 hello 고급 액세스 정책에서 템플릿 배포에 대 한 Azure 리소스 관리자 액세스를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-170">Just make sure toofirst enable Azure Resource Manager access for template deployment in hello Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="b28da-171">Hello Visual Studio 출력 창에 hello 배포 프로세스의 hello 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-171">You can monitor hello progress of hello deployment process in hello Visual Studio output window.</span></span> <span data-ttu-id="b28da-172">Hello 템플릿 배포가 완료 되 면 새 클러스터가 준비 toouse 되었습니다!</span><span class="sxs-lookup"><span data-stu-id="b28da-172">Once hello template deployment is completed, your new cluster is ready toouse!</span></span>

> [!NOTE]
> <span data-ttu-id="b28da-173">PowerShell이 현재 사용 중인 hello 컴퓨터에서 사용 되는 tooadminister Azure 않은 경우 toodo 약간 정리 작업 필요.</span><span class="sxs-lookup"><span data-stu-id="b28da-173">If PowerShell was never used tooadminister Azure from hello machine that you are using now, you need toodo a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="b28da-174">PowerShell 스크립팅 hello를 실행 하 여 사용 하도록 설정 [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-174">Enable PowerShell scripting by running hello [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="b28da-175">개발 컴퓨터인 경우 "제한 없음" 정책이 일반적으로 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-175">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="b28da-176">결정 여부 Azure PowerShell 명령 및 실행에서 진단 데이터 수집 tooallow [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) 또는 [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) 필요에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-176">Decide whether tooallow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="b28da-177">이렇게 하면 템플릿 배포 중 발생하는 불필요한 프롬프트를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-177">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="b28da-178">오류가 있는 경우 이동 toohello [Azure 포털](https://portal.azure.com/) 및 열기 hello 리소스 그룹에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-178">If there are any errors, go toohello [Azure portal](https://portal.azure.com/) and open hello resource group that you deployed to.</span></span> <span data-ttu-id="b28da-179">클릭 **모든 설정을**, 클릭 **배포** hello 설정 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-179">Click **All settings**, then click **Deployments** on hello settings blade.</span></span> <span data-ttu-id="b28da-180">리소스 그룹 배포에 오류가 발생한 경우 여기에 자세한 진단 정보를 남깁니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-180">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="b28da-181">서비스 패브릭 클러스터 특정 개수의 toomaintain 가용성을 노드 toobe 필요 하 고 상태-"쿼럼을 유지 관리 합니다." 참조 tooas 유지</span><span class="sxs-lookup"><span data-stu-id="b28da-181">Service Fabric clusters require a certain number of nodes toobe up toomaintain availability and preserve state - referred tooas "maintaining quorum."</span></span> <span data-ttu-id="b28da-182">따라서,는 것은 안전 tooshut hello 클러스터의 hello 시스템의 모든 작동 중지 처음 수행 하지 않는 한는 [시/도의 전체 백업](service-fabric-reliable-services-backup-restore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-182">Therefore, it is not safe tooshut down all of hello machines in hello cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b28da-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b28da-183">Next steps</span></span>
* [<span data-ttu-id="b28da-184">Hello Azure 포털을 사용 하 여 서비스 패브릭 클러스터를 설정 하는 방법에 대 한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="b28da-184">Learn about setting up Service Fabric cluster using hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="b28da-185">자세한 내용은 방법 toomanage Visual Studio를 사용 하 여 서비스 패브릭 응용 프로그램 및 배포</span><span class="sxs-lookup"><span data-stu-id="b28da-185">Learn how toomanage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
