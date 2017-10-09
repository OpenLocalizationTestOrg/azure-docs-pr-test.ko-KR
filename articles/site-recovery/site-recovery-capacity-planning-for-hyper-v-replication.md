---
title: "사이트 복구를 위한 aaaRun hello Hyper-v 용량 계획 도구 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery에 대 한 toorun Hyper-v 용량 계획 도구 hello 하는 방법을 설명합니다"
services: site-recovery
documentationcenter: na
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 2bc3832f-4d6e-458d-bf0c-f00567200ca0
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: b853598e5cd290c48b59794ba48eefc72ac8ded6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-hyper-v-capacity-planner-tool-for-site-recovery"></a>사이트 복구에 대 한 hello Hyper-v 용량 계획 도구를 실행 합니다.

Azure 사이트 복구 배포의 일환으로, toofigure 복제 및 대역폭 요구 사항이 필요 합니다. 사이트 복구를 위한 용량 계획 도구 hello Hyper-v 사용 하면 있습니다 toodo이 Hyper-v 가상 컴퓨터 복제에 대 한 있습니다.

이 문서에서는 toorun Hyper-v 용량 계획 도구를 hello 하는 방법을 설명 합니다. 이 도구를 사용 하 여 hello 정보 해야 [사이트 복구를 위한 용량 계획](site-recovery-capacity-planner.md)합니다.

## <a name="before-you-start"></a>시작하기 전에
기본 사이트에서 Hyper-v 서버 또는 클러스터 노드의 hello 도구를 실행합니다. toorun hello 도구 hello Hyper-v 호스트 서버가 필요 합니다.

* 운영 체제: Windows Server 2012 또는 2012 R2
* 메모리: 20MB(최소)
* CPU: 5% 오버헤드(최소)
* 디스크 공간: 5MB(최소)

Hello 도구를 실행 하기 전에 tooprepare hello 기본 사이트가 필요 합니다. 간에 복제 하는 경우 두 개의 온-프레미스 사이트 있으며 toocheck 대역폭을 tooprepare 복제본 서버에도 필요 합니다.

## <a name="step-1-prepare-hello-primary-site"></a>1 단계: 준비 hello 기본 사이트

1. Hello 기본 사이트에서 tooreplicate, 및 hello Hyper-v 호스트/클러스터에 날짜별 hello 원하는 Hyper-v Vm의 모든 목록을 확인 합니다. hello 도구 함께 두만 단일 클러스터에 대 한 여러 독립 실행형 호스트에 대해 실행할 수 있습니다. 또한 필요한 toorun 개별적으로 각 운영 체제에 대 한 다음과 같은 Hyper-v 서버에 대 한 정보를 수집 해야 합니다.

   * Windows Server 2012 독립 실행형 서버
   * Windows Server 2012 클러스터
   * Windows Server 2012 R2 독립 실행형 서버
   * Windows Server 2012 R2 클러스터
2. 원격 액세스 tooWMI 모든 hello Hyper-v 호스트 및 클러스터에서 사용 하도록 설정 합니다. 각 서버/클러스터에서이 명령을 실행 toomake 있는지 방화벽 규칙 및 사용자 권한 설정 됩니다.

        netsh firewall set service RemoteAdmin enable
3. 다음과 같이 서버와 클러스터에서 성능 모니터링을 활성화합니다.

   * Hello로 열기 hello Windows 방화벽 **고급 보안이** 스냅인 다음 enable hello 다음 인바운드 규칙 및: **COM + 네트워크 액세스 (DCOM IN)** hello에서 모든 규칙 및 **원격 이벤트 로그 관리 그룹**합니다.

## <a name="step-2-prepare-a-replica-server-on-premises-tooon-premises-replication"></a>2 단계: 복제 서버 (온-프레미스 tooon 온-프레미스 복제) 준비
않아도 toodo이 tooAzure를 복제 하는 경우.

더미 VM 복제 tooit toocheck 대역폭 될 수 있도록 복구 서버로 단일 Hyper-v 호스트를 설정할 것이 좋습니다.  이 건너뛸 수 있지만 수행 하지 않는 한 수 toomeasure 대역폭 됩니다.

