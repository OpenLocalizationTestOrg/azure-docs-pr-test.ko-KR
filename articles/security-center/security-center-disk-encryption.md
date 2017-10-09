---
title: "Azure 가상 컴퓨터 aaaEncrypt | Microsoft Docs"
description: "이 문서 Azure 보안 센터에서 경고를 받은 후 tooencrypt Azure 가상 컴퓨터를 사용 합니다."
services: security, security-center
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: 
ms.assetid: f6c28bc4-1f79-4352-89d0-03659b2fa2f5
ms.service: security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: tomsh
ms.openlocfilehash: 7c7c6eed39d16bde8a0dfaffe3a3331c58101634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-an-azure-virtual-machine"></a>Azure 가상 컴퓨터 암호화
암호화되지 않은 가상 컴퓨터가 있는 경우 Azure 보안 센터에서 알려줍니다. 이러한 경고는 심각도 높은 및 hello 권장 사항으로 표시 됩니다 tooencrypt 이러한 가상 컴퓨터입니다.

![디스크 암호화 권장 사항](./media/security-center-disk-encryption/security-center-disk-encryption-fig1.png)

> [!NOTE]
> 이 문서에서 hello 정보 (이 Azure 백업을 사용 하 여 가상 컴퓨터 백업에 필요한) 키 암호화 키를 사용 하지 않고 tooencrypting 가상 컴퓨터를 적용 합니다. Hello 문서를 참조 하세요 [Azure 디스크 암호화에 대 한 Windows 및 Linux Azure 가상 컴퓨터](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) 방법에 대 한 내용은 toouse 키 암호화 키 toosupport 암호화 된 Azure 가상 컴퓨터에 대 한 Azure 백업 합니다.
>
>

Azure 보안 센터에 의해 암호화는 것으로 확인 된 Azure 가상 컴퓨터 tooencrypt 단계를 수행 하는 hello를 권장 됩니다.

* Azure PowerShell을 설치하고 구성합니다. 이렇게 하면 toorun hello PowerShell 명령을 필요한 tooset hello 필수 구성 요소 필요 tooencrypt Azure 가상 컴퓨터를 구성 합니다.
* 구하여 hello Azure 디스크 암호화 필수 구성 요소가 Azure PowerShell 스크립트를 실행 합니다.
* 가상 컴퓨터 암호화

이 문서의 hello ֲ tooenable 있습니다 tooencrypt 거의 또는 전혀 배경 Azure PowerShell에 있는 경우에 가상 컴퓨터.
이 문서에서는 Azure 디스크 암호화를 구성 하는 hello 클라이언트 컴퓨터와 Windows 10을 사용 하는 가정 합니다.

사용 되는 toosetup hello 필수 구성 요소 및 Azure 가상 컴퓨터에 대 한 tooconfigure 암호화 될 수 있는 방법은 여러 가지가 있습니다. 이미 Azure PowerShell 또는 Azure CLI 잘 알고 있다면 toouse 대체 방법을 할 수도 있습니다.

> [!NOTE]
> Azure 가상 컴퓨터에 대 한 대체 방법 tooconfiguring 암호화에 대해 자세히 toolearn를 참조 하세요 [Azure 디스크 암호화에 대 한 Windows 및 Linux Azure 가상 컴퓨터](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)합니다.
>
>

## <a name="install-and-configure-azure-powershell"></a>Azure PowerShell 설치 및 구성
Azure PowerShell 버전 1.2.1 이상이 컴퓨터에 설치되어야 합니다. hello 문서 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) tooprovision Azure PowerShell을 사용 하 여 컴퓨터 toowork를 해야 하는 모든 hello 단계를 포함 합니다. hello 가장 간단한 방법은 toouse hello 웹 PI 설치 방식에서는 해당 문서에 언급 된 것입니다. 이미 있는 경우에 Azure PowerShell 설치는 최신 버전의 Azure PowerShell hello hello 웹 PI 접근을 사용 하 여 다시 설치 합니다.

## <a name="obtain-and-run-hello-azure-disk-encryption-prerequisites-configuration-script"></a>구하여 hello Azure 디스크 암호화 필수 구성 요소 구성 스크립트 실행
hello Azure 디스크 암호화 필수 구성 요소 구성 스크립트는 Azure 가상 컴퓨터를 암호화 하는 데 필요한 모든 hello 필수를 설정 합니다.

