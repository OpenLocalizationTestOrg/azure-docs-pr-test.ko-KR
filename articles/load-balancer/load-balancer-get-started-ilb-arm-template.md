---
title: "내부 부하 분산 장치-Azure 템플릿 aaaCreate | Microsoft Docs"
description: "내부 프로그램 toocreate 리소스 관리자에서 서식 파일을 사용 하 여 분산 장치를 로드 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="27c79-103">템플릿을 사용하여 내부 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="27c79-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="27c79-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="27c79-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="27c79-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="27c79-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="27c79-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="27c79-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="27c79-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="27c79-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="27c79-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="27c79-109">사용 하 여이 문서에서는 Microsoft hello 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델 [클래식 배포 모델](load-balancer-get-started-ilb-classic-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="27c79-110">Hello 템플릿을 사용 하 여 배포 toodeploy 클릭</span><span class="sxs-lookup"><span data-stu-id="27c79-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="27c79-111">hello 공용 저장소에서 사용할 수 있는 hello 샘플 템플릿 hello 기본 사용 되는 값 toogenerate hello 위에서 언급 한 시나리오를 포함 하는 매개 변수 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="27c79-112">toodeploy toodeploy, 클릭 하 여 사용 하 여이 서식 파일에 따라 [이 링크](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), 클릭 **tooAzure 배포**hello 기본 매개 변수 값, 필요한 경우 바꾼 hello 포털의 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-112">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="27c79-113">PowerShell을 사용 하 여 hello 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="27c79-114">PowerShell을 사용 하 여 다운로드 한 toodeploy hello 템플릿을 다음 hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="27c79-115">Azure PowerShell을 처음 사용 하는 경우 참조 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azure/overview) 모든 hello 방식으로 toohello toosign를 Azure로 끝나고 구독을 선택 하는 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="27c79-116">Hello 매개 변수 파일 tooyour 로컬 디스크를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-116">Download hello parameters file tooyour local disk.</span></span>
3. <span data-ttu-id="27c79-117">Hello 파일을 편집 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-117">Edit hello file and save it.</span></span>
4. <span data-ttu-id="27c79-118">Hello 실행 **새로 AzureRmResourceGroupDeployment** 사용 하 여 리소스 그룹 cmdlet toocreate hello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="27c79-118">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="27c79-119">Hello Azure CLI를 사용 하 여 hello 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-119">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="27c79-120">hello Azure CLI를 사용 하 여 toodeploy hello 템플릿을 다음 hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-120">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="27c79-121">Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="27c79-122">Hello 실행 **azure 구성 모드** 명령 tooswitch tooResource 관리자 모드에서는 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="27c79-123">다음은 위의 hello 명령에 대 한 예상 hello 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-123">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="27c79-124">Hello 매개 변수 파일을 열고 해당 내용을 선택한 컴퓨터에 tooa 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-124">Open hello parameter file, select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="27c79-125">이 예에서는 저장 hello 매개 변수 파일 너무*parameters.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-125">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="27c79-126">Hello 실행 **으로 azure 그룹 배포 만들기** toodeploy hello 템플릿 및 매개 변수를 사용 하 여 새로운 내부 부하 분산 장치를 hello 명령 파일을 다운로드 하 고 위에서 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-126">Run hello **azure group deployment create** command toodeploy hello new internal load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="27c79-127">hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c79-127">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="27c79-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="27c79-128">Next steps</span></span>

[<span data-ttu-id="27c79-129">원본 IP 선호도를 사용하여 부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="27c79-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="27c79-130">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="27c79-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

