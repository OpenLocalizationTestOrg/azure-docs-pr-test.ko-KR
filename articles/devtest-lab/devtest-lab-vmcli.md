---
title: "aaaCreate Azure CLI와 DevTest Labs에서 가상 컴퓨터 및 관리 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure DevTest Labs toocreate Azure CLI 2.0과 함께 가상 컴퓨터 및 관리"
services: devtest-lab,virtual-machines
documentationcenter: na
author: lisawong19
manager: douge
editor: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: liwong
ms.openlocfilehash: 98ea3aa7b2489bff61971573aaf584984cd811e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a><span data-ttu-id="4a7bb-103">만들고 hello Azure CLI를 사용 하 여 DevTest Labs를 사용 하 여 가상 컴퓨터 관리</span><span class="sxs-lookup"><span data-stu-id="4a7bb-103">Create and manage virtual machines with DevTest Labs using hello Azure CLI</span></span>
<span data-ttu-id="4a7bb-104">이 빠른 시작은 랩에서 개발 컴퓨터를 만들고, 시작하고, 연결하고, 업데이트하고, 정리하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="4a7bb-105">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="4a7bb-105">Before you begin:</span></span>

* <span data-ttu-id="4a7bb-106">랩을 만들지 않은 경우 지침은 [여기](devtest-lab-create-lab.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="4a7bb-107">[CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4a7bb-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="4a7bb-108">toostart, az 로그인 toocreate Azure와의 연결을 실행된 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-108">toostart, run az login toocreate a connection with Azure.</span></span> 

## <a name="create-and-verify-hello-virtual-machine"></a><span data-ttu-id="4a7bb-109">만들고 hello 가상 컴퓨터를 확인</span><span class="sxs-lookup"><span data-stu-id="4a7bb-109">Create and verify hello virtual machine</span></span> 
<span data-ttu-id="4a7bb-110">ssh 인증을 사용하여 Marketplace 이미지에서 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="4a7bb-111">Hello 배치 **lab의 리소스 그룹** hello-리소스 그룹 매개 변수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-111">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="4a7bb-112">Hello-수식 매개 변수를 사용 하 여 수식을 사용 하는 VM toocreate을 원하는 경우 [az 랩 vm 만들기](https://docs.microsoft.com/cli/azure/lab/vm#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-112">If you want toocreate a VM using a formula, use hello --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="4a7bb-113">사용 가능한 VM 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-113">Verify that hello VM is available.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand 'properties($expand=ComputeVm,NetworkInterface)' --query '{status: computeVm.statuses[0].displayStatus, fqdn: fqdn, ipAddress: networkInterface.publicIpAddress}'
```
```json
{
  "fqdn": "lisalabvm.southcentralus.cloudapp.azure.com",
  "ipAddress": "13.85.228.112",
  "status": "Provisioning succeeded"
}
```

## <a name="start-and-connect-toohello-virtual-machine"></a><span data-ttu-id="4a7bb-114">시작 하 고 toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-114">Start and connect toohello virtual machine</span></span>
<span data-ttu-id="4a7bb-115">VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="4a7bb-116">Hello 배치 **lab의 리소스 그룹** hello-리소스 그룹 매개 변수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-116">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="4a7bb-117">Tooa VM 연결: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) 또는 [원격 데스크톱](../virtual-machines/windows/connect-logon.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-117">Connect tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a><span data-ttu-id="4a7bb-118">Hello 가상 컴퓨터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-118">Update hello virtual machine</span></span>
<span data-ttu-id="4a7bb-119">VM 아티팩트 tooa를 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-119">Apply artifacts tooa VM.</span></span>
```azurecli
az lab vm apply-artifacts --lab-name  sampleLabName --name sampleVMName  --resource-group sampleResourceGroup  --artifacts @/artifacts.json
```

```json
[
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-java",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-install-nodejs",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-apt-package",
    "parameters": [
      {
        "name": "packages",
        "value": "abcd"
      },
      {
        "name": "update",
        "value": "true"
      },
      {
        "name": "options",
        "value": ""
      }
    ]
  } 
]
```

<span data-ttu-id="4a7bb-120">Hello 랩에서 사용할 수 있는 아티팩트를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-120">List artifacts available in hello lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a><span data-ttu-id="4a7bb-121">중지 하 고 hello 가상 컴퓨터 삭제</span><span class="sxs-lookup"><span data-stu-id="4a7bb-121">Stop and delete hello virtual machine</span></span>    
<span data-ttu-id="4a7bb-122">VM을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="4a7bb-123">VM을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4a7bb-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]