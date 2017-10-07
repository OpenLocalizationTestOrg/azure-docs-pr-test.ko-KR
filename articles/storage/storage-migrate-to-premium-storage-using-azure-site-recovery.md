---
title: "프리미엄 저장소를 Azure Site Recovery를 사용 하 여 aaaMigrating tooAzure | Microsoft Docs"
description: "프리미엄 저장소를 사이트 복구를 사용 하 여 기존 가상 컴퓨터 tooAzure 마이그레이션하십시오. 프리미엄 저장소는 Azure 가상 컴퓨터에서 실행되는 I/O 사용량이 많은 작업에 대해 대기 시간이 짧은 고성능 디스크 지원을 제공합니다."
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: luywang
ms.openlocfilehash: cb71c06e4a1a73d484e226a573d1ade48c87664d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-toopremium-storage-using-azure-site-recovery"></a>Azure Site Recovery를 사용 하 여 저장소 마이그레이션 tooPremium

[Azure Premium Storage](storage-premium-storage.md)는 I/O 사용량이 많은 작업을 실행하는 VM(가상 컴퓨터)에서 대기 시간이 짧은 고성능 디스크 지원을 제공합니다. hello이이 가이드의 목적은 toohelp 사용자 개인 VM 디스크가 표준 저장소 계정 tooa 프리미엄 저장소 계정에서에서 사용 하 여 마이그레이션 [Azure Site Recovery](../site-recovery/site-recovery-overview.md)합니다.

사이트 복구는 tooyour 비즈니스 연속성 영향을 주는 Azure 서비스 및 재해 복구 전략을 오케스트레이션 하 여 hello 온-프레미스 물리적 서버 및 Vm toohello 클라우드 (Azure) 또는 tooa 보조 데이터 센터의 복제 합니다. 기본 위치에서 중단이 발생할 때 장애 조치 toohello 보조 위치 tookeep 응용 프로그램 및 워크 로드에 사용할 수 있습니다. Toonormal 작업을 반환 하는 경우 백 tooyour 기본 위치를 실패 합니다. Site Recovery 테스트 장애 조치 toosupport 재해 복구 훈련 프로덕션 환경에 영향을 주지 않고 제공 합니다. 데이터 손상을 최소화하면서(복제 빈도에 따라) 예기치 않은 재해에 대해 장애 조치(failover)를 실행할 수 있습니다. Hello 시나리오에 tooPremium 저장소를 마이그레이션하는 데 hello [사이트 복구에서 장애 조치](../site-recovery/site-recovery-failover.md) Azure Site Recovery toomigrate 대상 디스크 tooa 프리미엄 저장소 계정에에서 있습니다.

마이그레이션하는 것이 좋습니다이 옵션 최소한의 가동 중지 시간을 제공 하 고 디스크를 복사 하 고 새 Vm을 만드는 hello 수동 실행을 방지 하기 때문에 사이트 복구를 사용 하 여 저장소 tooPremium 합니다. Site Recovery는 체계적으로 디스크를 복사하고 장애 조치(failover) 중 새 VM을 만듭니다. Site Recovery는 최소한의 가동 중지 시간 또는 가동 중지 시간 없이 다양한 유형의 장애 조치(failover)를 지원합니다. tooplan 가동 중지 시간 및 예상 데이터 손실 hello 참조 [유형의 장애 조치](../site-recovery/site-recovery-failover.md) 사이트 복구에서 테이블입니다. 경우 있습니다 [tooconnect tooAzure Vm 장애 조치 후 준비](../site-recovery/site-recovery-vmware-to-azure.md)를 Azure VM 수 tooconnect toohello 있어야 RDP를 사용 하 여 장애 조치 후 합니다.

![][1]

## <a name="azure-site-recovery-components"></a>Azure Site Recovery 구성 요소

이 hello Site Recovery 구성 요소 관련 toothis 마이그레이션 시나리오입니다.

