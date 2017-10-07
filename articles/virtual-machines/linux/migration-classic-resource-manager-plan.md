---
title: "클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션에 대 한 aaaPlanning | Microsoft Docs"
description: "클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 계획"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 78492a2c-2694-4023-a7b8-c97d3708dcb7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/01/2017
ms.author: kasing
ms.openlocfilehash: 53c6f640425b69cae2ef10afb8c92b8ac4394267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="planning-for-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 계획
Azure 리소스 관리자는 수많은 놀라운 기능을 제공 하는 경우 것은 중요 한 tooplan 것 유연 하 게 수행 하 여 마이그레이션 여행 toomake 아웃 합니다. 계획에 시간을 들이면 마이그레이션 활동을 수행하는 동안 문제가 발생하지 않습니다. 

> [!NOTE] 
> hello 지침 과도 하 게 적용 된 tooby hello Azure 고객 자문 팀 및 클라우드 솔루션 설계자에 마이그레이션 큰 enviornments 고객과 협력 했습니다. 따라서이 문서는 tooget 성공의 새로운 패턴의 등장으로 때문에 참조 tootime toosee 시간에서 다시 새 권장 사항이 있는 경우에 따라 업데이트를 계속 합니다.

Hello 마이그레이션 작업의 4 개의 일반적인 단계로 가지가 있습니다.

![마이그레이션 단계](../media/virtual-machines-windows-migration-classic-resource-manager/plan-labtest-migrate-beyond.png)

## <a name="plan"></a>계획

### <a name="technical-considerations-and-tradeoffs"></a>기술적 고려 사항 및 장단점

기술 요구 사항 크기, 지역 및 운영 방법에 따라 tooconsider를 설정할 수 있습니다.

1. 조직에 Azure Resource Manager가 필요한 이유는 무엇인가요?  마이그레이션에 대 한 hello 비즈니스 이유는 무엇입니까?
2. Azure 리소스 관리자에 대 한 hello 기술 이유는 무엇입니까?  기능 (있는 경우) 추가 Azure 서비스 tooleverage 보 시겠습니까 메시지를 표시 합니다.
3. 어떤 응용 프로그램 (또는 가상 컴퓨터 집합) hello 마이그레이션에 포함 되어 있습니까?
4. API hello 마이그레이션을 사용 하 여 어떤 시나리오가 지원 되나요?  검토 hello [기능 및 구성을 지원 되지 않는](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations)합니다.
5. 운영 팀이 이제 클래식 및 Azure Resource Manager에서 응용 프로그램/VM을 지원하나요?
6. Azure Resource Manager에서는 VM 배포, 관리, 모니터링 및 보고 프로세스를 어떻게 변경하나요(변경할 수 있는 경우)?  배포 스크립트를 업데이트 하는 toobe 필요 합니까?
7. Tooalert 관련자 (최종 사용자, 응용 프로그램 소유자 및 인프라 소유자)를 계획 hello 통신 란?
8. Hello 환경의 hello 복잡성에 따라 해야 있을 수 있는 유지 관리 기간 여기서 hello 응용 프로그램은 사용할 수 없는 tooend 사용자와 tooapplication 소유자?  그 기간은 얼마나 되나요?
9. 지식 및 Azure 리소스 관리자에 능숙 한는 hello 교육 계획 tooensure 이해 관계자 이란?
10. Hello 프로그램 관리 또는 hello 마이그레이션에 대 한 프로젝트 관리 계획 란?
11. 기술도로 지도 관련 코드 및 기타 hello Azure 리소스 관리자 마이그레이션에 대 한 hello 타임 라인은 무엇입니까?  최적으로 정렬되어 있나요?

### <a name="patterns-of-success"></a>성공 패턴

성공적인 고객 세부 종료할 hello 설명, 문서화 및 적용 된 계획.  광범위 하 게 전달된 toosponsors 및 관련 자가 hello 마이그레이션 계획을 확인 합니다.  마이그레이션 옵션에 대한 지식을 갖추기 위해 아래의 마이그레이션 관련 문서를 참조하는 것이 좋습니다.

