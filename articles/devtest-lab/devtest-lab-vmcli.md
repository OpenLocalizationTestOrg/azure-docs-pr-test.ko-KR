---
title: "Azure CLI를 사용하여 DevTest Labs에서 가상 컴퓨터 만들기 및 관리 | Microsoft Docs"
description: "Azure DevTest Labs를 사용하여 Azure CLI 2.0에서 가상 컴퓨터를 만들고 관리하는 방법을 알아봅니다."
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
ms.openlocfilehash: 42b0448c1bcdfa909715abd5075353d63cab8389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-the-azure-cli"></a><span data-ttu-id="d3d0b-103">Azure CLI를 사용하여 DevTest Labs에서 가상 컴퓨터 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="d3d0b-103">Create and manage virtual machines with DevTest Labs using the Azure CLI</span></span>
<span data-ttu-id="d3d0b-104">이 빠른 시작은 랩에서 개발 컴퓨터를 만들고, 시작하고, 연결하고, 업데이트하고, 정리하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="d3d0b-105">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d3d0b-105">Before you begin:</span></span>

* <span data-ttu-id="d3d0b-106">랩을 만들지 않은 경우 지침은 [여기](devtest-lab-create-lab.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="d3d0b-107">[CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d3d0b-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="d3d0b-108">시작하려면 az login을 실행하여 Azure와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-108">To start, run az login to create a connection with Azure.</span></span> 

## <a name="create-and-verify-the-virtual-machine"></a><span data-ttu-id="d3d0b-109">가상 컴퓨터 만들기 및 확인</span><span class="sxs-lookup"><span data-stu-id="d3d0b-109">Create and verify the virtual machine</span></span> 
<span data-ttu-id="d3d0b-110">ssh 인증을 사용하여 Marketplace 이미지에서 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="d3d0b-111">**랩의 리소스 그룹** 이름을 --resource-group 매개 변수에 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-111">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="d3d0b-112">수식을 사용하여 VM을 만들려는 경우 [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create)에서 --formula 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-112">If you want to create a VM using a formula, use the --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="d3d0b-113">VM을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-113">Verify that the VM is available.</span></span>
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

## <a name="start-and-connect-to-the-virtual-machine"></a><span data-ttu-id="d3d0b-114">가상 컴퓨터 시작 및 연결</span><span class="sxs-lookup"><span data-stu-id="d3d0b-114">Start and connect to the virtual machine</span></span>
<span data-ttu-id="d3d0b-115">VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="d3d0b-116">**랩의 리소스 그룹** 이름을 --resource-group 매개 변수에 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-116">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="d3d0b-117">VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) 또는 [원격 데스크톱](../virtual-machines/windows/connect-logon.md)에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-117">Connect to a VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-the-virtual-machine"></a><span data-ttu-id="d3d0b-118">가상 컴퓨터 업데이트</span><span class="sxs-lookup"><span data-stu-id="d3d0b-118">Update the virtual machine</span></span>
<span data-ttu-id="d3d0b-119">VM에 아티팩트를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-119">Apply artifacts to a VM.</span></span>
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

<span data-ttu-id="d3d0b-120">랩에서 사용할 수 있는 아티팩트를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-120">List artifacts available in the lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-the-virtual-machine"></a><span data-ttu-id="d3d0b-121">가상 컴퓨터 중지 및 삭제</span><span class="sxs-lookup"><span data-stu-id="d3d0b-121">Stop and delete the virtual machine</span></span>    
<span data-ttu-id="d3d0b-122">VM을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="d3d0b-123">VM을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d3d0b-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]