* **구성 서버**는 통신을 조정하고 데이터 복제 및 복구 프로세스를 관리하는 Azure VM입니다. 이 VM에서이 단일 설치 파일 tooinstall hello 구성 서버와 복제 게이트웨이로 프로세스 서버 라고 하는 추가 구성 요소를 실행 합니다. [구성 서버 필수 조건](../site-recovery/site-recovery-vmware-to-azure.md)을 읽어보세요. 구성 서버만 toobe 한 번 구성 하며 모든 마이그레이션 toohello에 사용할 수 같은 지역입니다.

* **프로세스 서버** 소스 Vm에서에서 복제 데이터를 수신 하는 복제 게이트웨이 캐싱, 압축 및 암호화를 사용 하 여 hello 데이터를 최적화 하 고 tooa 저장소 계정 보냅니다. 또한 hello 이동성 서비스 toosource Vm의 강제 설치를 처리 하 고 원본 Vm의 자동 검색을 수행 합니다. hello 기본 프로세스 서버 hello 구성 서버에 설치 됩니다. 배포 추가 독립 실행형 프로세스 서버 tooscale를 배포할 수 있습니다. [프로세스 서버 배포에 대한 모범 사례](https://azure.microsoft.com/blog/best-practices-for-process-server-deployment-when-protecting-vmware-and-physical-workloads-with-azure-site-recovery/) 및 [추가 프로세스 서버 배포](../site-recovery/site-recovery-plan-capacity-vmware.md#deploy-additional-process-servers)를 읽어보세요. 프로세스 서버만 toobe 한 번 구성 하며 모든 마이그레이션 toohello에 사용할 수 같은 지역입니다.

* **모바일 서비스** 배포 되는 구성 요소는 원하는 tooreplicate 표준 모든 VM에 합니다. 데이터 쓰기를 캡처할 표준 VM hello 되 고 toohello 프로세스 서버에 전달 합니다. [복제된 컴퓨터 필수 조건](../site-recovery/site-recovery-vmware-to-azure.md)을 읽어보세요.

이 그래픽은 이러한 구성 요소가 어떻게 상호 작용하는지 보여 줍니다.

![][15]

> [!NOTE]
> 사이트 복구는 hello 마이그레이션 저장소 공간 디스크를 지원 하지 않습니다.

다른 시나리오에 대 한 추가 구성 요소를 참조 하십시오 너무[시나리오 아키텍처](../site-recovery/site-recovery-vmware-to-azure.md)합니다.

## <a name="azure-essentials"></a>Azure Essentials

이 마이그레이션 시나리오에 대 한 Azure 요구 사항을 hello는 이러한 합니다.

* Azure 구독
* Azure 프리미엄 저장소 계정 toostore 복제 된 데이터
* Azure 가상 네트워크 (VNet) toowhich Vm 장애 조치에 만들 때 연결 됩니다. hello Azure VNet에 있어야 사이트 복구에 실행 되는 hello에 hello으로 같은 지역 hello
* 어떤 toostore 복제 로그에 표준 Azure 저장소 계정입니다. 이 수 만큼 마이그레이션되는 hello VM 디스크 저장소 계정과 동일한 계정 hello

## <a name="prerequisites"></a>필수 조건

* Hello 섹션 앞의 hello 관련 마이그레이션 시나리오 구성 요소 이해
* Hello에 대 한 학습 하면 가동 중지 시간이 계획 [사이트 복구에서 장애 조치](../site-recovery/site-recovery-failover.md)

## <a name="setup-and-migration-steps"></a>설정 및 마이그레이션 단계

지역 간 또는 동일한 지역 내에서 사이트 복구 toomigrate Azure IaaS Vm을 사용할 수 있습니다. hello 다음 지침에 맞게 만들어졌습니다 hello 아티클에서이 마이그레이션 시나리오 [복제 VMware Vm 또는 실제 서버 tooAzure](../site-recovery/site-recovery-vmware-to-azure.md)합니다. 이 문서에 추가 toohello 지침에 설명 된 자세한 단계에 대 한 hello 링크를 수행 하십시오.

1. **Recovery Services 자격 증명 모음을 만듭니다**. 만들기 및 hello 통해 hello 사이트 복구 자격 증명 모음 관리 [Azure 포털](https://portal.azure.com)합니다. **새로 만들기** > **관리** > **백업** 및 **Site Recovery(OMS)**를 클릭합니다. 또는 **찾아보기** > **Recovery Services 자격 증명 모음** > **추가**를 클릭합니다. Vm 복제 toohello 영역이이 단계에서 지정 됩니다. Hello에서 마이그레이션 hello 목적을 위해 동일한 지역, 소스 Vm 및 저장소 계정은 소스를 선택 하는 hello 지역입니다. 마이그레이션 tooPremium 저장소 계정은 hello에만 지원 [Azure 포털](https://portal.azure.com), 하지 hello [클래식 포털](https://manage.windowsazure.com)합니다.

2. hello 다음 단계를 통해 하면 **보호 목표 선택**합니다.

    2a. Hello tooinstall hello 구성 서버를 원하는 VM에서 엽니다 hello [Azure 포털](https://portal.azure.com)합니다. 너무 이동**복구 서비스 자격 증명 모음** > **설정을**합니다. **설정**에서 **Site Recovery**를 선택합니다. **Site Recovery**에서 **1단계: 인프라 준비**를 선택합니다. **인프라 준비**에서 **보호 목표**를 선택합니다.

    ![][2]

    2b. 아래 **보호 목표**hello 첫 번째 드롭다운 목록에서 선택 **tooAzure**합니다. Hello 두 번째 드롭다운 목록에서 선택 **하지 가상화 된 / 기타**, 클릭 하 고 **확인**합니다.

    ![][3]

3. hello 다음 단계를 통해 하면 **hello 소스 환경 (구성 서버)를 설정**합니다.

    3a. Hello 다운로드 **Azure Site Recovery 통합 설치** 및 hello **자격 증명 모음 등록 키** toohello 이동 하 여 **준비 인프라**  >  **준비 소스** > **서버 추가** 블레이드입니다. Hello 자격 증명 모음 등록 키 toorun hello 통합 설정 해야 합니다. hello 키가 생성 한 후 5 일 동안 유효 합니다.

    ![][4]

    3b. Hello에서 구성 서버를 추가 **서버 추가** 블레이드입니다.

    ![][5]

    3c. Hello hello 구성 서버를 사용 하는 VM에서 통합 설치 tooinstall hello 구성 서버 및 hello 프로세스 서버를 실행 합니다. Hello 스크린 샷을 진행할 수 [여기](../site-recovery/site-recovery-vmware-to-azure.md) toocomplete hello 설치 합니다. 이 마이그레이션 시나리오에 대 한 지정 된 단계에 대 한 스크린 샷을 다음 toohello를 참조할 수 있습니다.

    **시작 하기 전에**선택, **hello 구성 서버와 프로세스 서버 설치**합니다.

    ![][6]

    3d. **등록**찾아 hello 자격 증명 모음에서 다운로드 한 hello 등록 키를 선택 합니다.

    ![][7]

    3e. **환경 정보**tooreplicate VMware Vm 거 여부를 선택 합니다. 이 마이그레이션 시나리오의 경우 **아니오**를 선택합니다.

    ![][8]

    3f. Hello 설치가 완료 되 면 hello 나타납니다 **Microsoft Azure 사이트 복구 구성 서버** 창. Hello를 사용 하 여 **계정 관리** 사이트 복구는 자동 검색에 사용할 수 있는 toocreate hello 계정을 탭 합니다. (물리적 컴퓨터를 보호 하는 방법에 대 한 hello 시나리오에서는 hello 계정 설정 관련 않지만 하나 이상 계정 tooenable 하나의 hello 단계를 수행 해야 합니다. 이 경우에서 이름을 지정할 수 있습니다 hello 계정 및 암호와.) 사용 하 여 hello **자격 증명 모음 등록** 탭 tooupload hello 자격 증명 모음 자격 증명 파일입니다.

    ![][9]

4. **Hello 대상 환경 설정**합니다. 클릭 **준비 인프라** > **대상**, 장애 조치 후 Vm에 대 한 toouse 원하는 hello 배포 모델을 지정 합니다. 시나리오에 따라 **클래식** 또는 **리소스 관리자**를 선택할 수 있습니다.

    ![][10]

    Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다. 프리미엄 저장소 계정 복제 된 데이터를 사용 하는 경우 추가 표준 저장소 계정 toostore 복제를 tooset을 필요를 로그 합니다.

5. **복제 설정을 지정합니다**. 따르십시오 [복제 설정을](../site-recovery/site-recovery-vmware-to-azure.md) 구성 서버를 만들면 hello 복제 정책이 성공적으로 연관 된 tooverify 합니다.

6. **용량 계획**. 사용 하 여 hello [용량 플래너](../site-recovery/site-recovery-capacity-planner.md) tooaccurately 예상 네트워크 대역폭, 저장소 및 기타 요구 사항 toomeet 복제 해야 합니다. 작업을 마쳤으면 **용량 계획을 완료하셨나요?**에서 **예**를 선택합니다.

    ![][11]

7. hello 다음 단계를 통해 하면 **모바일 서비스를 설치 하 고 복제를 사용 하도록 설정**합니다.

    7a. 너무 선택할 수 있습니다[강제 설치](../site-recovery/site-recovery-vmware-to-azure.md) tooyour 소스 Vm 또는 너무[이동성 서비스를 수동으로 설치할](../site-recovery/site-recovery-vmware-to-azure-install-mob-svc.md) 소스 Vm에 있습니다. 제공 된 hello 링크에서 푸시 설치의 hello 요구 사항 및 hello 수동 설치 관리자의 hello 경로 찾을 수 있습니다. 수동 설치를 수행 하는 경우 toouse 내부 IP 주소 toofind hello 구성 서버를 할 수 있습니다.

    ![][12]

    hello 실패 한 VM은 두 개의 임시 디스크: 기본 VM 및 hello 다른 hello hello 복구 영역에는 VM의 프로 비전 시 만든 hello에서 하나입니다. tooexclude hello 임시 디스크 복제 하기 전에 복제를 활성화 하기 전에 hello 모바일 서비스를 설치 합니다. toolearn tooexclude 임시 디스크 hello 하는 방법에 대 한 자세한 참조 너무[디스크 복제에서 제외할](../site-recovery/site-recovery-vmware-to-azure.md)합니다.

    7b. 이제 다음과 같이 복제를 활성화합니다.
      * **응용 프로그램 복제** > **원본**을 클릭합니다. 활성화 한 후 추가 컴퓨터에 대 한 hello 자격 증명 모음 tooenable 복제에서 복제 +는 처음으로 hello에 대 한 복제 클릭 합니다.
      * 1단계에서 프로세스 서버로 원본을 설정합니다.
      * 2 단계에서 hello 장애 조치 후 배포 모델를 프리미엄 저장소 계정 toomigrate, 표준 저장소 계정 toosave 로그 및를 가상 네트워크 toofail를 지정 합니다.
      * 3 단계에서 IP 주소를 통해 보호 되는 Vm을 추가 (내부 IP 주소 toofind 해야 해당).
      * 4 단계에서 이전에 hello 프로세스 서버에서 설정한 hello 계정을 선택 하 여 hello 속성을 구성 합니다.
      * 5 단계에서 복제 설정을 설정 이전에 만든 hello 복제 정책을 선택 합니다.
      **확인**을 클릭하고 복제를 활성화합니다.

    > [!NOTE]
    > Azure VM은 할당 취소 되 고 다시 시작 하는 경우 가져오게 됩니다을 보장 하지 있습니다 hello 동일한 IP 주소입니다. Hello 구성 서버/프로세스 서버 또는 hello hello IP 주소 변경 Azure Vm을 보호 하는 경우이 시나리오에서는 hello 복제 제대로 작동 하지 수도 있습니다.

    ![][13]

    Azure Storage 환경을 디자인할 때 가용성 집합의 각 VM에 대해 별도의 저장소 계정을 사용하는 것이 좋습니다. 너무 hello hello 저장소 계층의 모범 사례를 수행 하는 것이 좋습니다[여러 저장소 계정을 사용 하 여 각 가용성 집합에 대 한](../virtual-machines/windows/manage-availability.md)합니다. VM 디스크 toomultiple 저장소 계정은 배포 tooimprove 저장소 가용성을 사용 하면 한 hello Azure 저장소 인프라를 통해 hello I/O를 배포 합니다. Vm에 하나의 저장소 계정에 모든 Vm의 디스크를 복제 하는 대신 가용성 집합에 있는 경우 높은 여러 Vm을 여러 번 마이그레이션하 있도록 좋습니다 hello Vm에 hello 동일한 단일 저장소 계정의 가용성 집합을 공유 하지 않습니다. 사용 하 여 hello **복제 사용** 블레이드 tooset를 한 번에 하나씩 각 VM에 대해 대상 저장소 계정입니다. Tooyour 필요에 따라 장애 조치 후 배포 모델을 선택할 수 있습니다. 관리자 RM (리소스)로 장애 조치 후 배포 모델을 선택 하면 RM VM tooan RM VM을 장애 조치할 수 있습니다 또는 클래식 VM tooan RM VM 장애 조치할 수 있습니다.

8. **테스트 장애 조치(failover)를 실행합니다**. toocheck 프로그램 복제가 완료 되 면 있는지 여부를 사이트 복구를 클릭 한 다음 클릭 **설정** > **복제 항목**합니다. Hello 상태 및 복제 프로세스의 백분율 나타납니다. 초기 복제 후 테스트 장애 조치 toovalidate 완전 하 고 실행을 복제 전략입니다. 테스트 장애 조치의 자세한 단계를 참조 하십시오 너무[사이트 복구에서 테스트 장애 조치 실행](../site-recovery/site-recovery-vmware-to-azure.md)합니다. 테스트 장애 조치에서의 hello 상태를 확인할 수 **설정** > **작업** > **YOUR_FAILOVER_PLAN_NAME**합니다. Hello 블레이드에서 hello 단계 및 성공/실패 결과 간략하게를 표시 됩니다. 어느 단계에서 hello 테스트 장애 조치에 실패 하면 hello 단계 toocheck hello 오류 메시지를 클릭 합니다. Vm 및 복제 전략 장애 조치를 실행 하기 전에 hello 요구 사항을 만족 하는지 확인 합니다. 읽기 [사이트 복구에서 테스트 장애 조치 tooAzure](../site-recovery/site-recovery-test-failover-to-azure.md) 자세한 내용 및 지침은의 테스트 장애 조치 합니다.

9. **장애 조치(Failover) 실행**. Hello 테스트 장애 조치 완료 되 면 장애 조치 toomigrate 프로그램 디스크 tooPremium 저장소를 실행 하 고 hello VM 인스턴스를 복제 합니다. 따르십시오 hello 자세한 단계에서 [장애 조치를 실행할](../site-recovery/site-recovery-failover.md#run-a-failover)합니다. 선택 했는지 확인 **Vm을 종료 하 고 hello 최신 데이터를 동기화** toospecify Site Recovery 보호 hello Vm 아래로 tooshut를 시도 하 고 hello hello 데이터의 최신 버전은 장애 조치 되도록 hello 데이터를 동기화 해야 합니다. 이 옵션을 선택 하지 않으면 또는 hello 시도가 성공 하지 못한 경우에 VM hello에 대 한 hello 사용 가능한 최근 복구 지점에서 hello 장애 조치가 됩니다. 사이트 복구와 동일 하거나 유사한 tooa 프리미엄 저장소-지원 VM hello 형식이 VM 인스턴스를 만들어집니다. 너무 이동 하 여 hello 성능 및 가격이 다양 한 VM 인스턴스를 확인할 수[Windows 가상 컴퓨터 가격](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) 또는 [Linux 가상 컴퓨터 가격](https://azure.microsoft.com/pricing/details/virtual-machines/linux/)합니다.

## <a name="post-migration-steps"></a>마이그레이션 후 단계

1. **해당 하는 경우 설정 된 복제 된 Vm toohello 가능 여부 구성**합니다. 사이트 복구는 가용성 집합 hello 함께 마이그레이션 Vm을 지원 하지 않습니다. 복제 된 VM의 hello 배포에 따라 hello 다음 중 하나를 수행 합니다.
  * Hello 클래식 배포 모델을 사용 하 여 만든 VM에 대 한: hello Azure 포털에서에서 설정 하는 hello VM toohello 가용성을 추가 합니다. 자세한 단계에 대 한 이동 너무[기존 가상 컴퓨터 tooan 가용성 집합을 추가](../virtual-machines/windows/classic/configure-availability.md#addmachine)합니다.
  * Hello 리소스 관리자 배포 모델에 대 한: hello VM의 구성을 저장 한 후 다음 삭제을 hello 가용성 집합의 hello Vm을 다시 만듭니다. 사용 하 여 hello 스크립트에서 toodo [설정 Azure 리소스 관리자 VM 가용성 집합](https://gallery.technet.microsoft.com/Set-Azure-Resource-Manager-f7509ec4)합니다. 이 스크립트의 hello 제한을 확인 하 고 hello 스크립트를 실행 하기 전에 가동 중지 시간을 계획 합니다.

2. **이전 VM 및 디스크를 삭제합니다**. 이 삭제 하기 전에 hello 프리미엄 디스크 소스 디스크와 새 Vm hello 원본 Vm 역할을 할 동일 hello를 수행 하는 hello와 일치 하는지을 확인 하십시오. Hello 관리자 RM (리소스) 배포 모델에서 hello VM을 삭제 하 고 hello Azure 포털에서에서 원본 저장소 계정에서 hello 디스크를 삭제 합니다. Hello 클래식 배포 모델에서 VM hello 및 hello 클래식 포털 또는 Azure 포털에서 디스크를 삭제할 수 있습니다. 에 hello 디스크는 삭제 되지 hello VM을 삭제 하는 경우에 하는 문제가 있는 경우 참조 하십시오. [Vhd를 삭제 하면 오류 문제 해결](storage-resource-manager-cannot-delete-storage-account-container-vhd.md)합니다.

3. **클린 hello Azure 사이트 복구 인프라**합니다. 사이트 복구를 더 이상 필요한 경우 복제 된 항목, hello 구성 서버 및 hello 복구 정책을 삭제 한 후 hello Azure Site Recovery 자격 증명 모음을 삭제의 인프라를 정리할 수 없습니다.

## <a name="troubleshooting"></a>문제 해결

* [가상 컴퓨터 및 물리적 서버를 위한 보호 모니터링 및 문제 해결](../site-recovery/site-recovery-monitoring-and-troubleshooting.md)
* [Microsoft Azure Site Recovery 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)

## <a name="next-steps"></a>다음 단계

Hello 다음 가상 컴퓨터 마이그레이션에 대 한 특정 시나리오에 대 한 리소스를 참조 하십시오.

* [저장소 계정 간에 Azure 가상 컴퓨터 마이그레이션](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [만들고 Windows Server VHD tooAzure 업로드 합니다.](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [만들고 해당 Contains hello Linux 운영 체제 가상 하드 디스크를 업로드 합니다.](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [AWS Amazon tooMicrosoft Azure에서에서 가상 컴퓨터를 마이그레이션하거나](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

또한, 다음 Azure 저장소 및 Azure 가상 컴퓨터에 대 한 자세한 리소스 toolearn hello를 참조 하십시오.

* [Azure 저장소](https://azure.microsoft.com/documentation/services/storage/)
* [Azure 가상 컴퓨터](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [프리미엄 저장소: Azure 가상 컴퓨터 워크로드를 위한 고성능 저장소](storage-premium-storage.md)

[1]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-1.png
[2]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-2.png
[3]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-3.png
[4]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-4.png
[5]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-5.png
[6]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-6.PNG
[7]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-7.PNG
[8]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-8.PNG
[9]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-9.PNG
[10]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-10.png
[11]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-11.PNG
[12]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-12.PNG
[13]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-13.png
[14]:../site-recovery/media/site-recovery-vmware-to-azure/v2a-architecture-henry.png
[15]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-14.png