1. Toouse 하려는 경우 클러스터 노드가 hello 복제본으로 Hyper-v 복제본 브로커를 구성 합니다.

   * **서버 관리자**에서 **장애 조치 클러스터 관리자**를 엽니다.
   * Toohello 클러스터에 연결 하 고 hello 클러스터 이름이 강조 표시를 클릭 **동작** > **역할 구성** tooopen hello 고가용성 마법사.
   * **역할 선택**에서 **Hyper-V 복제본 브로커**를 클릭합니다. Hello 마법사에서 제공 된 **NetBIOS 이름** hello 및 **IP 주소** toobe hello 연결 지점 toohello 클러스터 (클라이언트 액세스 지점 이라고 함)으로 사용 합니다. hello **Hyper-v 복제본 브로커** 구성할 지, 점에 유의 해야 하는 클라이언트 액세스 지점 이름이 됩니다.
   * Hello Hyper-v 복제본 브로커 역할 성공적으로 온라인 상태가 되 고 hello 클러스터의 모든 노드 간에 장애 조치할 수를 확인 합니다. toodo hello 역할을 마우스 오른쪽 단추로 클릭이, 너무 가리킨**이동**, 클릭 하 고 **노드 선택**합니다. 노드 > **OK**를 선택합니다.
   * 인증서 기반 인증을 사용 하는 경우 모든 hello 인증서가 설치 되어 클라이언트 액세스 지점 hello 및 각 클러스터 노드를 확인 합니다.
2. 복제본 서버를 활성화합니다.

   * 클러스터에 대 한 오류 클러스터 관리자를 열고 toohello 클러스터에 연결 하 고 클릭 **역할** > 역할 선택 > **복제 설정을** > **복제본이이 클러스터 사용 서버**합니다. 클러스터를 사용 하 여 hello 복제본으로 toohave hello Hyper-v 복제본 브로커 역할이 기본 사이트 에서도 hello hello 클러스터에 필요 합니다.
   * 독립 실행형 서버의 경우 Hyper-V 관리자를 엽니다. Hello에 **동작** 창에서 클릭 **Hyper-v 설정** tooenable, 원하는 hello 서버에 대 한 및 **복제 구성** 클릭 **이 데이터베이스 사용 컴퓨터를 복제본 서버로**합니다.
3. 인증을 설정합니다.

   * **인증 및 포트**tooauthenticate hello 주 서버와 hello 인증 포트 방법을 선택 합니다. 인증서 한 번의 클릭을 사용 하는 경우 **인증서 선택** tooselect 하나입니다. Hello 기본 및 복구 Hyper-v 호스트가 hello에 경우에 Kerberos를 사용 하 여 동일한 도메인 또는 트러스트 된 도메인입니다. 서로 다른 도메인 또는 작업 그룹 배포의 경우 인증서를 사용합니다.
   * **권한 부여 및 저장소**, 허용 **모든** 서버 (주) toosend 복제 데이터 toothis 복제본 서버를 인증 합니다.

     ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image1.png)
   * 실행 **netsh http show servicestate**, toocheck 해당 hello 수신기가 실행 되는 hello 프로토콜/지정한 포트:  
4. 방화벽을 설정합니다. Hyper-v가 설치 하는 동안 방화벽 규칙이 hello 기본 포트 (443에 HTTPS, 80에 Kerberos)에서 tooallow 트래픽을 만들어집니다. 이러한 규칙을 다음과 같이 활성화합니다.
  - 클러스터에서 인증서 인증(443): ``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"}}``
  - 클러스터에서 Kerberos 인증(80): ``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"}}``
  - 독립 실행형 서버에서 인증서 인증: ``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"``
  - 독립 실행형 서버에서 Kerberos 인증: ``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"``

## <a name="step-3-run-hello-capacity-planner-tool"></a>3 단계: hello 용량 계획 도구를 실행합니다.
기본 사이트가 준비 복구 서버 설정 한 후에 hello 도구를 실행할 수 있습니다.

