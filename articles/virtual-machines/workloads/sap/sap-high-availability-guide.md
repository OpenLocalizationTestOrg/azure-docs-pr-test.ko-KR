---
title: "가상 컴퓨터의 SAP NetWeaver에 대 한 고가용성 aaaAzure | Microsoft Docs"
description: "Azure Virtual Machines의 SAP NetWeaver에 대한 고가용성 가이드입니다."
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a>SAP NetWeaver에 대한 Azure Virtual Machines 고가용성

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



Azure 가상 컴퓨터에는 최소한의 시간 및 긴 조달 주기 없이 계산, 저장소 및 네트워크 리소스를 필요로 하는 조직 위한 hello 솔루션입니다. Azure 가상 컴퓨터 toodeploy 클래식와 같은 응용 프로그램의 SAP NetWeaver 기반 ABAP, Java 및 ABAP + Java 스택을 사용할 수 있습니다. 추가 온-프레미스 리소스 없이도 안정성과 가용성을 확장할 수 있습니다. Azure Virtual Machines는 크로스-프레미스 연결을 지원하므로 Azure Virtual Machines를 조직의 온-프레미스 도메인, 사설 클라우드 및 SAP 시스템 지형에 통합할 수 있습니다.

이 문서에서는 수행할 수 있는 toodeploy SAP 시스템 가용성이 높은 Azure의 hello Azure 리소스 관리자 배포 모델을 사용 하 여 hello 단계를 다룹니다. 다음과 같은 주요 작업을 진행하게 됩니다.

* 오른쪽 SAP Note 및 설치 가이드 hello에 나열 된 hello 찾습니다 [리소스] [ sap-ha-guide-2] 섹션. 이 문서는 SAP 설치 설명서를 보완 하 게 하는 hello 기본 리소스는 SAP Note 설치 및 특정 플랫폼에 SAP 소프트웨어를 배포 합니다.
* Hello hello Azure 리소스 관리자 배포 모델 및 hello Azure 클래식 배포 모델의 차이점에 알아봅니다.
* Azure 배포에 적합 한 hello 모델을 선택할 수 있도록 Windows Server 장애 조치 클러스터링 쿼럼 모드에 알아봅니다.
* Azure 서비스의 Windows Server 장애 조치 클러스터링 공유 Storage에 대해 자세히 알아보세요.
* Toohelp 오류의 단일 지점 구성 요소와 같은 고급 비즈니스 응용 프로그램 프로그래밍 (ABAP) SAP 중앙 서비스 (ASCS)을 보호 하는 방법에 대해 알아봅니다 SAP 중앙 서비스 SCS () 및 데이터베이스 관리 시스템 (DBMS)와 중복 구성 요소 등의 SAP / Azure에서 응용 프로그램 서버
* Azure Resource Manager를 사용하여 Azure의 Windows Server 장애 조치 클러스터링 클러스터에서 고가용성 SAP 시스템을 설치하고 구성하는 단계별 작업 예제를 따르세요.
* Windows Server 장애 조치 클러스터링 Azure에서 추가 단계가 필요한 toouse 하지만 온-프레미스 배포에 필요 하지 않은 방법을 알아봅니다.

사용 하 여 toosimplify 배포 하 고이 문서에서는 구성 SAP 3 계층 가용 리소스 관리자 템플릿을 hello 합니다. hello 템플릿 고가용성 SAP 시스템에 필요한 hello 전체 인프라의 배포를 자동화 합니다. hello 인프라는 SAP 시스템의 SAP 응용 프로그램 성능 표준 (SAPS) 크기 조정도 지원합니다.

## <a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> 필수 조건
시작 하기 전에 hello 다음 섹션에서에서 설명 하는 hello 필수 구성 요소를 충족 하는지 확인 합니다. 또한 있는지 toocheck hello에 나열 된 모든 리소스를 될 [리소스] [ sap-ha-guide-2] 섹션.

이 문서에서는 [관리 디스크를 사용하는 3계층 SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/)용 Azure Resource Manager 템플릿을 사용합니다. 유용한 템플릿 개요를 보려면 [SAP Azure Resource Manager 템플릿](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/)을 참조하세요.

## <a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> 리소스
이 문서에서는 Azure의 SAP 배포에 대해 설명합니다.

* [SAP NetWeaver에 대한 Azure Virtual Machines 계획 및 구현][planning-guide]
* [SAP NetWeaver에 대한 Azure Virtual Machines 배포][deployment-guide]
* [SAP NetWeaver에 대한 Azure Virtual Machines DBMS 배포][dbms-guide]
* [SAP NetWeaver에 대한 Azure Virtual Machines 고가용성(이 가이드)][sap-ha-guide]

> [!NOTE]
> 가능 하면 항상 저희가 SAP 설치 가이드를 참조 하는 링크 toohello (hello 참조 [SAP 설치 가이드][sap-installation-guides]). 필수 구성 요소와 그 좋습니다 tooread hello SAP NetWeaver 설치 안내를 신중 하 게 hello 설치 프로세스에 대 한 정보입니다. 이 문서에서는 Azure Virtual Machines와 함께 사용할 수 있는 SAP NetWeaver 기반 시스템에 대한 특정 작업만 다룹니다.
>
>

이러한 SAP Note는 Azure에서 sap 관련된 toohello 항목:

| Note 번호 | 제목 |
| --- | --- |
| [1928533] |Azure의 SAP 응용 프로그램: 지원 제품 및 크기 조정 |
| [2015553] |Microsoft Azure의 SAP: 지원 필수 조건 |
| [1999351] |향상된 SAP용 Azure 모니터링 |
| [2178632] |Microsoft Azure의 SAP용 주요 모니터링 메트릭 |
| [1999351] |Windows에서의 가상화: 향상된 모니터링 |
| [2243692] |SAP DBMS 인스턴스에 Azure Premium SSD Storage 사용 |

Hello에 대 한 자세한 [Azure 구독 제한인][azure-subscription-service-limits-subscription], 일반 기본 제한 및 최대 제한 사항을 포함 합니다.

## <a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>가용성이 높은 SAP hello Azure 클래식 배포 모델 및 Azure 리소스 관리자와
hello Azure 리소스 관리자 및 Azure 클래식 배포 모델 hello 다음 영역에서에서 달라 집니다.

- 리소스 그룹
- Azure 내부 부하 분산 장치에 hello Azure 리소스 그룹에 대 한 종속성
- SAP 다중 SID 지원 시나리오

