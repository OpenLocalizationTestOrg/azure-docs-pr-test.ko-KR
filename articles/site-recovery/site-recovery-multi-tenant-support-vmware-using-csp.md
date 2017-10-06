---
title: "VMware VM 복제 tooAzure (CSP 프로그램)에 대 한 aaaMulti 테 넌 트 지원 | Microsoft Docs"
description: "어떻게 다중 테 넌 트 환경 tooorchestrate 복제, 장애 조치 및 복구에 toodeploy Azure Site Recovery 온-프레미스 hello CSP 프로그램을 통해 VMware 가상 컴퓨터 (Vm) tooAzure hello Azure 포털을 사용 하 여 설명 합니다."
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: manayar
ms.openlocfilehash: 9be555c9a438f66e6d3dfcdc9f507a84763846d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-support-in-azure-site-recovery-for-replicating-vmware-virtual-machines-tooazure-through-csp"></a>Azure 사이트 복구에서 CSP 통해 VMware 가상 컴퓨터 tooAzure 복제 하기 위한 다중 테 넌 트 지원

Azure Site Recovery는 테넌트 구독을 위해 다중 테넌트 환경을 지원합니다. 또한 생성 및 hello Microsoft 클라우드 솔루션 공급자 (CSP) 프로그램을 통해 관리 되는 테 넌 트 구독에 대 한 다중 테 넌 트를 지원 합니다. 이 문서는의 구현 및 다중 테 넌 트 Azure에 VMware 시나리오를 관리 하기 위한 hello 지침을 설명 합니다. CSP를 통한 테넌트 구독 생성 및 관리도 설명합니다.

이 지침은 hello 기존 VMware 가상 컴퓨터 tooAzure 복제 설명서에서 과도 하 게 그립니다. 자세한 내용은 참조 [Site Recovery와 복제 VMware 가상 컴퓨터 tooAzure](site-recovery-vmware-to-azure.md)합니다.

## <a name="multi-tenant-environments"></a>다중 테넌트 환경
세 가지 주요 다중 테넌트 모델이 있습니다.

* **공유 호스팅 서비스 공급자 (HSP)**: hello 파트너 hello 실제 인프라를 소유 하 고 공유 리소스 (vCenter, 데이터 센터, 실제 저장소 및 등)를 사용 하 여 toohost 여러 테 넌 트의 Vm으로 동일한 인프라 hello 합니다. hello 파트너 관리 되는 서비스로 재해 복구 관리 하거나 hello 테 넌 트 셀프 서비스 솔루션으로 서 재해 복구를 소유할 수 있습니다.

* **호스팅 서비스 공급자 전용**: hello 파트너가 hello 실제 인프라 전용된 리소스 (여러 Vcenter, 실제 데이터 저장소 및 등)를 사용 하지만 소유 toohost 별도 인프라에 있는 각 테 넌 트의 Vm입니다. hello 파트너 관리 되는 서비스로 재해 복구 관리 하거나 hello 테 넌 트 셀프 서비스 솔루션으로 소유할 수 있습니다.

* **관리 서비스 공급자 (MSP)**: hello 고객 hello Vm을 호스팅하는 hello 실제 인프라를 소유 하 고 hello 파트너 재해 복구 구현 지원 및 관리를 제공 합니다.

## <a name="shared-hosting-multi-tenant-guidance"></a>공유 호스팅 다중 테넌트 지침
이 섹션에서는 hello 공유 호스팅 시나리오를 자세히 설명 합니다. hello 다른 두 가지 시나리오는 hello 공유 호스팅 시나리오의 하위 집합 hello를 사용 하 고 동일한 원칙입니다. hello 차이점 hello 끝 hello 공유 호스팅 지침에 설명 되어 있습니다.

hello 기본 다중 테 넌 트 시나리오에서 중요 한 점은 tooisolate hello 다양 한 테 넌 트입니다. 단일 테 넌 트 안 수 tooobserve의 hosted 다른 테 넌 트 됩니다. 이 요구 사항은 셀프 서비스 환경에서는 중요할 수 있으나 파트너 관리형 환경에서는 그만큼 중요하지 않습니다. 이 지침에서는 테넌트 격리가 필요한 것으로 가정합니다.

