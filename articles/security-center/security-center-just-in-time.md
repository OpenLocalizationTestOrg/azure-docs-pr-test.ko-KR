---
title: "Azure 보안 센터에서 aaaJust 시간 가상 컴퓨터에 액세스 | Microsoft Docs"
description: "이 문서를 안내해 어떻게 just-in-time Azure 보안 센터를 통해 제어할 수에서 VM 액세스 액세스 tooyour Azure 가상 컴퓨터."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a>Just-In-Time를 사용하여 가상 컴퓨터 액세스 관리

시간 가상 컴퓨터 (VM)에 액세스는 인바운드 트래픽 tooyour Azure Vm에서 쉽게 액세스할 수 있도록 tooconnect tooVMs 필요할 때 제공 하는 동안 노출 tooattacks 감소를 사용 하는 toolock 수 있습니다.

> [!NOTE]
> 시간 기능에만 있는 hello 되며 미리 보기에서 hello 보안 센터의 표준 계층에 있습니다.  참조 [가격 책정](security-center-pricing.md) 보안 센터에 대해 자세히 toolearn 가격 책정 계층이 있습니다.
>
>

## <a name="attack-scenario"></a>공격 시나리오

무차별 암호 대입 공격 수단 toogain 액세스 tooa VM으로 일반적으로 대상 관리 포트가 있습니다. 성공 하면 공격자 hello VM에 대 한 제어를 수행할를 업데이트 하 고 한 발판을 마련 환경으로 연결할 수 있습니다.

한 가지 방법은 tooreduce 노출 tooa 무차별 암호 대입 공격은 toolimit hello의 포트가 열려 있는 시간입니다. 관리 포트가 언제 든 toobe 열기는 필요 하지 않습니다. Toobe만 해야 하는 동안 열려는 연결 된 VM을 예를 들어 tooperform toohello 관리 또는 유지 관리 작업입니다. 보안 센터를 사용 하는 just-in-time에서 활성화 되 면 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md) 공격자가 대상으로 지정할 수 있도록 액세스 toomanagement 포트를 제한 하는 (NSG) 규칙을 합니다.

![Just-In-Time 시나리오][1]

## <a name="how-does-just-in-time-access-work"></a>Just-In-Time 액세스는 어떻게 작동하나요?

Just-in-time에서 활성화 되 면 NSG 규칙을 만들어 보안 센터 인바운드 트래픽 tooyour Azure Vm 아래로 잠급니다. Hello 포트 선택 hello VM toowhich에 인바운드 트래픽을 잠기는 합니다. 이러한 포트는 hello 시간 솔루션에만 있는 것으로 제어 됩니다.

보안 센터 해당 hello 사용자가을 확인 한 사용자 액세스 tooa VM를 요청 하면 [역할 기반 액세스 제어 (RBAC)](../active-directory/role-based-access-control-configure.md) hello Azure 리소스에 대 한 쓰기 액세스를 제공 하는 사용 권한입니다. 인바운드 트래픽 toohello 관리 포트 지정 된 시간을 양의 hello에 대 한 쓰기 권한이 있는, hello 요청이 승인 되 고 보안 센터 (Nsg) 네트워크 보안 그룹 tooallow hello를 자동으로 구성 하는 경우. Hello 시간 기간이 만료 되 면 보안 센터 hello Nsg tootheir 이전 상태로 복원 합니다.

> [!NOTE]
> Security Center Just-In-Time VM 액세스는 현재 Azure Resource Manager를 통해 배포된 VM만 지원합니다. 클래식 hello 및 리소스 관리자 배포 모델에 대 한 자세한 참조 toolearn [Azure 리소스 관리자 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md)합니다.
>
>

## <a name="using-just-in-time-access"></a>Just-In-Time 액세스 사용

hello **VM 액세스 시간에에서만** hello에 바둑판식으로 배열 **보안 센터** 블레이드 지난주 hello에 대 한 액세스 승인 된 요청 시간 액세스 및 hello 수에만 있는 것에 대해 구성 된 Vm의 hello 수를 표시 합니다.

선택 hello **VM 액세스 시간에에서만** 타일 및 hello **VM 액세스 시간에에서만** 블레이드를 엽니다.

![Just-In-Time VM 액세스 타일][2]

hello **VM 액세스 시간에에서만** 블레이드 Vm의 hello 상태에 대해 설명 합니다.

