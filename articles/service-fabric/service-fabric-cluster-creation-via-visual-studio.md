---
title: "Visual Studio를 사용하여 Service Fabric 클러스터 설정 | Microsoft Docs"
description: "Visual Studio의 Azure 리소스 그룹 프로젝트에 의해 만들어진 Azure Resource Manager 템플릿을 사용하여 Service Fabric 클러스터를 설정하는 방법을 설명합니다."
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
ms.openlocfilehash: c43145b96cdbdfaa7e1893e50d027321fe4c0510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="38b47-103">Visual Studio를 사용하여 서비스 패브릭 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="38b47-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="38b47-104">이 문서에서는 Visual Studio 및 Azure Resource Manager 템플릿을 사용하여 Azure Service Fabric 클러스터를 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-104">This article describes how to set up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="38b47-105">Visual Studio Azure 리소스 그룹 프로젝트를 사용하여 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-105">We will use a Visual Studio Azure resource group project to create the template.</span></span> <span data-ttu-id="38b47-106">템플릿이 만들어지면 Visual Studio에서 Azure에 직접 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-106">After the template has been created, it can be deployed directly to Azure from Visual Studio.</span></span> <span data-ttu-id="38b47-107">스크립트에서 또는 CI(연속 통합) 기능의 일부로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="38b47-108">Azure 리소스 그룹 프로젝트를 사용하여 서비스 패브릭 클러스터 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="38b47-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="38b47-109">시작하려면 Visual Studio를 열고 Azure 리소스 그룹 프로젝트( **클라우드** 폴더에서 사용할 수 있음)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-109">To get started, open Visual Studio and create an Azure resource group project (it is available in the **Cloud** folder):</span></span>

![선택한 Azure 리소스 그룹 프로젝트를 사용하는 새 프로젝트 대화 상자][1]