1. Hello 있는 이동 toohello GitHub 페이지 [Azure 디스크 암호화 필수 구성 요소 설치 스크립트](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1)합니다.
2. Hello GibHub 페이지 클릭 hello **Raw** 단추입니다.
3. 사용 하 여 **CTRL A** 모든 tooselect hello hello 페이지에 텍스트를 선택한 다음 **CTRL + C** toocopy 모든 hello hello 페이지 toohello 클립보드에 텍스트입니다.
4. 열기 **메모장** hello 복사한 텍스트를 메모장에 붙여넣습니다.
5. **AzureADEScript**라는 C: 드라이브에 새 폴더를 만듭니다.
6. Hello 메모장 파일을 저장 – 클릭 **파일**, 클릭 **다른 이름으로 저장**합니다. Hello 파일 이름 텍스트 상자에 입력 **"ADEPrereqScript.ps1"** 클릭 **저장**합니다. (hello 이름 주위에 따옴표 hello를 추가할 수 있는지 확인, 그렇지 않으면 hello 파일이.txt 파일 확장명으로 저장 됩니다 것).

Hello 스크립트 콘텐츠를 저장 했으므로 hello 스크립트를 hello PowerShell ISE를 엽니다.

1. 시작 메뉴 hello 클릭 **Cortana**합니다. 요청 **Cortana** "PowerShell"을 입력 하 여 **PowerShell** hello Cortana 검색 텍스트 상자에 있습니다.
2. 마우스 오른쪽 단추로 **Windows PowerShell ISE**를 클릭하고 **관리자 권한으로 실행**을 클릭합니다.
3. Hello에 **관리자: Windows PowerShell ISE** 창 클릭 **보기** 클릭 하 고 **스크립트 창 표시**합니다.
4. Hello 표시 되 면 **명령을** hello 창의 hello 오른쪽 창을 클릭 hello **"x"** hello의 오른쪽 위 모서리 hello 창 tooclose에에서 것입니다. 사용 하 여 hello 텍스트 toosee 하기에 너무 작은 경우 **CTRL + 추가** ("추가"는 hello "+" 기호). 사용 하 여 hello 텍스트 너무 크면 **CTRL + 빼기** (빼기는 hello "-" 기호).
5. **파일**을 클릭한 후 **열기**를 클릭합니다. Toohello 이동 **C:\AzureADEScript** hello에 두 번 클릭 폴더와 hello **ADEPrereqScript**합니다.
6. hello **ADEPrereqScript** 내용을 이제 hello PowerShell ISE에에서 표시 되며 색으로 구분 된 toohelp 명령, 매개 변수 및 변수 등의 다양 한 구성 요소를 보다 쉽게 볼 수 있습니다.

이제 다음과 같이 아래 hello 그림 표시 됩니다.

![PowerShell ISE 창](./media/security-center-disk-encryption/security-center-disk-encryption-fig2.png)

위쪽 창의 hello 참조 tooas hello "스크립트 창" 고 hello 아래쪽 창이 참조 tooas hello "console" 합니다. 이 문서의 뒷부분에서 이러한 용어를 사용합니다.

## <a name="run-hello-azure-disk-encryption-prerequisites-powershell-command"></a>Hello Azure 디스크 암호화 필수 구성 요소 PowerShell 명령 실행
hello Azure 디스크 암호화 필수 구성 요소 스크립트는 hello hello 스크립트를 시작한 후 다음 정보에 대 한 메시지를 표시 합니다.

