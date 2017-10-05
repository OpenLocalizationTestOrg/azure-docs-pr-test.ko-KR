---
title: "가상 컴퓨터의 Azure Resource Manager 템플릿 보기 및 사용 | Microsoft Docs"
description: "가상 컴퓨터에서 Azure Resource Manager 템플릿을 사용하여 다른 VM을 만드는 방법을 알아봅니다."
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a759d9ce-655c-4ac6-8834-cb29dd7d30dd
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: tarcher
ms.openlocfilehash: 12cdb61667f77215c894800d5c439235e767a26b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a>가상 컴퓨터의 Azure Resource Manager 템플릿 사용

[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040)을 통해 DevTest Labs에서 VM(가상 컴퓨터)을 만드는 경우 VM을 저장하기 전에 Azure Resource Manager 템플릿을 볼 수 있습니다. 그런 다음 템플릿을 기초로 사용해서 동일한 설정으로 더 많은 랩 VM을 만들 수 있습니다.

이 문서에서는 VM을 만들 때 Resource Manager 템플릿을 보는 방법 및 나중에 템플릿을 배포하여 동일한 VM의 생성을 자동화하는 방법을 설명합니다.

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a>다중 VM 및 단일 VM Resource Manager 템플릿
Resource Manager 템플릿을 사용하여 DevTest Labs에서 VM을 만드는 두 가지 방법은 Microsoft.DevTestLab/labs/virtualmachines 리소스를 프로비전하거나 Microsoft.Commpute/virtualmachines 리소스를 프로비전하는 것입니다. 각 방법은 서로 다른 시나리오에서 사용되며, 필요한 사용 권한도 다릅니다.

- Microsoft.DevTestLab/labs/virtualmachines 리소스 종류(템플릿의 “resource” 속성에 선언됨)를 사용하는 Resource Manager 템플릿은 개별 랩 VM을 프로비전할 수 있습니다. 그러면 각 VM이 DevTest Labs 가상 컴퓨터 목록에서 단일 항목으로 표시됩니다.

   ![DevTest Labs 가상 컴퓨터 목록에서 단일 항목으로 표시되는 VM 목록](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   이 형식의 Resource Manager 템플릿은 Azure PowerShell 명령 **New-AzureRmResourceGroupDeployment** 또는 Azure CLI 명령 **az group deployment create**를 통해 프로비전할 수 있습니다. 관리자 권한이 필요하므로 DevTest Labs 사용자 역할이 할당된 사용자는 배포를 수행할 수 없습니다. 

- Microsoft.Compute/virtualmachines 리소스 종류를 사용하는 Resource Manager 템플릿은 여러 VM을 DevTest Labs 가상 컴퓨터 목록의 단일 환경으로 프로비전할 수 있습니다.

   ![DevTest Labs 가상 컴퓨터 목록에서 단일 항목으로 표시되는 VM 목록](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   동일한 환경의 VM은 함께 관리할 수 있으며, 동일한 수명 주기를 공유합니다. DevTest Labs 사용자 역할이 할당된 사용자는 이러한 템플릿을 사용하여 환경을 만들 수 있지만 관리자가 해당 방식으로 랩을 구성한 경우에만 가능합니다.

이 문서의 나머지 부분에서는 Mirosoft.DevTestLab/labs/virtualmachines를 사용하는 Resource Manager 템플릿에 대해 설명합니다. 이러한 템플릿은 랩 관리자가 랩 VM 생성(예: 클레임 가능한 VM) 또는 골든 이미지 생성(예: 이미지 팩터리)을 자동화하는 데 사용됩니다.

[Azure Resource Manager 템플릿 작성에 대한 모범 사례](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)에 안정적이고 사용하기 쉬운 Azure Resource Manager 템플릿을 만드는 데 도움이 되는 다양한 지침과 제안이 나와 있습니다.

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a>가상 컴퓨터의 Resource Manager 템플릿 보기 및 저장
1. [랩에서 첫 번째 VM 만들기](devtest-lab-create-first-vm.md)의 단계에 따라 가상 컴퓨터 생성을 시작합니다.
1. 가상 컴퓨터에 대한 필요한 정보를 입력하고 이 VM에 사용하려는 아티팩트를 모두 추가합니다.
1. 설정 구성 창의 맨 아래에서 **ARM 템플릿 보기**를 선택합니다.

   ![ARM 템플릿 보기 단추](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. 나중에 다른 가상 컴퓨터를 만드는 데 사용할 Resource Manager 템플릿을 복사하고 저장합니다.

   ![나중에 사용하기 위해 저장할 Resource Manager 템플릿](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

Resource Manager 템플릿을 저장한 후 먼저 템플릿의 매개 변수 섹션을 업데이트해야 템플릿을 사용할 수 있습니다. 실제 Resource Manager 템플릿 외부에서 매개 변수만 사용자 지정하는 parameter.json을 만들 수 있습니다. 

![JSON 파일을 사용하여 매개 변수 사용자 지정](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-to-create-a-vm"></a>Resource Manager 템플릿을 배포하여 VM 만들기
Resource Manager 템플릿을 저장하고 요구에 맞게 사용자 지정한 후 이 템플릿을 사용하여 VM 생성을 자동화할 수 있습니다. [Resource Manager 템플릿 및 Azure PowerShell을 사용하여 리소스 배포](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)에서는 Resource Manager 템플릿과 함께 Azure PowerShell을 사용하여 Azure에 리소스를 배포하는 방법을 설명합니다. [Resource Manager 템플릿 및 Azure CLI를 사용하여 리소스 배포](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli)에서는 Resource Manager 템플릿과 함께 Azure CLI를 사용하여 Azure에 리소스를 배포하는 방법을 설명합니다.

> [!NOTE]
> 랩 소유자 권한을 가진 사용자만 Azure PowerShell을 사용하여 Resource Manager 템플릿에서 VM을 만들 수 있습니다. Resource Manager 템플릿을 사용하여 VM 생성을 자동화하려고 하는데 사용자 권한만 있는 경우 [CLI의 **az lab vm create** 명령](https://docs.microsoft.com/cli/azure/lab/vm#create)을 사용할 수 있습니다.

### <a name="next-steps"></a>다음 단계
* [Resource Manager 템플릿으로 다중 VM 환경을 만드는](devtest-lab-create-environment-from-arm.md) 방법을 알아봅니다.
* [공용 DevTest Labs GitHub 리포지토리](https://github.com/Azure/azure-quickstart-templates)에서 DevTest Labs 자동화를 위한 기타 빠른 시작 Resource Manager 템플릿을 살펴봅니다.
