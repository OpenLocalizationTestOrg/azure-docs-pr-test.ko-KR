---
title: "Microsoft Azure에서 aaaOracle 솔루션 | Microsoft Docs"
description: "Microsoft Azure의 Oracle 솔루션에 대한 지원되는 구성 및 제한 사항을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
manager: timlt
author: rickstercdn
tags: azure-resource-management
ms.assetid: 5d71886b-463a-43ae-b61f-35c6fc9bae25
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: rclaus
ms.openlocfilehash: 54dc62e76129535da7fb6f131af90c83adfec6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="oracle-solutions-and-their-deployment-on-microsoft-azure"></a>Microsoft Azure의 Oracle 솔루션 및 배포
이 문서에서는 Microsoft Azure에서 다양 한 Oracle 솔루션을 배포 하는 필수 toosuccesfully 정보를 다룹니다. 이러한 솔루션은 Azure 마켓플레이스 hello에 Oracle에서 게시 하는 가상 컴퓨터 이미지를 기반으로 합니다. hello 다음 명령을 실행 하는 현재 사용할 수 있는 이미지 목록 tooget:
```azurecli-interactive
az vm image list --publisher oracle -o table --all
```
이미지의 6-16-2017 hello 목록을 기준으로 hello 다음과가 같습니다.
```bash
Offer                   Publisher    Sku                     Urn                                                          Version
----------------------  -----------  ----------------------  -----------------------------------------------------------  -------------
Oracle-Database-Ee      Oracle       12.1.0.2                Oracle:Oracle-Database-Ee:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Database-Se      Oracle       12.1.0.2                Oracle:Oracle-Database-Se:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Linux            Oracle       6.4                     Oracle:Oracle-Linux:6.4:6.4.20141206                         6.4.20141206
Oracle-Linux            Oracle       6.7                     Oracle:Oracle-Linux:6.7:6.7.20161007                         6.7.20161007
Oracle-Linux            Oracle       6.8                     Oracle:Oracle-Linux:6.8:6.8.20161020                         6.8.20161020
Oracle-Linux            Oracle       6.9                     Oracle:Oracle-Linux:6.9:6.9.20170406                         6.9.20170406
Oracle-Linux            Oracle       7.0                     Oracle:Oracle-Linux:7.0:7.0.20141217                         7.0.20141217
Oracle-Linux            Oracle       7.2                     Oracle:Oracle-Linux:7.2:7.2.20161020                         7.2.20161020
Oracle-Linux            Oracle       7.3                     Oracle:Oracle-Linux:7.3:7.3.20170320                         7.3.20170320
Oracle-WebLogic-Server  Oracle       Oracle-WebLogic-Server  Oracle:Oracle-WebLogic-Server:Oracle-WebLogic-Server:12.1.2  12.1.2
```

이러한 이미지는 "사용자 라이선스가 필요"한 것으로 간주되며, 따라서 VM을 실행하는 데 발생한 계산, 저장소 및 네트워킹 비용만 청구됩니다.  사용 중인 올바르게 사용이 허가 된 toouse Oracle 소프트웨어 및 Oracle 있는 위치에서 현재 지원 계약 있다고 가정 합니다. Oracle는 온-프레미스 tooAzure에서 라이선스 이동성을 보장 합니다. 게시 된 hello 참조 [Oracle 및 Microsoft](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html) 라이선스 이동에 대 한 자세한 내용은 참고 합니다. 

개인 toobase가 솔루션은 Azure에서 처음부터 새로 만들거나 자신의 온-프레미스 환경에서 사용자 지정 이미지를 업로드 하는 사용자 지정 이미지에서 선택할 수도 수 있습니다.

## <a name="support-for-jd-edwards"></a>JD Edwards 지원
TooOracle 지원 참고에 따라 [Doc ID 2178595.1](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=573435677515785&id=2178595.1&_afrWindowMode=0&_adf.ctrl-state=o852dw7d_4) , JD Edwards EnterpriseOne 버전으로 9.2 이상에서 지원 **모든 공용 클라우드 제품** 구체적인에 맞는 `Minimum Technical Requirements` (MTR).  Toocreate 사용자 지정 이미지를 운영 체제 및 소프트웨어 응용 프로그램 호환성에 대 한 자신의 MTR 사양을 충족 해야 합니다. 