hello 아키텍처 hello 다음 다이어그램에에서 표시 됩니다.

![하나의 vCenter를 사용한 공유 HSP](./media/site-recovery-multi-tenant-support-vmware-using-csp/shared-hosting-scenario.png)  
**하나의 vCenter를 사용한 공유 호스팅 시나리오**

Hello 다이어그램 앞에서 같이 각 고객에 별도 관리 서버를 있습니다. 이 구성 제한 테 넌 트 tootenant 특정 Vm에 액세스 하 고 테 넌 트 격리를 활성화 합니다. VMware 가상 컴퓨터 복제 시나리오 hello 구성 서버 toomanage 계정 toodiscover Vm을 사용 하 고 에이전트를 설치 합니다. Hello 따릅니다 동일한 원칙 vCenter 통해 VM 검색 제한 hello 추가 사용 하 여 다중 테 넌 트 환경에 대 한 액세스 제어 합니다.

hello 데이터 격리 요구 사항 (예: 액세스 자격 증명) 모든 중요 한 인프라 정보가 알려지지 tootenants 된 상태를 유지 해야 합니다. 이러한 이유로 hello 관리 서버의 모든 구성 요소는 hello 파트너의 한 독점적인 제어권 hello에서 유지 하는 것이 좋습니다. hello 관리 서버 구성 요소입니다.
* 구성 서버(CS)
* 프로세스 서버(PS)
* 마스터 대상 서버(MT) 

확장 PS hello 파트너의 제어 이기도합니다.

### <a name="every-cs-in-hello-multi-tenant-scenario-uses-two-accounts"></a>두 개의 계정을 사용 하는 hello 다중 테 넌 트 시나리오에서 모든 CS

- **vCenter 액세스 계정**:이 계정 toodiscover 테 넌 트 Vm을 사용 합니다. Tooit (hello 다음 섹션에서 설명)으로 할당 된 vCenter 액세스 권한을 보유 합니다. toohelp 실수로 액세스 누수를 방지, 파트너 hello 구성 도구에서 이러한 자격 증명 자체를 입력 하는 것이 좋습니다.

- **가상 컴퓨터 액세스 계정을**: hello 테 넌 자동 푸시를 통해 Vm에이 계정 tooinstall hello 모바일 에이전트를 사용 합니다. 일반적으로 도메인 계정, 또는 hello 파트너 수를 직접 관리 또는 테 넌 트 tooa 파트너를 제공할 수 있습니다. 테 넌 트 싶어하지 tooshare hello 세부 정보 hello 파트너와 직접, 자신이 수 허용 기간 한정 통해 tooenter hello 자격 증명 액세스 toohello CS 하거나, hello 파트너의 지원을 사용 하면 모바일 에이전트를 수동으로 설치 합니다.

### <a name="requirements-for-a-vcenter-access-account"></a>vCenter 액세스 계정에 대한 요구 사항

Hello 섹션 앞에서 언급 했 듯이 특별 한 역할 할당 tooit 있는 계정으로 hello CS를 구성 해야 합니다. hello 역할 할당 해야 toohello vCenter 액세스 계정을 각 vCenter 개체에 대해 적용 하 고 toohello 자식 개체를 전파 되지 않습니다. 실수로 액세스 tooother 개체 액세스 전파 될 수 있으므로 테 넌 트 격리를 보장 하는이 구성 합니다.

![hello 전파 tooChild 개체 옵션](./media/site-recovery-multi-tenant-support-vmware-using-csp/assign-permissions-without-propagation.png)

hello 대신 tooassign hello 사용자 계정 및 hello 데이터 센터 개체에서 역할 이며 toohello 자식 개체를 전파 합니다. 다음 hello 계정에 부여 된 *에 액세스할 수 없는* 액세스할 수 없는 tooa 특정 테 넌 트 이어야 하는 모든 개체 (예: 다른 테 넌 트의 Vm)에 대 한 역할입니다. 이 구성은 번거롭게 이며 모든 새 자식 개체가 hello 부모 로부터 상속 되는 액세스도 자동으로 부여 되므로는 실수로 액세스 컨트롤을 노출 합니다. 따라서 hello 첫 번째 방법을 사용 하는 것이 좋습니다.