* [클래식 tooAzure 리소스 관리자에서에서 리소스를 IaaS 플랫폼에서 지 원하는 마이그레이션 개요](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 플랫폼 지원에 기술 심층 분석](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 계획](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 PowerShell toomigrate IaaS 리소스를 사용 하 여](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI toomigrate IaaS 리소스 클래식 tooAzure 리소스 관리자를에서 사용 하 여](migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 지원에 대 한 커뮤니티 도구](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [가장 일반적인 마이그레이션 오류 검토](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 IaaS 리소스에 대 한 가장 자주 묻는 질문 검토 hello](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="pitfalls-tooavoid"></a>문제 tooavoid

- Tooplan 실패 합니다.  이 마이그레이션을 hello 기술 단계는 검증 및 hello 결과 예측할 수 있습니다.
- 모든 시나리오에 대 한 지원 플랫폼 마이그레이션 API hello 가정 사항도 고려 합니다. 읽기 hello [기능 및 구성을 지원 되지 않는](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations) toounderstand 어떤 시나리오가 지원 됩니다.
- 최종 사용자에게 잠재적인 응용 프로그램 중단을 계획하지 않음  충분 한 버퍼를 계획 tooadequately 잠재적으로 사용할 수 없는 응용 프로그램 시간의 최종 사용자에 게 경고 합니다.


## <a name="lab-test"></a>랩 테스트 

**환경 복제 및 테스트 마이그레이션 수행**
  > [!NOTE]
  > 기존 환경의 정확한 복제는 Microsoft 지원에서 공식적으로 지원하지 않는 커뮤니티 제공 도구를 사용하여 실행됩니다. 따라서는 **선택적** 단계 않은 hello 가장 좋은 방법은 toofind 프로덕션 환경 건드리지 않고 간단히 문제입니다. 커뮤니티 제공 도구를 사용 하는 옵션을 없으면 다음 아래 유효성 검사/준비/Abort 예행 권장 hello 알아봅니다.
  >
  
  정확한 시나리오 (계산, 네트워킹 및 저장소)의 랩 테스트를 수행 하는 것이 hello 가장 좋은 방법은 tooensure 원활한 마이그레이션. 이렇게 하면 다음과 같은 이점을 얻을 수 있습니다.

  - 전체적으로 별도 랩 또는 기존는 개발 및 테스팅 환경 tootest 합니다. 반복적으로 마이그레이션할 수 있고 안전하게 수정할 수 있는 완전히 분리된 랩을 사용하는 것이 좋습니다.  Hello 실제 구독에서 스크립트 toocollect/hydrate 메타 데이터는 다음과 같습니다.
  - 별도 구독에서 좋습니다 toocreate hello 랩 이며 hello 이유는 hello 랩에 반복 해 서 조각난 별도 having, 격리 된 구독 됩니다 줄이려면 hello 삭제 실제 문제가 실수로 받습니다.

  이 hello AsmMetadataParser 도구를 사용 하 여 수행할 수 있습니다. [이 도구에 대해 자세히 알아보기 ](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

### <a name="patterns-of-success"></a>성공 패턴

hello 다음 다양 한 hello 큰 마이그레이션 중에 발견 된 문제가 있었습니다. 이 완전 한 목록 및 toohello 참조 해야 [기능 및 구성을 지원 되지 않는](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations) 자세한 세부 정보에 대 한 합니다. 이러한 기술적인 문제가 발생할 수도 있고 그렇지 않을 수도 있지만, 마이그레이션을 시도하기 전에 문제를 해결하면 더 원활한 환경을 갖출 수 있습니다.

- **유효성 검사/준비/Abort 예행 수행** -이 hello 가장 중요 한 단계 tooensure 클래식 tooAzure 리소스 관리자 마이그레이션 성공입니다. hello 마이그레이션 API 세 가지 주요 단계는: 유효성 검사, 준비 및 커밋. 가 유효성을 검사 클래식 환경의 hello 상태를 읽고 모든 문제는 결과 반환 합니다. 그러나 hello Azure 리소스 관리자 스택의 일부 문제가 있는지, 유효성 검사는 모든 catch 하지 않습니다. 마이그레이션 프로세스의 다음 단계를 hello 준비 문제 별로 노출 도움이 됩니다. 가 준비 이동 클래식 tooAzure 리소스 관리자에서에서 메타 데이터를 hello 됩니다 하지 커밋 이동 hello 및 됩니다 제거 하거나 hello 기본 측에 아무 것도 변경 합니다. hello 마이그레이션을 준비 하 고 다음 중단 hello 예행 포함 됩니다 (**커밋하지 않고**) hello 마이그레이션 준비 합니다. 유효성을 검사/준비/abort 예행 hello ֲ toosee 검사 모든 hello Azure 리소스 관리자 스택의 hello 메타 데이터 (*프로그래밍 방식으로 또는 포털에서*), 및 제대로 마이그레이션합니다 모든 것을 확인 하 고 협의 기술 문제입니다.  또한 마이그레이션 기간도 제공하므로 이에 따라 가동 중지 시간을 적절하게 계획할 수도 있습니다.  유효성 검사/준비/abort; 사용자 중단 시간 발생 하지 않습니다. 따라서 무중단 tooapplication 사용법을입니다.
  - 아래 hello 항목 hello 예행 하기 전에 해결 toobe 필요 하지만 누락 된 경우 이러한 준비 단계 예행 테스트 플러시도 안전 하 게 됩니다. 엔터프라이즈 마이그레이션하는 동안 आ म क ा hello 예행 toobe 안전 하 고 중요 한 방식으로 tooensure 마이그레이션 준비 합니다.
  - 준비 때 실행 중인 hello 제어 평면 (Azure 관리 작업) 잠기는 hello 전체 가상 네트워크에 대 한 하므로 수 변경 되지 tooVM 메타 데이터의 유효성을 검사/준비/중단 중입니다.  그러나 그렇지 않은 경우 모든 응용 프로그램 기능(RD, VM 사용 등)에 영향을 주지 않습니다.  Hello Vm의 사용자가 실행 되 고 해당 hello 예행 모르게 됩니다.

- **ExpressRoute 회로 및 VPN**. 현재 권한 부여 링크가 있는 ExpressRoute 게이트웨이는 가동 중지 시간을 통해 마이그레이션할 수 있습니다. Hello 해결 방법에 대 한 참조 [마이그레이션할 ExpressRoute 회로 및 가상 네트워크를 hello 클래식 toohello 리소스 관리자 배포 모델에서 연결 된](../../expressroute/expressroute-migration-classic-resource-manager.md)합니다.

- **VM 확장** -가상 컴퓨터 확장은 잠재적으로 hello 가장 큰 장애물 toomigrating 실행 중인 Vm 중 하나입니다. VM 확장을 재구성하는 데 1-2일이 걸릴 수 있으므로 이에 따라 적절히 계획해야 합니다.  Azure 에이전트 작업은 실행 중인 Vm의 필요한 tooreport 백 VM 확장 상태입니다. Hello 상태는 실행 중인 VM에 대 한 다시 불량 섹터 상태가 되 면이 마이그레이션을 중단 됩니다. hello 에이전트 자체 toobe 받으세요 tooenable 마이그레이션에 필요 하지 않지만 확장에 있는 경우 hello VM을 마이그레이션 toomove 앞에 작업 에이전트 AND 아웃 바운드 인터넷 연결 (DNS)이 필요 합니다.
  - BGInfo v 1 제외한 모든 VM 확장을 마이그레이션하는 동안 연결 tooa DNS 서버를 손실 됩니다. \* 필요 toofirst 제거할 모든 마이그레이션 준비 하기 전에 VM 및 이후에 다시 추가 뒤로 toohello VM에서 Azure 리소스 관리자 마이그레이션 후 합니다.  **이 작업은 실행 중인 VM에만 해당됩니다.**  Hello Vm 할당 취소 중지 되 면 VM 확장 제거 toobe가 필요 하지 않습니다. **참고:** 다양한 확장 프로그램(예: Azure 진단 및 보안 센터 모니터링)은 마이그레이션 후에 다시 설치되므로 제거하더라도 문제가 되지 않습니다.
  - 또한 네트워크 보안 그룹이 아웃바운드 인터넷 액세스를 제한하지 않는지 확인합니다. 이는 일부 네트워크 보안 그룹 구성에서 발생할 수 있습니다. 아웃 바운드 인터넷 액세스 (및 DNS) VM 확장에 필요한 toobe tooAzure 리소스 관리자 마이그레이션. 
  - 두 가지 버전의 hello BGInfo 확장의: v1 및 v2 합니다.  Hello VM hello 클래식 포털 또는 PowerShell을 사용 하 여 만들어진 경우 hello VM hello v1 확장에에 있을 것입니다. 이 확장 toobe 제거 하지 않아도 및 건너뜁니다 (마이그레이션되지) hello 마이그레이션 API에 의해 합니다. 그러나 hello 새 Azure 포털에서 클래식 VM hello를 만든 경우 것 있을 것 hello JSON 기반 v2 버전의 BGInfo, 마이그레이션된 tooAzure hello 에이전트 작동 하 고 아웃 바운드 인터넷 액세스 (및 DNS)가 리소스 관리자에서 제공 될 수 있습니다. 
  - **재구성 옵션 1**: Vm에 작업 중인 DNS 서비스에 액세스 하 고 준비 하기 전에 hello 마이그레이션의 일환으로 모든 VM 확장을 제거 합니다 hello Vm에 Azure 에이전트 작업, 아웃 바운드 인터넷 없을 것을 알고 있는 경우 마이그레이션 후 hello VM 확장 한 다음 다시 설치 합니다. 
  - **재구성 옵션 2**: VM 확장이 장애물 너무 큰 경우 두 번째 방법은 tooshutdown/할당 취소 마이그레이션 시작 하기 전에 모든 Vm입니다. Vm을 할당 취소 하는 hello 마이그레이션 다음 hello Azure 리소스 관리자 측면에서 다시 시작 합니다. hello 이점은 VM 확장 마이그레이션할 예정입니다. hello 단점은 모든 공용 가상 Ip 손실 됩니다 (비-스타터 수 있음)와 분명히 hello Vm 종료 결국 훨씬 큰 영향을 줍니다 작업 응용 프로그램에 발생 합니다.

    > [!NOTE] 
    > Hello 보안 정책 확장을 제거 하기 전에 중지 toobe 요구, 그렇지 않은 경우에 모니터링 확장을 자동으로 다시 설치할 됩니다 hello 보안 hello 후 VM을 실행 중인 Vm 마이그레이션 중인 hello에 대 한 Azure 보안 센터 정책이 구성 된 경우 제거 됩니다.

- **가용성 집합** -가상 네트워크 (vNet) toobe tooAzure 리소스 관리자 마이그레이션, 클래식 배포 (예: 클라우드 서비스)가 포함 된 Vm hello 모두에 있어야 하나의 가용성 집합 또는 hello Vm 가용성 집합에 있는 전체 이어야 합니다. 둘 이상의의 가용성 집합 hello 클라우드 서비스는 Azure 리소스 관리자와 호환 되지 않습니다 및 마이그레이션 중단 됩니다.  또한 가용성 집합에 일부 VM이 없는 한편 가용성 집합에 없는 일부 VM이 있을 수 있습니다. tooresolve이 tooremediate 필요 하거나 클라우드 서비스 들을 이동 합니다.  여기에는 시간이 오래 걸릴 수 있으므로 적절히 계획합니다. 

- **웹/작업자 역할 배포가** -클라우드 서비스 웹 및 작업자 역할을 포함 하는 리소스 관리자 tooAzure 마이그레이션할 수 없습니다. 마이그레이션을 시작 하기 전에 hello 웹/작업자 역할 hello 가상 네트워크에서 제거 해야 합니다.  일반적인 솔루션은 toojust 이동 웹/작업자 역할 인스턴스 tooa 별도 클래식 가상 네트워크를 연결 된 tooan ExpressRoute 회로 또는 toomigrate hello 코드 toonewer PaaS 응용 프로그램 서비스 (이 설명은이 문서의 hello 다루지 않습니다) 이기도 합니다. Hello 전자 대/소문자를 다시 배포, 새 클래식 가상 네트워크 만들기, 이동/hello 웹/작업자 역할 toothat 새 가상 네트워크를 재배포 한 후 hello 이동 되는 가상 네트워크에서 hello 배포를 삭제 합니다. 코드 변경이 필요 없습니다. 새 hello [가상 네트워크 피어 링](../../virtual-network/virtual-network-peering-overview.md) 사용된 toopeer 함께 hello 클래식 가상 네트워크 hello 웹/작업자 역할에 포함 된 지정할 수 있습니다 및 다른 가상 네트워크에 hello 같은 Azure 지역 가상 네트워크 hello 예 마이그레이션 (**겹치기 가상 네트워크를 마이그레이션할 수 없는 대로 가상 네트워크 마이그레이션 완료 된 후**), 따라서 기능을 제공 하 hello 동일한 성능 손실 없이 및 대기 시간/대역폭 따른 위약금도 없습니다. Hello 추가 제공 [가상 네트워크 피어 링](../../virtual-network/virtual-network-peering-overview.md), 웹/작업자 역할 배포가 이제 쉽게 완화 될 수 이며 hello 마이그레이션 tooAzure 리소스 관리자를 차단 하지 않습니다.

- **Azure Resource Manager 할당량** - Azure 지역에는 클래식 및 Azure Resource Manager 모두에 대해 별도의 할당량/제한이 있습니다. 마이그레이션 시나리오에서 새 하드웨어를 사용 되 고 없는 경우에 *(클래식 tooAzure 리소스 관리자에서에서 기존 Vm 스왑 하는 것)*, Azure 리소스 관리자 할당량 계속 하기 전에 충분 한 용량이 있는 위치에서 toobe 사용 해야 함 마이그레이션을 시작할 수 있습니다. 아래에 나열 된 hello 주요 제한 버퍼 오버런 문제를 일으킬 됩니다.  열기 할당량 지원 티켓 tooraise hello 제한합니다. 

    > [!NOTE]
    > 이러한 제한은 필요 toobe에서 발생 하 여 현재 환경의 toobe 마이그레이션됩니다 동일한 지역 hello 합니다.
    >

    - 네트워크 인터페이스
    - 부하 분산 장치
    - 공용 IP
    - 고정 공용 IP
    - 코어 수
    - 네트워크 보안 그룹
    - 경로 테이블

    최신 버전의 Azure CLI 2.0 hello 사용 하 여 명령을 수행 하는 hello를 사용 하 여 현재 Azure 리소스 관리자 할당량을 확인할 수 있습니다.

    **계산** *(코어, 가용성 집합)*

    ```bash
    az vm list-usage -l <azure-region> -o jsonc 
    ```

    **네트워크** *(가상 네트워크, 고정 공용 IP, 공용 IP, 네트워크 보안 그룹, 네트워크 인터페이스, 부하 분산 장치, 경로 테이블)*
    
    ```bash
    az network list-usages -l <azure-region> -o jsonc
    ```

    **저장소** *(저장소 계정)*
    
    ```bash
    az storage account show-usage
    ```

- **Azure Resource Manager API 조정 제한** - 충분히 큰 환경이 있는 경우(예: > 400 VNET의 Vm) hello 기본 API 제한 쓰기에 대 한 제한에 도달 하기가 (현재 **1200 쓰기/시간**) Azure 리소스 관리자입니다. 마이그레이션을 시작 하기 전에 구독에 대 한 지원 티켓 tooincrease에이 제한을 발생 시켜야 합니다.

- **프로 비전 VM 상태 아웃 시간이** -모든 VM의 hello 상태에 **프로비저닝이 시간 초과**,이 요구 toobe 마이그레이션 전 확인 합니다. hello 유일한 방법은 toodo 이것은 가동 중지 시간을 다시 프로 비전 해제/프로 비전 hello VM (hello 디스크에 유지 하 고 hello VM을 다시 만들, delete)입니다. 

- **RoleStateUnknown VM 상태** 인해 중지 되는 마이그레이션-tooa **역할 상태를 알 수 없는** 오류 메시지를 검사 hello 포털을 사용 하 여 VM hello 하 고 실행 중인지 확인 합니다. 이 오류는 일반적으로 몇 분 후에 자체적으로 해결되며(재구성 필요 없음), 종종 가상 컴퓨터 **시작**, **중지**, **다시 시작** 작업 중에 자주 나타나는 일시적인 유형입니다. **권장 사항:** 몇 분 후에 마이그레이션을 다시 시도합니다. 

- **패브릭 클러스터가 존재하지 않음** - 경우에 따라 뜻밖의 다양한 이유로 특정 VM을 마이그레이션할 수 없습니다. 이러한 알려진된 경우 중 하나에 hello VM hello 지난 주 정도) (내가 최근에 만들어졌으므로 및 Azure 리소스 관리자 작업을 위해 아직 되어 있지 않은 하는 Azure 클러스터 tooland 발생 한 경우입니다.  오류를 얻게 됩니다 **패브릭 클러스터 존재 하지 않는** hello VM 마이그레이션할 수 없습니다. Hello 클러스터는 Azure 리소스 관리자 사용 곧 이해 하는 대로 며칠 대기 중이 특정 문제에 일반적으로 해결 됩니다. 그러나 즉시 해결 방법 중 하나는 너무`stop-deallocate` VM hello, 한 다음 계속 앞으로 마이그레이션을 사용 되 고 시작 hello VM 백업 Azure 리소스 관리자에서 마이그레이션한 후 합니다.

### <a name="pitfalls-tooavoid"></a>문제 tooavoid

- 바로 가기 걸리고 hello 유효성을 검사/준비/abort 예행 마이그레이션을 생략 하지 마십시오.
- 아니지만 대부분,의 잠재적인 문제에 대해 노출할 hello 유효성을 검사/준비/abort 단계입니다.

## <a name="migration"></a>마이그레이션

### <a name="technical-considerations-and-tradeoffs"></a>기술적 고려 사항 및 장단점

이제 준비가 hello 알려진 사용자 환경 문제를 학습 하기 때문에 있습니다.

Hello 실제 마이그레이션에 대 한 tooconsider를 설정할 수 있습니다.

1. 계획 및 우선 순위 증가 따라 hello 가상 네트워크 (마이그레이션의 최소 단위)을 예약 합니다.  단순 가상 네트워크를 먼저 hello 수행 하 고 더 많은 hello 사용 하 여 진행률 가상 네트워크를 복잡 합니다.
2. 대부분의 고객은 비프로덕션 환경과 프로덕션 환경을 갖추게 되므로  프로덕션 환경을 마지막으로 예약합니다.
3. **(선택 사항)** 예기치 않은 문제가 발생할 경우에 대비하여 충분한 양의 버퍼로 유지 관리 가동 중지 시간을 예약합니다.
4. 문제가 발생할 경우 지원 팀과 연락하여 조정합니다.

### <a name="patterns-of-success"></a>성공 패턴

hello 기술 지침 hello 위의 랩 테스트 섹션에서에서 고려해 야 하며 이전 tooa 실제 마이그레이션 수 있습니다.  적절 한 테스트와 hello 마이그레이션은 실제로 이벤트가 아닌 합니다.  프로덕션 환경에 대 한 신뢰할 수 있는 Microsoft 파트너 또는 Microsoft 프리미어 서비스와 같은 유용한 toohave 추가 지원을 수도 있습니다.

### <a name="pitfalls-tooavoid"></a>문제 tooavoid

완전히 테스트 문제가 발생할 수 있습니다 및 hello 마이그레이션 지연 시간입니다.  

## <a name="beyond-migration"></a>마이그레이션 외

### <a name="technical-considerations-and-tradeoffs"></a>기술적 고려 사항 및 장단점

Azure 리소스 관리자 인 경우 했으므로 hello 플랫폼을 최대화 합니다.  읽기 hello [Azure 리소스 관리자 개요](../../azure-resource-manager/resource-group-overview.md) 추가 혜택에 대 한 아웃 toofind 합니다.

작업 tooconsider:

- 다른 활동을 사용 하 여 hello 마이그레이션을 번들입니다.  대부분의 고객은 응용 프로그램 유지 관리 기간을 선택합니다.  Toouse이 가동 중지 시간 tooenable 할 수 있으므로, 다른 Azure 리소스 관리자 기능 같은 암호화 및 마이그레이션 tooManaged 디스크.
- Hello 기술 및 비즈니스 상의 이유로 Azure 리소스 관리자에 대 한 다시 확인 hello 추가 서비스에 Azure 리소스 관리자 에서만 사용할 수 있는 적용 되는 tooyour 환경 사용 하도록 설정 합니다.
- PaaS 서비스를 사용하여 환경을 현대화합니다.

### <a name="patterns-of-success"></a>성공 패턴

서비스를 지금 원하는 tooenable Azure 리소스 관리자에 고의적인 수 있습니다.  많은 고객이 Azure 환경에 대 한 강력한 아래 hello를 찾습니다.

- [역할 기반 액세스 제어](../../azure-resource-manager/resource-group-overview.md#access-control)
- [쉽고 제어 가능한 배포를 위한 Azure Resource Manager 템플릿](../../azure-resource-manager/resource-group-overview.md#template-deployment)
- [태그](../../azure-resource-manager/resource-group-using-tags.md).
- [활동 제어](../../azure-resource-manager/resource-group-audit.md)
- [리소스 정책](../../azure-resource-manager/resource-manager-policy.md)

### <a name="pitfalls-tooavoid"></a>문제 tooavoid

이 기본 tooAzure 리소스 관리자 마이그레이션 여정을 시작 하는 이유를 기억 합니다.  Hello 원래 비즈니스 이유는 무엇 이었습니까? Hello 비즈니스 적 사유가 얻을 있습니다.


## <a name="next-steps"></a>다음 단계

* [클래식 tooAzure 리소스 관리자에서에서 리소스를 IaaS 플랫폼에서 지 원하는 마이그레이션 개요](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 플랫폼 지원에 기술 심층 분석](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 계획](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 PowerShell toomigrate IaaS 리소스를 사용 하 여](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 지원에 대 한 커뮤니티 도구](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [가장 일반적인 마이그레이션 오류 검토](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 IaaS 리소스에 대 한 가장 자주 묻는 질문 검토 hello](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
