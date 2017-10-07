---
title: "aaaAzure 가상 컴퓨터 보안 모범 사례 | Microsoft Docs"
description: "이 문서에서는 다양 한 보안 모범 사례 toobe Azure에 있는 가상 컴퓨터에 사용 합니다."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 5e757abe-16f6-41d5-b1be-e647100036d8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: b03bcc75fde6d49897f9a7f6f15aec87456edd0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-vm-security"></a>Azure VM 보안에 대한 모범 사례

서비스 (IaaS) 시나리오와 대부분 인프라에 [Azure 가상 컴퓨터 (Vm)](https://docs.microsoft.com/en-us/azure/virtual-machines/) hello 주 작업 클라우드를 사용 하는 조직에 대 한 계산 됩니다. 이 사실은에서 특히 분명 하 게 [하이브리드 시나리오](https://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) 있는 조직에서는 원하는 tooslowly 마이그레이션 작업 toohello 클라우드입니다. 이러한 시나리오에 따라 hello [IaaS에 대 한 일반적인 보안 고려 사항](https://social.technet.microsoft.com/wiki/contents/articles/3808.security-considerations-for-infrastructure-as-a-service-iaas.aspx), 보안 모범 사례 tooall Vm에 적용 합니다.

이 문서에서는 각각 VM을 사용하여 고객과 우리의 고유한 직접 경험으로부터 파생된 다양한 VM 보안 모범 사례를 설명합니다.

hello에 대 한 유용한 정보 의견의 의견에 기반 하며 현재 Azure 플랫폼 기능을 사용 하며 집합 기능. Tooupdate 계획 의견 및 기술 시간이 지나면서 달라질 수, 때문에이 문서에서는 정기적으로 tooreflect 해당 변경 내용이 있습니다.

각 모범 사례에 대 한 hello 문서 설명합니다.

* 어떤 hello 최상의 방법이입니다.
* 것이 좋습니다 tooenable 것입니다.
* Tooenable을 방법을 학습할 수 있는 것입니다.
* Tooenable 실패 하는 경우 어떻게 될 것입니다.
* 가능한 대안 toohello 것이 좋습니다.

hello 문서 hello VM 보안 최선의 구현 방법을 검사 합니다.

* VM 인증 및 액세스 제어
* VM 가용성 및 네트워크 액세스
* 암호화를 적용하여 VM에서 미사용 데이터 보호
* VM 업데이트 관리
* VM 보안 태세 관리
* VM 성능 모니터링

## <a name="vm-authentication-and-access-control"></a>VM 인증 및 액세스 제어

VM 보호 hello 첫 번째 단계는 권한이 있는 사용자만 tooensure는 새 vm 수 tooset 것입니다. 사용할 수 있습니다 [Azure 리소스 관리자 정책](../azure-resource-manager/resource-manager-policy.md) tooestablish 규칙은 조직의 리소스에 대 한 사용자 지정된 정책을 만들고 이러한 정책을 tooresources와 같은 적용 [리소스 그룹](../azure-resource-manager/resource-group-overview.md).

Tooa 리소스 그룹을 자연스럽 게 속해 있는 Vm에서 정책을 상속 합니다. 이 방법은 toomanaging Vm을 권장 하지만 수도 있습니다 제어 액세스 tooindividual VM 정책을 사용 하 여 [역할 기반 액세스 제어 (RBAC)](../active-directory/role-based-access-control-configure.md)합니다.

리소스 관리자 정책 및 RBAC toocontrol VM 액세스를 사용 하면 전반적인 VM 보안을 향상 시킬 수 있습니다. Hello에 같은 수명 주기 hello로 Vm을 통합 하는 것이 좋습니다 동일한 리소스 그룹입니다. 리소스 그룹을 사용하여 리소스에 대한 비용 청구를 배포, 모니터링 및 롤업할 수 있습니다. tooenable 사용자 tooaccess 및 Vm 설정을 사용 하 여 한 [최소 권한 접근 방식을](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models)합니다. 고 toousers 권한을 할당 하면 기본 제공 Azure 역할에 따라 toouse hello를 계획 합니다.

- [가상 컴퓨터 참가자](../active-directory/role-based-access-built-in-roles.md#virtual-machine-contributor): Vm을 관리할 수 있지만 연결 된 가상 네트워크 또는 저장소 계정 toowhich 하지 hello 합니다.
- [클래식 가상 컴퓨터 참가자](../active-directory/role-based-access-built-in-roles.md#classic-virtual-machine-contributor): 하지 hello 가상 네트워크 또는 저장소 계정 toowhich hello Vm에 연결 되어 있지만 hello 클래식 배포 모델을 사용 하 여 만든 Vm을 관리할 수 있습니다.
- [보안 관리자](../active-directory/role-based-access-built-in-roles.md#security-manager): 보안 구성 요소, 보안 정책 및 VM을 관리할 수 있습니다.
- [DevTest 실습 사용자](../active-directory/role-based-access-built-in-roles.md#devtest-labs-user): 모든 항목을 볼 수 있으며 VM을 연결, 시작, 다시 시작 및 종료할 수 있습니다.

관리자 간 계정 및 암호를 공유하거나, 여러 사용자 계정 또는 서비스, 특히 소셜 미디어 또는 기타 비 관리 작업에 암호를 다시 사용하지 마세요. 이상적으로 사용 해야 [Azure 리소스 관리자](../azure-resource-manager/resource-group-authoring-templates.md) 템플릿 tooset Vm 안전 하 게 합니다. 이 방법을 사용 하면 배포 선택 강화 수 있으며 hello 배포에서 보안 설정을 적용할 수 있습니다.

RBAC와 같은 기능을 활용하여 데이터 액세스 제어를 적용하지 않는 조직은 사용자에게 필요 이상으로 많은 권한을 부여하게 될 수 있습니다. 직접 부적절 한 사용자 액세스 toocertain 데이터에는 해당 데이터 손상 될 수 있습니다.

## <a name="vm-availability-and-network-access"></a>VM 가용성 및 네트워크 액세스

VM toohave 높은 가용성을 필요로 하는 중요 한 응용 프로그램을 실행 하는 경우 여러 Vm을 사용 하는 것이 좋습니다. 더 나은 가용성에 대 한 hello에 두 개 이상의 Vm을 만들 [가용성 집합](../virtual-machines/windows/tutorial-availability-sets.md)합니다.

[Azure 부하 분산 장치](../load-balancer/load-balancer-overview.md) 부하 분산 된 Vm toohello 속함이 필요 동일한 가용성 집합입니다. 이러한 Vm hello 인터넷에서에서 액세스할 수 있어야를 구성 해야는 [인터넷 연결 부하 분산 장치](../load-balancer/load-balancer-internet-overview.md)합니다.

Vm을 노출 된 toohello 인터넷 것이 중요 하 [보안 Nsg (네트워크 그룹)를 사용 하 여 네트워크 트래픽 흐름 제어](../virtual-network/virtual-networks-nsg.md)합니다. Nsg 적용된 toosubnets 일 수 있으므로 서브넷에서 리소스를 그룹화 하 고 Nsg toohello 서브넷을 적용 하 여 hello 수가 Nsg 최소화할 수 있습니다. hello 의도 toocreate 제대로 hello를 구성 하 여 수행할 수 있는 네트워크 격리 수준의 [네트워크 보안](../best-practices-network-security.md) Azure의 기능입니다.

원격 액세스 tooa을 지닌 Azure 보안 센터 toocontrol hello 적시에 (JIT) VM 액세스 기능을 사용할 수도 있습니다 특정 VM 및 기간에 대 한 합니다.

TooInternet 지향 Vm이 제약 조건을 네트워크 액세스를 적용 하지 않는 조직에서는 프로토콜 RDP (원격 데스크톱) 무차별 암호 대입 공격과 같은 toosecurity 위험에 노출 합니다.

## <a name="protect-data-at-rest-in-your-vms-by-enforcing-encryption"></a>암호화를 적용하여 VM에서 미사용 데이터 보호

[미사용 데이터 암호화](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/)는 데이터 프라이버시, 규정 준수 및 데이터 주권을 위한 필수 단계입니다. [Azure 디스크 암호화](../security/azure-security-disk-encryption.md) IT 관리자가 tooencrypt Windows 및 Linux IaaS VM 디스크를 사용 하도록 설정 합니다. 디스크 암호화 hello 업계 표준 Windows BitLocker 기능과 hello Linux dm crypt 기능 tooprovide 볼륨에 대 한 암호화 hello OS 및 데이터 디스크 hello 되어 있습니다.

디스크 암호화를 적용할 수 있습니다 toohelp 보호 데이터 toomeet 조직 보안 및 규정 준수 요구 사항입니다. 암호화를 사용 하 여 조직 고려해 야 toohelp 관련된 toounauthorized 데이터 액세스 위험을 완화 합니다. 또한 중요 한 데이터 toothem를 작성 하기 전에 드라이브를 암호화 하는 것이 좋습니다.

있는지 tooencrypt에서 Azure 저장소 계정에 놓으면 사용자 VM 데이터 볼륨 tooprotect 수 있습니다. Hello 암호화 키 및 암호를 사용 하 여 보호 [Azure 키 자격 증명 모음](https://azure.microsoft.com/en-us/documentation/articles/key-vault-whatis/)합니다.

데이터 암호화를 실행 하지 않는 조직에서는 노출된 toodata 무결성 문제를 있습니다. 예를 들어, 권한이 없는 사용자나 악의적인 사용자가 손상 된 계정에서 데이터를 훔칠 수도 무단된 액세스 toodata ClearFormat에 코드를 얻을 수 있습니다. 이러한 위험에 대 한 만들기, 업계 규정 toocomply 외에도 회사 성실을 연습해는 및 올바른 보안을 사용 하 여 제어 tooenhance의 데이터 보안을 증명 해야 합니다.

디스크 암호화에 대해 자세히 toolearn 참조 [Azure 디스크 암호화에 대 한 Windows 및 Linux IaaS Vm](azure-security-disk-encryption.md)합니다.


## <a name="manage-your-vm-updates"></a>VM 업데이트 관리

하므로 Azure Vm에서 모든 마찬가지로 온-프레미스 Vm에는 의도 한 toobe 사용자 관리, Azure에 Windows 업데이트 toothem 푸시 하지 않습니다. 그러나는 tooleave hello 자동 Windows 업데이트 설정을 사용을 권장 합니다. 두 번째 방법은 toodeploy [WSUS Windows Server Update Services ()](https://technet.microsoft.com/windowsserver/bb332157.aspx) 또는 다른 적절 한 업데이트 관리 제품 중 하나에 다른 VM 이나 온-프레미스입니다. WSUS와 Windows 업데이트 모두 VM을 최신 상태로 유지합니다. 또한 모든 IaaS Vm toodate 가동 중인 검색 제품 tooverify를 사용 하는 것이 좋습니다.

Azure에서 제공 하는 주식 이미지는 Windows 업데이트의 round 가장 최근의 정기적으로 업데이트 된 tooinclude hello입니다. 그러나 보장이 없습니다 hello 이미지 배포 시 현재 됩니다. 공용 릴리스 뒤에 약간의 지연(몇 주)이 발생할 수도 있습니다. 확인 및 모든 Windows 업데이트를 설치 합니다. 모든 배포의 첫 번째 단계 hello 이어야 합니다. 이 측정값은 또는 사용자 고유의 라이브러리에서 제공 하는 이미지를 배포할 때 tooapply 특히 중요 합니다. Hello Azure Marketplace의 일부로 제공 되는 이미지는 기본적으로 자동으로 업데이트 됩니다.

소프트웨어 업데이트 정책을 적용 하지 않는 조직에서는 알려진, 이전에 고정 취약점을 악용 노출 된 toothreats 더 됩니다. 이러한 보안 위협을 toocomply 업계 규정에 손상을 주지 외에도 회사 성실을 연습해는 및 hello 보안 hello 클라우드에 있는 프로그램 작업의 올바른 보안 컨트롤 toohelp를 사용 하 여 확인 증명 해야 합니다.

기존 데이터 센터에 대 한 유용한 소프트웨어 업데이트는 중요 한 tooemphasize 선택한 Azure IaaS 유사한 점이 있습니다. 따라서 프로그램 현재 소프트웨어 업데이트 정책을 tooinclude Vm을 평가 하는 것이 좋습니다.

## <a name="manage-your-vm-security-posture"></a>VM 보안 태세 관리

사이버 위협 발전을 있으며 Vm 보호 신속 하 게 위험을 검색, tooyour 리소스에 무단으로 액세스를 방지, 경고가 트리거되고 하 고 수 있는 거짓 긍정을 줄일 풍부한 기능을 모니터링 합니다. 이러한 작업에 대 한 hello 보안 상태는 업데이트 관리 toosecure 네트워크 액세스가 hello VM의 모든 보안 측면을 구성합니다.

toomonitor hello 보안 환경과 프로그램 [Windows](../security-center/security-center-virtual-machine.md) 및 [Linux Vm](../security-center/security-center-linux-virtual-machine.md)를 사용 하 여 [Azure 보안 센터](../security-center/security-center-intro.md)합니다. Azure 보안 센터에서 hello 다음 기능을 활용 하 여 Vm을 보호:

* 권장된 구성 규칙으로 OS 보안 설정 적용
* 누락될 수 있는 시스템 보안 및 중요 업데이트 식별 및 다운로드
* 끝점 맬웨어 방지 보호 권장 사항 배포
* 디스크 암호화 유효성 검사
* 취약점 평가 및 해결
* 위협 감지

Security Center는 위협을 적극적으로 모니터링할 수 있으며 잠재적 위협은 **보안 경고**에서 공개됩니다. 상호 관련된 위협은 **보안 인시던트**라고 하는 단일 보기로 집계됩니다.

toounderstand 보안 센터 수, Azure에 있는 Vm에 대 한 잠재적 위협을 식별 하는 방법에 hello 다음 비디오 보기:

<iframe src="https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Security-Center-in-Incident-Response/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

권한이 없는 사용자가 설정 된 toocircumvent 보안 컨트롤에서의 Vm에 대 한 강력한 보안 상태를 적용 하지는 조직 잠재적인 시도 인식 하지 않고 남아 있습니다.

## <a name="monitor-vm-performance"></a>VM 성능 모니터링

리소스 남용은 VM 프로세스가 소비해야 하는 것보다 더 많은 리소스를 소비하는 경우 문제가 될 수 있습니다. 성능 문제는 VM으로 가용성 hello 보안 원칙을 위반 하는 tooservice 중단이 될 수 있습니다. 이러한 이유로 명령적 toomonitor VM 액세스 프로비저닝하지, 문제가 발생 하는 동안 적극적으로 있지만 정상적인 작업 중에 측정 된 기준 성능에 대 한 합니다.

[Azure 진단 로그 파일](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/)을 분석하여 VM 리소스를 모니터링하고 성능 및 가용성을 손상시킬 수 있는 잠재적인 문제를 식별할 수 있습니다. Azure 진단 확장 hello Windows 기반 Vm에서 모니터링 및 진단 기능을 제공합니다. Hello의 일환으로 hello 확장명을 포함 하 여 이러한 기능을 사용할 수 있습니다 [Azure 리소스 관리자 템플릿](../virtual-machines/windows/extensions-diagnostics-template.md)합니다.

사용할 수도 있습니다 [Azure 모니터](../monitoring-and-diagnostics/monitoring-overview-metrics.md) 리소스의 상태에 대 한 toogain 가시성 합니다.

VM 성능 모니터링 하지 않는 하는 조직에서는 정상 또는 비정상 성능 패턴의 특정 변경 내용이 있는지 여부를 없습니다 toodetermine를 있습니다. Hello VM 보통 때 보다 더 많은 리소스를 소비 하는 경우 이러한 특이 외부 리소스 또는 hello VM에서에서 실행 되는 손상 된 프로세스에서 잠재적 공격을 나타낼 수 있습니다.