* **리소스 그룹 이름** -이름 hello tooput 리소스 그룹의 hello를 주요 자격 증명 모음입니다.  절이 없는 경우 이미 만든 해당 이름으로 입력 하는 hello 이름으로 새 리소스 그룹 만들어질 수 있습니다. 이 구독에서 toouse 원하는 리소스 그룹이 이미 있는 경우 해당 리소스 그룹의 hello 이름을 입력 합니다.
* **키 자격 증명 모음 이름** -어떤 암호화 키가 배치 toobe hello 키 자격 증명 모음 이름입니다. 이 이름을 가진 자격 증명 모음 키가 없는 경우 해당 이름을 가진 새 키 자격 증명 모음이 생성됩니다. 키 자격 증명 모음 toouse 원하는 이미 있는 경우 키 자격 증명 모음을 기존 hello hello 이름을 입력 합니다.
* **위치** -hello 자격 증명 모음 키의 위치입니다. 암호화 된 hello 주요 자격 증명 모음 및 Vm toobe hello에 있는지 확인 동일한 위치입니다. 방법을 보여 주는이 문서의 뒷부분에 나오는 단계 hello 위치를 모르는 경우 toofind 아웃 합니다.
* **Azure Active Directory 응용 프로그램 이름** -hello 사용된 toowrite 비밀 toohello 주요 자격 증명 모음 될 Azure Active Directory 응용 프로그램의 이름입니다. 이 이름을 가진 새 응용 프로그램이 없는 경우 생성됩니다. 원하는 toouse Azure Active Directory 응용 프로그램을 이미 보유 하는 경우 Azure Active Directory 응용 프로그램의 hello 이름을 입력 합니다.

> [!NOTE]
> Toocreate Azure Active Directory 응용 프로그램 해야 toowhy로 내용은 참조 하세요 *응용 프로그램을 Azure Active Directory 등록* hello 문서의 섹션 [Azure키자격증명모음시작](../key-vault/key-vault-get-started.md).
>
>

Hello 단계 tooencrypt Azure 가상 컴퓨터를 다음을 수행 합니다.

