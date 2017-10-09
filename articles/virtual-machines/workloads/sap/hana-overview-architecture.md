---
title: "aaaOverview 및 Azure (대형 인스턴스)에서 아키텍처의 SAP HANA | Microsoft Docs"
description: "방법의 아키텍처 개요 (대형 인스턴스) Azure에서 SAP HANA tooDeploy 합니다."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e3ee6864af37ac322635eaef43e3c20101e3a769
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-overview-and-architecture-on-azure"></a>Azure의 SAP HANA(대규모 인스턴스) 개요 및 아키텍처

## <a name="what-is-sap-hana-on-azure-large-instances"></a>SAP HANA on Azure(대규모 인스턴스)란?

(대형 인스턴스) Azure에서 SAP HANA 고유의 솔루션을 tooAzure입니다. 또한 Azure 가상 컴퓨터 배포 및 실행할 SAP HANA를 Azure의 hello 목적을 위해 제공 tooproviding 가능성 toorun hello 하 고 고객으로 서 전용된 tooyou 완전 복구 서버에 SAP HANA를 배포 합니다. Azure (대형 인스턴스) 솔루션에서 SAP HANA hello tooyou 고객으로 서 할당 된 호스트/서버 공유 되지 않은 완전 하드웨어 기반으로 합니다. hello 서버 하드웨어는 계산/서버, 네트워킹 및 저장소 인프라를 포함 하는 큰 스탬프에 포함 됩니다. 이는 하나의 조합으로 HANA TDI 인증을 받았습니다. hello 서비스 제공 서비스 (대형 인스턴스) Azure에서 SAP HANA의 다양 한 다른 서버 Sku 또는 960 Cpu 및 20TB 메모리를가지고 768 GB 메모리 toounits 단위 72 Cpu가 있는 상태에서 시작 하는 크기를 제공 합니다.

세부 정보에는 다음과 같은 테 넌 트 hello 고객 격리 hello 인프라 스탬프 내에서 수행 됩니다.

- 네트워킹: 고객 할당 테넌트별로 가상 네트워크를 통해 인프라 스택 내의 고객 격리. 테 넌 트에 단일 고객 tooa 할당 됩니다. 고객은 여러 개의 테넌트를 둘 수 있습니다. 테 넌 트의 네트워크 격리 hello hello 인프라 스탬프 수준에서 테 넌 트 간의 네트워크 통신을 금지합니다. 테 넌 트 toohello 속한 경우에 동일한 고객 합니다.
- 저장소 구성 요소: 저장소 볼륨이 있는 저장소 가상 컴퓨터를 통해 격리 tooit 할당 합니다. 저장소 볼륨 tooone 저장소 가상 컴퓨터만 할당할 수 있습니다. 저장소 가상 컴퓨터에 독점적으로 tooone 단일 테 넌 트 hello SAP HANA TDI 인증 된 인프라 스택에 할당 됩니다. 따라서 tooa 저장소 가상 컴퓨터를 할당 하는 저장소 볼륨은 하나의 구체적이 고 관련 테 넌 트에만 액세스할 수 있습니다. 및 hello 다른 배포 된 테 넌 트 간에 표시 되지 않습니다.
- 서버 또는 호스트: 서버 또는 호스트 단위는 고객 또는 테넌트 간 공유되지 않습니다. 서버 또는 호스트 tooa 고객 배포, tooone 단일 테 넌 트에 할당 된 완전 계산 원자성 단위입니다. 고객이 호스트 또는 서버를 다른 고객과 공유하는 결과를 초래할 수 있는 하드웨어 파티션 또는 소프트 파티션은 사용되지 **않습니다**. Hello 특정 테 넌 트의 toohello 저장소 가상 컴퓨터에 할당 된 저장소 볼륨에 탑재 된 toosuch 서버는. 테 넌 트에만 할당 된 다른 Sku의 toomany 서버 단위를 하나 있을 수 있습니다.
- Azure (대형 인스턴스) 인프라 스탬프에서 SAP HANA, 내에서 여러 다른 테 넌 트 배포 되 고 네트워킹, 저장소 및 계산 수준에 hello 테 넌 트 개념을 통해 서로 대해 격리 합니다. 


이러한 완전 서버 단위는 지원 되는 toorun SAP HANA만입니다. hello SAP 응용 프로그램 계층 또는 작업 웨어 중간 계층에는 Microsoft Azure 가상 컴퓨터에서 실행 중입니다. SAP HANA hello Azure (대형 인스턴스)에서 실행 하는 hello 인프라 스탬프 단위는 연결 된 toohello Azure 네트워크 백본을, 짧은 대기 시간 단위 (대형 인스턴스)를 Azure에 SAP HANA와 Azure 가상 컴퓨터 연결이 제공 되는입니다.

이 문서를 (대형 인스턴스) Azure에서 SAP HANA의 hello 주제를 다루는 5 개 문서 중 하나입니다. 이 문서에서는 hello 기본 아키텍처, 책임, 제공 된 서비스를 통해 선택한 hello 솔루션의 기능을 통해 높은 수준의 있네요. 대부분의 네트워킹 및 연결, 같은 hello 영역에 대 한 hello 다른 4 개의 문서 세부 정보를 대상으로 하 고 드릴 다운 합니다. hello 설명서 (대형 인스턴스) Azure에서 SAP HANA의 SAP NetWeaver 설치의 측면 또는 Azure Vm에서 SAP NetWeaver의 배포를 다루지 않습니다. 이 항목은 동일한 hello에 있는 별도 설명서에 대해서는 설명서 컨테이너입니다. 


이 가이드의 hello 5 부 hello 다음 항목을 포함 합니다.

