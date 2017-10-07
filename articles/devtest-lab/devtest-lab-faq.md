---
title: aaaAzure DevTest Labs FAQ | Microsoft Docs
description: "Toocommon Azure DevTest Labs 질문 대답을 확인"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: afe83109-b89f-4f18-bddd-b8b4a30f11b4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: tarcher
ms.openlocfilehash: 07d4c870eca21856750a472ed503de4a2734a438
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-devtest-labs-faq"></a>Azure DevTest Labs FAQ
이 문서 hello Azure DevTest Labs에 대 한 가장 일반적인 질문과 대답을 제공 합니다.

**일반**
## <a name="what-if-my-question-isnt-answered-here"></a>여기서 내 질문에 대답하지 않으면 어떻게 하나요?
찾는 질문이 여기에 없으면 저희에게 알려주세요. 답변을 찾을 수 있도록 도와드리겠습니다.

* Hello에 질문을 게시 [Disqus 스레드](#comments) hello 끝이 FAQ에 hello Azure 캐시 팀 및 다른 커뮤니티 구성원 들이 문서에 대 한 의견을 교환 하 고 있습니다.
* hello에 질문을 게시 하는 넓은 audience tooreach [Azure DevTest Labs MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureDevTestLabs), hello Azure DevTest Labs 팀과 hello 커뮤니티의 다른 구성원에 문의 하 고 있습니다.
* toomake 기능 요청 제출 요청 및 아이디어 toohello [Azure DevTest Labs 사용자 음성](https://feedback.azure.com/forums/320373-azure-devtest-labs)합니다.

## <a name="why-should-i-use-azure-devtest-labs"></a>Azure DevTest Labs를 사용해야 하는 이유는 무엇인가요?
Azure DevTest Labs를 통해 팀 시간과 비용을 절약할 수 있습니다. 개발자가 다양 한 기반의 사용 하 여 자신의 환경 만들고 tooquickly 배포 및 응용 프로그램을 구성 하는 아티팩트를 사용할 수 있습니다. 사용자 지정 이미지 및 수식을 사용하여 가상 컴퓨터는 템플릿으로 저장되어 쉽게 재현될 수 있습니다. 또한 랩 랩 관리자가 tooreduce 낭비 하 고 팀의 환경 관리를 허용 하는 구성 가능한 여러 가지 정책을 제공 합니다. 이러한 정책에는 자동 종료, 비용 임계값, 사용자당 최대 VM 및 최대 VM 크기가 포함됩니다. 읽을 hello에 대 한 심도 있는 설명은 Azure DevTest Labs, [개요](devtest-lab-overview.md) 또는 조사식 hello [소개 비디오](/documentation/videos/videos/what-is-azure-devtest-labs)합니다.

## <a name="what-does-worry-free-self-service-mean"></a>"걱정 없는 무료, 셀프 서비스"는 무슨 의미인가요?
"걱정 없는 셀프 서비스" 개발자와 테스터 필요에 따라 자신의 환경을 만드는 관리자가 Azure DevTest Labs를 최소화할 수 있는지 알 낭비 되 고 비용을 제어 hello 보안을 의미 합니다. 관리자는 hello 최대 Vm 수는 VM 크기 허용 여부와 Vm의 시작 및 종료할 때 지정할 수 있습니다. Azure DevTest Labs을 사용 하면 쉽게 toomonitor 비용 및 설정 경고 toostay 리소스 hello 랩에서 사용 되는 방식을 알고 있습니다.

## <a name="how-can-i-use-azure-devtest-labs"></a>Azure DevTest Labs를 어떻게 사용할 수 있나요?
필요한 개발 또는 테스트 환경에서는 고 tooreproduce 하려는 언제 든 지 azure DevTest Labs 유용 합니다. 이러한 신속 하 게 정책을 저장 하는 비용으로 관리 및/또는 합니다.

고객이 Azure DevTest Labs를 사용하는 몇 가지 시나리오는 다음과 같습니다.

* 한 곳에서 개발 및 테스트 환경 관리, 정책 tooreduce 비용 및 사용자 지정 이미지 tooshare 사용 하 여 hello 팀에서 빌드를 합니다.
* 사용자 지정 이미지 toosave hello 디스크 상태 hello 개발 단계를 사용 하 여 응용 프로그램을 개발 합니다.
* 관계 tooprogress에 hello 비용을 추적 합니다.
* 품질 보증 테스트에 대한 대량 테스트 환경 만들기.
* 아티팩트 및 수식 tooeasily를 사용 하 여 구성 하 고 다양 한 환경에서 응용 프로그램을 재현 합니다.
* Hackathons (공동 개발 또는 테스트 작업)에 대 한 Vm을 배포 하 고 쉽게 프로 비전 해제에 hello 이벤트 종료 될 때입니다.

## <a name="how-am-i-billed-for-azure-devtest-labs"></a>Azure DevTest Labs에 대한 요금은 어떻게 청구되나요?
Azure DevTest Labs는 무료 서비스 랩을 만들고 hello 정책, 템플릿 및 아티팩트 구성는 무료입니다. 가상 컴퓨터, 저장소 계정 및 가상 네트워크와 같은 환경에서 내에서 사용 하는 Azure 리소스 hello에 대해서만 지불 합니다. 랩 리소스의 hello 비용에 자세한 내용은 참고 [Azure DevTest Labs 가격](https://azure.microsoft.com/pricing/details/devtest-lab/)합니다.


**보안**
## <a name="what-are-hello-different-security-levels-in-azure-devtest-labs"></a>DevTest Labs Azure의에서 hello 다른 보안 수준은 무엇 인가요?
보안 액세스는 [Azure 역할 기반 액세스 제어(RBAC)](../active-directory/role-based-access-built-in-roles.md)를 통해 결정됩니다. toounderstand works 액세스 하는 방법을, RBAC에 정의 된 대로 toounderstand hello 간의 차이점 권한, 역할, 범위는 데 도움이 됩니다.

* **사용 권한** -사용 권한은 정의 된 액세스 tooa 특정 작업입니다. 예를 들어 사용 권한을 읽기 액세스 tooall 가상 컴퓨터를 수 있습니다.
* **역할** -역할은 그룹화 하 고 할당 된 tooa 사용자 수 있는 사용 권한 집합입니다. 예를 들어 "구독 소유자"에 게는 구독 내의 tooall 리소스에 액세스 합니다.
* **범위** -범위는 Azure 리소스의 hello 계층 내의 수준입니다. 예를 들어 범위를 리소스 그룹 또는 단일 랩 또는 hello 전체 구독 수 있습니다.

DevTest Labs Azure의 hello 범위는 두 가지 유형의 역할 toodefine 사용자의 사용 권한: 랩 소유자 및 랩 사용자입니다.

* **랩 소유자** -랩 소유자에 게 hello hello 랩에서 tooany 리소스에 액세스 합니다. 따라서 있습니다 수 정책 수정, 읽기 및 쓰기 Vm, hello 가상 네트워크를 변경 등에입니다.
* **랩 사용자** - 랩 사용자는 VM, 정책 및 가상 네트워크와 같은 모든 랩 리소스를 볼 수 있지만 정책 또는 다른 사용자가 만든 VM을 수정할 수 없습니다. Azure DevTest Labs에 사용자 지정 역할 가능한 toocreate 이기도 및 학습할 수 있는 방법을 hello 문서의 toodo [toospecific 랩 정책 사용자 권한 부여](devtest-lab-grant-user-permissions-to-specific-lab-policies.md)합니다.

범위는 계층적이므로 사용자가 특정 범위에서 사용 권한을 가진 경우 포함된 모든 하위 수준 범위에서 해당 사용 권한이 자동으로 부여됩니다. 예를 들어, 사용자가 구독 소유자의 toohello 역할에 할당 한 경우 다음 있는데 tooall 리소스 액세스는 구독에 이러한 리소스에는 모든 가상 컴퓨터, 모든 가상 네트워크 및 모든 랩이 포함됩니다. 따라서 구독 소유자는 자동으로 랩 소유자의 hello 역할을 상속합니다. 그러나 hello 반대 사실이 아닙니다. 랩 소유자에 게는 hello 구독 수준 보다 낮은 범위 tooa 랩에 액세스 합니다. 따라서 랩 소유자 수 toosee 가상 컴퓨터 또는 가상 네트워크 또는 랩 hello 외부에 있는 모든 리소스 하지 않습니다.

## <a name="how-do-i-create-a-role-tooallow-users-tooperform-a-specific-task"></a>역할 tooallow 사용자 tooperform 특정 작업으로 만드는 방법
어떻게 toocreate 사용자 지정 역할 및 사용 권한 toothat 역할 할당 있어야 하는 방법에 대 한 포괄적인 아티클. "DevTest Labs 고급 사용자", 권한 toostart 개이고 hello 랩에 있는 모든 Vm을 중지 하는 hello 역할을 만드는 스크립트의 예는 다음과 같습니다.

    $policyRoleDef = Get-AzureRmRoleDefinition "DevTest Labs User"
    $policyRoleDef.Actions.Remove('Microsoft.DevTestLab/Environments/*')
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "DevTest Labs Advance User"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("subscriptions/<subscription Id>")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Start/action")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Stop/action")
    $policyRoleDef = New-AzureRmRoleDefinition -Role $policyRoleDef  


**CI/CD 통합 및 자동화**
## <a name="does-azure-devtest-labs-integrate-with-my-cicd-toolchain"></a>Azure DevTest Labs는 CI/CD 도구 체인과 통합되나요?
VSTS를 사용 하는 경우는 [Azure DevTest Labs 작업 확장](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) tooautomate 릴리스 파이프라인 DevTest Labs Azure에서에서 사용할 수 있는 합니다. 이 확장의 hello 용도 중 일부는 다음과 같습니다.

* 만들기 및 VM을 자동으로 배포 및 PowerShell VSTS 또는 Azure 파일 복사 작업을 사용 하 여 hello 최신 빌드를 사용 하 여 구성 합니다.
* 추가 조사를 위해 동일한 VM hello tooreproduce 버그에서 테스트 한 후에 VM의 hello 상태를 자동으로 캡처.
* Hello 삭제 VM hello hello 끝날 때 해제 파이프라인 더 이상 필요 합니다.

hello 다음 블로그 게시물 지침과 제공 hello VSTS 확장을 사용 하는 방법에 대 한 정보:

* [Azure DevTest Labs – VSTS 확장](https://blogs.msdn.microsoft.com/devtestlab/2016/06/15/azure-devtest-labs-vsts-extension/)
* [VSTS에서 기존 AzureDevTestLab의 새 VM 배포](http://www.visualstudiogeeks.com/blog/DevOps/Deploy-New-VM-To-Existing-AzureDevTestLab-From-VSTS)
* [VSTS 릴리스 관리를 사용 하 여 연속 배포 tooAzureDevTestLabs에 대 한](http://www.visualstudiogeeks.com/blog/DevOps/Use-VSTS-ReleaseManagement-to-Deploy-and-Test-in-AzureDevTestLabs)

다른 CI/CD toolchains에 대 한 모든 hello 앞에서 언급 한 hello VSTS 작업 확장 배포를 통해 마찬가지로 구현할 수 있습니다를 통해 구현할 수 있는 시나리오 [Azure 리소스 관리자 템플릿을](https://aka.ms/dtlquickstarttemplate) 를 사용 하 여 [ Azure PowerShell cmdlet](../azure-resource-manager/resource-group-template-deploy.md) 및 [.NET Sdk](https://www.nuget.org/packages/Microsoft.Azure.Management.DevTestLabs/)합니다. 사용할 수도 있습니다 [DevTest Labs에 대 한 REST Api](http://aka.ms/dtlrestapis) toointegrate 프로그램 도구 체인으로 합니다.  


**가상 컴퓨터**
## <a name="why-cant-i-see-certain-vms-in-hello-azure-virtual-machines-blade-that-i-see-within-azure-devtest-labs"></a>특정 Vm에서 DevTest Labs Azure 내에서 표시 하는 hello Azure 가상 컴퓨터 블레이드 보이지 않는 이유
권한에 DevTest Labs Azure에서는 VM을 만들 때 tooaccess 해당 VM을 제공 합니다. Tooview 수는 모두 hello 랩 블레이드 및 hello **가상 컴퓨터** 블레이드입니다. Hello DevTest Labs 역할의 사용자가 hello 랩 통해 hello 랩에서 만든 모든 가상 컴퓨터를 볼 수 **모든 가상 컴퓨터** 블레이드입니다. 그러나 hello DevTest Labs 역할의 사용자에에서 대 한 읽기 액세스 tooVM 리소스를 다른 사람이 만든을 자동으로 부여 되지 않습니다. 따라서 이러한 Vm hello에 표시 되지 않는 **가상 컴퓨터** 블레이드입니다.

## <a name="what-is-hello-difference-between-custom-images-and-formulas"></a>사용자 지정 이미지와 수식을 hello 차이 무엇입니까?
사용자 지정 이미지는 VHD(가상 하드 디스크)인 반면 수식은 저장하고 재현할 수 있는 추가 설정으로 구성할 수 있는 이미지입니다. 이미지를 사용자 지정 하려는 경우 tooquickly hello로 만들에 여러 환경을 더 적합할 수 있습니다 같은 기본, 변경할 수 없는 이미지입니다. 수식은 hello 최신 비트로, 가상 네트워크/서브넷 또는 특정 크기와 VM의 tooreproduce hello 구성 하려는 경우 더 나은 수 있습니다. 에 대 한 자세한 설명은 hello 문서를 참조 [DevTest Labs의 수식 및 사용자 지정 이미지 비교](devtest-lab-comparing-vm-base-image-types.md)합니다.

## <a name="how-do-i-create-multiple-vms-from-hello-same-template-at-once"></a>어떻게 만드나요 여러 Vm hello에서 한 번에 같은 템플릿?
Hello를 사용할 수 있습니다 [VSTS 작업 확장](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) 또는 [Azure 리소스 관리자 템플릿을 생성할](devtest-lab-add-vm.md#save-azure-resource-manager-template) VM을 만드는 동안 및 [Windows PowerShell에서 Azure 리소스 관리자 템플릿을 hello 배포 ](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="how-do-i-move-my-existing-azure-vms-into-my-azure-devtest-labs-lab"></a>기존 Azure VM을 Azure DevTest Labs 랩으로 어떻게 이동하나요?
프로그램 기존 Vm tooAzure DevTest Labs hello 단계 toocopy 아래 키를 따르세요.

1. 이 사용 하 여 기존 VM의 hello VHD 파일을 복사 [Windows PowerShell 스크립트](https://github.com/Azure/azure-devtestlab/blob/master/Scripts/CopyVHDFromVMToLab.ps1)
2. [Hello 사용자 지정 이미지 만들기](devtest-lab-create-template.md) Azure DevTest Labs 랩 내 합니다.
3. 사용자 지정 이미지에서 hello 랩에는 VM 만들기

## <a name="can-i-attach-multiple-disks-toomy-vms"></a>여러 디스크 toomy Vm에 연결할 수 있나요?
연결 하는 여러 개의 디스크 tooVMs 지원 됩니다.  

## <a name="if-i-want-toouse-a-windows-os-image-for-my-testing-do-i-have-toopurchase-an-msdn-subscription"></a>내 테스트에 대 한 toouse Windows 운영 체제 이미지를 원하는 경우 용량은 toopurchase MSDN 구독
사용자가 개발 하거나 Azure에서 테스트에 대 한 toouse Windows 클라이언트 운영 체제 이미지 (Windows 7 이상) 해야 할 경우 다음 예, 해야 합니다.

- [MSDN 구독을 구입하세요](https://www.visualstudio.com/products/how-to-buy-vs).
- 기업 계약을 설정한 경우 생성 된 Azure 구독은 hello로 [엔터프라이즈 개발/테스트 제공](https://azure.microsoft.com/en-us/offers/ms-azr-0148p)합니다.

Hello에 대 한 자세한 내용은 각 MSDN 제공에 대 한 Azure 크레딧 참조 [Visual Studio 구독자에 대 한 월간 Azure 크레딧](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/)합니다.

## <a name="how-do-i-automate-hello-process-of-uploading-vhd-files-toocreate-custom-images"></a>사용자 지정 이미지를 toocreate VHD 파일 업로드 hello 프로세스를 자동화 하는 방법
두 가지 옵션이 있습니다.

* [Azure AzCopy](../storage/common/storage-use-azcopy.md#blob-upload) 사용된 toocopy 하거나 hello 랩와 연결 된 VHD 파일 toohello 저장소 계정을 업로드할 수 있습니다.
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) 는 Windows, OSX 및 Linux에서 실행되는 독립 실행형 앱입니다.   

toofind hello 대상 저장소 계정에 연결 된 랩에는 다음이 단계를 따르십시오.

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
2. 선택 **리소스 그룹** hello 왼쪽된 패널에서 합니다.
3. 찾아 랩와 연결 된 hello 리소스 그룹을 선택 합니다.
4. Hello에 **개요** 블레이드에서 hello 저장소 계정 중 하나를 선택 합니다.
5. **Blob**을 선택합니다.
6. Hello 목록에서 업로드를 찾습니다. 없을 경우 tooStep # 4를 반환 하 고 다른 저장소 계정 사용을 시도 합니다.
7. 사용 하 여 hello **URL** AzCopy 명령에 대상으로 합니다.

## <a name="how-can-i-automate-hello-process-of-deleting-all-hello-vms-in-my-lab"></a>내 랩의 모든 hello Vm을 삭제할 경우의 hello 프로세스를 자동화할 수는 방법
또한 Vm에서 hello Azure 포털에서에서 랩 toodeleting, PowerShell 스크립트를 사용 하 여 랩에서 모든 hello Vm를 삭제할 수 있습니다. Hello에서 hello에서 hello 매개 변수 값을 수정 다음 예제를 **값 toochange** 메모 합니다. Hello를 검색할 수 있습니다 `subscriptionId`, `labResourceGroup`, 및 `labName` hello Azure 포털에서에서 hello 랩 블레이드의 값으로에서.

    # Delete all hello VMs in a lab

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource group here>"
    $labName = "<Enter lab name here>"

    # Login tooyour Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. This step is optional
    # if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Get hello lab that contains hello VMs toodelete.
    $lab = Get-AzureRmResource -ResourceId ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)

    # Get hello VMs from that lab.
    $labVMs = Get-AzureRmResource | Where-Object {
              $_.ResourceType -eq 'microsoft.devtestlab/labs/virtualmachines' -and
              $_.ResourceName -like "$($lab.ResourceName)/*"}

    # Delete hello VMs.
    foreach($labVM in $labVMs)
    {
        Remove-AzureRmResource -ResourceId $labVM.ResourceId -Force
    }

**아티팩트**
## <a name="what-are-artifacts"></a>아티팩트는 무엇입니까?
아티팩트는 VM으로 최신 프로그램 파일 또는 프로그램 개발자 도구 사용된 toodeploy 수 있는 사용자 지정 가능한 요소입니다. 연결 된 tooyour VM 몇 번를 만드는 동안 이며 hello VM이 프로 비전 되 면 hello 아티팩트를 배포 및 VM을 구성 합니다. [공용 GitHub 리포지토리](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts)에 다양한 기존 아티팩트가 있지만 손쉽게 [사용자 고유의 아티팩트](devtest-lab-artifact-author.md)를 작성할 수도 있습니다.


**랩 구성**
## <a name="how-do-i-create-a-lab-from-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿에서 어떻게 랩을 만듭니까?
제공 된 [랩 Azure 리소스 관리자 템플릿 GitHub 리포지토리](https://aka.ms/dtlquickstarttemplate) 으로 배포할 수 있는-되었거나 toocreate 환경에서 사용자 지정 템플릿을 수정 합니다. Toodeploy hello 랩을 클릭할 수 있는 링크를 포함 하는 이러한 각 템플릿은-사용자의 Azure 구독 중인 hello 서식 파일을 사용자 지정할 수 있습니다 및 [PowerShell 또는 Azure CLI를 사용 하 여 배포](../azure-resource-manager/resource-group-template-deploy.md)합니다.

## <a name="why-are-my-vms-created-in-different-resource-groups-with-arbitrary-names-can-i-rename-or-modify-these-resource-groups"></a>서로 다른 리소스 그룹에서 만들어진 VM이 임의의 이름을 갖는 이유는 무엇인가요? 이름을 변경하거나 이러한 리소스 그룹을 수정할 수 있습니까?
리소스 그룹은 Azure DevTest Labs toomanage hello 사용자 권한 및 액세스 toovirtual 컴퓨터에 대 한 순서로 이러한 방식으로 만들어집니다. 원하는 이름으로 hello VM tooanother 리소스 그룹 이동, 하지만 이렇게 하면 되므로 권장 되지 않습니다. 작업을이 경험 tooallow 더 많은 유연성을 개선 합니다.   

## <a name="how-many-labs-can-i-create-under-hello-same-subscription"></a>개수 랩 hello에서 만들 수 있나요 동일한 구독?
구독 당 만들 수 있는 랩 hello 수에는 특정 제한은 없습니다. 그러나 사용 하는 hello 리소스 구독 당 제한 됩니다. Hello에 대 한 읽을 수 [Azure 구독에 적용 된 제한 및 할당량](../azure-subscription-service-limits.md) 및 [어떻게 tooincrease 이러한 제한을](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests)합니다.

## <a name="how-many-vms-can-i-create-per-lab"></a>랩당 얼마나 많은 VM을 만들 수 있습니까?
랩 당 만들 수 있는 Vm의 hello 수에는 특정 제한은 없습니다. 그러나 사용 하는 hello 리소스 구독 당 제한 됩니다 (예: VM 코어 공개 Ip 등.). Hello에 대 한 읽을 수 [Azure 구독에 적용 된 제한 및 할당량](../azure-subscription-service-limits.md) 및 [어떻게 tooincrease 이러한 제한을](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests)합니다.

## <a name="how-do-i-share-a-direct-link-toomy-lab"></a>직접 링크 toomy 랩을 공유 하려면 어떻게 해야 합니까?
직접 링크 tooshare tooyour 랩 사용자 hello 절차를 수행할 수 있습니다.

1. Toohello 랩을 hello Azure 포털에서에서 찾습니다.
2. 브라우저에서 hello 랩 URL을 복사 하 고 랩 사용자와 공유할 합니다.

> [!NOTE]
> 랩 사용자에 게는 외부 사용자에 게 하는 경우는 [Microsoft 계정](#what-is-a-microsoft-account) 및 tooyour 회사의 Active directory 속해, toohello 제공 된 링크를 탐색할 때 오류가 나타날 수 있습니다. 오류를 받을 경우 지시의 hello 오른쪽 위 모퉁이 있는 이름을 hello Azure 포털 및 hello hello 랩이 존재 하는 위치 선택 hello 디렉터리 tooclick **디렉터리** hello 메뉴의 섹션입니다.
>
>

## <a name="what-is-a-microsoft-account"></a>Microsoft 계정이란?
Microsoft 계정이란 Microsoft 장치 및 서비스를 가지고 하는 거의 모든 것에 대해 사용하는 계정입니다. 전자 메일 주소와 암호 toosign tooSkype, Outlook.com, OneDrive, Windows Phone 및 Xbox LIVE-에서 사용 하 여 파일, 사진, 연락처, 의미 및 인지 설정을 tooany 장치 따를 수는

> [!NOTE]
> Microsoft 계정을 사용 toobe "Windows Live ID" 라고 합니다.
>
>


**문제 해결**
## <a name="my-artifact-failed-during-vm-creation-how-do-i-troubleshoot-it"></a>VM 생성 도중 아티팩트가 실패했습니다. 어떻게 해결합니까?
너무 참조[어떻게 DevTest Labs의 toodiagnose 아티팩트 오류](devtest-lab-troubleshoot-artifact-failure.md) toolearn tooobtain 프로그램 실패 한 아티팩트에 대 한 기록 하는 방법입니다.

## <a name="why-isnt-my-existing-virtual-network-saving-properly"></a>기존 가상 네트워크가 제대로 저장되지 않는 이유는 무엇입니까?
한 가지 가능성은 가상 네트워크 이름에 기간이 포함되어 있는 것입니다. 따라서 제거 hello 마침표 또는 이러한 하이픈으로 대체 한 다음 저장 안녕 가상 네트워크.

## <a name="why-do-i-get-a-parent-resource-not-found-error-when-provisioning-a-vm-from-powershell"></a>PowerShell에서 VM을 프로비전할 때 "부모 리소스를 찾을 수 없음" 오류가 표시되는 이유는 무엇인가요?
하나의 리소스 부모 tooanother 리소스인 경우 hello 부모 리소스 hello 자식 리소스를 만들기 전에 존재 해야 합니다. 부모 리소스가 없는 경우 **ParentResourceNotFound** 오류가 표시됩니다. Hello 부모 리소스에 대 한 종속성을 지정 하지 않으면 hello 부모 하기 전에 hello 자식 리소스 배포 될 수 있습니다.

리소스 그룹의 랩에서 VM은 자식 리소스입니다. PowerShell 통해 Azure 리소스 관리자 템플릿 toodeploy를 사용 하면 PowerShell 스크립트 hello에 제공 된 hello 리소스 그룹 이름에는 hello 랩의 hello 리소스 그룹 이름 이어야 합니다. 자세한 내용은 [일반적인 Azure 배포 문제 해결 ](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-common-deployment-errors#parentresourcenotfound)를 참조하세요.

## <a name="where-can-i-find-more-error-information-if-a-vm-deployment-fails"></a>VM 배포에 실패하면 오류 정보를 어디에서 더 찾을 수 있나요?
VM 배포 오류 hello 활동 로그에 캡처됩니다. 랩 hello 통해 Vm 활동 로그를 찾을 수 있습니다 **감사 로그** 또는 **가상 컴퓨터 진단** hello 랩 VM 블레이드에서 hello 리소스 메뉴 (hello 블레이드 에서VMhello를선택한후표시**내 가상 컴퓨터** 목록).

경우에 따라 hello 배포 오류 VM hello를 사용 하 여 만든 리소스에 대 한 hello 구독 제한을 초과 하는 경우 같은-hello VM 배포를 시작 하기 전에 발생 합니다. Hello 오류 세부 정보 hello 랩 수준에 기록 되는 경우 **활동 로그** hello hello 맨 아래에 찾을 수 있는 **구성 및 정책** 설정 합니다. 활동을 사용 하는 방법에 대 한 자세한 내용은 Azure을 로그인에 대 한 참조 [리소스에 tooaudit 작업을 기록 하는 활동 보기](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-audit)합니다.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]