### <a name="f76af273-1993-4d83-b12d-65deeae23686"></a> 리소스 그룹
Azure 리소스 관리자를 사용할 수 있습니다 리소스 그룹 toomanage hello 응용 프로그램 리소스를 모두 Azure 구독에서. 리소스 그룹에는 통합 된 접근 방식을 모든 리소스는 hello 같은 수명 주기 합니다. 예를 들어 모든 리소스가 생성 hello에서 동일한 시간 및 이러한 hello 시에 삭제 됩니다 동시 합니다. [리소스 그룹](../../../azure-resource-manager/resource-group-overview.md#resource-groups)에 대해 알아봅니다.

### <a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure 내부 부하 분산 장치에 hello Azure 리소스 그룹에 대 한 종속성

Hello Azure 클래식 배포 모델에서 hello Azure 내부 부하 분산 장치 (Azure 부하 분산 장치 서비스)와 hello 클라우드 서비스 간의 종속성이 있습니다. 모든 내부 부하 분산 장치에는 하나의 클라우드 서비스가 필요합니다.

Azure 리소스 관리자의 모든 Azure 리소스에는 Azure 리소스 그룹에 배치 toobe 필요 하며이 Azure 부하 분산 장치에 대 한 유효한 것입니다. 그러나 Azure 부하 분산 장치 당 필요 toohave 하나의 Azure 리소스 그룹이 없으므로, 예를 들어 하나의 Azure 리소스 그룹 여러 Azure 부하 분산 장치를 포함할 수 있습니다. hello 환경에 더 간단 하 고 보다 유연 합니다. 

### <a name="support-for-sap-multi-sid-scenarios"></a>SAP 다중 SID 지원 시나리오

Azure Resource Manager에서 하나의 클러스터에 여러 SAP SID(시스템 식별자) ASCS/SCS 인스턴스를 설치할 수 있습니다. 각 Azure 내부 부하 분산 장치의 여러 IP 주소에 대한 지원으로 인해 다중 SID 인스턴스가 가능합니다.

toouse hello Azure 클래식 배포 모델에 설명 된 hello 절차를 수행 하십시오 [Azure에서 SAP NetWeaver: SIOS datakeeper를 통해 Azure에서 Windows Server 장애 조치 클러스터링을 사용 하 여 클러스터링 SAP ASCS/SCS 인스턴스에](http://go.microsoft.com/fwlink/?LinkId=613056)합니다.

> [!IMPORTANT]
> SAP 설치에 대 한 hello Azure 리소스 관리자 배포 모델을 사용 하는 것이 좋습니다. Hello 클래식 배포 모델에서 사용할 수 없는 많은 이점을 제공 합니다. Azure [배포 모델][virtual-machines-azure-resource-manager-architecture-benefits-arm]에 대해 자세히 알아봅니다.   
>
>

## <a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server 장애 조치 클러스터링
Windows Server 장애 조치 클러스터링은 고가용성 SAP ASCS/SCS 설치 및 Windows의 DBMS의 hello 기반 합니다.

장애 조치 클러스터는 1 + n 독립 서버 (노드) 응용 프로그램 및 서비스의 tooincrease hello 가용성 함께 작동 하는 그룹입니다. 노드 오류가 발생할 경우 hello는 정상 상태를 유지 관리 하는 동안 발생할 수 있는 오류 수를 계산 Windows Server 장애 조치 클러스터링 tooprovide 응용 프로그램 및 서비스를 클러스터 합니다. 다른 쿼럼 모드 tooachieve 장애 조치 클러스터링에서 선택할 수 있습니다.

### <a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> 쿼럼 모드
Windows Server 장애 조치 클러스터링을 사용하는 경우 다음 4개의 쿼럼 모드 중에서 선택할 수 있습니다.

* **노드 과반수**. Hello 클러스터의 각 노드에 응답할 수 있습니다. hello 클러스터 에서만 작동 과반수 응답이, 즉, 절반 이상이 hello로 응답 합니다. 노드 수가 균일하지 않은 클러스터에 대해 이 옵션을 사용하는 것이 좋습니다. 예를 들어 7 노드 클러스터에 세 개의 노드 실패 수 및 hello 클러스터 스틸 대부분을 toorun를 계속 합니다.  
* **노드 및 디스크 과반수**. 각 노드와 hello 클러스터 저장소의 지정 된 디스크 (디스크 감시) 사용할 수 있을 때 및 통신에 응답할 수 있습니다. hello 클러스터 에서만 작동 대부분 hello의 절반 이상이 hello 응답으로 즉, 응답 합니다. 이 모드는 노드 수가 짝수인 클러스터 환경에 적합합니다. 절반 hello 노드 및 디스크 hello 온라인 인 경우 hello 클러스터 정상 상태로 유지 됩니다.
* **노드 및 파일 공유 과반수**. Hello 노드 및 파일 공유를 사용할 수 있는지 여부에 관계 없이 고 통신 관리자 hello 하는 지정 된 파일 공유 (파일 공유 감시)을 만듭니다 더하기에 각 노드에서 투표 수 있습니다. hello 클러스터 에서만 작동 대부분 hello의 절반 이상이 hello 응답으로 즉, 응답 합니다. 이 모드는 노드 수가 짝수인 클러스터 환경에 적합합니다. 비슷한 toohello 노드 및 디스크 과반수 모드 있지만 미러링 모니터 파일 공유 감시 디스크 대신 사용 합니다. 이 모드는 쉽게 tooimplement 하지만 가용성이 높지 않은 자체 hello 파일 공유 하는 경우, 단일 실패 지점이 않을 수 있습니다.
* **과반수 없음: 디스크만**. 하나의 노드가 사용 가능 하 고 hello 클러스터 저장소의 특정 디스크와 통신의 경우 hello 클러스터에 쿼럼이 있습니다. 해당 디스크와의 통신에도 있는 hello 노드만 hello 클러스터에 가입할 수 있습니다. 이 모드는 사용하지 않는 것이 좋습니다.
 

## <a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server 장애 조치 클러스터링 온-프레미스
그림 1에서는 두 노드 클러스터를 보여 줍니다. Hello hello 노드 사이의 네트워크 연결 실패 하 고 두 노드를 유지 하 고 실행, 쿼럼 디스크 또는 파일 공유 결정 tooprovide hello 클러스터의 응용 프로그램 및 서비스 노드에 계속 됩니다. hello 노드가 액세스 toohello 쿼럼 디스크 또는 파일 공유를 통해 서비스 계속 hello 노드가 합니다.

이 예에서는 2 개 노드 클러스터를 사용 하므로 hello 노드 및 파일 공유 과반수 쿼럼 모드 사용 합니다. hello 노드 및 디스크 과반수는 올바른 옵션이 합니다. 프로덕션 환경에서는 쿼럼 디스크를 사용하는 것이 좋습니다. 네트워크 및 저장소 시스템 기술 toomake에서는 항상 사용 가능한 것입니다.

![그림 1: Azure에서 SAP ASCS/SCS에 대한 Windows Server 장애 조치 클러스터링 구성 예제][sap-ha-guide-figure-1000]

_**그림 1:** Azure에서 SAP ASCS/SCS에 대한 Windows Server 장애 조치 클러스터링 구성 예제_

### <a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> 공유 Storage
그림 1에는 2 노드 공유 Storage 클러스터도 나와 있습니다. 온-프레미스 공유 저장소 클러스터를 사용 하는 hello 클러스터의 모든 노드에서 공유 저장소를 검색합니다. Hello 데이터 손상 으로부터 보호 하는 잠금 메커니즘 합니다. 모든 노드는 다른 노드에 장애가 있는지 알 수 있습니다. 한 노드가 실패 하면 hello 남아 있는 노드 hello 저장소 리소스의 소유권을 가져오면 및 hello 서비스의 가용성을 보장 합니다.

> [!NOTE]
> SQL Server와 같은 일부 DBMS 응용 프로그램에서는 가용성을 높이기 위해 공유 디스크를 사용할 필요가 없습니다. SQL Server Always On hello 한 개의 클러스터 노드 toohello 다른 클러스터 노드의 로컬 디스크의 로컬 디스크에서 DBMS 데이터 및 로그 파일을 복제합니다. 이 경우 hello Windows 클러스터 구성에는 공유 디스크가 필요 하지 않습니다.
>
>

### <a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> 네트워킹 및 이름 확인
클라이언트 컴퓨터에 연결할 hello 클러스터 가상 IP 주소와 가상 호스트 이름을 통해 DNS 서버를 제공 하는 hello. hello 온-프레미스 노드 및 hello DNS 서버에서 여러 IP 주소를 처리할 수 있습니다.

표준 설치에서는 다음 두 가지 이상의 네트워크 연결을 사용합니다.

* 전용된 연결이 toohello 저장소
* Hello 하트 비트에 대 한 클러스터 내부 네트워크 연결
* 클라이언트가 tooconnect toohello 클러스터를 사용 하는 공용 네트워크

## <a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Azure의 Windows Server 장애 조치 클러스터링
Toobare 금속 또는 사설 클라우드 배포에 비해 Azure 가상 컴퓨터에 Windows Server 장애 조치 클러스터링 하는 추가 단계 tooconfigure 필요 합니다. 공유 클러스터 디스크를 빌드할 때 hello SAP ASCS/SCS 인스턴스에 tooset 여러 IP 주소와 가상 호스트 이름이 필요 합니다.

이 문서에서는 주요 개념에 설명 하 고 Azure의 SAP 고가용성 중앙 서비스 클러스터는 추가 단계가 필요한 toobuild hello 합니다. Hello 타사 도구 SIOS DataKeeper를 tooset 및 어떻게 tooconfigure hello Azure 내부 부하 분산 장치에 어떻게 하면 보여줍니다. Azure에서 파일 공유 미러링 모니터 서버와 이러한 도구 toocreate Windows 장애 조치 클러스터를 사용할 수 있습니다.

![그림 2: 공유 디스크를 사용하지 않는 Azure의 Windows Server 장애 조치 클러스터링 구성][sap-ha-guide-figure-1001]

_**그림 2:** 공유 디스크를 사용하지 않는 Azure의 Windows Server 장애 조치 클러스터링 구성_

### <a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> SIOS DataKeeper를 사용한 Azure의 공유 디스크
고가용성 SAP ASCS/SCS 인스턴스를 위해서는 클러스터 공유 Storage가 필요합니다. 2016 년 9 월의 Azure 제공 하지 않으면 공유 저장소를 공유 저장소 클러스터 toocreate를 사용할 수 있습니다. 제 3 자 소프트웨어 SIOS DataKeeper Cluster Edition toocreate 클러스터 공유 저장소를 시뮬레이션 하는 미러된 저장소를 사용할 수 있습니다. hello SIOS 솔루션 동기 실시간 데이터 복제를 제공합니다. 다음은 클러스터에 대한 공유 디스크 리소스를 만드는 방법입니다.

1. 추가 디스크 tooeach hello 가상 컴퓨터 (Vm)의 Windows 클러스터 구성에 연결 합니다.
2. 두 가상 컴퓨터 노드에서 SIOS DataKeeper Cluster Edition을 실행합니다.
3. Hello 대상 가상 컴퓨터의 hello 원본 가상 컴퓨터 toohello 추가 디스크를 연결 된 볼륨에서 hello 추가 디스크를 연결 된 볼륨의 hello 콘텐츠를 미러링합니다 SIOS DataKeeper Cluster Edition을 구성 합니다. SIOS DataKeeper 소스 및 대상 로컬 볼륨 hello를 추상화 한 다음 공유 디스크로 서버 장애 조치 클러스터링 tooWindows 제공 합니다.

[SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/)에 대한 자세한 정보를 참조하세요.

![그림 3: SIOS DataKeeper를 사용하는 Azure의 Windows Server 장애 조치 클러스터링 구성][sap-ha-guide-figure-1002]

_**그림 3:** SIOS DataKeeper를 사용하는 Azure의 Windows Server 장애 조치 클러스터링 구성_

> [!NOTE]
> SQL Server와 같은 일부 DBMS 제품에서는 가용성을 높이기 위해 공유 디스크를 사용할 필요가 없습니다. SQL Server Always On hello 한 개의 클러스터 노드 toohello 다른 클러스터 노드의 로컬 디스크의 로컬 디스크에서 DBMS 데이터 및 로그 파일을 복제합니다. 이 경우 hello Windows 클러스터 구성에는 공유 디스크가 필요 하지 않습니다.
>
>

### <a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Azure의 이름 확인
hello Azure 클라우드 플랫폼 hello 옵션 tooconfigure 가상 IP 주소, 예: 부동 IP 주소를 제공 하지 않습니다. 가상 IP 주소 tooreach hello 클러스터에서에서 리소스를 hello 클라우드는 대체 솔루션 tooset이 필요합니다.
Azure 내부 부하 분산 장치는 hello Azure 부하 분산 서비스에 저장 합니다. Hello 내부 부하 분산 장치와 클라이언트 hello 클러스터 가상 IP 주소를 통해 hello 클러스터에 도달 합니다.
Toodeploy hello 내부 부하 분산 장치 hello 클러스터 노드를 포함 하는 hello 리소스 그룹에 필요 합니다. 그런 다음 모든 필요한 포트 전달 규칙 hello 프로브와 hello 내부 부하 분산 장치의 포트를 구성 합니다.
hello 클라이언트 hello 가상 호스트 이름을 통해 연결할 수 있습니다. hello DNS 서버 hello 클러스터 IP 주소와 toohello hello 클러스터의 활성 노드를 전달 하는 hello 내부 부하 분산 장치 핸들 포트를 확인 합니다.

## <a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Azure IaaS(Infrastructure-as-a-Service)의 SAP NetWeaver 고가용성
tooachieve SAP 소프트웨어 구성 요소에 대해 다음과 같은 구성 요소가 tooprotect hello 해야와 같은 응용 프로그램 고가용성 SAP:

* SAP 응용 프로그램 서버 인스턴스
* SAP ASCS/SCS 인스턴스
* DBMS 서버

고가용성 시나리오에서 SAP 구성 요소 보호에 대한 자세한 내용은 [SAP NetWeaver에 대한 Azure Virtual Machines 계획 및 구현][planning-guide-11]을 참조하세요.

### <a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> 고가용성 SAP 응용 프로그램 서버
일반적으로 hello SAP 응용 프로그램 서버 및 대화 상자 인스턴스는 특정 가용성 우선 솔루션이 필요 하지 않습니다. 중복성으로 고가용성을 달성하고 다른 Azure Virtual Machines 인스턴스에서 여러 대화 상자 인스턴스를 구성합니다. 두 개의 Azure Virtual Machines 인스턴스에 2개 이상의 SAP 응용 프로그램 인스턴스가 설치되어 있어야 합니다.

![그림 4: 고가용성 SAP 응용 프로그램 서버][sap-ha-guide-figure-2000]

_**그림 4:** 고가용성 SAP 응용 프로그램 서버_

호스트 SAP 응용 프로그램 서버 인스턴스가 동일한 Azure 가용성 집합 hello는 모든 가상 컴퓨터를 배치 해야 합니다. Azure 가용성 집합은 다음을 확인합니다.

* Hello의 일부인 모든 가상 컴퓨터가 동일한 도메인을 업그레이드 합니다. 업그레이드 도메인에 있는 예를 들어 실행 하면 hello 가상 컴퓨터 되지 업데이트 hello에 시간 동안 가동 중지 시간이 계획 된 유지 관리 합니다.
* Hello의 일부인 모든 가상 컴퓨터가 동일한 장애 도메인입니다. 오류 도메인 예를 들어 하면 제대로 모든 가상 컴퓨터의 hello 사용할 수 없는 단일 실패 지점이 되도록 가상 컴퓨터 배포 됩니다.

너무 방법에 대 한 자세한[관리 가상 컴퓨터의 가용성을 hello][virtual-machines-manage-availability]합니다.

관리 되지 않는 디스크 에서만: 중요 한 toohave 변수가 hello Azure 저장소 계정에 잠재적인 단일 실패 지점이 이므로 두 개 이상의 Azure 저장소 계정, 두 개 이상의 가상 컴퓨터 배포 됩니다. 이상적인 설치 프로그램에서 다른 저장소 계정에 SAP 대화 상자 인스턴스를 실행 하는 각 가상 컴퓨터의 디스크 hello이 배포 합니다.

### <a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> 고가용성 SAP ASCS/SCS 인스턴스
그림 5는 고가용성 SAP ASCS/SCS 인스턴스의 예입니다.

![그림 5: 고가용성 SAP ASCS/SCS 인스턴스][sap-ha-guide-figure-2001]

_**그림 5:** 고가용성 SAP ASCS/SCS 인스턴스_

#### <a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Azure에서 Windows Server 장애 조치 클러스터링을 사용한 SAP ASCS/SCS 인스턴스 고가용성
Toobare 금속 또는 사설 클라우드 배포에 비해 Azure 가상 컴퓨터에 Windows Server 장애 조치 클러스터링 하는 추가 단계 tooconfigure 필요 합니다. Windows 장애 조치 클러스터 toobuild 필요 공유 클러스터 디스크, 여러 개의 IP 주소가, 여러 가상 호스트 이름 및 Azure 내부 부하 분산 장치는 SAP ASCS/SCS 인스턴스를 클러스터링 합니다. 이 부분은 hello 문서 뒷부분에 보다 자세히 합니다.

![그림 6: SIOS DataKeeper를 사용하는 Azure의 SAP ASCS/SCS용 Windows Server 장애 조치 클러스터링 구성][sap-ha-guide-figure-1002]

_**그림 6:** SIOS DataKeeper를 사용하는 Azure의 SAP ASCS/SCS용 Windows Server 장애 조치 클러스터링 구성_

### <a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a> 고가용성 DBMS 인스턴스
hello DBMS은는 SAP의 단일 접촉 지점입니다. Tooprotect 필요한 고가용성 솔루션을 사용 하 여 합니다. Windows Server 장애 조치 클러스터링 및 hello Azure 내부 부하 분산 장치, 그림 7 Azure에서 SQL Server Always On 고가용성 솔루션을 보여 줍니다. SQL Server Always On은 자체 DBMS 복제를 사용하여 DBMS 데이터 및 로그 파일을 복제합니다. 이 경우 없습니다 필요를 클러스터링 할 공유 디스크 hello 전체 설치를 단순화 하 합니다.

![그림 7: SQL Server Always On을 사용하는 고가용성 SAP DBMS 예제][sap-ha-guide-figure-2003]

_**그림 7:** SQL Server Always On을 사용하는 고가용성 SAP DBMS 예제_

Hello Azure 리소스 관리자 배포 모델을 사용 하 여 Azure의 SQL Server를 클러스터링 하는 방법에 대 한 자세한 내용은 다음이 문서를 참조 합니다.

* [Resource Manager를 사용하여 Azure Virtual Machines에서 수동으로 Always On 가용성 그룹 구성][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]
* [Azure에서 Always On 가용성 그룹에 대한 Azure 내부 부하 분산 장치 구성][virtual-machines-windows-portal-sql-alwayson-int-listener]

## <a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> 종단간 고가용성 배포 시나리오

### <a name="deployment-scenario-using-architectural-template-1"></a>아키텍처 템플릿 1을 사용하여 배포 시나리오

그림 8에서는 **단일** SAP 시스템을 위한 Azure의 SAP NetWeaver 고가용성 아키텍처 예제를 보여 줍니다. 이 시나리오는 다음과 같이 설정됩니다.

- 하나의 전용된 클러스터 hello SAP ASCS/SCS 인스턴스에 사용 됩니다.
- 하나의 전용된 클러스터 hello DBMS 인스턴스에서 사용 됩니다.
- SAP 응용 프로그램 서버 인스턴스는 자체의 전용 VM에 배포됩니다.

![그림 8: ASCS/SCS 및 DBMS용 전용 클러스터를 사용하는 SAP 고가용성 아키텍처 템플릿 1][sap-ha-guide-figure-2004]

_**그림 8:** SAP 고가용성 아키텍처 템플릿 1, ASCS/SCS 및 DBMS용 전용 클러스터_

### <a name="deployment-scenario-using-architectural-template-2"></a>아키텍처 템플릿 2를 사용하여 배포 시나리오

그림 9에서는 **단일** SAP 시스템을 위한 Azure의 SAP NetWeaver 고가용성 아키텍처 예제를 보여 줍니다. 이 시나리오는 다음과 같이 설정됩니다.

- 하나의 전용된 클러스터에 사용 되 **둘 다** hello SAP ASCS/SCS 인스턴스 및 DBMS hello 합니다.
- SAP 응용 프로그램 서버 인스턴스는 자체의 전용 VM에 배포됩니다.

![그림 9: SAP 고가용성 아키텍처 템플릿 2 - ASCS/SCS 전용 클러스터 및 DBMS 전용 클러스터][sap-ha-guide-figure-2005]

_**그림 9:** SAP 고가용성 아키텍처 템플릿 2 - ASCS/SCS 전용 클러스터 및 DBMS 전용 클러스터_

### <a name="deployment-scenario-using-architectural-template-3"></a>아키텍처 템플릿 3을 사용하여 배포 시나리오

그림 10에서는 &lt;SID1&gt; 및 &lt;SID2&gt;의 **두** SAP 시스템을 위한 Azure의 SAP NetWeaver 고가용성 아키텍처의 예제를 보여 줍니다. 이 시나리오는 다음과 같이 설정됩니다.

- 하나의 전용된 클러스터에 사용 되 **둘 다** hello SAP ASCS/SCS SID1 인스턴스 *및* hello SAP ASCS/SCS SID2 인스턴스 (클러스터).
- 하나의 전용 클러스터는 DBMS SID1에 사용되고 다른 전용 클러스터는 DBMS SID2에 사용됩니다(두 개의 클러스터).
- SAP 시스템 SID1 hello에 대 한 SAP 응용 프로그램 서버 인스턴스는 전용된 Vm을 가집니다.
- SAP 시스템 SID2 hello에 대 한 SAP 응용 프로그램 서버 인스턴스는 전용된 Vm을 가집니다.

![그림 10: SAP 고가용성 아키텍처 템플릿 3 - 다른 ASCS/SCS 인스턴스 전용 클러스터][sap-ha-guide-figure-6003]

_**그림 10:** SAP 고가용성 아키텍처 템플릿 3 - 다른 ASCS/SCS 인스턴스 전용 클러스터_

## <a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Hello 인프라 준비

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a>템플릿 1 아키텍처에 대 한 hello 인프라 준비
SAP용 Azure Resource Manager 템플릿은 필요한 리소스의 배포를 간소화하도록 도와줍니다.

hello 3 계층 템플릿은 Azure 리소스 관리자는 또한 두 클러스터에 있는 템플릿 1 아키텍처와 같은 고가용성 시나리오를 지원 합니다. 각 클러스터는 SAP ASCS/SCS 및 DBMS에 대한 SAP 단일 실패 지점입니다.

이 문서에서 설명 하는 hello 예제 시나리오에 대 한 Azure 리소스 관리자 템플릿을 읽을 수 있는 다음과 같습니다.

* [Azure Marketplace 이미지](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [관리 디스크를 사용하는 Azure Marketplace 이미지](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [사용자 지정 이미지](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [관리 디스크를 사용하는 사용자 지정 이미지](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

템플릿 1 아키텍처에 대 한 tooprepare hello 인프라:

- Hello hello에 Azure 포털에서에서 **매개 변수** 블레이드 hello **SYSTEMAVAILABILITY** 상자 **HA**합니다.

  ![그림 11: SAP 고가용성 Azure Resource Manager 매개 변수 설정][sap-ha-guide-figure-3000]

_**그림 11:** SAP 고가용성 Azure Resource Manager 매개 변수 설정_


  hello 템플릿을 만듭니다.

  * **가상 컴퓨터**:
    * SAP 응용 프로그램 서버 가상 컴퓨터: <*SAPSystemSID*>-di-<*Number*>
    * ASCS/SCS 클러스터 가상 컴퓨터: <*SAPSystemSID*>-ascs-<*Number*>
    * DBMS 클러스터: <*SAPSystemSID*>-db-<*Number*>

  * **연결된 IP 주소를 갖는 모든 가상 컴퓨터에 대한 네트워크 카드**:
    * <*SAPSystemSID*>-nic-di-<*Number*>
    * <*SAPSystemSID*>-nic-ascs-<*Number*>
    * <*SAPSystemSID*>-nic-db-<*Number*>

  * **Azure Storage 계정(비관리 디스크에만 해당)**

  * 다음에 대한 **가용성 그룹**:
    * SAP 응용 프로그램 서버 가상 컴퓨터: <*SAPSystemSID*>-avset-di
    * SAP ASCS/SCS 클러스터 가상 컴퓨터: <*SAPSystemSID*>-avset-ascs
    * DBMS 클러스터 가상 컴퓨터: <*SAPSystemSID*>-avset-db

  * **Azure 내부 부하 분산 장치**:
    * Hello ASCS/SCS 인스턴스 및 IP 주소에 대 한 모든 포트와 <*SAPSystemSID*> 파운드-ascs
    * Hello SQL Server DBMS 및 IP 주소에 대 한 모든 포트와 <*SAPSystemSID*> 파운드-db

  * **네트워크 보안 그룹**: <*SAPSystemSID*>-nsg-ascs-0  
    * 열린 외부 프로토콜 RDP (원격 데스크톱) 포트 toohello와 <*SAPSystemSID*> 0-ascs-가상 컴퓨터

> [!NOTE]
> Azure 내부 부하 분산 장치 및 hello 네트워크 카드의 모든 IP 주소는 **동적** 기본적으로 합니다. 너무 변경**정적** IP 주소입니다. 설명 방법을 toodo hello 문서의 뒷부분에 나오는이 있습니다.
>
>

### <a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>프로덕션 환경에서 회사 네트워크 연결 (크로스-프레미스) toouse로 가상 컴퓨터 배포
프로덕션 SAP 시스템의 경우 Azure 사이트 간 VPN 또는 Azure ExpressRoute를 사용하여 [회사 네트워크 연결(크로스-프레미스)][planning-guide-2.2]를 통해 Azure 가상 컴퓨터를 배포합니다.

> [!NOTE]
> Azure 가상 네트워크 인스턴스를 사용할 수 있습니다. hello 가상 네트워크 및 서브넷 이미 생성 되어 준비 합니다.
>
>

1.  Hello hello에 Azure 포털에서에서 **매개 변수** 블레이드 hello **NEWOREXISTINGSUBNET** 상자 **기존**합니다.
2.  Hello에 **SUBNETID** 상자에서 준비 된 Azure 네트워크 SubnetID 설치할 toodeploy Azure 가상 컴퓨터의 전체 문자열 hello를 추가 합니다.
3.  Azure 네트워크의 모든 서브넷 목록을 tooget PowerShell 명령을 실행 합니다.

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  hello **ID** 필드 표시 hello **SUBNETID**합니다.
4. 모든 목록이 tooget **SUBNETID** 이 PowerShell 명령을 실행 하는 값:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  hello **SUBNETID** 다음과 같습니다.

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> 테스트 및 데모용 클라우드 전용 SAP 인스턴스 배포
클라우드 전용 배포 모델에서 고가용성 SAP 시스템을 배포할 수 있습니다. 기본적으로 이러한 종류의 배포는 데모 및 테스트 사용 사례에 사용할 수 있습니다. 프로덕션 사용 사례에는 적합하지 않습니다.

- Hello hello에 Azure 포털에서에서 **매개 변수** 블레이드 hello **NEWOREXISTINGSUBNET** 상자 **새**합니다. Hello 둡니다 **SUBNETID** 필드가 비어 있습니다.

  hello SAP Azure 리소스 관리자 템플릿을 자동으로 만듭니다. Azure 가상 네트워크 및 서브넷 hello 합니다.

> [!NOTE]
> 또한 toodeploy 해야 DNS를 Azure 가상 네트워크의 동일한 인스턴스에 hello 및 Active Directory에 대 한 가상 컴퓨터를 전용 하나 이상 있습니다. hello 템플릿 이러한 가상 컴퓨터를 만들지 않습니다.
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a>템플릿 2 아키텍처에 대 한 hello 인프라 준비

SAP toohelp 단순화 SAP 아키텍처 템플릿 2에 대 한 필요한 인프라 리소스의 배포에 대 한이 Azure 리소스 관리자 템플릿을 사용할 수 있습니다.

이 배포 시나리오를 위한 Azure Resource Manager 템플릿을 가져올 수 있는 위치는 다음과 같습니다

* [Azure Marketplace 이미지](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [관리 디스크를 사용하는 Azure Marketplace 이미지](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [사용자 지정 이미지](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [관리 디스크를 사용하는 사용자 지정 이미지](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a>템플릿 3 아키텍처에 대 한 hello 인프라 준비

Hello 인프라를 준비 하 고 구성에 대 한 SAP 있습니다 **다중 SID**합니다. 예를 들어 추가 SAP ASCS/SCS 인스턴스를 *기존* 클러스터 구성에 추가할 수 있습니다. 자세한 내용은 참조 [Azure 리소스 관리자는 기존 클러스터 구성 toocreate SAP SID 다중 구성에 추가 SAP ASCS/SCS 인스턴스 구성][sap-ha-multi-sid-guide]합니다.

새 다중 SID 클러스터 toocreate 경우 hello 다중 SID를 사용할 수 있습니다 [GitHub의 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates)합니다.
새 다중 SID 클러스터 toocreate toodeploy hello 다음 세 개의 템플릿이 필요 합니다.

* [ASCS/SCS 템플릿](#ASCS-SCS-template)
* [데이터베이스 템플릿](#database-template)
* [응용 프로그램 서버 템플릿](#application-servers-template)

hello 다음 섹션에서는 있어야 hello 템플릿 및 tooprovide hello 템플릿에 필요한 hello 매개 변수에 대 한 자세한 정보.

#### <a name="ASCS-SCS-template"></a> ASCS/SCS 템플릿

hello ASCS/SCS 템플릿 toocreate 여러 ASCS/SCS 인스턴스를 호스트 하는 Windows Server 장애 조치 클러스터를 사용할 수 있는 두 가상 컴퓨터를 배포 합니다.

hello에 hello ASCS/SCS 다중 SID 서식 파일을 tooset [ASCS/SCS 다중 SID 템플릿] [ sap-templates-3-tier-multisid-xscs-marketplace-image] 또는 [관리 하는 디스크를 사용 하 여 ASCS/SCS 다중 SID 템플릿을] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], hello 매개 변수 뒤에 대 한 값을 입력 합니다.

  - **리소스 접두사**.  Hello 리소스 접두사를 사용 하는 tooprefix hello 배포 중에 생성 되는 모든 리소스를 설정 합니다. Hello 리소스 tooonly 단일 SAP 시스템에 속하지 않으면, hello 리소스의 hello 접두사 hello 단일 SAP 시스템의 SID 하지 않습니다.  hello 접두사 사이 여야 합니다 **3-6 개의 문자**합니다.
  - **스택 유형**. Hello SAP 시스템의 hello 스택 유형을 선택 합니다. Hello 스택 종류에 따라 Azure 부하 분산 장치 (ABAP 또는 Java만) 하나 또는 두 개 (ABAP + Java) 개인 하나의 IP 주소를 SAP 시스템에 있습니다.
  -  **OS 종류**. Hello 가상 컴퓨터의 hello 운영 체제를 선택 합니다.
  -  **SAP 시스템 수**. Hello 수를 선택 합니다.이 클러스터의 tooinstall SAP 시스템의 원하는 합니다.
  -  **시스템 가용성**. **HA**를 선택합니다.
  -  **관리자 사용자 이름 및 관리자 암호**. Toohello 컴퓨터에서 사용 되는 toosign 일 수 있는 새 사용자를 만듭니다.
  -  **새 또는 기존 서브넷**. 새 가상 네트워크와 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 설정합니다. 가상 네트워크는 연결 된 tooyour 온-프레미스 네트워크를 이미 있는 경우 선택 **기존**합니다.
  -  **서브넷 ID**. 가상 컴퓨터를 연결 하는 hello 서브넷 toowhich hello의 hello ID를 설정 합니다. 가상 사설망 (VPN) 또는 ExpressRoute 가상 네트워크 tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크의 서브넷을 hello를 선택 합니다. hello ID는 일반적으로 다음과 같이 보입니다.

   /subscriptions/<*구독 ID*>/resourceGroups/<*리소스 그룹 이름*>/providers/Microsoft.Network/virtualNetworks/<*가상 네트워크 이름*>/subnets/<*서브넷 이름*>

hello 템플릿 여러 SAP 시스템을 지 원하는 Azure 부하 분산 장치가 인스턴스 하나를 배포 합니다.

- 인스턴스 번호가 00, 10, 20 hello ASCS 인스턴스 구성 됩니다.
- hello SCS 인스턴스는 인스턴스 번호 01, 11, 21에 대해 구성 됩니다...
- hello ASCS Enqueue 복제 서버 (호출자) (Linux에만 해당) 인스턴스는 인스턴스 번호 02, 12, 22에 대해 구성 됩니다...
- hello SCS 호출자 (Linux에만 해당) 인스턴스는 인스턴스 번호 03, 13, 23에 대해 구성 됩니다...

hello 부하 분산 장치 1에 포함 되어 (Linux 용 2) VIP(s), ASCS/SCS에 대 한 1 x VIP와 호출자 (Linux에만 해당)에 대 한 1 x VIP 합니다.

hello 다음 목록은 모든 부하 분산 규칙 (여기서 x는 hello 수가 hello SAP 시스템, 1, 2, 3... 등).
- 모든 SAP 시스템에 대한 Windows 특정 포트: 445, 5985
- ASCS 포트(x0 인스턴스 번호): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016
- SCS 포트(x1 인스턴스 번호): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116
- Linux의 ASCS ERS 포트(x2 인스턴스 번호): 33x2, 5x213, 5x214, 5x216
- Linux의 SCS ERS 포트(x3 인스턴스 번호): 33x3, 5x313, 5x314, 5x316

hello 부하 분산 장치는 프로브 포트 (여기서 x는 hello 수가 hello SAP 시스템, 예를 들어 1, 2, 3 …)를 수행 하는 구성 된 toouse hello:
- ASCS/SCS 내부 부하 분산 장치 프로브 포트: 620x0
- ERS 내부 부하 분산 장치 프로브 포트(Linux 전용): 621x2

#### <a name="database-template"></a> 데이터베이스 템플릿

tooinstall를 사용할 수 있는 두 개의 가상 컴퓨터가 단일 SAP 시스템에 대 한 관계형 데이터베이스 관리 시스템 (RDBMS) hello 또는 hello 데이터베이스 서식 파일 하나를 배포 합니다. 예를 들어 5 개의 SAP 시스템에 대 한 ASCS/SCS 템플릿을 배포 하는 경우 필요한 toodeploy이 서식이 파일 5 번입니다.

hello에 hello 데이터베이스 다중 SID 서식 파일을 tooset [데이터베이스 다중 SID 템플릿을] [ sap-templates-3-tier-multisid-db-marketplace-image] 또는 [관리 하는 디스크를 사용 하 여 데이터베이스 다중 SID 템플릿을] [ sap-templates-3-tier-multisid-db-marketplace-image-md], hello 매개 변수 뒤에 대 한 값을 입력 합니다.

  -  **SAP 시스템 ID**. Hello tooinstall 원하는 SAP 시스템의 hello SAP 시스템 ID를 입력 합니다. hello ID는 배포 된 hello 리소스에 대 한 접두사로 사용 됩니다.
  -  **OS 종류**. Hello 가상 컴퓨터의 hello 운영 체제를 선택 합니다.
  -  **데이터베이스 유형**. Hello 유형을 선택 하려는 hello 클러스터에서 tooinstall hello 데이터베이스의 합니다. 선택 **SQL** tooinstall Microsoft SQL Server를 선택 합니다. 선택 **HANA** hello 가상 컴퓨터에서 SAP HANA tooinstall 하려는 경우. Tooselect hello 올바른 운영 체제 형식이 있는지 확인: 선택 **Windows** SQL, 및 HANA에 대 한 Linux 배포를 선택 합니다. hello 연결된 toohello 가상 컴퓨터는 Azure 부하 분산 장치 구성 toosupport hello 선택한 데이터베이스 유형:
    * **SQL**. hello 부하 분산 장치 부하를 분산 포트를 1433 됩니다. SQL Server Always On 설치 프로그램에 대 한이 포트 toouse 있는지를 확인 합니다.
    * **HANA**. hello 부하 분산 장치 부하 분산을 포트 35015 및 35017 됩니다. 인스턴스 번호와 SAP HANA tooinstall 있는지 확인 **50**합니다.
    hello 부하 분산 장치 프로브 포트 62550 사용 합니다.
  -  **SAP 시스템 크기**. 설정 hello 개수의 SAPS hello 새 시스템을 제공 합니다. SAPS hello 시스템 내용의 확실 하지 않은 경우 SAP 기술 파트너 또는 시스템 통합자에 게 요청 합니다.
  -  **시스템 가용성**. **HA**를 선택합니다.
  -  **관리자 사용자 이름 및 관리자 암호**. Toohello 컴퓨터에서 사용 되는 toosign 일 수 있는 새 사용자를 만듭니다.
  -  **서브넷 ID**. Hello ASCS/SCS 템플릿 배포의 일부로 생성 된 hello 서브넷의 hello ID 또는 hello ASCS/SCS 템플릿의 hello 배포 중에 사용 하는 hello 서브넷의 hello ID를 입력 합니다.

#### <a name="application-servers-template"></a> 응용 프로그램 서버 템플릿

hello 응용 프로그램 서버 템플릿은 단일 SAP 시스템에 대 한 SAP 응용 프로그램 서버 인스턴스로 사용할 수 있는 두 개 이상의 가상 컴퓨터를 배포 합니다. 예를 들어 5 개의 SAP 시스템에 대 한 ASCS/SCS 템플릿을 배포 하는 경우 필요한 toodeploy이 서식이 파일 5 번입니다.

hello에 hello 응용 프로그램 서버 다중 SID 템플릿을를 tooset [응용 프로그램 서버 다중 SID 템플릿을] [ sap-templates-3-tier-multisid-apps-marketplace-image] 또는 [관리하는디스크를사용하여응용프로그램서버다중SID템플릿] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], hello 매개 변수 뒤에 대 한 값을 입력 합니다.

  -  **SAP 시스템 ID**. Hello tooinstall 원하는 SAP 시스템의 hello SAP 시스템 ID를 입력 합니다. hello ID는 배포 된 hello 리소스에 대 한 접두사로 사용 됩니다.
  -  **OS 종류**. Hello 가상 컴퓨터의 hello 운영 체제를 선택 합니다.
  -  **SAP 시스템 크기**. hello 수가 SAPS hello 새 시스템을 제공 합니다. SAPS hello 시스템 내용의 확실 하지 않은 경우 SAP 기술 파트너 또는 시스템 통합자에 게 요청 합니다.
  -  **시스템 가용성**. **HA**를 선택합니다.
  -  **관리자 사용자 이름 및 관리자 암호**. Toohello 컴퓨터에서 사용 되는 toosign 일 수 있는 새 사용자를 만듭니다.
  -  **서브넷 ID**. Hello ASCS/SCS 템플릿 배포의 일부로 생성 된 hello 서브넷의 hello ID 또는 hello ASCS/SCS 템플릿의 hello 배포 중에 사용 하는 hello 서브넷의 hello ID를 입력 합니다.


### <a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure 가상 네트워크
예에서 hello Azure 가상 네트워크의 주소 공간 hello 10.0.0.0/16 됩니다. **Subnet**이라는 서브넷이 하나 있으며 주소 범위는 10.0.0.0/24입니다. 모든 가상 컴퓨터와 내부 부하 분산 장치는 이 가상 네트워크에 배포됩니다.

> [!IMPORTANT]
> 변경 하지 않은 hello 게스트 운영 체제 내의 toohello 네트워크 설정 합니다. 여기에는 IP 주소, DNS 서버 및 서브넷이 포함됩니다. Azure에서 모든 네트워크 설정을 구성합니다. hello 동적 호스트 구성 프로토콜 (DHCP) 서비스 설정에 전파합니다.
>
>

### <a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP 주소

tooset hello 필요한 DNS IP 주소, 단계 hello지 않습니다.

1.  Hello hello에 Azure 포털에서에서 **DNS 서버** 블레이드에서 있는지 확인 가상 네트워크가 **DNS 서버** 옵션이 너무 설정**사용자 지정 DNS**합니다.
2.  네트워크의 hello 형식에 따라 설정을 선택 합니다. 자세한 내용은 다음 리소스는 hello 참조:
    * [회사 네트워크 연결 (크로스-프레미스)][planning-guide-2.2]: hello hello 온-프레미스 DNS 서버의 IP 주소를 추가 합니다.  
    온-프레미스 DNS 서버 toohello 가상 컴퓨터가 Azure에서 실행 되는 확장할 수 있습니다. 이 시나리오에서는 hello Azure의 hello IP 주소를 추가할 수 있습니다 hello DNS 서비스를 실행 하는 가상 컴퓨터.
    * [클라우드 전용 배포][planning-guide-2.1]: hello에 추가 가상 컴퓨터가 배포 DNS 서버 역할을 하는 동일한 가상 네트워크 인스턴스. Hello Azure의 hello IP 주소 추가 toorun DNS 서비스를 설정한 가상 컴퓨터.

    ![그림 12: Azure Virtual Network를 위한 DNS 서버 구성][sap-ha-guide-figure-3001]

    _**그림 12:** Azure Virtual Network를 위한 DNS 서버 구성_

  > [!NOTE]
  > Toorestart hello Azure 가상 컴퓨터 tooapply 필요한 hello hello DNS 서버의 IP 주소를 변경 하면 변경 hello 및 hello 새 DNS 서버를 전파 합니다.
  >
  >

예에서 hello DNS 서비스가 설치 되 고 이러한 Windows 가상 컴퓨터에 구성:

| 가상 컴퓨터 역할 | 가상 컴퓨터 호스트 이름 | 네트워크 카드 이름 | 고정 IP 주소 |
| --- | --- | --- | --- |
| 첫 번째 DNS 서버 |domcontr-0 |pr1-nic-domcontr-0 |10.0.0.10 |
| 두 번째 DNS 서버 |domcontr-1 |pr1-nic-domcontr-1 |10.0.0.11 |

### <a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>호스트 이름 및 hello SAP ASCS/SCS 클러스터 인스턴스 및 DBMS 클러스터형된 인스턴스에 대 한 고정 IP 주소

온-프레미스 배포에 대해 다음의 예약된 호스트 이름 및 IP 주소가 필요합니다.

| 가상 호스트 이름 역할 | 가상 호스트 이름 | 가상 고정 IP 주소 |
| --- | --- | --- |
| SAP ASCS/SCS 첫 번째 클러스터 가상 호스트 이름(클러스터 관리용) |pr1-ascs-vir |10.0.0.42 |
| SAP ASCS/SCS 인스턴스 가상 호스트 이름 |pr1-ascs-sap |10.0.0.43 |
| SAP DBMS 두 번째 클러스터 가상 호스트 이름(클러스터 관리용) |pr1-dbms-vir |10.0.0.32 |

Hello 클러스터를 만들 때 hello 가상 호스트 이름을 만들려면 **pr1-ascs-vir** 및 **pr1-dbms-vir** 및 hello 관련 hello 클러스터 자체를 관리 하는 IP 주소입니다. 방법에 대 한 정보에 대 한 toodo이,이 참조 [클러스터 구성에서 클러스터 노드 수집][sap-ha-guide-8.12.1]합니다.

수동으로 만들 수 있습니다 hello 다른 두 개의 가상 호스트 이름, **pr1 ascs sap** 및 **pr1 dbms sap**, hello hello DNS 서버의 IP 주소를 연결 합니다. hello 클러스터 SAP ASCS/SCS 인스턴스 및 클러스터형 hello DBMS 인스턴스 사용 하 여 이러한 리소스. 방법에 대 한 내용은 toodo이,이 참조 [클러스터 SAP ASCS/SCS 인스턴스의 가상 호스트 이름을 만들][sap-ha-guide-9.1.1]합니다.

### <a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Hello SAP 가상 컴퓨터에 대 한 고정 IP 주소를 설정 합니다.
클러스터의 가상 컴퓨터 toouse hello를 배포한 후 모든 가상 컴퓨터 tooset 고정 IP 주소가 필요 합니다. Hello 게스트 운영 체제 아니라 hello Azure 가상 네트워크 구성에이 작업을 수행 합니다.

1.  Hello Azure 포털에서에서 선택 **리소스 그룹** > **네트워크 카드** > **설정** > **IP 주소** .
2.  Hello에 **IP 주소** 블레이드 아래 **할당**선택, **정적**합니다. Hello에 **IP 주소** 상자 toouse 원하는 hello IP 주소를 입력 합니다.

  > [!NOTE]
  > Toorestart hello Azure 가상 컴퓨터 tooapply hello 네트워크 카드의 hello IP 주소를 변경 하는 경우 해야 hello 변경 합니다.  
  >
  >

  ![그림 13: 각 가상 컴퓨터의 네트워크 카드 hello에 대 한 고정 IP 주소 설정][sap-ha-guide-figure-3002]

  _**그림 13:** 각 가상 컴퓨터의 네트워크 카드 hello에 대 한 고정 IP 주소를 설정 합니다._

  즉, Active Directory/DNS 서비스에 대 한 toouse 되도록 가상 컴퓨터를 포함 하 여 모든 가상 컴퓨터에 대 한 모든 네트워크 인터페이스에 대해이 단계를 반복 합니다.

예제에서는 다음 가상 컴퓨터 및 고정 IP 주소를 사용합니다.

| 가상 컴퓨터 역할 | 가상 컴퓨터 호스트 이름 | 네트워크 카드 이름 | 고정 IP 주소 |
| --- | --- | --- | --- |
| 첫 번째 SAP 응용 프로그램 서버 인스턴스 |pr1-di-0 |pr1-nic-di-0 |10.0.0.50 |
| 두 번째 SAP 응용 프로그램 서버 인스턴스 |pr1-di-1 |pr1-nic-di-1 |10.0.0.51 |
| ... |... |... |... |
| 마지막 SAP 응용 프로그램 서버 인스턴스 |pr1-di-5 |pr1-nic-di-5 |10.0.0.55 |
| ASCS/SCS 인스턴스의 첫 번째 클러스터 노드 |pr1-ascs-0 |pr1-nic-ascs-0 |10.0.0.40 |
| ASCS/SCS 인스턴스의 두 번째 클러스터 노드 |pr1-ascs-1 |pr1-nic-ascs-1 |10.0.0.41 |
| DBMS 인스턴스의 첫 번째 클러스터 노드 |pr1-db-0 |pr1-nic-db-0 |10.0.0.30 |
| DBMS 인스턴스의 두 번째 클러스터 노드 |pr1-db-1 |pr1-nic-db-1 |10.0.0.31 |

### <a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Hello Azure 내부 부하 분산 장치에 대 한 고정 IP 주소 설정

hello SAP Azure 리소스 관리자 템플릿 hello SAP ASCS/SCS 인스턴스 클러스터와 hello DBMS 클러스터에 사용 되는 Azure 내부 부하 분산 장치를 만듭니다.

> [!IMPORTANT]
> hello SAP ASCS/SCS는 hello의 hello 가상 호스트 이름의 IP 주소 hello 동일 hello SAP ASCS/SCS 내부 부하 분산 장치의 hello IP 주소로: **pr1-lb-ascs**합니다.
> hello DBMS는 hello의 가상 이름 hello의 IP 주소 hello 동일 hello DBMS 내부 부하 분산 장치의 hello IP 주소로: **pr1 lb dbms**합니다.
>
>

tooset 내부 Azure hello에 대 한 고정 IP 주소를 부하 분산 장치:

1.  hello 초기 배포 hello 내부 부하 분산 장치 IP 주소 설정 너무**동적**합니다. Hello hello에 Azure 포털에서에서 **IP 주소** 블레이드 아래 **할당**선택, **정적**합니다.
2.  Hello 내부 부하 분산 장치의 IP 주소 hello 설정 **pr1-lb-ascs** hello SAP ASCS/SCS 인스턴스의 hello 가상 호스트 이름의 toohello IP 주소입니다.
3.  Hello 내부 부하 분산 장치의 IP 주소 hello 설정 **pr1 lb dbms** hello DBMS 인스턴스 hello 가상 호스트 이름의 toohello IP 주소입니다.

  ![그림 14: hello SAP ASCS/SCS 인스턴스에 대 한 hello 내부 부하 분산 장치에 대 한 고정 IP 주소 설정][sap-ha-guide-figure-3003]

  _**그림 14:** hello SAP ASCS/SCS 인스턴스에 대 한 hello 내부 부하 분산 장치에 대 한 고정 IP 주소 설정_

예제에서는 다음과 같은 고정 IP 주소를 가진 두 개의 Azure 내부 부하 분산 장치가 사용됩니다.

| Azure 내부 부하 분산 장치 역할 | Azure 내부 부하 분산 장치 이름 | 고정 IP 주소 |
| --- | --- | --- |
| SAP ASCS/SCS 인스턴스 내부 부하 분산 장치 |pr1-lb-ascs |10.0.0.43 |
| SAP DBMS 내부 부하 분산 장치 |pr1-lb-dbms |10.0.0.33 |


### <a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>기본 ASCS/SCS 부하 분산 hello Azure 내부 부하 분산 장치에 대 한 규칙

hello SAP Azure 리소스 관리자 템플릿은 hello 포트를 만듭니다.
* Hello 기본 인스턴스 수와 ABAP ASCS 인스턴스 **00**
* Hello 기본 인스턴스 번호를 사용 하는 Java SCS 인스턴스 **01**

Hello 기본 인스턴스 수를 사용 해야 SAP ASCS/SCS 인스턴스를 설치할 때 **00** 프로그램 ABAP ASCS 인스턴스 및 hello 기본 인스턴스 수에 대 한 **01** Java SCS 인스턴스에 대 한 합니다.

다음에 필요한 내부 부하 분산 hello SAP NetWeaver 포트에 대 한 끝점을 만듭니다.

toocreate 필수 내부 부하 분산 끝점을 먼저 이러한 부하 분산 hello SAP NetWeaver ABAP ASCS 포트에 대 한 끝점을 만듭니다.

| 서비스/부하 분산 규칙 이름 | 기본 포트 번호 | (인스턴스 번호가 00인 ASCS 인스턴스)(ERS가 10)에 대한 구체적인 포트 |
| --- | --- | --- |
| 서버를 큐에 넣기/ *lbrule3200* |32<*InstanceNumber*> |3200 |
| ABAP 메시지 서버/ *lbrule3600* |36<*InstanceNumber*> |3600 |
| 내부 ABAP 메시지/ *lbrule3900* |39<*InstanceNumber*> |3900 |
| 메시지 서버 HTTP/ *Lbrule8100* |81<*InstanceNumber*> |8100 |
| SAP 시작 서비스 ASCS HTTP/ *Lbrule50013* |5<*InstanceNumber*>13 |50013 |
| SAP 시작 서비스 ASCS HTTP/ *Lbrule50014* |5<*InstanceNumber*>14 |50014 |
| 복제를 큐에 넣기/ *Lbrule50016* |5<*InstanceNumber*>16 |50016 |
| SAP 시작 서비스 ERS HTTP/ *Lbrule51013* |5<*InstanceNumber*>13 |51013 |
| SAP 시작 서비스 ERS HTTP *Lbrule51014* |5<*InstanceNumber*>14 |51014 |
| Win RM *Lbrule5985* | |5985 |
| 파일 공유 *Lbrule445* | |445 |

_**표 1:** 포트 번호가 hello SAP NetWeaver ABAP ASCS 인스턴스_

그런 다음 이러한 부하 분산 hello SAP NetWeaver Java SCS 포트에 대 한 끝점을 만듭니다.

| 서비스/부하 분산 규칙 이름 | 기본 포트 번호 | (인스턴스 번호가 01인 SCS 인스턴스)(ERS가 11)에 대한 구체적인 포트 |
| --- | --- | --- |
| 서버를 큐에 넣기/ *lbrule3201* |32<*InstanceNumber*> |3201 |
| 게이트웨이 서버/ *lbrule3301* |33<*InstanceNumber*> |3301 |
| Java 메시지 서버/ *lbrule3900* |39<*InstanceNumber*> |3901 |
| 메시지 서버 HTTP/ *Lbrule8101* |81<*InstanceNumber*> |8101 |
| SAP 시작 서비스 SCS HTTP/ *Lbrule50113* |5<*InstanceNumber*>13 |50113 |
| SAP 시작 서비스 SCS HTTP/ *Lbrule50114* |5<*InstanceNumber*>14 |50114 |
| 복제를 큐에 넣기/ *Lbrule50116* |5<*InstanceNumber*>16 |50116 |
| SAP 시작 서비스 ERS HTTP *Lbrule51113* |5<*InstanceNumber*>13 |51113 |
| SAP 시작 서비스 ERS HTTP *Lbrule51114* |5<*InstanceNumber*>14 |51114 |
| Win RM *Lbrule5985* | |5985 |
| 파일 공유 *Lbrule445* | |445 |

_**표 2:** 포트 번호가 hello SAP NetWeaver Java SCS 인스턴스의_

![그림 15: 기본 ASCS/SCS 부하 분산 hello Azure 내부 부하 분산 장치에 대 한 규칙][sap-ha-guide-figure-3004]

_**그림 15:** 기본 ASCS/SCS 부하 분산 hello Azure 내부 부하 분산 장치에 대 한 규칙_

Hello 부하 분산 장치의 IP 주소 hello 설정 **pr1 lb dbms** hello DBMS 인스턴스 hello 가상 호스트 이름의 toohello IP 주소입니다.

### <a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Hello ASCS/SCS 기본 부하 분산 규칙 hello Azure 내부 부하 분산 장치에 대 한 변경

Hello SAP ASCS 또는 SCS 인스턴스에 대 한 숫자가 다른 toouse 원하는 기본값에서 해당 포트의 hello 이름 및 값을 변경 해야 합니다.

1.  Hello Azure 포털에서에서 선택  **<* SID*> 파운드-ascs 부하 분산 장치 * * > **부하 분산 규칙**합니다.
2.  모든를 부하 분산 toohello SAP ASCS 또는 SCS 인스턴스에 속하는 규칙에 대 한 이러한 값을 변경 합니다.

  * 이름
  * 포트
  * 백 엔드 포트

  예를 들어 00 too31에서 toochange hello 기본 ASCS 인스턴스 번호를 사용 하도록 하려는 경우 표 1에 나열 된 모든 포트에 대 한 toomake hello 변경 해야 합니다.

  다음은 포트 *lbrule3200*에 대한 업데이트 예제입니다.

  ![그림 16: hello ASCS/SCS 기본 부하 분산 규칙 hello Azure 내부 부하 분산 장치에 대 한 변경][sap-ha-guide-figure-3005]

  _**그림 16:** 변경 hello ASCS/SCS 기본 부하 분산 hello Azure 내부 부하 분산 장치에 대 한 규칙_

### <a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Windows 가상 컴퓨터 toohello 도메인 추가

정적 IP 주소 toohello 가상 컴퓨터를 할당 하면 hello 가상 컴퓨터 toohello 도메인을 추가 합니다.

![그림 17: 가상 컴퓨터 tooa 도메인 추가][sap-ha-guide-figure-3006]

_**그림 17:** 가상 컴퓨터 tooa 도메인 추가_

### <a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Hello SAP ASCS/SCS 인스턴스의 클러스터 노드 모두에 레지스트리 항목을 추가 합니다.

Azure 부하 분산 장치 닫히는 연결 hello 연결의 일정 시간 동안 유휴 상태인 시간 (유휴 시간 제한을) 하는 내부 부하 분산 장치를 있습니다. 대화 상자 인스턴스 열려 있는 연결 toohello SAP 인 큐에서 SAP 작업 프로세스 요구 toobe 전송 요청 hello 첫 큐에 넣지/큐에서 제거 되는 즉시 처리 합니다. 이러한 연결은 일반적으로 시작할 때 까지는 설정 된 hello 작업 프로세스 또는 hello enqueue 프로세스가 다시 시작 합니다. 그러나 설정된 된 시간 동안에 대 한 hello 연결이 유휴 상태 이면 경우 hello Azure 내부 부하 분산 장치 닫히는 hello 연결 합니다. 더 이상 없으면 hello 연결 toohello enqueue 프로세스를 다시 만들고 hello SAP 작업 프로세스 때문에 문제가 되지 않습니다. 이러한 활동은 SAP 프로세스의 개발자 추적이 hello에 설명 되어 있지만 해당 추적에 많은 양의 추가 콘텐츠를 만들 합니다. 것이 좋습니다 toochange hello TCP/IP `KeepAliveTime` 및 `KeepAliveInterval` 클러스터 노드 모두에 있습니다. 이러한 변경에 SAP 프로필 매개 변수를 hello 문서의 뒷부분에 설명 된 hello TCP/IP 매개 변수를 결합 합니다.

먼저, hello SAP ASCS/SCS 인스턴스의 클러스터 노드 모두에서 tooadd 레지스트리 항목 이러한 Windows 레지스트리 항목에 대 한 SAP ASCS/SCS Windows 클러스터 노드 모두에 추가합니다.

| Path | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| 변수 이름 |`KeepAliveTime` |
| 변수 유형 |REG_DWORD(10진수) |
| 값 |120000 |
| 링크 toodocumentation |[https://technet.microsoft.com/en-us/library/cc957549.aspx](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

_**표 3:** 변경 hello 첫 번째 TCP/IP 매개 변수_

그런 다음 SAP ASCS/SCS에 대한 두 Windows 클러스터 노드에 대해 다음 Windows 레지스트리 항목을 추가합니다.

| Path | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| 변수 이름 |`KeepAliveInterval` |
| 변수 유형 |REG_DWORD(10진수) |
| 값 |120000 |
| 링크 toodocumentation |[https://technet.microsoft.com/en-us/library/cc957548.aspx](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

_**표 4:** 변경 hello 두 번째 TCP/IP 매개 변수_

**클러스터 노드 모두를 다시 시작 tooapply hello 변경**합니다.

### <a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> SAP ASCS/SCS 인스턴스에 대한 Windows Server 장애 조치 클러스터링 클러스터 설정

SAP ASCS/SCS 인스턴스의 Windows Server 장애 조치(failover) 클러스터링 클러스터 설정은 다음과 같은 작업을 포함합니다.

- 클러스터 구성에서 클러스터 노드 hello를 수집합니다.
- 클러스터 파일 공유 감시 구성

#### <a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>클러스터 구성에서 클러스터 노드 hello를 수집 합니다.

1.  Hello 추가 역할 및 기능 마법사에서 장애 조치 클러스터링 tooboth 클러스터 노드를 추가 합니다.
2.  장애 조치 클러스터 관리자를 사용 하 여 hello 장애 조치 클러스터를 설정 합니다. 장애 조치 클러스터 관리자에서 선택 **클러스터 만들기**, 다음 hello 첫 번째 클러스터, 노드 A의 hello 이름만 추가 아직; hello 두 번째 노드 추가 하지 마십시오 이후 단계에서 hello 두 번째 노드를 추가 합니다.

  ![그림 18: hello 서버 또는 가상 컴퓨터 이름 hello 첫 번째 클러스터 노드 추가][sap-ha-guide-figure-3007]

  _**그림 18:** hello 첫 번째 클러스터 노드 추가 hello 서버 또는 가상 컴퓨터 이름_

3.  Hello hello 클러스터의 네트워크 이름 (가상 호스트 이름)을 입력 합니다.

  ![그림 19: hello 클러스터 이름을 입력 하십시오.][sap-ha-guide-figure-3008]

  _**그림 19:** hello 클러스터 이름 입력_

4.  Hello 클러스터를 만든 후 클러스터 유효성 검사 테스트를 실행 합니다.

  ![그림 20: hello 클러스터 유효성 검사를 실행합니다.][sap-ha-guide-figure-3009]

  _**그림 20:** hello 클러스터 유효성 검사를 실행 합니다._

  Hello 프로세스의이 시점에 디스크에 대 한 경고를 무시할 수 있습니다. 파일 공유 감시 및 hello SIOS 공유 디스크 나중에 추가 합니다. 이 단계에서는 tooworry 쿼럼에 대 한 필요는 없습니다.

  ![그림 21: 쿼럼 디스크가 없음][sap-ha-guide-figure-3010]

  _**그림 21:** 쿼럼 디스크가 없음_

  ![그림 22: 새 IP 주소가 필요한 코어 클러스터 리소스][sap-ha-guide-figure-3011]

  _**그림 22:** 새 IP 주소가 필요한 코어 클러스터 리소스_

5.  Hello 코어 클러스터 서비스의 hello IP 주소를 변경 합니다. hello 클러스터 hello 서버의 IP 주소가 hello tooone hello 가상 컴퓨터 노드를 가리키므로 hello 핵심 클러스터 서비스의 hello IP 주소를 변경할 때까지 시작할 수 없습니다. Hello에서 이렇게 **속성** hello 코어 클러스터 서비스의 IP 리소스의 페이지입니다.

  예를 들어 tooassign IP 주소 필요 (예에서 **10.0.0.42**) hello 클러스터 가상 호스트 이름에 대 한 **pr1-ascs-vir**합니다.

  ![그림 23: hello 속성 대화 상자, hello IP 주소를 변경][sap-ha-guide-figure-3012]

  _**그림 23:** hello에 **속성** 대화 상자, hello IP 주소 변경_

  ![그림 24: hello 클러스터에 대 한 예약 된 hello IP 주소를 할당 합니다.][sap-ha-guide-figure-3013]

  _**그림 24:** hello 클러스터에 대 한 예약 된 hello IP 주소 할당_

6.  Hello 클러스터 가상 호스트 이름을 온라인 상태로 전환 합니다.

  ![그림 25: 클러스터 코어 서비스가 작동 중 이며 hello로 실행 되 고 IP 주소를 수정][sap-ha-guide-figure-3014]

  _**그림 25:** 클러스터 코어 서비스가 작동 중 이며 실행 되 고 hello로 IP 주소를 수정_

7.  Hello 두 번째 클러스터 노드를 추가 합니다.

  Hello 코어 클러스터 서비스가 실행 되 고, 했으므로 hello 두 번째 클러스터 노드를 추가할 수 있습니다.

  ![그림 26: hello 두 번째 클러스터 노드 추가][sap-ha-guide-figure-3015]

  _**그림 26:** 추가 hello 두 번째 클러스터 노드_

8.  두 번째 클러스터 노드 호스트 hello에 대 한 이름을 입력 합니다.

  ![그림 27: hello 두 번째 클러스터 노드 호스트 이름을 입력 하십시오.][sap-ha-guide-figure-3016]

  _**그림 27:** hello 두 번째 클러스터 노드 호스트 이름 입력_

  > [!IMPORTANT]
  > 해당 hello 해야 **모든 적합 한 저장소 toohello 클러스터 추가** 확인란은 **하지** 선택한 합니다.  
  >
  >

  ![그림 28: hello 확인란을 선택 하지 마십시오][sap-ha-guide-figure-3017]

  _**그림 28:** 않습니다 **하지** 선택 hello 확인란_

  쿼럼 및 디스크에 대한 경고는 무시해도 됩니다. 설정 hello 쿼럼 및 공유 hello 디스크 나중에 설명 된 대로 [SAP ASCS/SCS 클러스터 공유 디스크에 대 한 SIOS DataKeeper Cluster Edition 설치][sap-ha-guide-8.12.3]합니다.

  ![그림 29: hello 디스크 쿼럼에 대 한 경고를 무시 합니다.][sap-ha-guide-figure-3018]

  _**그림 29:** hello 디스크 쿼럼에 대 한 경고를 무시_


#### <a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> 클러스터 파일 공유 감시 구성

클러스터 파일 공유 감시 구성은 다음과 같은 작업을 포함합니다.

- 파일 공유 만들기
- 장애 조치 클러스터 관리자에서 파일 공유 감시 쿼럼 hello 설정

##### <a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> 파일 공유 만들기

1.  쿼럼 디스크 대신 파일 공유 감시를 선택합니다. SIOS DataKeeper는 이 옵션을 지원합니다.

  이 문서의 hello 예에서 hello 파일 공유 감시는 Azure에서 실행 중인 hello Active Directory/DNS 서버에 있습니다. hello 파일 공유 감시 라고 **domcontr 0**합니다. 사이트 간 VPN 이나 Azure express 경로) (통해 VPN 연결 tooAzure 구성한 것 때문에 Active Directory/DNS 서비스가 온-프레미스 이며 되지 않습니다. 적합 한 toorun 파일 공유 감시 합니다.

  > [!NOTE]
  > 온-프레미스 Active Directory/DNS 서비스가 실행 되는 경우 온-프레미스를 실행 하는 hello Active Directory/DNS Windows 운영 체제에서 파일 공유 감시를 구성 하지 마십시오. Azure 및 Active Directory/DNS 온-프레미스로 실행되는 클러스터 노드 간 네트워크 대기 시간이 너무 커서 연결 문제를 일으킬 수 있습니다. 닫기 toohello 클러스터 노드를 실행 하는 Azure 가상 컴퓨터에 있는지 tooconfigure hello 파일 공유 감시를 수 있습니다.  
  >
  >

  hello 쿼럼 드라이브에는 최소한 1, 024 MB의 여유 공간이 필요합니다. 2, 048 MB의 여유 공간 hello 쿼럼 드라이브에 대 한 사용 하는 것이 좋습니다.

2.  Hello 클러스터 이름 개체를 추가 합니다.

  ![그림 30: hello 클러스터 이름 개체에 대 한 hello 공유에 hello 권한 할당][sap-ha-guide-figure-3019]

  _**그림 30:** hello 클러스터 이름 개체에 대 한 hello 공유에 hello 권한 할당_

  Hello 권한을 hello 클러스터 이름 개체에 대 한 hello 공유 hello 기관 toochange 데이터를 포함 (예에서 **pr1-ascs-vir$**).

3.  tooadd hello 클러스터 이름 개체 toohello 목록 **추가**합니다. 그림 31에 표시 된 더하기 toothose에서 컴퓨터 개체에 대 한 필터 toocheck hello를 변경 합니다.

  ![그림 31: hello 개체 유형 tooinclude 컴퓨터 변경][sap-ha-guide-figure-3020]

  _**그림 31:** hello 개체 유형 tooinclude 컴퓨터 변경_

  ![그림 32: hello 컴퓨터 확인란을 선택][sap-ha-guide-figure-3021]

  _**그림 32:** 선택 hello **컴퓨터** 확인란_

4.  그림 31와 같이 hello 클러스터 이름 개체를 입력 합니다. Hello 레코드가 이미 생성 되어 때문에 그림 30에서와 같이 hello 사용 권한을 변경할 수 있습니다.

5.  선택 hello **보안** hello 공유를 제거한 다음 설정의 탭에는 자세한 hello 클러스터 이름 개체에 대 한 권한.

  ![그림 33: hello 파일 공유 쿼럼에 hello 클러스터 이름 개체에 대 한 보안 특성 hello 설정][sap-ha-guide-figure-3022]

  _**그림 33:** hello 파일 공유 쿼럼에 hello 클러스터 이름 개체에 대 한 hello 보안 특성을 설정 합니다._

##### <a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>장애 조치 클러스터 관리자에서 파일 공유 감시 쿼럼 hello 설정

1.  Hello 쿼럼 설정 구성 마법사를 엽니다.

  ![그림 34: hello 구성 클러스터 쿼럼 설정 마법사를 시작 합니다.][sap-ha-guide-figure-3023]

  _**그림 34:** 시작 hello 클러스터 쿼럼 구성 설정 마법사_

2.  Hello에 **쿼럼 구성 선택** 페이지 **hello 쿼럼 감시 선택**합니다.

  ![그림 35: 선택할 수 있는 쿼럼 구성][sap-ha-guide-figure-3024]

  _**그림 35:** 선택할 수 있는 쿼럼 구성_

3.  Hello에 **쿼럼 감시 선택** 페이지 **파일 공유 감시 구성**합니다.

  ![그림 36: 선택 hello 파일 공유 감시][sap-ha-guide-figure-3025]

  _**그림 36:** hello 파일 공유 감시를 선택 합니다._

4.  Hello UNC 경로 toohello 파일 공유를 입력 하십시오 (예제에서는 \\domcontr 0\FSW). toosee hello 변경할 수 있는, 선택 목록 **다음**합니다.

  ![그림 37: hello 미러링 모니터 서버 공유에 대 한 hello 파일 공유 위치를 정의 합니다.][sap-ha-guide-figure-3026]

  _**그림 37:** hello 미러링 모니터 서버 공유에 대 한 hello 파일 공유 위치를 정의 합니다._

5.  한 다음 선택 hello 변경 내용을 선택 **다음**합니다. Toosuccessfully 필요한 38 그림에에서 표시 된 대로 hello 클러스터 구성을 다시 구성 합니다.  

  ![Hello 클러스터를 다시 구성 했으므로 그림 38: 확인][sap-ha-guide-figure-3027]

  _**그림 38:** hello 클러스터를 다시 구성 했으면 확인_

Hello Windows 장애 조치 클러스터를 성공적으로 설치한 후 변경 내용을 toosome 임계값 tooadapt 장애 조치가 감지 tooconditions Azure에서 만든 toobe가 필요 합니다. hello 매개 변수 toobe 변경 사항은이 블로그: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ 합니다. Hello를 작성 하는 두 개의 Vm에 있다고 가정 하면 동일한 서브넷 hello, hello 다음 매개 변수 값이 필요한 변경 toobe toothese ASCS/SCS에 대 한 Windows 클러스터 구성에 있습니다.
- SameSubNetDelay = 2
- SameSubNetThreshold = 15

이러한 설정 및 고객과 테스트 충분히 복원 하는 유용한 toobe hello 한쪽에 제공 된 합니다. Hello에 다른 손 해당 설정 된 제공 빠른 SAP 소프트웨어 또는 노드/v M 실패 시 실제 오류 조건에 충분 한 장애 조치 합니다. 

### <a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Hello SAP ASCS/SCS 클러스터 공유 디스크에 대 한 SIOS DataKeeper 클러스터 Edition을 설치 합니다.

이제 Azure에서 Windows Server 장애 조치 클러스터링 구성이 완료되었습니다. 하지만 SAP ASCS/SCS 인스턴스에 tooinstall 공유 디스크 리소스가 필요 합니다. Azure에서 필요한 hello 공유 디스크 리소스를 만들 수 없습니다. SIOS DataKeeper Cluster Edition은 공급 업체 솔루션 toocreate 공유 디스크 리소스를 사용할 수 있습니다.

SAP ASCS/SCS hello에 대 한 SIOS DataKeeper 클러스터 버전을 설치할지 클러스터 공유 디스크 이러한 작업이 포함 됩니다.

- .NET Framework 3.5 hello를 추가합니다.
- SIOS DataKeeper 설치
- SIOS DataKeeper 설정

#### <a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>.NET Framework 3.5 hello를 추가 합니다.
자동으로 hello Microsoft.NET Framework 3.5 활성화 하거나 Windows Server 2012 r 2에 설치 되지 않습니다. SIOS DataKeeper에 DataKeeper를 설치 하는 모든 노드에서.NET Framework toobe hello를 필요로 하므로 hello 클러스터의 모든 가상 컴퓨터의 게스트 운영 체제 hello에 hello.NET Framework 3.5를 설치 해야 합니다.

두 가지 방법으로 tooadd hello.NET Framework 3.5 가지가 있습니다.

- 39 그림에에서 나와 있는 것 처럼 windows에서 hello 추가 역할 및 기능 마법사를 사용 합니다.

  ![그림 39: hello 추가 역할 및 기능 마법사를 사용 하 여 hello.NET Framework 3.5 설치][sap-ha-guide-figure-3028]

  _**그림 39:** hello 추가 역할 및 기능 마법사를 사용 하 여.NET Framework 3.5 설치 hello_

  ![Hello 추가 역할 및 기능 마법사를 사용 하 여 hello.NET Framework 3.5를 설치 하면 막대 그림 40: 설치 진행률][sap-ha-guide-figure-3029]

  _**그림 40:** 막대 hello 추가 역할 및 기능 마법사를 사용 하 여 hello.NET Framework 3.5를 설치 하면 설치 진행률_

- Hello 명령줄 도구 dism.exe를 사용 합니다. 이 유형의 설치 tooaccess hello SxS 디렉터리 hello Windows 설치 미디어에 필요합니다. 관리자 권한의 명령 프롬프트에서 다음을 입력합니다.

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <a name="dd41d5a2-8083-415b-9878-839652812102"></a> SIOS DataKeeper 설치

Hello 클러스터의 각 노드에서 SIOS DataKeeper Cluster Edition을 설치 합니다. SIOS datakeeper를 통해, 가상 공유 저장소를 toocreate 동기화 된 미러를 만들고 클러스터 공유 저장소를 시뮬레이션 합니다.

Hello SIOS 소프트웨어를 설치 하기 전에 hello 도메인 사용자를 만들어 **DataKeeperSvc**합니다.

> [!NOTE]
> Hello 추가 **DataKeeperSvc** 사용자 toohello **로컬 관리자** 그룹 클러스터 노드 모두에 있습니다.
>
>

tooinstall SIOS DataKeeper:

1.  클러스터 노드 모두에 hello SIOS 소프트웨어를 설치 합니다.

  ![SIOS 설치 관리자][sap-ha-guide-figure-3030]

  ![그림 41: hello SIOS DataKeeper 설치의 첫 번째 페이지][sap-ha-guide-figure-3031]

  _**그림 41:** hello SIOS DataKeeper 설치의 첫 번째 페이지_

2.  그림 42와 hello 대화 상자에서 선택 **예**합니다.

  ![그림 42: 서비스를 사용할 수 없다고 알리는 DataKeeper][sap-ha-guide-figure-3032]

  _**그림 42:** 서비스를 사용할 수 없다고 알리는 DataKeeper_

3.  그림 43에 표시 된 hello 대화 상자에서 선택 하는 권장 **도메인 또는 서버 계정**합니다.

  ![그림 43: SIOS DataKeeper에 대한 사용자 선택][sap-ha-guide-figure-3033]

  _**그림 43:** SIOS DataKeeper에 대한 사용자 선택_

4.  Hello 도메인 계정의 사용자 이름 및 SIOS DataKeeper를 위해 만든 암호를 입력 합니다.

  ![Hello SIOS DataKeeper 설치에 대 한 hello 도메인 사용자 이름 및 암호를 입력 하는 그림 44:][sap-ha-guide-figure-3034]

  _**그림 44:** hello SIOS DataKeeper 설치에 대 한 hello 도메인 사용자 이름 및 암호를 입력 합니다._

5.  그림 45 에서처럼 SIOS DataKeeper 인스턴스에 대 한 hello 라이선스 키를 설치 합니다.

  ![그림 45: SIOS DataKeeper 라이선스 키 입력][sap-ha-guide-figure-3035]

  _**그림 45:** SIOS DataKeeper 라이선스 키 입력_

6.  메시지가 표시 되 면 hello 가상 컴퓨터를 다시 시작 합니다.

#### <a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> SIOS DataKeeper 설정

두 노드에서 모두 SIOS DataKeeper를 설치한 후 toostart hello 구성을 해야 합니다. hello 구성의 hello 목표 hello 추가 디스크 간의 toohave 동기 데이터 복제 tooeach hello 가상 컴퓨터의 연결입니다.

1.  Hello DataKeeper 관리 및 구성 도구를 시작한 다음 선택 **서버 연결**합니다. 그림 46에서 이 옵션은 빨간색 원으로 표시되어 있습니다.

  ![그림 46: SIOS DataKeeper 관리 및 구성 도구][sap-ha-guide-figure-3036]

  _**그림 46:** SIOS DataKeeper 관리 및 구성 도구_

2.  Hello 이름을 입력 하거나, 하 고, 두 번째 단계에서는 두 번째 노드 hello TCP/IP 주소 hello 첫 번째 노드 hello 관리 및 구성 도구를 연결 해야 합니다.

  ![그림 47: 삽입 hello 이름이 나 TCP/IP 주소 hello 첫 번째 노드 hello 관리 및 구성 도구를 연결 해야 되며, 두 번째 단계에서는 hello 두 번째 노드][sap-ha-guide-figure-3037]

  _**그림 47:** 되며, 두 번째 노드 hello와 두 번째 단계에서 삽입 hello 이름이 나 TCP/IP 주소 hello 첫 번째 노드 hello 관리 및 구성 도구를 연결 해야_

3.  Hello 두 노드 사이의 hello 복제 작업을 만듭니다.

  ![그림 48: 복제 작업 만들기][sap-ha-guide-figure-3038]

  _**그림 48:** 복제 작업 만들기_

  마법사는 hello 복제 작업을 만드는 과정을 안내 합니다.
4.  Hello 이름, TCP/IP 주소 및 hello 소스 노드의 디스크 볼륨을 정의 합니다.

  ![그림 49: hello 복제 작업의 hello 이름 정의][sap-ha-guide-figure-3039]

  _**그림 49:** hello 복제 작업의 정의 hello 이름_

  ![그림 50: hello hello 현재 소스 노드가 있어야 하 고 hello 노드에 대 한 기본 데이터를 정의 합니다.][sap-ha-guide-figure-3040]

  _**그림 50:** hello hello 현재 소스 노드가 있어야 하 고 hello 노드에 대 한 기본 데이터를 정의 합니다._

5.  Hello 이름, TCP/IP 주소 및 hello 대상 노드의 디스크 볼륨을 정의 합니다.

  ![그림 51: hello hello 현재 대상 노드가 있어야 하 고 hello 노드에 대 한 기본 데이터를 정의 합니다.][sap-ha-guide-figure-3041]

  _**그림 51:** hello hello 현재 대상 노드가 있어야 하 고 hello 노드에 대 한 기본 데이터를 정의 합니다._

6.  Hello 압축 알고리즘을 정의 합니다. 예에서 hello 복제 스트림을 압축 하는 것이 좋습니다. 재 동기화의 경우에 특히 hello 복제 스트림의 hello 압축 다시 동기화 시간을 크게 줄입니다. Note 압축 가상 컴퓨터의 CPU 및 RAM 리소스 hello를 사용 합니다. Hello 압축 비율이 증가 하면 사용 하는 CPU 리소스 양의 hello지 않습니다 하므로 합니다. 나중에 이 설정을 조정할 수도 있습니다.

7.  필요한 설정 다른 toocheck이 비동기적 또는 동기적으로 hello 복제의 발생 여부. *SAP ASCS/SCS 구성을 보호할 때 동기 복제를 사용해야 합니다*.  

  ![그림 52: 복제 세부 정보 정의][sap-ha-guide-figure-3042]

  _**그림 52:** 복제 세부 정보 정의_

8.  Hello 복제 작업에 의해 복제 된 hello 볼륨 표현된 tooa 공유 디스크 클러스터 구성을 Windows Server 장애 조치 클러스터링 되어야 하는지 여부를 정의 합니다. Hello SAP ASCS/SCS 구성에 대 한 선택 **예** 클러스터에 게 표시 하는 hello Windows hello 클러스터 볼륨으로 사용할 수 있는 공유 디스크와 복제 된 볼륨 수 있도록 합니다.

  ![클러스터 볼륨으로 예 tooset hello 복제 볼륨을 선택 하는 그림 53:][sap-ha-guide-figure-3043]

  _**그림 53:** 선택 **예** tooset hello 복제 볼륨을 클러스터 볼륨으로_

  Hello 볼륨을 만든 후 해당 hello 복제 작업은 활성 상태가 hello DataKeeper 관리 및 구성 도구 보여 줍니다.

  ![그림 54: hello SAP ASCS/SCS 공유 디스크에 대 한 DataKeeper 동기 미러링이 활성화 되었습니다.][sap-ha-guide-figure-3044]

  _**그림 54:** DataKeeper 동기 미러링이 hello SAP ASCS/SCS 공유 디스크에 대 한 활성화 되었습니다_

  장애 조치 클러스터 관리자 55 그림에에서 나와 있는 것 처럼 hello DataKeeper 디스크 드라이브로 표시 됩니다.

  ![그림 55: 장애 조치 클러스터 관리자 hello 디스크를 DataKeeper 복제를 보여 줍니다.][sap-ha-guide-figure-3045]

  _**그림 55:** 장애 조치 클러스터 관리자가 복제 해당 DataKeeper hello 디스크 표시_

## <a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Hello SAP NetWeaver 시스템을 설치 합니다.

설정을 사용 하는 DBMS 시스템 hello에 따라 달라 지므로 hello DBMS 설치 프로그램에서 설명 하지 않습니다. 하지만 한다고 가정 가용성이 높은 DBMS hello 걱정과 hello 다양 한 DBMS 공급 업체를 Azure에 대 한 지원 hello 기능으로 처리 됩니다. 예로 SQL Server 및 Oracle 데이터베이스용 Oracle Data Guard에 대한 AlwaysOn 또는 데이터베이스 미러링을 들 수 있습니다. 이 문서에서 사용 하 여 hello 시나리오에서는 더 많은 보호 toohello DBMS 추가 하지 않았습니다.

Azure에서 여러 다른 DBMS 서비스가 이러한 종류의 클러스터형 SAP ASCS/SCS 구성과 상호 작용할 경우 특별한 고려 사항은 없습니다.

> [!NOTE]
> SAP NetWeaver ABAP 시스템과 Java 시스템 ABAP + Java 시스템의 설치 절차 hello 거의 동일합니다. 가장 중요 한 차이점 hello SAP ABAP 시스템 ASCS 인스턴스 한다는 것입니다. SAP Java 시스템 hello SCS 인스턴스 하나에 있습니다. SAP ABAP + Java 시스템 hello ASCS 인스턴스 하나 있으며에서 실행 되는 하나의 SCS 인스턴스에 hello 동일한 Microsoft 장애 조치 클러스터 그룹입니다. 각 SAP NetWeaver 설치 스택에 대한 설치 차이점은 명시적으로 언급됩니다. 다른 모든 파트 동일 hello는 가정할 수 있습니다.  
>
>

### <a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> 고가용성 ASCS/SCS 인스턴스에 SAP 설치

> [!IMPORTANT]
> 반드시 미러 볼륨 페이지 파일 크기가 DataKeeper tooplace 하지 않습니다. DataKeeper는 미러된 볼륨을 지원하지 않습니다. Hello 기본값 페이지 파일 hello 임시 드라이브는 Azure 가상 컴퓨터를 D에 둘 수 있습니다. 아직 매크로 실행 하지 않은 경우 hello Windows 페이지 파일 toodrive Azure 가상 컴퓨터의 d:를 이동 합니다.
>
>

고가용성 ASCS/SCS 인스턴스에 SAP 설치는 다음과 같은 작업을 포함합니다.

- 클러스터 된 hello SAP ASCS/SCS 인스턴스의 가상 호스트 이름을 만들기
- Hello SAP 첫 번째 클러스터 노드를 설치합니다.
- Hello ASCS/SCS 인스턴스의 hello SAP 프로필 수정
- 프로브 포트 추가
- Hello Windows 방화벽의 프로브 포트 열기

#### <a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>클러스터 된 hello SAP ASCS/SCS 인스턴스의 가상 호스트 이름을 만들기

1.  Hello Windows DNS 관리자에서 hello ASCS/SCS 인스턴스의 hello 가상 호스트 이름에 대 한 DNS 항목을 만듭니다.

  > [!IMPORTANT]
  > hello ASCS/SCS 인스턴스의 수 있어야 하는 hello의 toohello 가상 호스트 이름 지정 IP 주소 hello 동일 tooAzure 부하 분산 장치를 할당 하는 hello IP 주소로 (**<*SID*> 파운드-ascs **).  
  >
  >

  hello hello 가상 SAP ASCS/SCS 호스트 이름의 IP 주소 (**pr1 ascs sap**) Azure 부하 분산 장치의 hello IP 주소와 동일한 hello 됩니다 (**pr1-lb-ascs**).

  ![Hello SAP ASCS/SCS 클러스터 가상 이름 및 TCP/IP 주소에 대 한 hello DNS 항목을 정의 하는 그림 56:][sap-ha-guide-figure-3046]

  _**그림 56:** hello SAP ASCS/SCS 클러스터 가상 이름 및 TCP/IP 주소에 대 한 hello DNS 항목을 정의 합니다._

2.  toodefine hello IP 주소가 할당 toohello 가상 호스트 이름 선택 **DNS 관리자** > **도메인**합니다.

  ![그림 57: SAP ASCS/SCS 클러스터 구성을 위한 새 가상 이름 및 TCP/IP 주소][sap-ha-guide-figure-3047]

  _**그림 57:** SAP ASCS/SCS 클러스터 구성을 위한 새 가상 이름 및 TCP/IP 주소_

#### <a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Hello SAP 첫 번째 클러스터 노드를 설치 합니다.

1.  1. 클러스터 노드에서 hello 첫 번째 클러스터 노드 옵션을 실행 예를 들어 hello에 **pr1-ascs-0** 호스트 합니다.
2.  Azure 내부 hello에 대 한 tookeep hello 기본 포트는 부하 분산 장치, 선택:

  * **ABAP 시스템**: **ASCS** 인스턴스 번호 **00**
  * **Java 시스템**: **SCS** 인스턴스 번호 **01**
  * **ABAP+Java 시스템**: **ASCS** 인스턴스 번호 **00** 및 **SCS** 인스턴스 번호 **01**

  인스턴스와 hello Java SCS 인스턴스에 대 한 01 toouse 인스턴스 번호가 00 ABAP ASCS hello에 대 한 다른, toochange hello Azure 내부 부하 분산 장치 기본 부하 분산에 설명 된 규칙 먼저 [변경 hello ASCS/SCS 기본 로드 hello Azure 내부 부하 분산 장치에 대 한 규칙을 분산][sap-ha-guide-8.9]합니다.

hello 다음 몇 가지 작업 아닌 문서에 설명 된 hello 표준 SAP 설치 합니다.

> [!NOTE]
> SAP 설치 설명서 hello tooinstall 첫 번째 ASCS/SCS 클러스터 노드를 hello 하는 방법을 설명 합니다.
>
>

#### <a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Hello ASCS/SCS 인스턴스의 hello SAP 프로필 수정

새 프로필 매개 변수 tooadd가 필요합니다. hello 프로필 매개 변수는 너무 오랫동안 유휴 상태일 때 닫는에서 SAP 작업 프로세스와 hello enqueue 서버 사이의 연결을 방지 합니다. Hello 문제 시나리오에서 설명한 대로 [hello SAP ASCS/SCS 인스턴스의 클러스터 노드 모두에 레지스트리 항목을 추가][sap-ha-guide-8.11]합니다. 이 섹션에서도 도입 했습니다 두 변경 toosome 기본 TCP/IP 연결 매개 변수를입니다. 두 번째 단계에서는 tooset hello enqueue 서버 toosend 해야는 `keep_alive` hello 연결 hello Azure 내부 부하 분산 장치의 유휴 임계값에 도달 하지 않도록 신호입니다.

toomodify hello hello ASCS/SCS 인스턴스의 SAP 프로필:

1.  이 프로필 매개 변수 toohello SAP ASCS/SCS 인스턴스에 프로필을 추가 합니다.

  ```
  enque/encni/set_so_keepalive = true
  ```
  예에서 hello 경로:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  예를 들어 toohello SAP SCS 인스턴스에 프로필 및 해당 경로:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  tooapply hello 변경 hello /SCS SAP ASCS 인스턴스를 다시 시작 합니다.

#### <a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> 프로브 포트 추가

Azure 부하 분산 장치와 hello 내부 부하 분산 장치의 프로브 기능 toomake hello 전체 클러스터 구성 작업을 사용 합니다. hello Azure 내부 부하 분산 장치는 일반적으로 hello 들어오는 작업 참여 가상 컴퓨터 사이 고르게 배포합니다. 그러나 하나의 인스턴스만 활성 상태가 되므로 일부 클러스터 구성에서는 작동하지 않습니다. hello 다른 인스턴스는 수동 이므로 hello 작업 부하를 받아들일 수 없습니다. 프로브 기능에는 hello Azure 내부 부하 분산 장치 할당 작업만 tooan 활성 인스턴스 때 도움이 됩니다. Hello 프로브 기능을 통해 hello 내부 부하 분산 장치 인스턴스 활성화에 대 한 hello 작업과 hello 인스턴스만 대상을 검색할 수 있습니다.

tooadd 프로브 포트:

1.  Hello 현재 확인 **ProbePort** hello 다음 PowerShell 명령을 실행 하 여 설정 합니다. Hello 클러스터 구성에서 옵니다 hello 가상 컴퓨터 중 하나를 실행 합니다.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  프로브 포트를 정의합니다. hello 기본 프로브 포트 번호는 **0**합니다. 예제에서는 **62000** 프로브 포트를 사용합니다.

  ![그림 58: hello 클러스터 구성 프로브 포트는 기본적으로 0][sap-ha-guide-figure-3048]

  _**그림 58:** hello 기본 클러스터 구성 프로브 포트는 0_

  hello 포트 번호는 SAP Azure 리소스 관리자 템플릿을에 정의 됩니다. PowerShell에서 hello 포트 번호를 할당할 수 있습니다.

  hello에 대 한 새 ProbePort 값 tooset  **SAP <*SID*> IP * * 클러스터 리소스를 hello 다음 PowerShell 스크립트를 실행 합니다. 사용자 환경에 대 한 hello PowerShell 변수를 업데이트 합니다. Hello 스크립트를 실행 한 후 메시지 표시 toorestart hello SAP 클러스터 그룹 tooactivate hello 변경 됩니다.

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  Hello 상태로 전환한 후  **SAP <*SID*> * * 클러스터 역할을 온라인에서 **ProbePort** toohello 새 값으로 설정 되어 있습니다.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![그림 59: hello 새 값을 설정한 후 hello 클러스터 포트 프로브][sap-ha-guide-figure-3049]

  _**그림 59:** hello 새 값을 설정한 후 hello 클러스터 포트 프로브_

#### <a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Hello Windows 방화벽의 프로브 포트 열기

클러스터 노드 모두에서 Windows 방화벽 프로브 포트 tooopen이 필요합니다. 다음 스크립트는 Windows 방화벽의 프로브 포트 tooopen hello를 사용 합니다. 사용자 환경에 대 한 hello PowerShell 변수를 업데이트 합니다.

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

hello **ProbePort** 너무 설정**62000**합니다. Hello 파일 공유에 액세스할 수 이제  **\\\ascsha-clsap\sapmnt** 등에서 다른 호스트에서 **ascsha dba**합니다.

### <a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Hello 데이터베이스 인스턴스를 설치 합니다.

tooinstall hello 데이터베이스 인스턴스를 hello SAP 설치 설명서에에서 설명 된 hello 프로세스를 수행 합니다.

### <a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Hello 두 번째 클러스터 노드를 설치 합니다.

tooinstall hello 두 번째 클러스터 hello SAP 설치 가이드의에서 hello 단계를 수행 합니다.

### <a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Hello SAP 호출자 Windows 서비스 인스턴스의 hello 시작 유형을 변경합니다

Hello SAP 호출자 Windows 서비스의 시작 유형을 hello도 변경**자동 (지연 된 시작)** 클러스터 노드 모두에 있습니다.

![그림 60: hello SAP 호출자 인스턴스 toodelayed 자동에 대 한 hello 서비스 유형 변경][sap-ha-guide-figure-3050]

_**그림 60:** hello SAP 호출자 인스턴스 toodelayed 자동에 대 한 hello 서비스 유형 변경_

### <a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Hello SAP 기본 응용 프로그램 서버를 설치 합니다.

Hello 기본 응용 프로그램 서버 (PA) 인스턴스를 설치 <*SID*> 지정한 hello 가상 컴퓨터-di-0 toohost hello PAS 합니다. Azure 또는 DataKeeper 관련 설정과는 관련이 없습니다.

### <a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Hello SAP 추가 응용 프로그램 서버를 설치 합니다.

지정한 toohost SAP 응용 프로그램 서버 인스턴스는 모든 hello 가상 컴퓨터에는 SAP 추가 응용 프로그램 서버 (AAS)를 설치 합니다. 예를 들어 <*SID*>-d i-1 너무 <*SID*>-d i-&lt;n&gt;합니다.

> [!NOTE]
> 가용성이 높은 SAP NetWeaver 시스템의 hello 설치를 마칩니다. 다음으로 장애 조치 테스트를 진행합니다.
>


## <a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Hello SAP ASCS/SCS 인스턴스 장애 조치 및 SIOS 복제를 테스트 합니다.
쉽게 tootest 사용 되며 장애 조치 클러스터 관리자 및 hello SIOS DataKeeper 관리 및 구성 도구를 사용 하 여 SAP ASCS/SCS 인스턴스 장애 조치 및 SIOS 디스크 복제를 모니터링 합니다.

### <a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS 인스턴스가 클러스터 노드 A에서 실행되고 있습니다.

hello **SAP PR1** 클러스터 그룹 1. 클러스터 노드에서 실행 되 고 예를 들어에 **pr1-ascs-0**합니다. Hello에 참가 하는 hello 공유 디스크 드라이브를 할당 **SAP PR1** hello ASCS/SCS 인스턴스를 사용 하 여 toocluster 노드 A와 그룹을 클러스터링

![그림 61: 장애 조치 클러스터 관리자: hello SAP < SID > 클러스터 그룹이 클러스터 노드 A에서 실행 되 고][sap-ha-guide-figure-5000]

_**그림 61:** 장애 조치 클러스터 관리자: SAP hello <*SID*> 클러스터 그룹이 클러스터 노드 A에서 실행 되 고_

Hello SIOS DataKeeper 관리 및 구성 도구에서 해당 데이터는 hello 원본 볼륨 드라이브 S toohello 대상 볼륨 드라이브 S 2. 클러스터 노드에서 클러스터 노드에서에서 동기적으로 복제 hello 공유 디스크를 볼 수 있습니다. 예를 들어에서 복제 **pr1 ascs 0 [10.0.0.40]** 너무**pr1 ascs 1 [10.0.0.41]**합니다.

![그림 62:에서 SIOS DataKeeper를 복제할 수 hello 로컬 볼륨 클러스터 노드에서 toocluster 노드 B][sap-ha-guide-figure-5001]

_**그림 62:** SIOS DataKeeper를 클러스터 노드에서 toocluster 노드 B hello 로컬 볼륨 복제_

### <a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>노드 A toonode B에서에서 장애 조치

1.  Hello SAP의 장애 조치 옵션 tooinitiate 다음 중 하나를 선택 <*SID*> b: 클러스터 노드 A toocluster 노드에서 클러스터 그룹
  - 장애 조치(failover) 클러스터 관리자 사용  
  - 장애 조치 클러스터 PowerShell 사용

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  Hello Windows 게스트 운영 체제 내에서 클러스터 노드 A를 다시 시작 (hello SAP의 자동 장애 조치를 시작 하는이 <*SID*> 클러스터 그룹에서 노드 A toonode B).  
3.  Hello Azure 포털에서에서 클러스터 노드 A를 다시 시작 (hello SAP의 자동 장애 조치를 시작 하는이 <*SID*> 클러스터 그룹에서 노드 A toonode B).  
4.  Azure PowerShell을 사용 하 여 클러스터 노드 A를 다시 시작 (hello SAP의 자동 장애 조치를 시작 하는이 <*SID*> 클러스터 그룹에서 노드 A toonode B).

  장애 조치 후 SAP hello <*SID*> 2. 클러스터 노드에서 실행 되 고 클러스터 그룹 실행 되는 예를 들어 **pr1-ascs-1**합니다.

  ![그림 63: 장애 조치 클러스터 관리자에서 hello SAP < SID > 클러스터 그룹 노드에서 실행 중인 클러스터 B][sap-ha-guide-figure-5002]

  _**그림 63**: 장애 조치 클러스터 관리자에서 SAP hello <*SID*> 클러스터 그룹 B 클러스터 노드에서 실행 되 고_

  hello 공유 디스크가 현재 탑재 되어 클러스터에서 노드 2. SIOS DataKeeper를 복제 하 고 데이터 원본 볼륨 드라이브 S 1. 클러스터 노드에서 클러스터 노드 B tootarget 볼륨 드라이브 S에서 복제 되는 예를 들어 **pr1 ascs 1 [10.0.0.41]** 너무**pr1 ascs 0 [10.0.0.40]**합니다.

  ![그림 64: SIOS DataKeeper hello 로컬 볼륨 클러스터 노드 B toocluster 노드 A에서 복제][sap-ha-guide-figure-5003]

  _**그림 64:** SIOS DataKeeper 클러스터 노드 B toocluster 노드 A에서에서 hello 로컬 볼륨 복제_