- [Azure에서 SAP HANA(큰 인스턴스) 개요 및 아키텍처](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Azure의 SAP HANA(큰 인스턴스) 인프라 및 연결](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [어떻게 tooinstall Azure에서 SAP HANA (대형 인스턴스)를 구성 하 고](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Azure의 SAP HANA(큰 인스턴스) 고가용성 및 재해 복구](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Azure의 SAP HANA(큰 인스턴스) 문제 해결 및 모니터링](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="definitions"></a>정의

몇 가지 일반적인 정의가 hello 아키텍처 및 기술 배포 가이드에서 광범위 하 게 사용 됩니다. 참고 hello 용어 및 해당 의미에 따라:

- **IaaS:** Infrastructure as a Service
- **PaaS:** Platform as a Service
- **SaaS:** Software as a Service
- **SAP 구성 요소**: ECC, BW, Solution Manager 또는 EP 등의 개별 SAP 응용 프로그램. SAP 구성 요소는 기존의 ABAP 또는 Java 기술을 기반으로 하거나 비즈니스 개체와 같은 비NetWeaver 기반 응용 프로그램을 기반으로 사용할 수 있습니다.
- **SAP 환경:** 하나 이상의 SAP 구성 요소에 tooperform 개발, QAS, 학습, DR 또는 프로덕션 등의 비즈니스 기능을 논리적으로 그룹화 합니다.
- **SAP 지형:** IT 지형에 toohello 전체 SAP 자산을 참조 합니다. hello SAP 지형에는 모든 프로덕션 및 비프로덕션 환경이 포함 되어 있습니다.
- **SAP 시스템:** hello는 SAP ERP 개발 시스템, SAP BW 테스트 시스템, SAP CRM 프로덕션 시스템 등의 응용 프로그램 계층과 DBMS 계층의 조합입니다. Azure 배포에서는 온-프레미스와 Azure 간에 이러한 두 계층 분할을 지원하지 않습니다. 즉, SAP 시스템은 온-프레미스에 배포되거나 Azure에 배포됨을 의미합니다. 그러나 hello 서로 다른 시스템에 Azure 또는 온-프레미스 SAP 지형의을 배포할 수 있습니다. 예를 들어 hello SAP CRM 프로덕션 시스템 온-프레미스를 배포 하는 동안 Azure의 hello SAP CRM 개발 및 테스트 시스템을 배포할 수 있습니다. (대형 인스턴스) Azure에서 SAP HANA를 Azure Vm에서 SAP 시스템의 SAP 응용 프로그램 계층 hello 호스팅하고 hello HANA 큰 인스턴스 스탬프에서 장치 관련된 SAP HANA 인스턴스 hello이 됩니다.
- **대형 인스턴스 스탬프:** SAP HANA TDI 하드웨어 인프라 스택이 인증 하며 Azure 내에서 SAP HANA 인스턴스 toorun 전용입니다.
- **(대형 인스턴스) Azure에서 SAP HANA:** 에 인증 된 하드웨어에 큰 인스턴스 스탬프 서로 다른 Azure 지역에 배포 된 SAP HANA TDI의 Azure toorun HANA 인스턴스에 hello 제안에 대 한 공식 이름입니다. hello 관련 용어 **HANA 큰 인스턴스** (대형 인스턴스) Azure에서 SAP HANA 짧은 이며 널리이 기술 배포 가이드를 사용 합니다.
- **크로스-프레미스:** Vm 배포 tooan 사이트 간, 멀티 사이트 또는 hello 온-프레미스 센터와 Azure 간의 ExpressRoute 연결 된 Azure 구독에 있는 시나리오에 설명 합니다. 공통 Azure 설명서에서 이러한 종류의 배포를 프레미스 간 시나리오라고도 합니다. hello hello 연결에 대 한 원인은 tooextend 온-프레미스 도메인, 온-프레미스 Active Directory/OpenLDAP 및 온-프레미스 DNS Azure로입니다. hello 온-프레미스 가로 확장된 toohello hello Azure 구독의 Azure 자산 됩니다. Hello Vm이 확장명이 hello 온-프레미스 도메인의 일부를 수 있습니다. Hello 온-프레미스 도메인의 도메인 사용자 hello 서버에 액세스할 수 및 서비스를 실행할 수에 Vm (예: DBMS 서비스)입니다. 온-프레미스에 배포된 VM과 Azure에 배포된 VM 간의 통신 및 이름 확인이 가능합니다. 이 hello 일반적인 시나리오는 대부분 SAP 자산 배포 됩니다. hello 가이드를 참조 [계획 및 디자인 VPN 게이트웨이에 대 한](../../../vpn-gateway/vpn-gateway-plan-design.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 및 [hello Azure 포털을 사용 하 여 사이트 간 연결이 포함 된 VNet을 만들](../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 대 한 자세한 내용은 합니다.
- **테넌트:** HANA 대규모 인스턴스 스탬프에 배포되는 고객은 “테넌트"로 격리됩니다. 테 넌 트 hello 네트워킹, 저장소 및 다른 테 넌 트의 계산 계층에 격리 됩니다. 따라서 해당 저장소 및 계산 단위로 할당된 toohello 다른 테 넌 트를 서로 볼 수 없습니다 또는 hello에 서로 통신할 HANA 큰 인스턴스 수준에 스탬프입니다. 고객이 다른 테 넌 트에 toohave 배포를 선택할 수 있습니다. 도 hello HANA 큰 인스턴스 스탬프 수준에서 테 넌 트 간에 통신이 없습니다.

Microsoft Azure 공용 클라우드에서 SAP 작업 배포 hello 항목에 게시 된 추가 리소스는 여러 가지가 있습니다. 계획 하 고 Azure에서 SAP HANA의 배포를 실행 하는 모든 사용자는 숙련 된, Azure IaaS의 hello 보안 주체 및 Azure IaaS에서 SAP 워크 로드의 hello 배포 것이 좋습니다. hello 다음 리소스 자세한 정보를 제공 하 고 계속 하기 전에 참조 하도록:


- [Microsoft Azure Virtual Machines에서 SAP 솔루션 사용](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="certification"></a>인증

NetWeaver 인증 hello, 외에 SAP Azure IaaS 등의 특정 인프라에 SAP HANA toosupport SAP HANA에 대 한 특별 한 인증을 필요 합니다.

hello 코어 NetWeaver 및 tooa도 SAP HANA 인증에 SAP Note는 [SAP 참고 #1928533-Azure의 SAP 응용 프로그램: 제품 지원 및 Azure VM 유형](https://launchpad.support.sap.com/#/notes/1928533)합니다.

이 [SAP Note #2316233 - Microsoft Azure(큰 인스턴스)에서 SAP HANA](https://launchpad.support.sap.com/#/notes/2316233/E)도 중요합니다. 이 가이드에서 설명 하는 hello 솔루션을 설명 합니다. 또한 지원 되는 toorun hello GS5 VM 유형의 Azure에서 SAP HANA는 있습니다. [이 경우에 대 한 정보는 hello SAP 웹 사이트에 게시 되어](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html)합니다.

hello Azure (대형 인스턴스) 솔루션에서 SAP HANA 이라고 tooin SAP 참고 #2316233 Microsoft 제공 하며, SAP 고객 hello 기능 toodeploy 대형 SAP Business Suite, SAP 비즈니스 웨어하우스 (BW), S/4 HANA, BW/4HANA 또는 Azure에서 다른 SAP HANA 작업 합니다. hello 솔루션은 SAP HANA 전용된 하드웨어 스탬프 인증 hello 기반 ([SAP HANA 맞게 조정 된 데이터 센터 통합 – TDI](https://scn.sap.com/docs/DOC-63140)). SAP HANA TDI로 실행 중인 구성 된 솔루션 제공 hello 안심할 모든 SAP HANA 기반 응용 프로그램 (SAP HANA에 SAP Business Suite, SAP 비즈니스 웨어하우스 (BW)에 SAP HANA, S4/HANA 및 BW4/HANA 포함) hello toowork 진행 되는 알 수 있는 하드웨어 인프라입니다.

SAP HANA Azure 가상 컴퓨터가이 솔루션에 비해 toorunning 이점이-훨씬 더 큰 메모리 볼륨에 대 한 제공 합니다. 이 솔루션 tooenable 하려는 경우 몇 가지 주요 측면을 충분히 toounderstand 가지가 있습니다.

- hello SAP 응용 프로그램 계층 및 기타 응용 프로그램에서 Azure 가상 컴퓨터 (Vm) hello 일반적인 Azure 하드웨어 스탬프에서 호스트 되는 실행 합니다.
- 고객 온-프레미스 인프라, 데이터 센터 및 응용 프로그램 배포는 Azure express 경로 (권장)를 통해 연결 된 toohello Microsoft Azure 클라우드 플랫폼 또는 개인 네트워크 VPN (가상). Active Directory(AD) 및 DNS도 Azure로 확장됩니다.
- HANA 작업에 대 한 hello SAP HANA 데이터베이스 인스턴스 (대형 인스턴스) Azure에서 SAP HANA에서 실행 됩니다. hello 큰 인스턴스 스탬프는 Azure Vm에서 실행 되는 소프트웨어 HANA 대형 인스턴스에서 실행 hello HANA 인스턴스와 상호 작용할 수 있도록 Azure 네트워킹에 연결 되어 있습니다.
- Azure(큰 인스턴스)에서 SAP HANA의 하드웨어는 SUSE Linux Enterprise Server 또는 Red Hat Enterprise Linux가 미리 설치되어 IaaS(Infrastructure as a Service)로 제공되는 전용 하드웨어입니다. Azure 가상 컴퓨터와 앞서 업데이트 및 유지 관리 toohello 운영 체제에는 사용자의 책임이입니다.
- 설치 HANA 또는 모든 추가 구성 요소가 필요한 toorun SAP HANA HANA 큰 인스턴스의 단위에는 사용자의 책임 모든 해당 진행 중인 작업 및 Azure에서 SAP HANA의 관리 됩니다.
- 또한 여기에 설명 된 toohello 솔루션 tooSAP HANA Azure (대형 인스턴스)에 연결 하는 Azure 구독에서 다른 구성 요소를 설치할 수 있습니다.  와 통신 및/또는 직접 toohello SAP HANA 데이터베이스를 사용할 수 있는 구성 요소 예를 들어 (점프 서버, RDP 서버, SAP HANA Studio, SAP BI 시나리오에 대 한 SAP 데이터 서비스 또는 네트워크 모니터링 솔루션).
- Azure에서와 같이 HANA 큰 인스턴스는 고가용성 및 재해 복구 기능을 제공합니다.

## <a name="architecture"></a>아키텍처

상위 수준에서 hello Azure (대형 인스턴스) 솔루션에서 SAP HANA에 hello SAP 응용 프로그램 계층의 큰 인스턴스 스탬프에 있는 SAP TDI 구성 된 하드웨어에 있는 Azure Vm 및 hello 데이터베이스 계층에 있는 연결 된 동일한 Azure 지역 hello IaaS tooAzure 합니다.

> [!NOTE]
> Hello toodeploy hello SAP 응용 프로그램 계층에 필요한 SAP DBMS 계층 hello와 같은 Azure 지역입니다. 이 규칙은 Azure에서 SAP 워크로드에 대해 게시된 정보에 잘 문서화되어 있습니다. 

hello (대형 인스턴스) Azure에서 SAP HANA의 전체 아키텍처는 SAP TDI 인증 된 하드웨어 구성 (가상화 되지 않은, bare metal, hello SAP HANA 데이터베이스에 대 한 고성능 서버) 및 hello와 기능을 제공 Azure tooscale의 유연성 hello에 대 한 리소스를 SAP 응용 프로그램 계층 toomeet 필요 합니다.

![Azure(큰 인스턴스)에서 SAP HANA의 아키텍처 개요](./media/hana-overview-architecture/image1-architecture.png)

표시 된 hello 아키텍처는 3 개의 섹션으로 구분 됩니다.

- **오른쪽:** 최종 사용자가 LOB 응용 프로그램(예: SAP)에 액세스하는 데이터 센터에서 서로 다른 응용 프로그램을 실행하는 온-프레미스 인프라. 이상적으로이 온-프레미스 인프라 연결 되 azure tooAzure [ExpressRoute](https://azure.microsoft.com/services/expressroute/)합니다.

- **센터:** 표시 Azure IaaS 및 Azure Vm toohost SAP 또는 DBMS 시스템으로 SAP HANA를 사용 하는 다른 응용 프로그램의 경우에 사용 합니다. Azure Vm의 메모리를 hello 함수를 제공 하는 보다 작은 HANA 인스턴스의 해당 응용 프로그램 계층와 함께 Azure Vm에 배포 됩니다. [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/)에 대해 자세히 알아보세요.
<br />Azure 네트워킹은 다른 응용 프로그램을 Azure 가상 네트워크 (Vnet)을 함께 사용 되는 toogroup SAP 시스템입니다. 이러한 Vnet tooSAP Azure (대형 인스턴스)에서 HANA 뿐만 아니라 tooon 온-프레미스 시스템에 연결합니다.
<br />SAP NetWeaver 응용 프로그램 및 데이터베이스는 Microsoft Azure에서 toorun 지원에 대 한 참조 [SAP 지원 참고 #1928533-Azure의 SAP 응용 프로그램: 제품 지원 및 Azure VM 유형](https://launchpad.support.sap.com/#/notes/1928533)합니다. Azure에서 SAP 솔루션 배포에 대한 설명서는 다음을 검토합니다.

  -  [Windows VM(가상 컴퓨터)에서 SAP 사용](../../virtual-machines-windows-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  -  [Microsoft Azure Virtual Machines에서 SAP 솔루션 사용](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

- **왼쪽:** 표시 hello 인증 된 하드웨어 hello Azure 큰 인스턴스 스템 프에서 SAP HANA TDI 합니다. hello HANA 큰 인스턴스 단위는 연결 된 toohello Azure Vnet에서 hello 연결으로 동일한 기술 온-프레미스를 Azure로 hello를 사용 하 여 구독입니다.

hello Azure 큰 인스턴스 스탬프 자체는 다음과 같은 구성 요소가 hello를 결합 합니다.

- **컴퓨팅:** hello 필요한 컴퓨팅 기능을 제공 하며 SAP HANA를 인증 하는 Intel Xeon E7 8890v3 또는 Intel Xeon E7 8890v4 프로세서를 기반으로 하는 서버입니다.
- **네트워크:** A hello 컴퓨팅, 저장소 및 LAN 구성 요소를 상호 연결 하는 고속 네트워크 fabric을 통합 합니다.
- **저장소:** 통합된 네트워크 패브릭을 통해 액세스되는 저장소 인프라입니다. 특정 저장소 용량이 제공 hello에 따라 특정 SAP HANA Azure (대형 인스턴스) 구성에 배포 되 고 (저장소 용량을 추가로 추가 월별 비용 사용할 수 있음).

Hello 큰 인스턴스 스탬프의 hello 다중 테 넌 트 인프라 내에서 고객은 격리 된 테 넌 트 배포 됩니다. Hello 테 넌 트의 배포 시 Azure 등록 내 tooname Azure 구독 필요 합니다. 이 진행 중인 toobe hello Azure 구독 HANA 큰 인스턴스 hello에 대 한 청구 toobe를 하려고 합니다. 이러한 테 넌이 트 1:1 관계 toohello Azure 구독이 있어야 합니다. 네트워크 현명한 가능한 tooaccess HANA 대형 인스턴스 단위는 Azure 구독 한 테 넌 트 toodifferent 속하는 다른 Azure Vnet에서 Azure 지역에서에 배포 합니다. Azure 구독 필요 toobelong toohello 있지만 동일한 Azure 등록 합니다. 

Azure VM과 마찬가지로, Azure(큰 인스턴스)에서 SAP HANA이 여러 Azure 지역에 제공됩니다. 순서 toooffer 재해 복구 기능에 tooopt를 선택할 수 있습니다. 다른 큰 인스턴스 한 정치적 지리적 지역 내에서 매우 다른 tooeach 연결된 합니다. 예를 들어 미국 서 부 및 미국 동부 HANA 대형 인스턴스 스탬프가 DR 복제의 hello 용도 대 한 전용된 네트워크 링크를 통해 연결 됩니다. 

Azure Virtual Machines로 서로 다른 VM 유형 간에 선택할 수 있는 것처럼 SAP HANA의 다양한 워크로드 유형에 맞게 조정된 HANA 큰 인스턴스의 다양한 SKU 중에서 선택할 수 있습니다. Hello Intel 프로세서 세대에 따라 다양 한 작업에 메모리 tooprocessor 소켓 비율을 적용 하는 SAP-는 제공 하는 네 가지 SKU 유형이 있습니다.

2017 년 1 월을 기준으로 (대형 인스턴스) Azure에서 SAP HANA는 hello Azure 지역의 미국 서 부 및 미국 동부, 오스트레일리아 동부, 오스트레일리아 남동부, 서 부 유럽 및 유럽 북부에서 여러 구성에서 제공 됩니다.

| SAP 솔루션 | CPU | 메모리 | 저장소 | Availability |
| --- | --- | --- | --- | --- |
| OLAP에 대해 최적화됨: SAP BW, BW/4HANA<br /> 또는 SAP HANA(일반 OLAP 워크로드용) | Azure S72에서 SAP HANA<br /> – 2 x Intel® Xeon® 프로세서 E7-8890 v3<br /> 36 CPU 코어 및 72 CPU 스레드 |  768 GB |  3 TB | 사용 가능 |
| --- | Azure S144에서 SAP HANA<br /> – 4 x Intel® Xeon® 프로세서 E7-8890 v3<br /> 72 CPU 코어 및 144 CPU 스레드 |  1.5 TB |  6 TB | 더 이상 제공되지 않음 |
| --- | Azure S192에서 SAP HANA<br /> – 4 x Intel® Xeon® 프로세서 E7-8890 v4<br /> 96 CPU 코어 및 192 CPU 스레드 |  2.0 TB |  8 TB | 사용 가능 |
| --- | Azure S384에서 SAP HANA<br /> – 8 x Intel® Xeon® 프로세서 E7-8890 v4<br /> 192 CPU 코어 및 384 CPU 스레드 |  4.0 TB |  16 TB | 준비 tooOrder |
| OLTP에 대해 최적화됨: SAP Business Suite<br /> SAP HANA 또는 S/4HANA(OLTP)에서,<br /> 일반 OLTP | Azure S72m에서 SAP HANA<br /> – 2 x Intel® Xeon® 프로세서 E7-8890 v3<br /> 36 CPU 코어 및 72 CPU 스레드 |  1.5 TB |  6 TB | 사용 가능 |
|---| Azure S144m에서 SAP HANA<br /> – 4 x Intel® Xeon® 프로세서 E7-8890 v3<br /> 72 CPU 코어 및 144 CPU 스레드 |  3.0 TB |  12 TB | 더 이상 제공되지 않음 |
|---| Azure S192m에서 SAP HANA<br /> – 4 x Intel® Xeon® 프로세서 E7-8890 v4<br /> 96 CPU 코어 및 192 CPU 스레드  |  4.0 TB |  16 TB | 사용 가능 |
|---| Azure S384m에서 SAP HANA<br /> – 8 x Intel® Xeon® 프로세서 E7-8890 v4<br /> 192 CPU 코어 및 384 CPU 스레드 |  6.0 TB |  18 TB | 준비 tooOrder |
|---| Azure S384xm에서 SAP HANA<br /> – 8 x Intel® Xeon® 프로세서 E7-8890 v4<br /> 192 CPU 코어 및 384 CPU 스레드 |  8.0 TB |  22 TB |  준비 tooOrder |
|---| Azure S576에서 SAP HANA<br /> – 12 x Intel® Xeon® 프로세서 E7-8890 v4<br /> 288 CPU 코어 및 576 CPU 스레드 |  12.0 TB |  28 TB | 준비 tooOrder |
|---| Azure S768에서 SAP HANA<br /> – 16 x Intel® Xeon® 프로세서 E7-8890 v4<br /> 384 CPU 코어 및 768 CPU 스레드 |  16.0 TB |  36 TB | 준비 tooOrder |
|---| Azure S960에서 SAP HANA<br /> – 20 x Intel® Xeon® 프로세서 E7-8890 v4<br /> 480 CPU 코어 및 960 CPU 스레드 |  20.0 TB |  46 TB | 준비 tooOrder |

- CPU 코어 = hello 서버 단위 hello 프로세서 hello 합계의 비-하이퍼 스레드 CPU 코어 수의 합입니다.
- CPU 스레드 = hello 합계 hello 서버 단위 hello 프로세서의 CPU 코어 하이퍼 스레드된에서 제공 하는 계산 스레드는 sum입니다. 모든 장치는 하이퍼 스레딩 기본 toouse로 구성 됩니다.


hello 사용 가능 하거나 '에 제공 되지 않습니다 더 이상' 위의 서로 다른 구성에서 참조 되는 [SAP 지원 참고 #2316233 – Microsoft Azure (대형 인스턴스)에서 SAP HANA](https://launchpad.support.sap.com/#/notes/2316233/E)합니다. hello 구성 '준비 tooOrder'로 표시 된 SAP Note hello에 해당 항목을 곧 검색 됩니다. 하지만 이러한 인스턴스 Sku 순서를 지정할 수 이미 hello 다른 6에 대 한 Azure 지역 hello HANA 큰 인스턴스 서비스를 사용할 수 있습니다.

hello 특정 구성을 선택 작업 부하, CPU 리소스와 원하는 메모리에 따라 달라 집니다. OLTP 워크 로드 tooleverage hello OLAP 작업 부하에 맞게 최적화 된 Sku에 대 한 것 같습니다. 

모든 hello 제안에 대 한 기본 hello 하드웨어는 SAP HANA TDI 인증 합니다. 그러나이 hello Sku에 구분선 하드웨어의 서로 다른 두 클래스 구분 됩니다.

- S72, S72m, S144, S144m, S192, 및 S192m tooas hello '클래스 I t y'는 Sku입니다.
- S384, S384m, S384xm, S576, S768, 및은 기관 S960 tooas hello Sku의 ' Type II 클래스'.

단일 고객 &#39;에 대 한 전체 HANA 대형 인스턴스 스탬프 독점적으로 할당 되지 않은 중요 한 toonote는 s 사용 합니다. 이 팩트에도 Azure에 배포 된 네트워크 패브릭을 통해 연결 된 계산 및 저장소 리소스의 toohello 랙에 적용 됩니다. 서로 다른 고객을 배포 하는 Azure 등의 큰 인스턴스 HANA 인프라 &quot;테 넌 트&quot; hello 다음 세 가지 수준에서에서 서로 격리 되:

- Hello HANA 큰 인스턴스 스탬프 내의 가상 네트워크를 통해: 네트워크 격리 합니다.
- 저장소: 저장소 볼륨이 할당되고 테넌트 간 저장소 볼륨을 격리하는 저장소 가상 컴퓨터를 통해 격리.
- 계산: 전용 서버 단위 tooa 단일 테 넌 트의 할당 합니다. 서버 단위의 하드 또는 소프트 파티션 없음. 테넌트 간 단일 서버 또는 호스트 단위의 공유 없음. 

따라서 다른 테 넌 트 간의 HANA 큰 인스턴스 단위 hello 배포는 다른 tooeach 표시 되지 않습니다. 또는 다른 테 넌 트에 배포 된 HANA 큰 인스턴스 단위 직접 통신할 수 hello HANA 큰 인스턴스 스탬프 수준에서 서로 합니다. HANA 큰 인스턴스 단위만 한 테 넌 트 내에서 tooeach hello HANA 큰 인스턴스 스탬프 수준에 다른 통신할 수 있습니다.
Hello 큰 인스턴스 스템 프에서 배포 된 테 넌 트 청구 현명한 tooone Azure 구독에 할당 됩니다. 그러나 네트워크 현명한 다른 Azure 구독 내에서 Azure Vnet에서 액세스할 수 있습니다 hello 동일한 Azure 등록 합니다. 배포 하는 경우 hello에서 다른 Azure 구독과 동일한 Azure 지역 선택할 수도 tooask 분리 된 HANA 큰 인스턴스 테 넌 트에 대 한 합니다.

HANA 대규모 인스턴스에서 SAP HANA를 실행할 때와 Azure에 배포된 Azure VM에서 SAP HANA를 실행할 때는 상당한 차이가 있습니다.

- Azure(큰 인스턴스)의 SAP HANA의 경우 가상화 계층이 없습니다. Hello 기본 완전 하드웨어의 hello 성능을 얻을 수 있습니다.
- Azure와 달리 Azure (대형 인스턴스) 서버에서 SAP HANA hello는 전용된 tooa 특정 고객 합니다. 서버 단위 또는 호스트가 하드 또는 소프트 파티션될 가능성은 없습니다. 결과적으로, 고객으로 서 해당 tooyou와 전체 tooa tenant로 지정 되므로 HANA 큰 인스턴스 단위 사용 됩니다. Toohello 운영 체제와 다른 서버에 배포 되는 SAP HANA 다시 부팅 또는 종료의 hello 서버를 자동으로 발생 하지 않습니다. (형식에 대 한 Sku 클래스 I, hello 유일한 예외는 서버에 문제가 발생할 수 있습니다 및 재배포 toobe 다른 서버에서 수행 해야 하는 경우.)
- 여기서 호스트 프로세서 형식을 hello 최상의 가격 대비 성능 비율에 대 한 선택, Azure와 달리 hello 프로세서 종류 (대형 인스턴스) Azure에서 SAP HANA에 대해 선택한 Intel E7v3 및 E7v4 hello 프로세서 줄에 대 한 가장 높은 수행 hello 됩니다.


### <a name="running-multiple-sap-hana-instances-on-one-hana-large-instance-unit"></a>여러 SAP HANA 인스턴스를 하나의 HANA 큰 인스턴스 단위에서 실행함
Hello HANA 큰 인스턴스 그룹에 활성 SAP HANA 인스턴스가 둘 이상 가능한 toohost 이며 Toostill를 순서 대로 저장소 스냅숏 hello 기능을 제공 하며 이러한 구성은 재해 복구 볼륨 세트 인스턴스당 합니다. 지금 까지의 hello HANA 큰 인스턴스 단위 다음과 같이 세분화할 수 있습니다.

- S72, S72m, S144, S192: 가장 작은 크기는 256gb hello로 256GB 씩에서 단위를 시작합니다. 증분이 256GB, 512 GB 등과 같은 hello 단위의 hello 메모리 결합된 toohello 최대를 지정할 수 있습니다.
- S144m 및 S192m: 512GB hello 가장 작은 단위와 256GB 씩 증가 합니다. 증분이 512GB, 768 GB 등과 같은 hello 단위의 hello 메모리 결합된 toohello 최대를 지정할 수 있습니다.
- 입력 II 클래스: 2TB의 단위를 시작 하는 가장 작은 hello로 512GB 씩 증가 합니다. 증분이 512GB, 이전의 1TB, 1.5 t B 등 hello 단위의 hello 메모리의 결합 된 toohello 최대를 지정할 수 있습니다.

다음은 여러 SAP HANA 인스턴스 실행의 몇 가지 예입니다.

| SKU | 메모리 크기 | 저장소 크기 | 여러 데이터베이스가 장착된 크기 |
| --- | --- | --- | --- |
| S72 | 768 GB | 3 TB | 1x768 GB HANA 인스턴스<br /> 또는 1x512 GB 인스턴스 + 1x256 GB 인스턴스<br /> 또는 3x256 GB 인스턴스 | 
| S72m | 768 GB | 3 TB | 3x512GB HANA 인스턴스<br />또는 1x512 GB 인스턴스 + 1x1 TB 인스턴스<br />또는 6x256 GB 인스턴스<br />또는 1x1.5 TB 인스턴스 | 
| S192m | 4 TB | 16 TB | 8x512 GB 인스턴스<br />또는 4x1 TB 인스턴스<br />또는 4x512 GB 인스턴스 + 2x1 TB 인스턴스<br />또는 4x768 GB 인스턴스 + 2x512 GB 인스턴스<br />또는 1x4 TB 인스턴스 |
| S384xm | 8 TB | 22 TB | 4x2 TB 인스턴스<br />또는 2x4 TB 인스턴스<br />또는 2x3 TB 인스턴스 + 1x2 TB 인스턴스<br />또는 2x2.5 TB 인스턴스 + 1x3 TB 인스턴스<br />또는 1x8 TB 인스턴스 |


Hello 파악할 수 있습니다. 물론 다른 변형도 있습니다. 


## <a name="operations-model-and-responsibilities"></a>작업 모델 및 책임

hello 서비스 (대형 인스턴스) Azure에서 SAP HANA와 함께 제공 되는 Azure IaaS 서비스와 함께 정렬 됩니다. SAP HANA용으로 최적화된 운영 체제가 설치된 HANA 큰 인스턴스가 생성됩니다. Azure IaaS vm에서 대부분의 hello 작업 강화 hello HANA를 설치 해야 하는 추가 소프트웨어를 설치 하는 운영 체제는 운영 체제 및 HANA를 hello 작동 하 고 운영 체제 및 HANA hello 업데이트에 사용자의 책임이입니다. Microsoft는 사용자에게 OS 업데이트 또는 HANA 업데이트를 강요하지 않습니다.

![Azure(큰 인스턴스)에서 SAP HANA의 책임](./media/hana-overview-architecture/image2-responsibilities.png)

위의 hello 다이어그램에 보시 (대형 인스턴스) Azure에서 SAP HANA 사용 하는 다중 테 넌 트 인프라 서비스 제공 합니다. 및 결과적으로, 책임 hello 분산이 hello OS 인프라 경계 hello에 대 한 대부분의 파트 수 있습니다. Microsoft는 hello 운영 체제의 hello 줄 아래 hello 서비스의 모든 측면에 대해 책임 지지 되며 hello 운영 체제를 포함 하 여 hello 줄 위에 있습니다. 따라서 최신 온-프레미스 메서드 사용 될 수 있습니다 준수, 보안, 응용 프로그램 관리, 별로 및 운영 체제 관리에 대 한 사용 toobe를 계속할 수 있습니다. hello 시스템에 대 한 모든 예정에서 네트워크에 있는 것 처럼 나타납니다.

그러나이 서비스 사용자와 Microsoft 이곳 toowork 함께 toouse hello 기본 인프라 기능 최상의 결과 영역 되므로 SAP HANA에 대해 최적화 됩니다.

각 hello 레이어 및 사용자의 책임에 hello 목록 다음에 자세히를 제공 합니다.

**네트워킹:** 모든 hello SAP HANA, 해당 액세스 toohello 저장소 (예: 확장 및 기타 기능) hello 인스턴스, 연결 toohello 가로 및 연결 간의 연결을 실행 하는 hello 큰 인스턴스 스탬프에 대 한 내부 네트워크 tooAzure hello SAP 응용 프로그램 계층은 Azure 가상 컴퓨터를 호스트 하는 위치입니다. 재해 복구 용도 복제를 위해 Azure 데이터 센서 간 WAN 연결도 포함합니다. QOS 적용 한 모든 네트워크 hello 테 넌 트 별로 분할 됩니다.

**저장소:** hello 스냅숏 뿐만 아니라 hello SAP HANA 서버에 필요한 모든 볼륨에 대해 분할 된 저장소를 가상화 합니다. 

**서버:** hello 전용 실제 서버 toorun hello SAP HANA Db tootenants 할당 합니다. 서버 hello I 클래스 형식의 hello Sku의 하드웨어 추상화 됩니다. 이러한 유형의 서버 hello 서버 구성은 수집 되 고 하나의 물리적 하드웨어 tooanother 실제 하드웨어에서 이동할 수 있는 프로필에서 유지 관리 합니다. 비트 비교 될 수 있습니다 이러한 (수동) 이동 프로필의 작업에 의해 tooAzure 서비스 복구 합니다. hello 서버 hello의 Type II 클래스 Sku는 이러한 기능을 제공 하지 않는 합니다.

**SDDC:** 소프트웨어 방식 엔터티로 hello 관리 소프트웨어를 사용 하는 toomanage 데이터 센터입니다. 크기 조정, 가용성 및 성능을 위해 Microsoft toopool 리소스 수 있습니다.

**O/S:** (SUSE Linux 또는 Red Hat Linux)를 선택 하는 운영 체제 hello hello 서버에서 실행 중인 합니다. 제공 되는 hello OS 이미지는 SAP HANA 실행의 hello 용도 대 한 hello 개별 Linux 공급 업체 tooMicrosoft 제공한 hello 이미지입니다. 필요한 toohave hello 특정 SAP HANA 액세스에 최적화 된 이미지에 대 한 hello Linux 공급 업체와 함께 구독 됩니다. 사용자의 책임 hello 이미지 hello OS 공급 업체와 함께 등록을 포함 합니다. Microsoft에서 인계의 hello 점에서 책임이 있습니다도 모든 추가 패치 hello Linux 운영 체제의 합니다. SAP HANA 성공적인 설치에 필요할 수 있는 추가 패키지에 포함 되어이 패치는 또한 (tooSAP의 HANA 설치 설명서 및 SAP Note 참조) 하 고 hello 특정가 SAP HANA에 Linux 공급 업체에서 포함 하지는 OS 이미지를 최적화합니다. 또한 hello 고객의 hello 책임의 최적화 하는 관련 toomalfunction/hello OS 및 드라이버 관련된 toohello 특정 서버 하드웨어 hello OS 패치 포함 됩니다. 또는 모든 보안 또는 기능의 hello OS 패치를 적용 합니다. 고객은 다음 항목의 모니터링 및 용량 계획도 책임집니다.

- CPU 리소스 사용량
- 메모리 사용량
- 관련된 toofree 공간이 볼륨, IOPS, 및 대기 시간
- HANA 큰 인스턴스 및 SAP 응용 프로그램 계층 간의 네트워크 볼륨 트래픽

HANA 큰 인스턴스의 기본 인프라 hello hello OS 볼륨의 백업 및 복원에 대 한 기능을 제공합니다. 이 기능을 사용하는 것도 사용자의 책임입니다.

**미들웨어:** SAP HANA 인스턴스 주로 hello 합니다. 관리, 작업 및 모니터링은 사용자의 책임입니다. 기능은 수 있게 해 주는 toouse storage 스냅숏을 백업/복원 및 재해 복구 목적으로 제공 합니다. 이러한 기능은 hello 인프라에서 제공 됩니다. 그러나 이러한 기능으로 고가용성 또는 재해 복구를 설계하고 활용하며 저장소 스냅숏이 성공적으로 실행되었는지 모니터링하는 것도 사용자의 책임에 포함됩니다.

**데이터:** SAP HANA에서 관리하는 데이터 및 볼륨 또는 파일 공유에 있는 백업 파일과 같은 기타 데이터. 사용자의 책임 사용 가능한 디스크 공간을 모니터링 및 hello 볼륨에 hello 내용 관리 및 디스크 볼륨 및 저장소 스냅숏 백업의 hello 성공적인 실행을 모니터링에 포함 됩니다. 그러나 tooDR 사이트를 복제 하는 데이터의 성공적인 실행은 Microsoft hello 담당 합니다.

**응용 프로그램:** SAP 응용 프로그램 인스턴스 hello 하거나 비 SAP 응용 프로그램, 해당 응용 프로그램의 응용 프로그램 계층 hello 발생 합니다. 해당 응용 프로그램의 관련 toocapacity CPU 리소스 사용량, 메모리 사용, Azure 저장소 사용량 및 내에서 네트워크 대역폭 사용에 대 한 계획 및 배포, 관리, 작업, 사용자의 책임 포함 Azure Vnet에서 Azure Vnet tooSAP Azure (대형 인스턴스)에서 HANA 합니다.

**Wan:** hello 연결 작업에 대 한 온-프레미스 tooAzure 배포에서 설정 합니다. HANA 큰 인스턴스를 장착한 모든 고객은 연결을 위해 Azure ExpressRoute를 사용합니다. 이 연결은이 연결의 hello 설치 프로그램을 담당 하므로 Azure (대형 인스턴스) 솔루션에서 SAP HANA hello의 일부가 아닙니다.

**보관:** 저장소 계정에서 사용자 고유의 메서드를 사용 하 여 데이터의 tooarchive 복사본을 선호할 수 있습니다. 보관하려면 관리, 규정 준수, 비용 및 작업이 필요합니다. 사용자는 Azure에 보관 복사본과 백업을 생성하고 호환되는 방식으로 이를 저장합니다.

Hello 참조 [(대형 인스턴스) Azure에서 SAP HANA에 대 한 SLA](https://azure.microsoft.com/support/legal/sla/sap-hana-large/v1_0/)합니다.

## <a name="sizing"></a>크기 조정

HANA 큰 인스턴스에 대한 크기 조정은 일반적인 HANA에 대한 크기 조정과 다르지 않습니다. 기존 시스템을 배포 하 고 다른 RDBMS tooHANA에서 toomove 5d; SAP 다양 한 기존 SAP 시스템에서 실행 되는 보고서를 제공 합니다. Hello 데이터베이스가 이동된 tooHANA 경우 이러한 보고서는 hello 데이터를 확인 하 고 hello HANA 인스턴스에 대 한 메모리 요구 사항을 계산 합니다. 어떻게 toorun 이러한 보고서에 대 한 자세한 내용은 SAP Note tooget 다음 hello 읽기 방법과 tooobtain의 가장 최근 패치/버전:

- [SAP Note #1793345 - HANA에서 SAP Suite에 대한 크기 조정](https://launchpad.support.sap.com/#/notes/1793345)
- [SAP Note #1872170 - Suite on HANA 및 S/4 HANA 크기 조정 보고서](https://launchpad.support.sap.com/#/notes/1872170)
- [SAP Note #2121330 - FAQ: SAP BW on HANA 크기 조정 보고서](https://launchpad.support.sap.com/#/notes/2121330)
- [SAP Note #1736976 - BW on HANA에 대한 크기 조정 보고서](https://launchpad.support.sap.com/#/notes/1736976)
- [SAP Note #2296290 - BW on HANA에 대한 새 크기 조정 보고서](https://launchpad.support.sap.com/#/notes/2296290)

녹색 필드 구현에서는 SAP 빠른 조절기 hello 구현의 SAP HANA에 소프트웨어의 사용 가능한 toocalculate 메모리 요구 사항입니다.

데이터 볼륨 증가 HANA에 필요한 메모리를 늘리고, 이후 hello 않으므로 toobe 인식 이제 hello 메모리 소비를 원하는 수 toopredict에서 진행 중인 toobe 무엇 인지 합니다. Hello 메모리 요구 사항에 따라는 hello HANA 큰 인스턴스 Sku 중 하나로 보내는 요구를 다음 매핑할 수 있습니다.

## <a name="requirements"></a>요구 사항

이 목록은 Azure(더 큰 인스턴스)에서 SAP HANA를 실행하기 위한 요구 사항을 모읍니다.

**Microsoft Azure:**

- 연결 된 tooSAP HANA azure (대형 인스턴스) 일 수 있는 Azure 구독.
- Microsoft 프리미어 지원 계약입니다. 참조 [SAP 지원 참고 #2015553-Microsoft Azure의 SAP: 지원 필수 구성 요소](https://launchpad.support.sap.com/#/notes/2015553) toorunning Azure에서 SAP 관련 특정 정보에 대 한 합니다. HANA 인스턴스가 큰 단위 384 및 많은 수의 Cpu를 사용 해야 있습니다 tooextend hello 프리미어 지원 계약 tooinclude Azure 신속한 응답 (ARR).
- Hello HANA 큰 인스턴스 SAP와 필요한는 크기 조정을 수행한 후 실행 하는 Sku 알고 있어야 합니다.

**네트워크 연결:**

- 온-프레미스 tooAzure 간의 azure express 경로: tooconnect 프로그램 온-프레미스 데이터 센터 tooAzure 있는지 tooorder ISP에서 적어도 1 g b p s 연결을 확인 하십시오. 

**운영 체제:**

- SAP 응용 프로그램용 SUSE Linux Enterprise Server 12에 대한 라이선스

> [!NOTE] 
> Microsoft에서 제공 하는 운영 체제 hello SUSE, 등록 되지 않은 SMT 인스턴스와 연결 된 아닙니다.

- Azure VM에서 Azure에 배포된 SUSE Linux Subscription Management Tool(SMT). SAP HANA에 대 한 hello 기능 (대형 인스턴스) Azure toobe 등록 하 고 (이므로 HANA 큰 인스턴스 데이터 센터 내에서 인터넷에 액세스할) SUSE 업데이트할 각각에 제공 합니다. 
- SAP HANA용 Red Hat Enterprise Linux 6.7 또는 7.2에 대한 라이선스.

> [!NOTE]
> Red Hat 구독 관리자 인스턴스에 연결 하는 it tooa hello microsoft 운영 체제 아닙니다 Red Hat에 등록 되지 않았습니다.

- Azure VM에서 Azure에 배포된 Red Hat Subscription Manager. Red Hat 구독 관리자 hello Azure (대형 인스턴스) toobe 등록 하 고 각각 Red hat 업데이트할 (이므로 직접 인터넷 액세스가 없는에서 hello Azure 큰 인스턴스 스탬프에 배포 된 hello 테 넌 트 내에서)에 SAP HANA에 대 한 hello 기능을 제공 합니다.
- SAP toohave Linux 공급자도와 계약을 지원 해야 합니다. 이 요구 사항은 HANA 큰 인스턴스 또는 hello 팩트의 hello 솔루션에 의해 삭제 되지 않고 하는 Azure에서 실행된 프로그램 Linux. 와 달리 hello Linux Azure 갤러리 이미지의 일부와 hello 서비스 요금에에서 포함 되지 않습니다 HANA 큰 인스턴스 hello 솔루션 제공 합니다. 고객 toofulfill hello 요구 사항으로 sap 지원 계약에 대 한 hello Linux 배포자와 해야 됩니다.   
   - SUSE Linux에 대 한 지원의 요구 사항에서 계약 hello를 조회 [SAP 참고 #1984787 SUSE LINUX Enterprise Server 12: 설치 참고 사항](https://launchpad.support.sap.com/#/notes/1984787) 및 [SAP 참고 #1056161-SUSE 우선 순위SAP응용프로그램에대한지원](https://launchpad.support.sap.com/#/notes/1056161).
   - Red Hat Linux에 대 한 지원 및 (HANA 큰 인스턴스 toohello 운영 체제를 업데이트 서비스를 포함 하는 toohave hello 올바른 구독 수준 필요 합니다. Red Hat은 "RHEL for SAP Business Applications"를 구독할 것을 권장합니다. 지원 및 서비스와 관련하여 자세한 내용은 [SAP Note #2002167 - Red Hat Enterprise Linux 7.x: 설치 및 업그레이드](https://launchpad.support.sap.com/#/notes/2002167) 및 [SAP Note #1496410 - Red Hat Enterprise Linux 6.x: 설치 및 업그레이드](https://launchpad.support.sap.com/#/notes/1496410)를 확인하세요.

**데이터베이스:**

- SAP HANA에 대한 라이선스 및 소프트웨어 설치 구성 요소(플랫폼 및 Enterprise 버전).

**응용 프로그램:**

- 라이선스 및 HANA tooSAP 연결 하 고 SAP와 관련 된 모든 SAP 응용 프로그램에 대 한 설치 구성 요소 소프트웨어 계약을 지원 합니다.
- 라이선스 및 모든 비 SAP 응용 프로그램에 대 한 소프트웨어 설치 구성 요소 (대형 인스턴스) Azure 환경에 관계 tooSAP HANA에에서 사용 하 고 관련 지원 계약.

**기술:**

- Azure IaaS 및 해당 구성 요소에 대한 경험 및 지식
- Azure에서 SAP 워크로드 배포에 대한 경험 및 지식
- SAP HANA 설치 공인 전문가
- 설계자 기술 toodesign 고가용성 및 재해 복구 SAP HANA 주위 SAP 합니다.

**SAP:**

- SAP와의 지원 계약을 맺은 SAP 고객이기를 기대합니다.
- 특히 hello HANA 큰 인스턴스 Sku의 Type II 클래스에서 구현에서는 것이 좋습니다 tooconsult SAP와 SAP HANA 및 큰 크기의 수직 하드웨어에서 최종 구성의 버전입니다.


## <a name="storage"></a>저장소

hello 저장소 레이아웃 (대형 인스턴스) Azure에서 SAP HANA에 대해 구성 된 SAP HANA SAP 권장 hello에 설명 된 지침을 통해 Azure 서비스 관리에 의해 [SAP HANA 저장소 요구 사항을](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) 백서에 나와 있습니다.

저장소 볼륨으로 hello HANA 큰 hello I 클래스 유형 인스턴스를 4 번 hello 메모리 볼륨 함께 제공 됩니다. Hello 형식 인스턴스가 HANA 큰 단위 II 클래스에 대 한 hello 저장소는 잘못 된 toobe 4 번 더 합니다. hello 단위 HANA 트랜잭션 로그 백업을 저장 하기 위한 볼륨을 함께 제공 됩니다. 자세한 내용을 보려면 [어떻게 tooinstall Azure에서 SAP HANA (대형 인스턴스)를 구성 하 고](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

다음 표를 기준으로 저장소를 할당 하는 hello를 참조 하십시오. 대략 hello 표 hello hello 다른 HANA 큰 인스턴스 단위와 함께 제공 되는 서로 다른 볼륨에 대 한 hello 용량입니다.

| HANA 큰 인스턴스 SKU | hana/data | hana/log | hana/shared | hana/log/backup |
| --- | --- | --- | --- | --- |
| S72 | 1280 GB | 512 GB | 768 GB | 512 GB |
| S72m | 3328 GB | 768 GB |1280 GB | 768 GB |
| S192 | 4608 GB | 1024 GB | 1536 GB | 1024 GB |
| S192m | 11,520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384 | 11,520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384m | 12,000 GB | 2050 GB | 2050 GB | 2040GB |
| S384xm | 16,000 GB | 2050 GB | 2050 GB | 2040GB |
| S576 | 20,000 GB | 3100 GB | 2050 GB | 3100 GB |
| S768 | 28,000 GB | 3100 GB | 2050 GB | 3100 GB |
| S960 | 36,000 GB | 4100 GB | 2050 GB | 4100 GB |


실제 배포 된 볼륨 배포와 도구를 사용 하는 tooshow hello 볼륨 크기에 따라 약간 다를 수 있습니다.

HANA 큰 인스턴스 SKU를 세분화하면 가능한 분할 조각들의 몇 가지 예입니다.

| 메모리 파티션(GB) | hana/data | hana/log | hana/shared | hana/log/backup |
| --- | --- | --- | --- | --- |
| 256 | 400 GB | 160 GB | 304 GB | 160 GB |
| 512 | 768 GB | 384 GB | 512 GB | 384 GB |
| 768 | 1280 GB | 512 GB | 768 GB | 512 GB |
| 1024 | 1792 GB | 640 GB | 1024 GB | 640 GB |
| 1536 | 3328 GB | 768 GB | 1280 GB | 768 GB |


이러한 크기는 배포에 따라 약간씩 다를 수 있는 대략적인 볼륨 숫자 및 toolook hello 볼륨에서 사용 하는 도구입니다. 또한 2.5 TB와 같은 생각할 수 있는 다른 파티션 크기가 있습니다. 이러한 저장소 크기는 위의 hello 파티션에 대 한 사용 된 것과 비슷한 수식으로 계산 될 것입니다. hello 'partitions' 용어는 hello 운영 체제, 메모리 또는 CPU 리소스는 어떤 식으로든에서 분할을 나타내지 않습니다. 방금 hello 다른 HANA toodeploy 하나에 경우 단일 인스턴스가 HANA 큰 단위에 대 한 저장소 파티션을 나타냅니다. 

고객이 가질 수 있으므로으로 더 많은 저장 공간에 필요한, 이전의 1TB 단위에서 hello 가능성 tooadd 저장소 toopurchase 추가 저장소를 사용할 합니다. 이 추가 저장소 추가 볼륨으로 추가할 수 있습니다 또는 하나 이상의 기존 볼륨을 hello 사용된 tooextend 될 수 있습니다. 처음 배포 하 고 위의 hello 테이블 대부분 문서화 hello 볼륨의 가능한 toodecrease hello 크기 않습니다. 또한 없습니다 hello 볼륨의 가능한 toochange hello 이름이 나 탑재 이름. hello 저장소 볼륨 위에서 설명한 대로 연결 된 toohello HANA 큰 인스턴스 단위는 NFS4 볼륨으로.

Toouse storage 스냅숏을 백업/복원 및 재해 복구를 위해 선택할 수는 고객으로 서 있습니다. 이 항목에 대한 자세한 내용은 [Azure의 SAP HANA(큰 인스턴스) 고가용성 및 재해 복구](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에 설명되어 있습니다.

### <a name="encryption-of-data-at-rest"></a>미사용 데이터 암호화
HANA 대규모 인스턴스에 사용 되는 hello 저장소에서는 hello 디스크에 저장 된 hello 데이터의 투명 한 암호화를 허용 합니다. HANA 큰 인스턴스 단위 배포 시 해야 hello 옵션 toohave 이러한 종류의 암호화를 사용 합니다. 또한 선택할 수 있습니다 toochange tooencrypted 볼륨 이미 hello 배포 후. hello 이동 tooencrypted 암호화 되지 않은 볼륨에서 투명 한 가동 중지 시간이 필요 하지 않습니다. 

Sku, LUN에 저장 된 hello 볼륨 hello 부팅 클래스 I 유형 hello로 암호화 됩니다. Hello 형식 인스턴스의 Sku의 HANA 큰 II 클래스의 경우 OS 메서드로 tooencrypt hello 부팅 LUN 해야합니다. 


## <a name="networking"></a>네트워킹

Azure 네트워킹의 hello 아키텍처는 HANA 큰 인스턴스의 SAP 응용 프로그램의 핵심 구성 요소 toosuccessful 배포입니다. 일반적으로 Azure(큰 인스턴스)에서 SAP HANA 배포에는 다양한 데이터베이스 크기, CPU 리소스 사용량 및 메모리 사용률이 있는 서로 다른 여러 SAP 솔루션을 갖춘 더 큰 SAP 환경이 포함됩니다. 이러한 SAP 시스템 전부가 SAP HANA를 기반으로 할 가능성은 없으므로 사용자의 SAP 환경은 다음을 사용하는 하이브리드 형태일 것입니다.

- 온-프레미스에 배포된 SAP 시스템 Tootheir 크기 인해 이러한 시스템 현재에서 호스팅할 수 없는 Azure; 전형적인 예로 cpu를 더 많이 필요 (데이터베이스로 hello) Microsoft SQL Server에서 실행 하는 프로덕션 SAP ERP 시스템이 것 또는 Azure Vm의 메모리 리소스를 제공할 수 있습니다.
- 온-프레미스에 배포된 SAP HANA 기반 SAP 시스템.
- Azure VM에 배포된 SAP 시스템. 이러한 시스템 개발, 테스트, 샌드박스 되거나 프로덕션 hello SAP NetWeaver 기반 응용 프로그램의 리소스 소비와 메모리 요구에 따라 (Vm)에 Azure에서 성공적으로 배포할 수 있는 모든 인스턴스 수입니다. 이들 시스템은 또한 SQL Server([SAP Support Note #1928533 – Azure의 SAP 응용 프로그램: 지원 제품 및 Azure VM 유형](https://launchpad.support.sap.com/#/notes/1928533/E) 참조) 또는 SAP HANA([SAP HANA 인증 IaaS 플랫폼](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html) 참조)와 같은 데이터베이스를 기반으로 할 수도 있습니다.
- Azure 큰 인스턴스 스탬프로 Azure(큰 인스턴스)에서 SAP HANA를 활용하는 Azure(VM에서)에 배포된 SAP 응용 프로그램 서버.

하이브리드 SAP 환경(4개 이상의 다양한 배포 시나리오 포함)은 일반적인 반면에 Azure에서 실행되는 전체 SAP 환경은 고객에 맞춰진 경우가 많습니다. Microsoft Azure Vm 더 강력해졌습니다, hello Azure에서 모든 SAP 솔루션을 이동 하는 고객 수가 증가 합니다.

Azure의 SAP 시스템을 Azure에 배포 된 hello 컨텍스트에서 네트워킹은 복잡 합니다. 다음 원칙 hello은 기반으로 합니다.

- Azure 가상 네트워크 (Vnet) tooon 온-프레미스 네트워크를 연결 하는 연결 된 toobe toohello Azure express 경로 회로 필요 합니다.
- 일반적으로 온-프레미스 tooAzure 연결할 ExpressRoute 회로 1 g b p s 이상 대역폭이 있어야 합니다. 이 최소 대역폭을 적절 한 대역폭을 온-프레미스 시스템과 Azure Vm (뿐만 아니라 최종 사용자가 온-프레미스에서 연결 tooAzure 시스템)에서 실행 되는 시스템 간에 데이터를 전송할 수 있습니다.
- Azure 필요 toobe에 있는 모든 SAP 시스템에서 Azure Vnet toocommunicate 서로 설정합니다.
- 온-프레미스에서 호스트되는 Active Directory 및 DNS는 ExpressRoute를 통해 온-프레미스에서 Azure로 확장됩니다.


> [!NOTE] 
> 결제 관점에서 Azure 구독이 하나만 tooone 단일 테 넌 트 특정 Azure 지역에서 대형 인스턴스 스탬프에 연결할 수 하며 반대로 단일 인스턴스가 큰 스탬프 테 넌 연결할 수 있습니다 tooone Azure 구독. 이 팩트 다르지 tooany Azure의 다른 청구 가능 개체는

서로 다른 여러 Azure 지역에서 Azure (대형 인스턴스)에서 SAP HANA 배포, 별도 테 넌 트 toobe에 결과에 배포 된 hello 큰 인스턴스 스탬프. 그러나 hello에서 모두 실행할 수 있습니다 이러한 인스턴스는 hello 부분이 있다면 동일한 Azure 구독 동일한 SAP 지형이 합니다. 

> [!IMPORTANT] 
> Azure(큰 인스턴스)의 SAP HANA에서는 Azure Resource Management 배포만 지원됩니다.

 

### <a name="additional-azure-vnet-information"></a>Azure VNet 추가 정보

순서 tooconnect Azure VNet tooExpressRoute Azure 게이트웨이 만들어야 (참조 [ExpressRoute에 대 한 가상 네트워크 게이트웨이에 대 한](../../../expressroute/expressroute-about-virtual-network-gateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Azure 게이트웨이 사용할 수 있습니다 ExpressRoute tooan 인프라 외부에서 Azure (또는 tooan Azure 큰 인스턴스 스탬프)을 사용 하 여 또는 Azure Vnet 간의 tooconnect (참조 [PowerShell을 사용 하 여 리소스 관리자에 대 한 VNet 대 VNet 연결 구성 ](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). 이러한 연결은 서로 다른 MS 엔터프라이즈 가장자리 (MSEE) 라우터에서 들어오는으로 hello Azure 게이트웨이 tooa 최대 4 개의 다른 ExpressRoute 연결을 연결할 수 있습니다.  자세한 내용은 [Azure의 SAP HANA(큰 인스턴스) 인프라 및 연결](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요. 

> [!NOTE] 
> hello Azure 게이트웨이 제공 하는 처리량 차이가 있는 경우 둘 다 사용에 대 한 (참조 [에 대 한 VPN 게이트웨이](../../../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). hello 최대 처리량 낼 수 VNet 게이트웨이 통해 ExpressRoute 연결을 사용 하 여 10gbps입니다. 염두에서에 둬야는 Azure VNet 및 시스템에 있는 Azure VM 간에 파일을 복사 온-프레미스 (단일 복사본 스트림으로) hello 다른 게이트웨이 Sku의 hello 전체 처리량을 달성 하지 않습니다. hello VNet 게이트웨이 tooleverage hello의 전체 대역폭, 단일 파일의 병렬 스트림이 여러 스트림 또는 다른 파일 복사를 사용 해야 합니다.


### <a name="networking-architecture-for-hana-large-instances"></a>HANA 큰 인스턴스에 대한 네트워킹 아키텍처
아키텍처 HANA 큰 인스턴스에 대 한 네트워킹 hello 아래와 같이 분리할 때 4 개의 서로 다른 부분에:

- 온-프레미스 네트워킹 및 express 경로 연결 tooAzure 합니다. 이 부분은 hello 고객 도메인 및 ExpressRoute 통해 연결 된 tooAzure입니다. Hello 아래 hello 그래픽의 오른쪽 아래에 hello 부분입니다.
- Azure 네트워킹은 위에서 간단히 설명한 것처럼 Azure Vnet과 함께 다시 게이트웨이를 갖습니다. 응용 프로그램 요구 사항, 보안 및 규정 준수 요구 사항에 대 한 toofind hello에 대 한 적절 한 디자인을 해야 하는 영역입니다. HANA 큰 인스턴스를 사용 하는 다른 지점에서 Vnet 및 Azure 게이트웨이 Sku toochoose 수 측면에서 고려 사항입니다. Hello hello 그래픽의 오른쪽 위에 있는 hello 부분입니다.
- HANA 큰 인스턴스를 ExpressRoute 기술을 통해 Azure에 연결. 이 부분은 Microsoft에서 배포하고 처리합니다. Azure VNet(s) toohello 하기만 하면 toodo 고객은 tooprovide 일부 IP 주소 범위 및 HANA 큰 인스턴스 연결에 해당 자산의 hello 배포 후 hello ExpressRoute 회로 (참조 [SAP HANA (대형 인스턴스) 인프라 및 Azure에서 연결](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). 
- 고객에게 대부분 투명한 HANA 큰 인스턴스의 네트워킹.

![Azure VNet tooSAP HANA (대형 인스턴스)를 Azure와 온-프레미스에 연결](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

HANA 큰 인스턴스를 사용 하는 hello 팩트 hello 요구 사항 tooget tooAzure ExpressRoute 통해 연결 된 온-프레미스 자산을 변경 하지 않습니다. 하나 또는 여러 Vnet hello Azure Vm 인스턴스가 HANA 큰 단위에서 호스팅되는 toohello HANA 인스턴스를 연결 하는 호스트 hello 응용 프로그램 계층을 실행 하는 것에 대 한 hello 요구 사항을 변경 되지 않습니다. 

hello 팩트와 순수 hello 차이 tooSAP 배포 Azure에서 제공 하는:

- 고객 테 넌 트의 hello HANA 큰 인스턴스 단위는 Azure VNet(s)에 다른 ExpressRoute 회로 통해 연결 됩니다. Vnet ExpressRoute 링크와 Azure Vnet 및 HANA 큰 인스턴스 간의 링크를 공유 하지 않으므로 hello 온-프레미스 tooAzure hello 동일한 순서 tooseparate 부하 조건에서 라우터 합니다.
- hello SAP 응용 프로그램 계층 및 hello HANA 인스턴스 간에 작업 부하 프로필 hello은 많은 작은 요청의 다른 특성 및 데이터와 마찬가지로 버스트에서에서 전송 된 (결과 집합 지원) SAP HANA hello 응용 프로그램 계층에 있습니다.
- hello SAP 응용 프로그램 아키텍처에는 온-프레미스와 Azure 간에 데이터가 교환 가져옵니다 있는 일반적인 시나리오 보다 더 중요 한 toonetwork 대기 시간입니다.
- hello VNet 게이트웨이 두 개 이상의 ExpressRoute 연결 있으며 두 연결 hello hello VNet 게이트웨이의 들어오는 데이터에 대 한 최대 대역폭을 공유 합니다.

Azure Vm 및 HANA 큰 인스턴스 단위 간의 숙련 된 hello 네트워크 대기 시간 일반적인-VM 네트워크 왕복 대기 시간 보다 클 수 있습니다. Hello Azure 지역에 종속, 측정 hello 값을 초과할 수 있습니다에 대 한 평균 미달로 분류 된 hello 0.7 ms 왕복 지연이 [SAP 참고 #1100926 FAQ: 네트워크 성능을](https://launchpad.support.sap.com/#/notes/1100926/E)합니다. 그럼에도 고객들은 SAP HANA 기반 프로덕션 SAP 응용 프로그램을 SAP HANA 큰 인스턴스에서 매우 성공적으로 배포했습니다. 크게 향상 HANA 인스턴스가 큰 단위를 사용 하 여 SAP HANA에서의 SAP 응용 프로그램을 실행 하 여 보고 하는 hello 고객에 게 배포 합니다. 그렇더라도 사용자는 자신의 비지니스 프로세스를 Azure HANA 큰 인스턴스에서 철저하게 테스트해야 합니다.
 
순서 tooprovide 결정적 사이의 네트워크 대기 시간 Azure Vm 및 HANA 큰 인스턴스, Azure VNet 게이트웨이 SKU hello hello 선택이 중요 합니다. 온-프레미스와 Azure Vm 간의 트래픽 패턴 hello와 달리 Azure Vm 및 HANA 큰 인스턴스 간의 트래픽 패턴 hello 높은 하지만 크기가 작은 요청 및 전송 된 데이터 볼륨 toobe 버스트를 개발할 수 있습니다. 순서 toohave 잘 처리 이러한 버스트 좋습니다 hello UltraPerformance 게이트웨이 SKU의 hello 사용을 합니다. Hello HANA 큰 인스턴스 Sku의 Type II 클래스에 대 한 hello UltraPerformance 게이트웨이 SKU Azure VNet 게이트웨이로 hello 사용은 필수입니다.  

> [!IMPORTANT] 
> Hello 지정한 hello SAP 응용 프로그램 및 데이터베이스 계층 간에 전체 네트워크 트래픽만 hello HighPerformance 또는 UltraPerformance 게이트웨이 Vnet에 대 한 Sku tooSAP HANA Azure (대형 인스턴스)에 연결 하기 위해 지원 됩니다. HANA 큰 인스턴스 유형 II Sku, Azure VNet 게이트웨이로 hello UltraPerformance 게이트웨이 SKU만 지원 됩니다.



### <a name="single-sap-system"></a>단일 SAP 시스템

위에 표시 된 hello 온-프레미스 인프라에 Azure ExpressRoute를 통해 연결 되어 있고 hello ExpressRoute 회로에 Microsoft Enterprise Edge Router (MSEE) 연결 (참조 [express 경로 기술 개요](../../../expressroute/expressroute-introduction.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). 설정, 해당 경로에 연결 되는 Microsoft Azure hello backbone 하 고 액세스할 수 있는 모든 Azure 지역.

> [!NOTE] 
> Azure에서 SAP 지형을 실행 toohello MSEE 가장 가까운 toohello hello SAP 지형에 Azure 지역에 연결 합니다. Azure의 큰 인스턴스 스탬프가 전용된 MSEE 장치 toominimize 사이의 네트워크 대기 시간 Azure Vm에 Azure IaaS 또는 대형 인스턴스 스탬프가 통해 연결 됩니다.

hello VNet 게이트웨이 hello SAP 응용 프로그램 인스턴스를 호스트 하는 Azure Vm에 대 한 연결 된 toothat ExpressRoute 회로 이며 hello 동일한 VNet 연결된 tooa 별도 전용 MSEE 라우터 tooconnecting tooLarge 인스턴스 스탬프입니다.

여기서 hello SAP 응용 프로그램 계층은 Azure에서 호스트 하 고 hello SAP HANA 데이터베이스에서 Azure (대형 인스턴스)에서 SAP HANA 실행 단일 SAP 시스템의 간단한 예입니다. hello 된다고 가정해 2gbps의 hello VNet 게이트웨이 대역폭 또는 10 g b p s 처리량 병목을 나타내지 않습니다.

### <a name="multiple-sap-systems-or-large-sap-systems"></a>여러 SAP 시스템 또는 큰 SAP 시스템

여러 SAP 시스템 또는 대형 SAP 시스템 연결 tooSAP HANA Azure (대형 인스턴스), &#39;에 배포 하는 경우의 hello VNet 게이트웨이 s 합리적인 tooassume hello 처리량 병목 상태가 될 수 있습니다. 이 경우 여러 Azure Vnet으로 toosplit hello 응용 프로그램 계층 필요 합니다. 또한 것이 좋습니다 toocreate 수도 같은 경우에 대해 tooHANA 큰 인스턴스를 연결 하는 특별 한 Vnet:

- NFS 공유를 백업 수행 hello HANA 인스턴스에서 직접 HANA 큰 인스턴스 tooa Azure에서 VM에서에서 호스팅하는
- Azure에서 관리 되는 HANA 큰 인스턴스 단위 toodisk 공간에서 큰 백업 또는 다른 파일을 복사 합니다.

큰 파일을 여는 영향을 방지 하는 hello 저장소를 관리 하는 Vm 호스트 또는 데이터 전송 HANA 큰 인스턴스 tooAzure hello hello SAP 응용 프로그램 계층을 실행 하는 hello Vm 역할는 VNet 게이트웨이의 별도 Vnet을 사용 합니다. 

확장성 있는 네트워크 아키텍처를 위해서는 다음과 같이 합니다.

- 단일의 더 큰 SAP 응용 프로그램 계층에 여러 Azure VNet을 활용합니다.
- 각 배포 된 SAP 시스템을 비교 toocombining에 대 한 별도 Azure VNet을 하나의 배포에서 별도 서브넷에 SAP 시스템에 이러한 동일한 VNet hello 합니다.

 Azure(큰 인스턴스)에서 SAP HANA에 대한 보다 확장성 있는 네트워킹 아키텍처

![여러 Azure VNet에 걸쳐 SAP 응용 프로그램 계층 배포](./media/hana-overview-architecture/image4-networking-architecture.png)

해당 Azure Vnet에서 호스팅되는 hello 응용 프로그램 간 통신 중에 발생 한 대기 시간 불가피 한 오버 헤드를 도입 위에 표시 된 대로 여러 Azure Vnet를 통해 hello SAP 응용 프로그램 계층 또는 구성 요소를 배포 합니다. 기본적으로 Azure Vm 간의 네트워크 트래픽을 hello에 hello 통해 다른 Vnet 경로 MSEE 라우터가 구성에서 합니다. 그러나 2016년 9월부터 이 라우팅은 최적화될 수 있습니다. 방법은 toooptimize hello 이며 hello 두 간의 통신 대기 시간을 마감 Vnet 의도적으로 hello 내에서 Azure Vnet 피어 링 동일한 지역입니다. 해당 VNet이 다른 구독에 있더라도 가능합니다. Azure VNet 피어 링을 두 개의 서로 다른 Azure Vnet에 Vm 간의 통신 hello 사용 하 여 통신할 수 있습니다 사용할 hello Azure 네트워크 backbone toodirectly 서로. 함으로써 보여 주는 유사한 대기 시간 hello Vm의 것에 마치 hello 동일한 VNet입니다. Hello Azure VNet 게이트웨이 통해 연결 된 IP 주소 범위를 주소 지정 트래픽은 통해 라우팅됩니다 반면 hello VNet의 개별 VNet 게이트웨이 hello 합니다. Hello 문서에 피어 링 Azure VNet에 대 한 내용을 확인할 수 있습니다 [VNet 피어 링](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)합니다.


### <a name="routing-in-azure"></a>Azure에서 라우팅

Azure(큰 인스턴스)의 SAP HANA에 대한 두 가지 중요한 네트워크 라우팅 고려 사항이 있습니다.

1. (대형 인스턴스) Azure에서 SAP HANA만 Azure Vm에서 전용 hello ExpressRoute 연결;에 액세스할 수 온-프레미스에서 직접. 일부 관리 클라이언트와 온-프레미스, SAP Solution Manager toohello SAP HANA 데이터베이스에 연결할 수 없습니다와 같은 직접 액세스를 필요로 하는 모든 응용 프로그램이 합니다.

2. SAP HANA Azure (대형 인스턴스) 단위에 할당 된 IP 주소가 hello 서버 IP 풀 주소에서 제출 하는 hello 고객으로 서 범위 (참조 [SAP HANA (대형 인스턴스) 인프라와 Azure에서 연결](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 세부 정보에 대 한).  이 IP 주소는 Azure hello를 통해 액세스할 수 있는 구독 및 Azure (대형 인스턴스)에서 Azure Vnet tooHANA 연결 되는 express 경로입니다. hello 해당 서버 IP 풀 주소 범위를 벗어났습니다. 할당 된 IP 주소 toohello 하드웨어 단위 직접 할당 된 아니며 NAT'ed 이것이 hello이이 솔루션의 첫 번째 배포에서 hello 경우 처럼 더 이상. 

> [!NOTE] 
> 에 tooconnect tooSAP HANA Azure (대형 인스턴스)에서 필요한는 _데이터 웨어하우스_ 시나리오에서는 응용 프로그램 및/또는 최종 사용자가 해야 하는 (실행 직접) tooconnect toohello SAP HANA 데이터베이스, 다른 네트워킹 구성 요소 여야 합니다 사용: 역방향 프록시 tooroute 데이터에서 tooand 합니다. 예를 들어 F5 BIG-IP, NGINX(Traffic Manager 포함)가 가상 방화벽/트래픽 라우팅 솔루션으로 Azure에 배포되어 있습니다.

### <a name="internet-connectivity-of-hana-large-instances"></a>HANA 큰 인스턴스의 인터넷 연결
HANA 큰 인스턴스에는 직접 인터넷 연결이 없습니다. 이 예를 들어 hello OS 공급 업체와 직접 hello OS 이미지를 등록 하려면 능력을 제한 합니다. 따라서 로컬 SLES SMT 서버 또는 RHEL 구독 관리자와 toowork 할 수 있습니다.

### <a name="data-encryption-between-azure-vms-and-hana-large-instances"></a>Azure VM 및 HANA 큰 인스턴스 간의 데이터 암호화
HANA 큰 인스턴스 및 Azure VM 간에 전송된 데이터는 암호화되지 않습니다. 그러나 HANA DBMS 측면 hello 및 JDBC/ODBC 기반 응용 프로그램 간의 hello 교환을 위해 트래픽 암호화를 사용할 수 있습니다. [SAP에서 제공하는 이 설명서](http://help-legacy.sap.com/saphelp_hanaplatform/helpdata/en/db/d3d887bb571014bf05ca887f897b99/content.htm?frameset=/en/dd/a2ae94bb571014a48fc3b22f8e919e/frameset.htm&current_toc=/en/de/ec02ebbb57101483bdf3194c301d2e/plain.htm&node_id=20&show_children=false)를 참조하세요.

### <a name="using-hana-large-instance-units-in-multiple-regions"></a>여러 지역에서 HANA 큰 인스턴스 단위 사용하기

재해 복구 외에도 여러 Azure 지역에서 다른 이유로 toodeploy (대형 인스턴스) Azure에서 SAP HANA를 할 수 있습니다. 각각 hello에 배포 된 hello Vm의 tooaccess HANA 큰 인스턴스 수도 있습니다 다른 Vnet hello 지역에 있습니다. Hello IP 주소 할당 toohello 다른 HANA 큰 인스턴스 단위 hello Azure Vnet (즉 해당 게이트웨이 toohello 인스턴스를 통해 직접 연결 된) 이상 전파 되지 않습니다, 있습니다 진다는 toohello 위에서 소개 VNet 디자인을 변경 하는:는 Azure VNet 게이트웨이 다른 MSEEs 부족 다른 4 개의 ExpressRoute 회로 처리할 수 있습니다 및 hello 큰 인스턴스 스탬프의 연결 된 tooone 각 VNet에는 다른 Azure 지역에 연결 된 toohello 큰 인스턴스 스탬프가 될 수 있습니다.

![Azure Vnet tooAzure 큰 인스턴스 스탬프 서로 다른 Azure 지역에 연결](./media/hana-overview-architecture/image8-multiple-regions.png)

위의 그림 hello 모두에서 서로 다른 Azure Vnet을 어떻게 hello 영역은 두 Azure 지역에 사용 되는 tooconnect tooSAP HANA Azure (대형 인스턴스)에 있는 연결 된 tootwo 다른 ExpressRoute 회로 합니다. 새로 도입 된 hello 연결은 hello 사각형 빨강 선입니다. 이러한 연결을 통해 hello에서 Azure Vnet, 해당 Vnet 중 하나에서 실행 하는 hello Vm 각각 액세스할 수 hello 두 지역에 배포 된 hello 다른 HANA 큰 인스턴스 단위입니다. 온-프레미스 toohello 두 Azure 지역;에서 express 경로 연결을 두 개 있다고 가정 위의 hello 그래픽에 표시 재해 복구의 이유로 권장 합니다.

> [!IMPORTANT] 
> 여러 ExpressRoute 회로 사용 하는 경우 AS 경로 앞에 추가 하 고 로컬 기본 설정 BGP 설정을 사용 하는 tooensure 트래픽 라우팅을 적절 한 이어야 합니다.