- **구성** -VM 액세스 시간에만 구성 된 toosupport 상태인 Vm입니다. 표시 되는 hello 데이터 hello 지난 주에 대 한 이며 승인 된 요청, 마지막 사용 날짜 및 시간 및 마지막 사용자의 각 VM hello 번호에 대 한 포함 됩니다.
- **권장** - Just-In-Time VM 액세스를 지원할 수 있지만 구성되지 않은 VM입니다. 이러한 VM에는 Just-In-Time VM 액세스 제어를 사용하도록 설정하는 것이 좋습니다. [Just-In-Time VM 액세스 사용](#enable-just-in-time-vm-access)을 참조하세요.
- **권장 사항 없음** -권장 toobe 하지 VM을 일으킬 수 있는 원인은 다음과 같습니다.
  - NSG-시간 솔루션에만 있는 hello 누락 된 위치에는 NSG toobe가 필요 합니다.
  - 클래식 VM - Security Center Just-In-Time VM 액세스는 현재 Azure Resource Manager를 통해 배포된 VM만 지원합니다. 클래식 배포 시간 솔루션에만 있는 hello에서 지원 되지 않습니다.
  - 다른-VM 하나 공용 IP 없습니다 아니며 위치에서 NSG를 포함 하지 않는 솔루션 hello 구독 또는 hello 리소스 그룹의 보안 정책을 hello 꺼져 just-in-time에서 hello 또는 해당 hello VM이이 범주에는.

## <a name="configuring-a-just-in-time-access-policy"></a>Just-In-Time 액세스 정책 구성

tooselect hello tooenable 원하는 Vm:

1. Hello에 **VM 액세스 시간에에서만** 블레이드, 선택 hello **권장** 탭 합니다.

  ![Just-In-Time 액세스 사용][3]

2. 아래 **Vm**, 원하는 tooenable hello Vm을 선택 합니다. 확인 표시 다음 tooa VM을 추가합니다.
3. **VM에서 JIT 사용**을 선택합니다.
4. **저장**을 선택합니다.

### <a name="default-ports"></a>기본 포트

보안 센터는 적시에 사용 하도록 권장 되는 hello 기본 포트를 확인할 수 있습니다.

1. Hello에 **VM 액세스 시간에에서만** 블레이드, 선택 hello **권장** 탭 합니다.

  ![기본 포트 표시][6]

2. **VM** 아래에서 VM을 선택합니다. 이렇게 하면 추가 확인 표시가 다음 toohello VM과 열립니다 hello **JIT VM 액세스 구성** 블레이드입니다. 이 블레이드는 hello 기본 포트를 표시합니다.

### <a name="add-ports"></a>포트 추가

Hello에서 **JIT VM 액세스 구성** 블레이드를 추가 하 고 수도 있습니다 tooenable hello 시간 솔루션에만 있는 것을 원하는 새 포트를 구성 합니다.

1. Hello에 **JIT VM 액세스 구성** 블레이드를 **추가**합니다. Hello 열립니다 **포트 구성 추가** 블레이드입니다.

  ![포트 구성][7]

2. **포트 구성 추가** 허용 Ip, 소스 및 최대 요청 시간 hello 포트, 프로토콜 종류를 식별 블레이드를 만듭니다.

  승인 된 요청에 따라 hello IP 범위 허용된 tooget 액세스는 원본 Ip 허용 합니다.

  최대 요청 시간은 hello 최대 시간 창은 특정 포트를 열 수 있습니다.

3. **확인**을 선택합니다.

## <a name="requesting-access-tooa-vm"></a>VM 액세스 tooa 요청

toorequest 액세스 tooa VM:

1. Hello에 **VM 액세스 시간에에서만** 블레이드, 선택 hello **자동 구성** 탭 합니다.
2. 아래 **Vm**, tooenable 액세스 해야 하는 hello Vm을 선택 합니다. 확인 표시 다음 tooa VM을 추가합니다.
3. **액세스 요청**을 선택합니다. Hello 열립니다 **액세스 권한을 요청** 블레이드입니다.

  ![요청 액세스 tooa VM][4]

4. Hello에 **액세스 권한을 요청** hello 포트는 hello 원본 IP와 함께 각 VM hello 포트 tooopen는 hello에 대 한 포트를 열지 tooand hello 시간 창을 열에 대 한 구성 블레이드를 만듭니다. 시간 정책에만 있는 hello에 구성 된 액세스만 toohello 포트를 요청할 수 있습니다. 각 포트에 시간 정책에만 있는 hello에서 파생 된 최대 허용된 시간입니다.
5. **포트 열기**를 선택합니다.

## <a name="editing-a-just-in-time-access-policy"></a>Just-In-Time 액세스 정책 편집

VM의 시간 정책에 추가 하 고 해당 VM에 대 한 새 포트 tooopen를 구성 하 여 기존를 변경 하거나 다른 매개 변수를 변경 하 여 관련된 tooan 이미 보호 포트입니다.

주문 tooedit에서 기존 VM의 시간 정책에만 hello **자동 구성** 탭을 사용 합니다.

1. 아래 **Vm**를 해당 VM에 대 한 hello 행 내에서 hello 세 점을 클릭 하면 포트 tooby VM tooadd를 선택 합니다. 그러면 메뉴가 열립니다.
2. 선택 **편집** hello 메뉴에 있습니다. Hello 열립니다 **JIT VM 액세스 구성** 블레이드입니다.

  ![정책 편집][8]

3. Hello에 **JIT VM 액세스 구성** 블레이드에서 해당 포트를 클릭 하 여 hello 이미 보호 된 포트의 기존 설정을 편집 하거나 하거나 선택할 수 있습니다 **추가**합니다. Hello 열립니다 **포트 구성 추가** 블레이드입니다.

  ![포트 추가][7]

4. **포트 구성 추가** 블레이드 hello 포트, 프로토콜 종류, 허용 된 Ip, 소스 및 최대 요청 시간을 식별 합니다.
5. **확인**을 선택합니다.
6. **저장**을 선택합니다.

## <a name="auditing-just-in-time-access-activity"></a>Just-In-Time 액세스 활동 감사

로그 검색을 사용하여 VM 활동에 대한 정보를 얻을 수 있습니다. tooview 로그:

1. Hello에 **VM 액세스 시간에에서만** 블레이드, 선택 hello **자동 구성** 탭 합니다.
2. 아래 **Vm**를 해당 VM에 대 한 hello 행 내에서 hello 세 점을 클릭 하 여에 대 한 VM tooview 정보를 선택 합니다. 그러면 메뉴가 열립니다.
3. 선택 **활동 로그** hello 메뉴에 있습니다. Hello 열립니다 **활동 로그** 블레이드입니다.

![활동 로그 선택][9]

hello **활동 로그** 블레이드 시간, 날짜 및 구독 함께 해당 VM에 대 한 이전 작업의 필터링된 된 뷰를 제공 합니다.

![활동 로그 보기][5]

선택 하 여 hello 로그 정보를 다운로드할 수 **여기 toodownload 모든 항목을 클릭 hello CSV로**합니다.

Hello 필터를 수정 하 고 선택 **적용** toocreate 로그와으로 검색 합니다.

## <a name="using-just-in-time-vm-access-via-powershell"></a>PowerShell을 통해 Just-In-Time VM 액세스 사용

PowerShell 통해 시간 솔루션에만 순서 toouse hello에서 hello 있는지 확인 [최신](/powershell/azure/install-azurerm-ps) Azure PowerShell 버전입니다.
Tooinstall hello 이렇게 해야 [최신](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) hello PowerShell 갤러리에서 Azure 보안 센터입니다.

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a>VM에 대한 Just-In-Time 정책 구성

tooconfigure just가 특정 VM에 시간 정책에 필요한 toorun이이 명령은 PowerShell 세션에서: ASCJITAccessPolicy 집합입니다.
Hello cmdlet 설명서 toolearn 자세한를 따릅니다.

### <a name="requesting-access-tooa-vm"></a>VM 액세스 tooa 요청

로 보호 되는 특정 VM tooaccess 시간 솔루션에만 있는 hello, PowerShell 세션에서 toorun이이 명령은 필요: ASCJITAccess 호출 합니다.
Hello cmdlet 설명서 toolearn 자세한를 따릅니다.

## <a name="next-steps"></a>다음 단계
이 문서에서 배운 어떻게 just-in-time 보안 센터를 사용 하면 VM 액세스 액세스 tooyour Azure 제어 가상 컴퓨터.

보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

- [보안 정책 설정](security-center-policies.md) -학습 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
- [보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
- [보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
- [관리 및 toosecurity 경고 응답](security-center-managing-and-responding-alerts.md) -학습 방법을 toomanage 및 응답 toosecurity 경고 합니다.
- [파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
- [보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
- [Azure 보안 블로그](https://blogs.msdn.microsoft.com/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