<span data-ttu-id="38b47-111">이 프로젝트에 대한 새 Visual Studio 솔루션을 만들거나 기존 솔루션에 이 프로젝트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-111">You can create a new Visual Studio solution for this project or add it to an existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="38b47-112">클라우드 노드 아래에 Azure 리소스 그룹 프로젝트가 표시되지 않는 경우 Azure SDK가 설치되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-112">If you do not see the Azure resource group project under the Cloud node, you do not have the Azure SDK installed.</span></span> <span data-ttu-id="38b47-113">웹 플랫폼 설치 관리자를 시작한 다음(아직 설치하지 않은 경우[지금 설치](http://www.microsoft.com/web/downloads/platform.aspx) ) ".NET용 Azure SDK"를 검색하여 사용자의 Visual Studio 버전과 호환되는 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install the version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="38b47-114">확인 단추를 누르면 Visual Studio에서 만들 리소스 관리자 템플릿을 선택하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-114">After you hit the OK button, Visual Studio will ask you to select the Resource Manager template you want to create:</span></span>

![선택한 서비스 패브릭 클러스터 템플릿을 사용하여 Azure 템플릿 대화 상자를 선택합니다.][2]

<span data-ttu-id="38b47-116">서비스 패브릭 클러스터 템플릿을 선택하고 확인 단추를 다시 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-116">Select the Service Fabric Cluster template and hit the OK button again.</span></span> <span data-ttu-id="38b47-117">이제 프로젝트 및 리소스 관리자 템플릿이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-117">The project and the Resource Manager template have now been created.</span></span>

## <a name="prepare-the-template-for-deployment"></a><span data-ttu-id="38b47-118">배포용 템플릿 준비</span><span class="sxs-lookup"><span data-stu-id="38b47-118">Prepare the template for deployment</span></span>
<span data-ttu-id="38b47-119">클러스터를 만들기 위해 템플릿을 배포하기 전에 필요한 템플릿 매개 변수 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-119">Before the template is deployed to create the cluster, you must provide values for the required template parameters.</span></span> <span data-ttu-id="38b47-120">이러한 매개 변수 값은 리소스 그룹 프로젝트의 `Templates` 폴더에 있는 `ServiceFabricCluster.parameters.json` 파일에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-120">These parameter values are read from the `ServiceFabricCluster.parameters.json` file, which is in the `Templates` folder of the resource group project.</span></span> <span data-ttu-id="38b47-121">파일을 열고 다음 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-121">Open the file and provide the following values:</span></span>

| <span data-ttu-id="38b47-122">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="38b47-122">Parameter name</span></span> | <span data-ttu-id="38b47-123">설명</span><span class="sxs-lookup"><span data-stu-id="38b47-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="38b47-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="38b47-124">adminUserName</span></span> |<span data-ttu-id="38b47-125">서비스 패브릭 컴퓨터(노드)에 대한 관리자 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-125">The name of the administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="38b47-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="38b47-126">certificateThumbprint</span></span> |<span data-ttu-id="38b47-127">클러스터를 보호하는 인증서의 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-127">The thumbprint of the certificate that secures the cluster.</span></span> |
| <span data-ttu-id="38b47-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="38b47-128">sourceVaultResourceId</span></span> |<span data-ttu-id="38b47-129">저장된 클러스터를 보호하는 인증서가 있는 키 자격 증명 모음의 *리소스 ID* 입니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-129">The *resource ID* of the key vault where the certificate that secures the cluster is stored.</span></span> |
| <span data-ttu-id="38b47-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="38b47-130">certificateUrlValue</span></span> |<span data-ttu-id="38b47-131">클러스터 보안 인증서의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-131">The URL of the cluster security certificate.</span></span> |

<span data-ttu-id="38b47-132">Visual Studio 서비스 패브릭 리소스 관리자 템플릿은 인증서로 보호되는 보안 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-132">The Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="38b47-133">이 인증서는 마지막 3개의 템플릿 매개 변수(`certificateThumbprint`, `sourceVaultValue` 및 `certificateUrlValue`)로 식별되며 **Azure 주요 자격 증명 모음**에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-133">This certificate is identified by the last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="38b47-134">클러스터 보안 인증서를 만드는 방법에 대한 자세한 내용은 [서비스 패브릭 클러스터 보안 시나리오](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38b47-134">For more information on how to create the cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-the-cluster-name"></a><span data-ttu-id="38b47-135">선택 사항: 클러스터 이름 변경</span><span class="sxs-lookup"><span data-stu-id="38b47-135">Optional: change the cluster name</span></span>
<span data-ttu-id="38b47-136">모든 서비스 패브릭 클러스터에는 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="38b47-137">Azure에서 패브릭 클러스터가 만들어지면 클러스터 이름은 클러스터에 대한 DNS(Domain Name System) 이름을 Azure 지역과 함께 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-137">When a Fabric cluster is created in Azure, cluster name determines (together with the Azure region) the Domain Name System (DNS) name for the cluster.</span></span> <span data-ttu-id="38b47-138">예를 들어 클러스터 이름을 `myBigCluster`로 지정했으며 새 클러스터를 호스트할 리소스 그룹의 위치(Azure 하위 지역)가 미국 동부이면 클러스터의 DNS 이름은 `myBigCluster.eastus.cloudapp.azure.com`이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-138">For example, if you name your cluster `myBigCluster`, and the location (Azure region) of the resource group that will host the new cluster is East US, the DNS name of the cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="38b47-139">기본적으로 클러스터 이름은 자동으로 생성되며 임의의 접미사를 "cluster" 접두사에 추가하여 고유하게 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-139">By default the cluster name is generated automatically and made unique by attaching a random suffix to a "cluster" prefix.</span></span> <span data-ttu-id="38b47-140">이렇게 하면 템플릿을 **Ci(연속 통합)** 시스템의 일부로 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-140">This makes it very easy to use the template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="38b47-141">클러스터에 대해 사용자에게 의미가 있는 특정 이름을 사용하려는 경우 Resource Manager 템플릿 파일(`ServiceFabricCluster.json`)의 `clusterName` 변수 값을 선택한 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-141">If you want to use a specific name for your cluster, one that is meaningful to you, set the value of the `clusterName` variable in the Resource Manager template file (`ServiceFabricCluster.json`) to your chosen name.</span></span> <span data-ttu-id="38b47-142">해당 파일에 정의된 첫 번째 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-142">It is the first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="38b47-143">옵션: 공용 응용 프로그램 포트 추가</span><span class="sxs-lookup"><span data-stu-id="38b47-143">Optional: add public application ports</span></span>
<span data-ttu-id="38b47-144">배포하기 전에 클러스터에 대한 공용 응용 프로그램 포트를 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-144">You may also want to change the public application ports for the cluster before you deploy it.</span></span> <span data-ttu-id="38b47-145">기본적으로 템플릿에서는 두 개의 공용 TCP 포트(80과 8081)만 열립니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-145">By default, the template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="38b47-146">응용 프로그램에 더 많은 포트가 필요한 경우 템플릿에서 Azure 부하 분산 장치 정의를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-146">If you need more for your applications, modify the Azure Load Balancer definition in the template.</span></span> <span data-ttu-id="38b47-147">정의는 기본 템플릿 파일(`ServiceFabricCluster.json`)에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-147">The definition is stored in the main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="38b47-148">해당 파일을 열고 `loadBalancedAppPort`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="38b47-149">각 포트는 세 개의 아티팩트에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="38b47-150">포트에 대한 TCP 포트 값을 정의하는 템플릿 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="38b47-150">A template variable that defines the TCP port value for the port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="38b47-151">*프로브*는 Azure Load Balancer에서 다른 장치에 장애 조치하기 전에 특정 Service Fabric 노드를 얼마나 자주, 얼마나 오래 사용하려 하는지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-151">A *probe* that defines how frequently and for how long the Azure load balancer attempts to use a specific Service Fabric node before failing over to another one.</span></span> <span data-ttu-id="38b47-152">프로브는 부하 분산 장치 리소스의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-152">The probes are part of the Load Balancer resource.</span></span> <span data-ttu-id="38b47-153">다음은 첫 기본 응용 프로그램 포트에 대한 프로브 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-153">Here is the probe definition for the first default application port:</span></span>
   
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
3. <span data-ttu-id="38b47-154">포트 및 프로브를 함께 연결하여 서비스 패브릭 클러스터 노드 집합에서 부하 분산을 유지할 수 있도록 하는 *부하 분산 규칙* :</span><span class="sxs-lookup"><span data-stu-id="38b47-154">A *load-balancing rule* that ties together the port and the probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
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
   <span data-ttu-id="38b47-155">클러스터에 배포하려고 하는 응용 프로그램이 더 많은 포트를 필요로 하는 경우 추가 프로브 및 부하 분산 규칙 정의를 만들어 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-155">If the applications that you plan to deploy to the cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="38b47-156">Resource Manager 템플릿을 통해 Azure Load Balancer를 사용하는 방법에 대한 자세한 내용은 [템플릿을 사용하여 내부 부하 분산 장치 만들기 시작](../load-balancer/load-balancer-get-started-ilb-arm-template.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38b47-156">For more information on how to work with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-the-template-by-using-visual-studio"></a><span data-ttu-id="38b47-157">Visual Studio를 사용하여 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="38b47-157">Deploy the template by using Visual Studio</span></span>
<span data-ttu-id="38b47-158">`ServiceFabricCluster.param.dev.json` 파일에 모든 필수 매개 변수 값을 저장하면 템플릿을 배포하고 서비스 패브릭 클러스터를 만들 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-158">After you have saved all the required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready to deploy the template and create your Service Fabric cluster.</span></span> <span data-ttu-id="38b47-159">Visual Studio 솔루션 탐색기에서 리소스 그룹 프로젝트를 마우스 오른쪽 단추로 클릭하고 **배포 | 새 배포...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-159">Right-click the resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**.</span></span> <span data-ttu-id="38b47-160">필요한 경우 Visual Studio에서 **리소스 그룹에 배포** 대화 상자를 표시하고 Azure에 인증하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-160">If necessary, Visual Studio will show the **Deploy to Resource Group** dialog box, asking you to authenticate to Azure:</span></span>

![리소스 그룹 대화 상자에 배포][3]

<span data-ttu-id="38b47-162">대화 상자에서 클러스터에 대해 기존 리소스 관리자 리소스 그룹을 선택할 수 있고 새 리소스 그룹을 만들 수 있는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-162">The dialog box lets you choose an existing Resource Manager resource group for the cluster and gives you the option to create a new one.</span></span> <span data-ttu-id="38b47-163">일반적으로 서비스 패브릭 클러스터에 대한 별도 리소스 그룹을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-163">It normally makes sense to use a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="38b47-164">배포 단추를 누르면 Visual Studio에서 템플릿 매개 변수 값을 확인하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-164">After you hit the Deploy button, Visual Studio will prompt you to confirm the template parameter values.</span></span> <span data-ttu-id="38b47-165">**저장** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-165">Hit the **Save** button.</span></span> <span data-ttu-id="38b47-166">한 매개 변수에 지속형 값인 클러스터에 대한 관리자 계정 암호가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-166">One parameter does not have a persisted value: the administrative account password for the cluster.</span></span> <span data-ttu-id="38b47-167">Visual Studio에서 값을 제공하라는 메시지가 표시되면 암호 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-167">You need to provide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="38b47-168">Azure SDK 2.9부터는 Visual Studio에서 배포 중에 **Azure 주요 자격 증명 모음**에서 암호를 읽도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-168">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="38b47-169">템플릿 매개 변수 대화 상자에서 `adminPassword` 매개 변수 텍스트 상자의 오른쪽에는 작은 "열쇠" 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-169">In the template parameters dialog notice that the `adminPassword` parameter text box has a little "key" icon on the right.</span></span> <span data-ttu-id="38b47-170">이 아이콘을 사용하여 기존 주요 자격 증명 모음 암호를 클러스터에 대한 관리 암호로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-170">This icon allows you to select an existing key vault secret as the administrative password for the cluster.</span></span> <span data-ttu-id="38b47-171">먼저 주요 자격 증명 모음의 고급 액세스 정책에서 템플릿 배포에 대한 Azure Resource Manager 액세스를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-171">Just make sure to first enable Azure Resource Manager access for template deployment in the Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="38b47-172">Visual Studio 출력 창에서 배포 프로세스의 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-172">You can monitor the progress of the deployment process in the Visual Studio output window.</span></span> <span data-ttu-id="38b47-173">템플릿 배포가 완료되면 새 클러스터를 사용할 준비가 된 것입니다!</span><span class="sxs-lookup"><span data-stu-id="38b47-173">Once the template deployment is completed, your new cluster is ready to use!</span></span>

> [!NOTE]
> <span data-ttu-id="38b47-174">지금 사용하고 있는 컴퓨터에서 Azure를 관리하는 데 PowerShell을 사용한 적이 없는 경우 약간의 관리 유지 작업을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-174">If PowerShell was never used to administer Azure from the machine that you are using now, you need to do a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="38b47-175">[`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) 명령을 실행하여 PowerShell 스크립팅을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-175">Enable PowerShell scripting by running the [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="38b47-176">개발 컴퓨터인 경우 "제한 없음" 정책이 일반적으로 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-176">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="38b47-177">Azure PowerShell 명령에서 진단 데이터 수집을 허용할지 여부를 결정하고 필요에 따라 [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) 또는 [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx)을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-177">Decide whether to allow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="38b47-178">이렇게 하면 템플릿 배포 중 발생하는 불필요한 프롬프트를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-178">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="38b47-179">오류가 있는 경우 [Azure 포털](https://portal.azure.com/) 로 이동한 후 배포한 리소스 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-179">If there are any errors, go to the [Azure portal](https://portal.azure.com/) and open the resource group that you deployed to.</span></span> <span data-ttu-id="38b47-180">**모든 설정**을 클릭한 다음 설정 블레이드에서 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-180">Click **All settings**, then click **Deployments** on the settings blade.</span></span> <span data-ttu-id="38b47-181">리소스 그룹 배포에 오류가 발생한 경우 여기에 자세한 진단 정보를 남깁니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-181">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="38b47-182">가용성을 유지하고 상태를 보존하기 위해 Service Fabric 클러스터에서 특정 수의 노드가 작동 상태를 유지해야 하며, 이 숫자를 "유지 관리 쿼럼"이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-182">Service Fabric clusters require a certain number of nodes to be up to maintain availability and preserve state - referred to as "maintaining quorum."</span></span> <span data-ttu-id="38b47-183">따라서 [상태 전체 백업](service-fabric-reliable-services-backup-restore.md)을 처음으로 수행하는 경우 외에는 클러스터의 모든 컴퓨터를 종료하는 것은 안전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38b47-183">Therefore, it is not safe to shut down all of the machines in the cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="38b47-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="38b47-184">Next steps</span></span>
* [<span data-ttu-id="38b47-185">Azure 포털을 사용하여 서비스 패브릭 클러스터 설정에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="38b47-185">Learn about setting up Service Fabric cluster using the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="38b47-186">Visual Studio를 사용하여 서비스 패브릭 응용 프로그램을 관리 및 배포하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="38b47-186">Learn how to manage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
