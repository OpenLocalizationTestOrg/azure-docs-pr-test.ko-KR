---
title: "aaaCreate 인터넷 연결 부하 분산 장치-Azure 템플릿 | Microsoft Docs"
description: "어떻게 toocreate 인터넷 연결 부하 분산 장치 템플릿을 사용 하는 리소스 관리자에 알아봅니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="1e5e1-103">템플릿을 사용하여 인터넷 연결 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="1e5e1-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e5e1-104">포털</span><span class="sxs-lookup"><span data-stu-id="1e5e1-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="1e5e1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e5e1-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="1e5e1-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1e5e1-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="1e5e1-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="1e5e1-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="1e5e1-108">이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="1e5e1-109">수도 있습니다 [toocreate 인터넷 연결 부하 분산 장치 클래식 배포 모델을 사용 하는 방법에 대해 알아봅니다](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1e5e1-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="1e5e1-110">Hello 템플릿을 사용 하 여 배포 toodeploy 클릭</span><span class="sxs-lookup"><span data-stu-id="1e5e1-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="1e5e1-111">hello 공용 저장소에서 사용할 수 있는 hello 샘플 템플릿 hello 기본 사용 되는 값 toogenerate hello 위에서 언급 한 시나리오를 포함 하는 매개 변수 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="1e5e1-112">toodeploy toodeploy, 클릭 하 여 사용 하 여이 서식 파일에 따라 [이 링크](http://go.microsoft.com/fwlink/?LinkId=544801), 클릭 **tooAzure 배포**hello 기본 매개 변수 값, 필요한 경우 바꾼 hello 포털의 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-112">toodeploy this template using click toodeploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="1e5e1-113">PowerShell을 사용 하 여 hello 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="1e5e1-114">PowerShell을 사용 하 여 다운로드 한 toodeploy hello 템플릿을 다음 hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="1e5e1-115">Azure PowerShell을 처음 사용 하는 경우 참조 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azure/overview) 모든 hello 방식으로 toohello toosign를 Azure로 끝나고 구독을 선택 하는 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="1e5e1-116">Hello 실행 **새로 AzureRmResourceGroupDeployment** 사용 하 여 리소스 그룹 cmdlet toocreate hello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-116">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="1e5e1-117">Hello Azure CLI를 사용 하 여 hello 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-117">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="1e5e1-118">hello Azure CLI를 사용 하 여 toodeploy hello 템플릿을 다음 hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-118">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="1e5e1-119">Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-119">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="1e5e1-120">Hello 실행 **azure 구성 모드** 명령 tooswitch tooResource 관리자 모드에서는 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-120">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="1e5e1-121">다음은 위의 hello 명령에 대 한 예상 hello 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-121">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="1e5e1-122">브라우저에서 이동 너무[퀵 스타트 템플릿 hello](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules)hello json 파일의 내용을 hello 복사한 컴퓨터에서 새 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-122">From your browser, navigate too[hello Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy hello contents of hello json file and paste into a new file in your computer.</span></span> <span data-ttu-id="1e5e1-123">이 시나리오에서는 있습니다 것 수 값을 복사할 hello 라는 tooa 파일 아래 **c:\lb\azuredeploy.parameters.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-123">For this scenario, you would be copying hello values below tooa file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="1e5e1-124">Hello 실행 **으로 azure 그룹 배포 만들기** cmdlet toodeploy hello 새 부하 분산 장치 hello 템플릿 및 매개 변수를 사용 하 여 파일을 다운로드 하 고 위에서 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-124">Run hello **azure group deployment create** cmdlet toodeploy hello new load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="1e5e1-125">hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5e1-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="1e5e1-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e5e1-126">Next steps</span></span>

[<span data-ttu-id="1e5e1-127">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="1e5e1-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="1e5e1-128">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="1e5e1-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="1e5e1-129">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="1e5e1-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