1. [다운로드](https://www.microsoft.com/download/details.aspx?id=39057) hello Microsoft 다운로드 센터에서에서 hello 도구입니다.
2. Hello 도구 hello 주 서버 중 하나 (또는 hello 주 클러스터에서 hello 노드 중 하나)에서 실행 합니다. Hello.exe 파일을 마우스 오른쪽 단추로 클릭 하 고 눌러 **관리자 권한으로 실행**합니다.
3. **시작 하기 전에**, 원하는 toocollect 데이터 기간을 지정 합니다. 프로덕션 시간 tooensure 데이터를 대표 하는 동안 hello 도구를 실행 하는 것이 좋습니다. Toovalidate 네트워크 연결을 시도 하는 경우 몇 분만에 대해 수집할 수 있습니다.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image2.png)
4. **주 사이트 세부 정보**, 독립 실행형 호스트에 대 한 hello 서버 이름이 나 FQDN을 지정 하거나 hello hello 클라이언트의 FQDN을 지정 하는 클러스터에 대 한 점, 클러스터 이름 또는 hello 클러스터에에서 있는 노드를 동의 하 고 클릭 **다음**. hello 도구는 hello 서버에서 실행 되 고 hello 이름을 자동으로 검색 합니다. Vm에 대 한 모니터링할 수 있는 도구 선택 hello hello 지정 된 서버입니다.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image3.png)
5. **복제본 사이트 정보**tooa 보조 데이터 센터에 복제 하는 경우에 복제 서버를 설정 하지 않았으면 선택 하거나 tooAzure를 복제 하는 경우, **복제본 사이트에 관련 된 테스트를 건너뜁니다**합니다. Tooa 보조 데이터 센터를 복제 하는 복제본 종류를 설정한 경우의 FQDN을 입력 hello 독립 실행형 서버 또는 클라이언트 액세스 지점 hello hello 클러스터에 대 한에서 **서버 이름 (또는) Hyper-v 복제본 브로커 CAP**합니다.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image4.png)
6. **확장 된 복제본 세부 정보**, 사용 하도록 설정 **Skip hello 테스트와 관련 된 확장 된 복제본 사이트**합니다. 이 테스트는 Site Recovery에서 지원되지 않습니다.
7. **선택 Vm tooReplicate**hello 주 서버에서 실행 되는 디스크, hello 설정에 따라에서 지정한 hello 및 toohello 서버 또는 클러스터를 연결 하 고 Vm을 표시 하는 hello 도구, **주 사이트 세부 정보**  페이지. 이미 복제에 대해 활성화되었거나 실행되고 있지 않은 VM은 표시되지 않습니다. Toocollect 메트릭을 원하는 hello Vm을 선택 합니다. Hello Vhd를 선택 하면 자동으로 너무 hello Vm에 대 한 데이터를 수집 합니다.
8. 복제본 서버 또는 클러스터에 구성 하는 경우 **네트워크 정보**를 구성한 경우 생각 hello 대략적인 WAN 대역폭을 hello 주 파일 그룹 및 복제본 사이트 간에 선택 hello 인증서 사용 지정 인증서 인증 합니다.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image5.png)
9. **요약**hello 설정을 확인 하 고 클릭 **다음** toobegin 메트릭을 수집 합니다. 도구 진행률과 상태 hello에 표시 되 **용량 계산** 페이지. 클릭 하 여 hello 도구 실행이 끝나면 **보고서 보기** tooview hello 출력 합니다. 기본적으로 보고서와 로그는 **%systemdrive%\Users\Public\Documents\Capacity Planner**에 저장됩니다.

   ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image6.png)

## <a name="step-4-interpret-hello-results"></a>4 단계: hello 결과 해석 합니다.

다음은 중요 한 메트릭을 hello입니다. 여기에 나열되지 않은 메트릭은  사이트 복구와 관련이 없는 것이므로 무시할 수 있습니다.

### <a name="on-premises-tooon-premises-replication"></a>온-프레미스 tooon 온-프레미스 복제

* Hello 주 호스트의 계산, 메모리에서 복제의 영향
* Hello, 주 복구 호스트의 저장소 디스크 공간 IOPS에 대 한 복제의 영향
* 델타 복제(Mbps)에 필요한 총 대역폭
* 기본 호스트 hello와 hello 복구 호스트 (Mbps) 간의 관찰 된 네트워크 대역폭
* Hello 이상적인 hello 두 호스트/클러스터 간에 활성 병렬 전송 수에 대 한 제안

### <a name="on-premises-tooazure-replication"></a>온-프레미스 tooAzure 복제

* Hello 주 호스트의 계산, 메모리에서 복제의 영향
* Hello 주 호스트의 저장소 디스크 공간, IOPS에 대 한 복제의 영향
* 델타 복제(Mbps)에 필요한 총 대역폭

## <a name="more-resources"></a>추가 리소스
* Hello에 포함 된 문서 hello 도구 다운로드 hello 도구에 대 한 자세한 정보를 참조 하세요.
* Keith Mayer에 hello 도구의 연습 동영상 [TechNet 블로그](http://blogs.technet.com/b/keithmayer/archive/2014/02/27/guided-hands-on-lab-capacity-planner-for-windows-server-2012-hyper-v-replica.aspx)합니다.
* [Hello 결과가](site-recovery-performance-and-scaling-testing-on-premises-to-on-premises.md) 우리의 성능 온-프레미스 tooon 온-프레미스 Hyper-v 복제에 대 한 테스트의

## <a name="next-steps"></a>다음 단계

용량 계획을 마친 후에는 Site Recovery 배포를 시작할 수 있습니다.

* [VMM 클라우드 tooAzure Hyper-v Vm 복제](site-recovery-vmm-to-azure.md)
* [Hyper-v Vm (VMM 없음) tooAzure 복제](site-recovery-hyper-v-site-to-azure.md)
* [VMM 사이트 간에 Hyper-V VM 복제](site-recovery-vmm-to-vmm.md)