hello vCenter 계정 액세스 절차는 다음과 같습니다.

1. 미리 정의 된 hello를 복제 하 여 새 역할을 만들 *읽기 전용* 역할을 하 고 다음 편리한 이름 (예: Azure_Site_Recovery이이 예제에 표시 된 대로).

2. Hello 다음 사용 권한을 toothis 역할을 할당 합니다.

    * **데이터 저장소**: 공간 할당, 데이터 저장소 찾아보기, 낮은 수준 파일 작업, 파일 제거, 가상 컴퓨터 파일 업데이트

    * **네트워크**: 네트워크 할당

    * **리소스**: VM 할당 tooresource 풀, 전원 꺼짐 VM 마이그레이션, VM의 전원이 켜져 서 마이그레이션

    * **작업**: 만들기 작업, 업데이트 작업

    * **가상 컴퓨터**: 
        * 구성 > 모두
        * 상호 작용 -> 질문 응답, 장치 연결, CD 미디어 구성, 플로피 미디어 구성, 전원 끄기, 전원 켜기, VMware 도구 설치
        * 인벤토리 > 기존 항목에서 만들기, 새로 만들기, 등록, 등록 취소
        * 프로비전 -> 가상 컴퓨터 다운로드 허용, 가상 컴퓨터 파일 업로드 허용
        * 스냅숏 관리 > 스냅숏 제거

    ![hello 역할 편집 대화 상자](./media/site-recovery-multi-tenant-support-vmware-using-csp/edit-role-permissions.png)

3. 액세스 수준 toohello vCenter 계정 (hello CS 테 넌 트에 사용 됨)에 다양 한 개체를 다음과 같이 지정:

>| Object | 역할 | 설명 |
>| --- | --- | --- |
>| vCenter | 읽기 전용 | 서로 다른 개체를 관리 하기 위한 유일한 tooallow vCenter 액세스 필요 합니다. 되는 경우 hello 계정 되지 toobe tooa 테 넌 트를 제공 하거나 hello vCenter에 대 한 모든 관리 작업에 사용 되는이 사용 권한을 제거할 수 있습니다. |
>| 데이터 센터 | Azure_Site_Recovery |  |
>| 호스트 및 호스트 클러스터 | Azure_Site_Recovery | 다시만 액세스할 수 있는 호스트 및 테 넌 트 Vm 장애 조치 하기 전에 장애 복구 후 갖도록 hello 개체 수준에서 액세스 되는지 확인 합니다. |
>| 데이터 저장소 및 데이터 저장소 클러스터 | Azure_Site_Recovery | 앞과 동일합니다. |
>| 네트워크 | Azure_Site_Recovery |  |
>| 관리 서버 | Azure_Site_Recovery | Hello CS 컴퓨터 외부에 있는 모든 경우 (CS, PS, 및 MT) 액세스 tooall 구성 요소를 포함 합니다. |
>| 테넌트 VM | Azure_Site_Recovery | 통해 새 테 넌 트 특정 테 넌 트의 Vm에도이 액세스 권한을 얻기 하거나 hello Azure 포털을 통해 검색할 수 없습니다. |

hello vCenter 계정 액세스 이제 완료 되었습니다. 이 단계 hello 최소 권한 요구 사항 toocomplete 장애 복구 작업을 수행 합니다. 이러한 액세스 권한은 기존 정책과 함께 사용할 수도 있습니다. 방금 설명한 2 단계에서 있는 기존 사용 권한 집합 tooinclude의 역할 권한을 수정 합니다.

hello 장애 조치 상태가 될 때까지 toorestrict 재해 복구 작업 (즉, 장애 복구 기능 없이), hello 앞에 예외가 발생 하 여 절차를 따릅니다: hello를 할당 하는 대신 *Azure_Site_Recovery* 역할 toohello vCenter 액세스 계정으로 할당만는 *읽기 전용* 역할 toothat 계정. 이 권한 집합은 VM 복제 및 장애 조치(Failover)를 허용하지만 장애 복구(failback)는 허용하지 않습니다. Hello 앞에 프로세스의에서 다른 모든 그대로 유지 됩니다. tooensure 테 넌 트 격리 및 VM 검색, 모든 권한에 hello 개체 수준 및 전파 하지만 toochild 개체에 계속 할당 됩니다.