## <a name="oracle-database-virtual-machine-images"></a>Oracle Database 가상 컴퓨터 이미지
Oracle은 Oracle Linux 기반 가상 컴퓨터 이미지의 Azure에서 Oracle DB 12.1 Standard 및 Enterprise Edition을 실행하도록 지원합니다.  Azure에서 Oracle db 프로덕션 작업에 대 한 최상의 성능을 얻으려면 hello 있는지 tooproperly 크기 hello VM 이미지 될를 프리미엄 저장소에서 지원 되는 관리 되는 디스크를 사용 합니다. Tooquickly Oracle DB 어떻게 실행 중에에 대 한 지침은 Oracle hello를 사용 하 여 Azure VM 이미지를 게시 [hello Oracle DB 퀵 스타트 연습 시도](oracle-database-quick-create.md)합니다.

### <a name="attached-disk-configuration-options"></a>연결된 디스크 구성 옵션

연결 된 디스크 hello Azure Blob 저장소 서비스에 의존합니다. 각 표준 디스크는 이론적으로 최대 초당 500개의 입력/출력 작업(IOPS)을 할 수 있습니다. 우리의 프리미엄 디스크 기능 고성능 데이터베이스 작업에 대 한 기본 설정 이며 디스크당 too5000 IOps를 얻을 수 있습니다. 사용할 수 있지만 단일 디스크 성능을 충족 하는 경우 필요-여러 개의 연결 된 디스크를 사용 하 고, 데이터베이스 데이터 분산 다음 Oracle 자동 저장소 관리 (ASM)를 사용 하는 경우에 IOPS 성능을 효율적 hello를 향상 시킬 수 있습니다. Oracle ASM 관련 정보는 [Oracle 자동 저장소 개요](http://www.oracle.com/technetwork/database/index-100339.html)를 참조하세요. 방법의 예에 대 한 tooinstall hello를 시도할 수 있습니다-Azure Linux VM에서 Oracle ASM를 구성 하 고 [설치 및 저장소 관리를 자동화 된 Oracle 구성](configure-oracle-asm.md) 자습서입니다.

### <a name="oracle-realtime-application-cluster-rac"></a>Oracle RAC(Realtime Application Cluster)
Oracle RAC는 온-프레미스 다중 노드 클러스터 구성에서 단일 노드의 디자인 된 toomitigate hello 실패입니다.  네이티브 toohyper 규모의 공용 클라우드 환경 되지 않는 두 개의 온-프레미스 기술에 의존: 멀티 캐스트 네트워크 및 공유 디스크입니다. 타사 회사에서 만든 솔루션 [FlashGrid 같은](https://www.flashgrid.io/oracle-rac-in-azure/) 을 에뮬레이트하는 이러한 기술을 toodeploy Azure에서 Oracle RAC 필요 합니다. 

### <a name="high-availability-and-disaster-recovery-considerations"></a>높은 가용성 및 재해 복구 고려 사항
Azure에서 Oracle 데이터베이스를 사용할 때는 높은 가용성 및 재해 복구 솔루션 tooavoid 가동 중지 시간을 구현 해야 합니다. 

Azure에서 Oracle Database Enterprise Edition(RAC 제외)에 대한 고가용성 및 재해 복구는 두 가상 컴퓨터에 있는 두 개의 데이터베이스와 함께 [Data Guard, Active Data Guard](http://www.oracle.com/technetwork/articles/oem/dataguardoverview-083155.html) 또는 [Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate)를 사용하여 수행할 수 있습니다. 가상 컴퓨터 둘 다를 수에 hello 동일 [가상 네트워크](https://azure.microsoft.com/documentation/services/virtual-network/) tooensure hello 개인용 영구 IP 주소를 통해 서로 액세스할 수 있습니다.  또한 좋습니다 hello 가상 컴퓨터를 배치 hello에 동일한 가용성 집합 tooallow Azure tooplace 별도의 오류 도메인 및 업그레이드 도메인입니다.  Toohave 지리적 중복 하려는 다른 두 지역 간에 복제 하 여 연결 하 고 hello 두 개의 인스턴스가 있는 VPN 게이트웨이이 두 데이터베이스를 사용할 수 있습니다.

자습서는 "[Azure에서 Oracle DataGuard 구현](configure-oracle-dataguard.md)"는 안내 hello 기본 설정 절차 tootrial이 Azure에서.  

Oracle 데이터 가드로, 가상 컴퓨터에서 주 데이터베이스, 또 다른 가상 컴퓨터에서 보조(대기) 데이터 베이스에서 고가용성을 얻을 수 있으며, 양 데이터베이스 간에 단방향 복제를 설정할 수 있습니다. hello 결과 hello 데이터베이스의 읽기 권한을 toohello 복사본입니다. Oracle goldengate를 hello 두 데이터베이스 간의 양방향 복제를 구성할 수 있습니다. tooset 이러한 도구를 사용 하 여 데이터베이스에 대 한 고가용성 솔루션을 확인 하려면 어떻게 해야 toolearn [Active Data Guard](http://www.oracle.com/technetwork/database/features/availability/data-guard-documentation-152848.html) 및 [GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html) hello Oracle 웹 사이트에 대 한 설명서입니다. 하면 필요한 읽기 / 쓰기 액세스 toohello hello 데이터베이스 복사본을 사용 하 여 [Oracle Active Data Guard](http://www.oracle.com/uk/products/database/options/active-data-guard/overview/index.html)합니다.

자습서는 "[Azure에서 Oracle GoldenGate 구현](configure-oracle-golden-gate.md)"는 안내 hello 기본 seup 프로시저 tootrial이 Azure에서.

Azure에서 설계는 HA 및 DR 솔루션 하더라도 백업 전략에에서 있는 전체 toorestore 데이터베이스 tooensure 해야 합니다.  자습서는 [백업 및 복구 Oracle 데이터베이스](oracle-backup-recovery.md) consistant 백업을 설정 하기 위한 기본 절차 hello 안내 합니다.

## <a name="oracle-weblogic-server-virtual-machine-images"></a>Oracle WebLogic Server 가상 컴퓨터 이미지
* **클러스터링은 Enterprise Edition에서만 지원됩니다.** 사용이 허가 됩니다 WebLogic Server의 Enterprise Edition hello toouse 사용 하는 경우에 WebLogic 클러스터링 합니다. WebLogic Server Standard Edition으로 클러스터링을 사용하지 마십시오.
* **UDP 멀티 캐스트는 지원되지 않습니다.**  Azure는 UDP 유니캐스트를 지원하지만 멀티 캐스팅 및 브로드캐스팅은 지원하지 않습니다. WebLogic 서버는 Azure의 UDP 유니캐스트 기능에 수 toorely입니다. 최상의 결과 UDP 유니캐스트, 것이 좋습니다 hello WebLogic 클러스터 크기를 정적으로 유지 될에 대 한 또는 hello 클러스터에 포함 된 10 개의 관리 되는 서버를 유지 합니다.
* **WebLogic Server는 T3에 대해 동일한 경우에 액세스 (예를 들어 Enterprise JavaBeans를 사용 하 여) 공용 및 개인 포트 toobe hello가 필요 합니다.** **SLWLS**라는 vNet에 있는, 둘 이상의 VM으로 구성된 WebLogic Server 클러스터에서 서비스 계층(EJB) 응용 프로그램이 실행되는 다중 계층 시나리오를 고려해 보세요. hello에서 다른 서브넷에 hello 클라이언트 계층은 동일한 vNet을 hello 서비스 계층에서 EJB toocall를 시도 하는 단순한 Java 프로그램을 실행 합니다. 필요한 tooload 균형 hello 서비스 계층 이기 때문에 공용 부하 분산 된 끝점 toobe hello WebLogic Server 클러스터에에서 가상 컴퓨터 hello에 대 한 생성 해야 합니다. 지정 하는 hello 개인 포트 hello 공용 포트 (예를 들어 7006:7008)와에서 다른 경우에 hello 다음과 같은 오류가 발생 합니다.

       [java] javax.naming.CommunicationException [Root exception is java.net.ConnectException: t3://example.cloudapp.net:7006:

       Bootstrap to: example.cloudapp.net/138.91.142.178:7006' over: 't3' got an error or timed out]

   WebLogic Server는 T3 액세스에 대 한 hello 부하 분산 장치 포트를 요구 하 고 hello WebLogic 관리 서버 포트 toobe hello 동일 때문입니다. 대/소문자 위에 hello에서 hello 클라이언트 포트 7006 (부하 분산 장치 포트 hello)에 액세스 하 고 hello 관리 되는 서버는 7008 (개인 포트 hello)에서 수신 합니다. 이 제한은 T3 액세스에만 적용가능하며 HTTP에는 적용할 수 없습니다.

   tooavoid이 문제를 해결 방법 다음 hello 중 하나를 사용 합니다.

  * 사용 하 여 hello 개인 동일 부하에 대 한 공용 포트 번호 전용 끝점 tooT3 액세스 균등 하 게 합니다.
  * WebLogic Server를 시작할 때 JVM 매개 변수를 다음 hello를 다음과 같습니다.

         -Dweblogic.rjvm.enableprotocolswitch=true

관련 정보는 <http://support.oracle.com>에서 KB 문서 **860340.1**을 참조하세요.

* **동적 클러스터링 및 부하 분산 제한** Toouse WebLogic Server에서 동적 클러스터를 선택 하 고 끝점을 통해 단일, 공용 부하 분산 된 Azure에서 노출 가정 합니다. 이 고정 된 포트 번호를 사용 하 여 관리 하는 서버 (범위에서 할당 되지 동적으로) 각각 hello 및 관리자에 게 추적 하는 컴퓨터 보다 많은 관리 대상된 서버를 시작 하지 마십시오으로 수행할 수 있습니다 (즉, 여러 개 관리 virt 당 서버 ual 컴퓨터)입니다. 구성 중인 가상 컴퓨터 보다 시작 되 고 더 많은 WebLogic 서버에 따라 하는 경우 (즉, 여기서 여러 WebLogic Server 인스턴스 공유 hello 동일한 가상 컴퓨터), 이러한 WebLogic Server 인스턴스 중 하나 이상에 대 한 불가능 한 다음 서버 toobind tooa 포트 번호 – hello 해당 가상 컴퓨터에서 다른 사용자가 실패 합니다.

   Hello에 관리 서버 tooautomatically hello를 구성 하는 경우 고유 포트 번호 할당 tooits 관리 서버를 부하 분산 수 없으면 Azure 것 처럼 단일 공용 포트 toomultiple 개인 포트에서 매핑을 지원 하지 않으므로 다음 이 구성에 필요합니다.
* **가상 컴퓨터에서 Weblogic 서버의 여러 인스턴스입니다.** 배포의 요구 사항에 따라 hello 옵션 hello에서 WebLogic Server의 여러 인스턴스를 실행 해야 할 가상 컴퓨터가 hello 충분히 큰 경우 동일한 가상 컴퓨터. 예를 들어 두 개의 코어를 포함 하는 중간 크기 가상 컴퓨터에서 선택할 수 있습니다 toorun WebLogic Server의 두 인스턴스. 그러나 여전히 권장 되 WebLogic Server의 여러 인스턴스를 실행 하는 하나의 가상 컴퓨터를 사용한 경우 hello 사례 수 있는 아키텍처에 단일 실패 지점을 도입 하지 note 합니다. 두 개의 가상 컴퓨터를 사용하는 것이 더 나은 접근법이며, 각 가상 컴퓨터는 여러 WebLogic Server의 인스턴스를 실행할 수 있습니다. 각 WebLogic Server의이 인스턴스 수 hello 부분이 동일한 클러스터입니다. 그러나 참고, 현재 수 없으면 Azure 부하 분산 장치에 분산 하는 hello 부하 분산 서버 toobe 필요 하기 때문에 WebLogic Server 배포 내에 의해 노출 되는 Azure tooload 분산 toouse 끝점 hello 동일한 가상 컴퓨터 가상 컴퓨터를 고유 합니다.

## <a name="oracle-jdk-virtual-machine-images"></a>Oracle JDK 가상 컴퓨터 이미지
* **JDK 6 및7 최신 업데이트** Hello 최신 공용, 지원 되는 버전의 Java (현재 Java 8)를 사용 하 여을 권장 하는 동안 Azure 하면 JDK 6 및 7 이미지 사용할 수 있습니다. 이 항목은 레거시 응용 프로그램 준비 toobe 업그레이드 tooJDK 8이 아직을 위한 것입니다. 업데이트 tooprevious JDK 이미지 더 이상 사용할 수 있는 toohello 일반 대를 수 hello 지정 된 Microsoft Azure에서 제공 하는 7 이미지, Oracle 및 JDK 6 hello와 파트너 관계는 의도 된 것 toocontain에서 일반적으로 제공 하는 public이 아닌 최신 업데이트 Oracle tooonly의 Oracle 선택한 그룹의 고객 지원 되는 것입니다. 새 버전의 hello JDK 이미지 사용 가능 하 게 업데이트 된 릴리스가 출시 JDK 6 및 7의 시간에 따라 합니다.

   hello이 JDK 6에서 사용할 수 있는 JDK 7의 이미지 및 hello 가상 컴퓨터 및 이미지,에서 파생 된만 Azure 내에서 사용할 수 있습니다.
* **64비트 JDK.** hello Oracle WebLogic Server 가상 컴퓨터 이미지 및 Azure에서 제공 하는 hello Oracle JDK 가상 컴퓨터 이미지 hello 64 비트 버전의 Windows Server와 JDK hello 모두 포함 합니다.

## <a name="next-steps"></a>다음 단계
이제 Microsoft Azure의 현재 Oracle 솔루션에 대한 개요를 살펴보았습니다. 다음 단계는 toogo 하 고 Azure에서 Oracle 데이터베이스를 배포 합니다.
- Hello 시도 [Azure에서 Oracle 데이터베이스를 만들](oracle-database-quick-create.md) 자습서 tooget 시작 합니다.