1. PowerShell ISE hello을 닫은 경우 hello PowerShell ISE의 승격 된 인스턴스를 엽니다. PowerShell ISE 표시 되어 있지 hello 열 경우이 문서의 앞부분에서 hello 지침을 따릅니다. Hello 스크립트를 닫은 경우 다음 hello 엽니다 **ADEPrereqScript.ps1** 클릭 하면 **파일**, 다음 **열고** hello에서 hello 스크립트를 선택 하 고 **c:\ AzureADEScript** 폴더입니다. Hello 시작부터이 문서를 따랐는지 다시 toohello 다음 단계로 이동 합니다.
2. Hello PowerShell ISE (hello PowerShell ISE의 hello 아래쪽 창)의 hello 콘솔에서 입력 하 여 hello 스크립트의 hello 포커스 toohello 로컬 변경 **cd c:\AzureADEScript** 누릅니다 **ENTER**합니다.
3. Hello 스크립트를 실행할 수 있도록 컴퓨터에서 hello 실행 정책을 설정 합니다. 형식 **Set-executionpolicy Unrestricted** 콘솔 hello와 다음 ENTER 키를 누릅니다. Hello 변경 tooexecution 정책의 hello 효과 대 한 알리는 대화 상자가 표시 되 면 클릭 **tooall 예** 또는 **예** (표시 되 면 **tooall 예**를 경우 해당 옵션을 선택 합니다. 표시 되지 않으면 **tooall 예**, 클릭 **예**).
4. Azure 계정에 로그인합니다. Hello 콘솔 입력 **로그인 AzureRmAccount** 누릅니다 **ENTER**합니다. 자격 증명을 입력할 수 있는 대화 상자가 표시 됩니다 (권한 toochange hello 가상 컴퓨터-했는지 확인 권한 없는 수 tooencrypt 되지 것입니다 해당 합니다. 확실하지 않은 경우 구독 소유자 또는 관리자에게 문의합니다.) **환경**, **계정**, **TenantId**, **SubscriptionId** 및 **CurrentStorageAccount**에 대한 정보가 표시됩니다. 복사 hello **SubscriptionId** tooNotepad 합니다. 필요 toouse #6 단계에서 합니다.
5. 어떤 구독이 가상 컴퓨터를 찾을 위치로 tooand 속해 있습니다. 너무 이동[https://portal.azure.com](ttps://portal.azure.com) 로그인 하십시오.  Hello hello 페이지의 왼쪽, 클릭 **가상 컴퓨터**합니다. 가상 컴퓨터와 자신이 속한 hello 구독 목록이 표시 됩니다.

   ![가상 컴퓨터](./media/security-center-disk-encryption/security-center-disk-encryption-fig3.png)
6. PowerShell ISE toohello를 반환 합니다. Hello 스크립트는 실행 하는 hello 구독 컨텍스트를 설정 합니다. Hello 콘솔 입력 **선택 AzureRmSubscription – SubscriptionId < your_subscription_Id >** (대체 **< your_subscription_Id >** 실제 구독 ID로) 키를누릅니다 **입력**합니다. Hello 환경에 대 한 정보가 표시 됩니다 **계정**, **TenantId**, **SubscriptionId** 및 **CurrentStorageAccount**합니다.
7. 준비 toorun hello 스크립트입니다. Hello 클릭 **스크립트 실행** 단추를 클릭 하거나 눌러 **F5** hello 키보드에서.

   ![PowerShell 스크립트 실행](./media/security-center-disk-encryption/security-center-disk-encryption-fig4.png)
8. hello 스크립트에 대 한 요청 **resourceGroupName:** -hello 이름 입력 *리소스 그룹* toouse, 원하는 다음 키를 누릅니다 **ENTER**합니다. 없다면 하나 새 toouse 원하는 이름을 입력 합니다. 이미 있는 경우는 *리소스 그룹* toouse (예: hello 하나에 있는 가상 컴퓨터)를 원하는 hello 기존 리소스 그룹의 hello 이름을 입력 하 합니다.
9. hello 스크립트에 대 한 요청 **keyVaultName:** -hello hello 이름 입력 *키 자격 증명 모음* toouse, 원하는 다음 ENTER 키를 누릅니다. 없다면 하나 새 toouse 원하는 이름을 입력 합니다. 키 자격 증명 모음 toouse 원하는 이미 있는 경우 hello 기존 hello 이름을 입력 *키 자격 증명 모음*합니다.
10. hello 스크립트에 대 한 요청 **위치:** -hello 위치는 hello tooencrypt 원하는 VM의 위치를 가리키는의 hello 이름을 입력 한 다음 키를 눌러 **ENTER**합니다. Hello 위치를 기억 하지 못하는 경우 toostep # 5로 돌아갑니다.
11. hello 스크립트에 대 한 요청 **aadAppName:** -hello hello 이름 입력 *Azure Active Directory* toouse를 만들려는 응용 프로그램 키를 눌러 다음 **ENTER**합니다. 없다면 하나 새 toouse 원하는 이름을 입력 합니다. 이미 있는 경우는 *Azure Active Directory 응용 프로그램* toouse 원하는 hello 기존 hello 이름을 입력 하 *Azure Active Directory 응용 프로그램*합니다.
12. 로그인 대화 상자가 표시됩니다. 자격 증명을 제공 (예, 한 번 로그인 하면 있지만 이제 toodo 필요 다시).
13. hello 스크립트를 실행 하 고 완료 되 면 것을 요청 toocopy hello 값의 hello **aadClientID**, **aadClientSecret**, **diskEncryptionKeyVaultUrl**, 및 **keyVaultResourceId**합니다. 이러한 값 toohello 클립보드의 각 복사한 메모장에 붙여 넣습니다.
14. PowerShell ISE toohello 돌아간 누릅니다 hello 마지막 줄의 hello 끝에 hello 커서를 놓고 **ENTER**합니다.

hello 스크립트의 hello 출력 hello 화면 아래와 같은 같아야 합니다.

![PowerShell 출력](./media/security-center-disk-encryption/security-center-disk-encryption-fig5.png)

## <a name="encrypt-hello-azure-virtual-machine"></a>Hello Azure 가상 컴퓨터를 암호화 합니다.
사용자는 이제 준비 tooencrypt 가상 컴퓨터. 가상 컴퓨터에 있는 경우에 키 자격 증명 모음과 동일한 리소스 그룹을 hello toohello 암호화 단계 섹션으로 이동할 수 있습니다. 가상 컴퓨터에 없는 경우에 hello 같은 리소스 그룹 주요 자격 증명 모음으로, tooenter hello 다음 hello 콘솔의 hello PowerShell ISE에서 필요 합니다.

**$resourceGroupName = <’Virtual_Machine_RG’>**

대체 **< Virtual_Machine_RG >** 작은따옴표 hello 가상 컴퓨터가 포함 된 hello 리소스 그룹의 이름으로 둘러싸여 있습니다. **ENTER**키를 누릅니다.
hello 올바른 리소스 그룹 이름을 입력 했는지, PowerShell ISE 콘솔 hello에 hello 다음을 입력 하는 tooconfirm:

**$resourceGroupName**

**ENTER**키를 누릅니다. 가상 컴퓨터에 있는 리소스 그룹의 hello 이름이 표시 되어야 합니다. 예:

![PowerShell 출력](./media/security-center-disk-encryption/security-center-disk-encryption-fig6.png)

### <a name="encryption-steps"></a>암호화 단계
먼저 tootell PowerShell hello 이름을 원하는 tooencrypt hello 가상 컴퓨터의 합니다. Hello 콘솔에서 다음을 입력 합니다.

**$vmName = <’your_vm_name’>**

대체 **<'your_vm_name ' >** VM의 hello 이름으로 (hello 이름 주위에 작은따옴표 있는지 확인) 한 다음 키를 누릅니다 **ENTER**합니다.

VM 이름을 입력 한 올바른 hello를 입력 하는 tooconfirm:

**$vmName**

**ENTER**키를 누릅니다. Hello 이름이 나타나야 합니다. 원하는 tooencrypt hello 가상 컴퓨터의 합니다. 예:

![PowerShell 출력](./media/security-center-disk-encryption/security-center-disk-encryption-fig7.png)

두 개의 메서드 toorun hello 암호화 명령 tooencrypt 모든 드라이브에는 hello 가상 컴퓨터입니다. hello 첫 번째 메서드는 다음에 PowerShell ISE 콘솔 hello 명령을 tootype hello:

~~~
Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
~~~

이 명령 키를 입력한 후에 **ENTER**키를 누릅니다.

hello 두 번째 방법은 tooclick hello 스크립트 창 (hello PowerShell ISE의 위쪽 창 hello)에서 고 toohello hello 스크립트 맨 아래로 스크롤합니다. 위에 나열 된 hello 명령 강조 표시 하 고 다음 마우스 오른쪽 단추로 클릭 하 여 한 다음 클릭 **선택 항목 실행** 하거나 키를 눌러 **F8** hello 키보드에서.

![PowerShell ISE](./media/security-center-disk-encryption/security-center-disk-encryption-fig8.png)

사용 하면 hello 방법에 관계 없이 작업이 toocomplete hello에 대 한 10-15 분이 걸립니다 알리는 대화 상자가 표시 됩니다. **예**를 클릭합니다.

Hello 암호화 프로세스 작업이 발생 하는 동안 Azure 포털 toohello 되돌린 hello 가상 컴퓨터의 hello 상태를 확인할 수 있습니다. Hello hello 페이지의 왼쪽, 클릭 **가상 컴퓨터**, hello에 다음 **가상 컴퓨터** 블레이드를 암호화 하는 hello 가상 컴퓨터의 hello 이름을 클릭 합니다. 해당 hello 나타나는 hello 블레이드에서 보면 **상태** 임을 표시 **업데이트**합니다. 암호화가 진행 중임을 보여줍니다.

![Hello VM에 대 한 자세한 내용](./media/security-center-disk-encryption/security-center-disk-encryption-fig9.png)

PowerShell ISE toohello를 반환 합니다. Hello 스크립트가 완료 되 면 아래 hello 그림에 표시 표시 됩니다.

![PowerShell 출력](./media/security-center-disk-encryption/security-center-disk-encryption-fig10.png)

가상 컴퓨터를 hello toodemonstrate 이제 암호화 toohello Azure 포털을 반환 하 고 클릭 **가상 컴퓨터** hello hello 페이지의 왼쪽에 있습니다. 암호화 된 hello 가상 컴퓨터의 hello 이름을 클릭 합니다. Hello에 **설정** 블레이드에서 클릭 **디스크**합니다.

![설정 옵션](./media/security-center-disk-encryption/security-center-disk-encryption-fig11.png)

Hello에 **디스크** 블레이드를 확인 하 게 **암호화** 은 **Enabled**합니다.

![디스크 속성](./media/security-center-disk-encryption/security-center-disk-encryption-fig12.png)

## <a name="next-steps"></a>다음 단계
이 문서에서는 방법에 대해 배웠습니다 tooencrypt Azure 가상 컴퓨터. Azure 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) – toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고
* [Azure 보안 센터 FAQ](security-center-faq.md) – 찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) – Azure 보안 및 규정 준수에 관한 블로그 게시물 찾기