## <a name="other-multi-tenant-environments"></a>기타 다중 테넌트 환경

hello 방법을 설명 하는 섹션 앞에 오는 tooset 공유 호스팅 솔루션에 대 한 다중 테 넌 트 환경 구성 합니다. hello 다른 두 가지 주요 솔루션은 전용 호스팅 및 관리 되는 서비스입니다. 이러한 솔루션에 대 한 hello 아키텍처 hello 다음 섹션에에서 설명 되어 있습니다.

### <a name="dedicated-hosting-solution"></a>전용 호스팅 솔루션

Hello 다음 다이어그램에에서 나와 있는 것 처럼 전용된 호스팅 솔루션의 hello 아키텍처 차이 각 테 넌 트의 인프라에 대 한 해당 테 넌 트만 설정 되어 있는지는. 이기 때문에 테 넌 트 격리를 통해 별도 Vcenter hello 호스팅 공급자 공유 호스팅에 대해 제공 하는 hello CSP 단계를 따라 계속 해야 하지만 테 넌 트 격리에 대 한 tooworry 필요는 없습니다. CSP 설치는 변경되지 않고 유지됩니다.

![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/dedicated-hosting-scenario.png)  
**여러 vCenter를 사용한 전용 호스팅 시나리오**

### <a name="managed-service-solution"></a>관리형 서비스 솔루션

다음 다이어그램에서는 관리 되는 서비스 솔루션 아키텍처 차이 hello에서와 같이 hello로 각 테 넌 트의 인프라 다른 테 넌 트의 인프라에서 물리적으로 분리도 된다는 점입니다. 이 시나리오는 일반적으로 테 넌 트 hello hello 인프라를 소유 하 고 솔루션 공급자 toomanage 재해 복구 하려는 경우에 존재 합니다. 다시, 테 넌 트에서 다른 인프라를 통해 물리적으로 격리 되므로 hello 파트너 toofollow hello CSP 단계 공유 호스팅에 대해 제공 된 하지만 tooworry 테 넌 트 격리에 대 한 필요는 없습니다. CSP 프로비저닝은 그대로 유지됩니다.

![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/managed-service-scenario.png)  
**여러 vCenter를 사용하는 관리 서비스 시나리오**

## <a name="csp-program-overview"></a>CSP 프로그램 개요
hello [CSP 프로그램](https://partner.microsoft.com/en-US/cloud-solution-provider) 파트너 Office 365, Enterprise Mobility Suite 및 Microsoft Azure를 포함 하 여 모든 Microsoft 클라우드 서비스를 제공 하는 원활한 상호 스토리를 촉진 합니다. CSP를와 파트너 고객과 hello 종단 간 관계를 소유 하 고 hello 기본 관계 접점을 수 있습니다. 파트너는 고객에 대 한 Azure 구독을 배포 하 고 자신의 부가 가치, 사용자 지정 된 제품이 있는 hello 구독을 결합할 수 있습니다.

Azure Site Recovery와 파트너 CSP 통해 직접 고객에 대 한 hello 완벽 한 재해 복구 솔루션을 관리할 수 있습니다. 또는 CSP tooset 환경 Site Recovery를 사용 하 고 고객이 자신의 재해 복구 요구 사항을 셀프 서비스 방식으로 관리할 수 있습니다. 두 시나리오 모두 파트너는 사이트 복구와 고객 간의 hello 연락을 담당 합니다. 파트너는 hello 고객 관계 서비스 및 사이트 복구 사용에 대 한 고객 요금을 청구 합니다.

## <a name="create-and-manage-tenant-accounts"></a>테넌트 계정 만들기 및 관리

### <a name="step-0-prerequisite-check"></a>단계 0: 필수 구성 요소 확인

hello VM 필수 구성 요소는 hello hello에 설명 된 대로 동일한 [Azure Site Recovery 설명서](site-recovery-vmware-to-azure.md)합니다. 또한 toothose 필수 구성 요소에 있습니다 해야가 hello에 앞에서 언급 한 액세스 제어 CSP 통해 테 넌 트 관리를 계속 진행 하기 전에. 각 테 넌 트에 대 한 hello 테 넌 트 Vm 및 파트너의 vCenter와 통신할 수 있는 별도 관리 서버를 만듭니다. Hello 파트너에만 액세스 권한 toothis 서버를 있습니다.

### <a name="step-1-create-a-tenant-account"></a>1단계: 테넌트 계정 만들기

1. 통해 [Microsoft 파트너 센터](https://partnercenter.microsoft.com/), tooyour CSP 계정에 로그인 합니다. 
 
2. Hello에 **대시보드** 메뉴 선택 **고객**합니다.

    ![hello Microsoft 파트너 센터 고객 링크](./media/site-recovery-multi-tenant-support-vmware-using-csp/csp-dashboard-display.png)

3. 열리면 hello 페이지 클릭 hello **추가 고객** 단추입니다.

    ![hello 고객 추가 단추](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-new-customer.png)

4. Hello에 **신규 고객** 페이지 hello 계정 hello 테 넌 트에 대 한 세부 정보를 입력 하 고 클릭 **다음: 구독**합니다.

    ![hello 계정 정보 페이지](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-add-filled.png)

5. Hello 구독 선택 페이지에서 선택 hello **Microsoft Azure** 확인란 합니다. 지금 또는 나중에 다른 구독을 추가할 수 있습니다.

    ![Microsoft Azure 구독 hello 확인란](./media/site-recovery-multi-tenant-support-vmware-using-csp/azure-subscription-selection.png)

6. Hello에 **검토** 페이지 hello 테 넌 트 정보를 확인 하 고 클릭 **전송**합니다.

    ![hello 검토 페이지](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-summary-page.png)  

    Hello 테 넌 트 계정을 만든 후 확인 페이지가 표시 되는, 기본 계정 및 해당 구독에 대 한 암호를 hello hello의 hello 세부 정보를 표시 합니다. 

7. Hello 정보를 저장 하 고 나중에 필요에 따라 hello Azure 포털 로그인 페이지를 통해 hello 암호를 변경 합니다.  
 
    이라면 hello 테 넌 트와이 정보를 공유 하거나 만들고 필요한 경우 별도 계정을 공유할 수 있습니다.

### <a name="step-2-access-hello-tenant-account"></a>2 단계: hello 테 넌 트 계정에 액세스

에 설명 된 대로 hello 테 넌 트의 구독 hello Microsoft 파트너 센터 대시보드를 통해 액세스할 수 있습니다 "1 단계: 테 넌 트 계정을 만듭니다." 

1. Toohello 이동 **고객** 페이지를 선택한 다음 hello 테 넌 트 계정의 hello 이름을 클릭 합니다.

2. Hello에 **구독** 페이지 hello 테 넌 트 계정의 hello 기존 계정 구독을 모니터링 및 필요에 따라 더 많은 구독을 추가할 수 있습니다. toomanage hello 테 넌 트의 재해 복구 작업을 선택 **모든 리소스 (Azure 포털)**합니다.

    ![hello 모든 리소스 링크](./media/site-recovery-multi-tenant-support-vmware-using-csp/all-resources-select.png)  
    
    클릭 하면 **모든 리소스** toohello 테 넌 트의 Azure 구독 액세스 권한을 부여 합니다. Hello에 hello Azure Active Directory 링크를 클릭 하 여 액세스를 확인할 수 있습니다 hello Azure 포털의 오른쪽 위에 있습니다.

    ![Azure Active Directory 링크](./media/site-recovery-multi-tenant-support-vmware-using-csp/aad-admin-display.png)

이제 hello Azure 포털을 통해 테 넌 트 hello에 대 한 모든 사이트 복구 작업을 수행 하 고 hello 재해 복구 작업을 관리할 수 있습니다. 앞에서 설명한 다음 hello 프로세스를 tooaccess hello 테 넌 트 구독 CSP 통해 관리 되는 재해 복구에 대 한 합니다.

### <a name="step-3-deploy-resources-toohello-tenant-subscription"></a>3 단계: 리소스 toohello 테 넌 트 구독에 배포
1. Hello Azure 포털에서 리소스 그룹을 만들고 hello 일반적인 프로세스당 복구 서비스 자격 증명 모음을 배포 합니다. 
 
2. Hello 자격 증명 모음 등록 키를 다운로드 합니다.

3. Hello 자격 증명 모음 등록 키를 사용 하 여 hello 테 넌 트에 대 한 hello CS를 등록 합니다.

4. Hello 두 액세스 계정에 대 한 hello 자격 증명 입력: vCenter 액세스 계정 및 VM 계정에 액세스 합니다.

    ![관리자 구성 서버 계정](./media/site-recovery-multi-tenant-support-vmware-using-csp/config-server-account-display.png)

### <a name="step-4-register-site-recovery-infrastructure-toohello-recovery-services-vault"></a>4 단계: 등록 사이트 복구 인프라 toohello 복구 서비스 자격 증명 모음에
1. Hello Azure 포털에서 앞에서 만든 hello 자격 증명 모음에 등록 하는 hello vCenter 서버 toohello CS 등록에서 "3 단계: 리소스 toohello 테 넌 트 구독을 배포 합니다." 이 목적을 위해 hello vCenter 액세스 계정을 사용 합니다.
2. 사이트 복구에 대 한 hello 일반적인 프로세스당 hello "준비 인프라" 프로세스를 완료 합니다.
3. hello Vm 준비 toobe 복제 됩니다. 만 hello 테 넌 트의 Vm이 표시 되는지 확인 hello에 **가상 컴퓨터 선택** hello 아래 블레이드 **복제** 옵션입니다.

    ![Hello 선택 가상 컴퓨터 블레이드를 테 넌 트 Vm 목록](./media/site-recovery-multi-tenant-support-vmware-using-csp/tenant-vm-display.png)

### <a name="step-5-assign-tenant-access-toohello-subscription"></a>5 단계: 테 넌 트를 액세스 toohello 구독 할당

셀프 서비스 재해 복구를 위해 toohello 테 넌 트 hello 계정 세부 정보를 제공, hello의 6 단계에서 설명 했 듯이 "1 단계: 테 넌 트 계정 만들기" 섹션. Hello 파트너 hello 재해 복구 인프라를 설정한 후이 작업을 수행 합니다. 관리 되는 또는 셀프 서비스 hello 재해 복구 형식 인지 파트너 hello CSP 포털을 통해 테 넌 트 구독을 액세스 해야 합니다. hello 파트너 소유 자격 증명 모음을 설정 하 고 인프라 toohello 테 넌 트 구독을 등록 합니다.

또한 파트너 hello 다음을 수행 하 여 hello CSP 포털을 통해 새 사용자 toohello 테 넌 트 구독을 추가할 수 있습니다.

1. Toohello 테 넌 트의 CSP 구독 페이지에서 선택한 후 선택 hello **사용자 및 라이선스** 옵션입니다.

    ![hello 테 넌 트의 CSP 구독 페이지](./media/site-recovery-multi-tenant-support-vmware-using-csp/users-and-licences.png)

    이제 hello 관련 세부 정보를 입력 하 고 사용 권한을 선택 하 여 또는 CSV 파일의 사용자 목록을 hello를 업로드 하 여 새 사용자를 만들 수 있습니다.

2. 새 사용자를 만든 후 돌아가서 toohello Azure 포털을 선택한 다음 hello **구독** 블레이드, 선택 hello 관련 구독 합니다.

3. 열리면 hello 블레이드에서 선택 **액세스 제어 (IAM)**, 클릭 하 고 **추가** tooadd hello 관련 액세스 수준이 있는 사용자입니다.      
    hello CSP 포털을 통해 생성 된 hello 사용자 액세스 수준을 클릭 하면 열리는 hello 블레이드에 자동으로 표시 됩니다.

    ![사용자 추가](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-user-subscription.png)

    대부분의 관리 작업에 대 한 hello *참가자* 역할은 충분 합니다. 이 액세스 수준을 가진 사용자는 액세스 수준 변경(*소유자* 수준 액세스가 필요)을 제외하고 구독에 관한 모든 작업을 수행할 수 있습니다. 필요에 따라 hello 액세스 수준을 미세 조정할 수 있습니다.
