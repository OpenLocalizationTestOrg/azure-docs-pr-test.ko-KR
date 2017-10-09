---
title: "빠른 시작: Azure Virtual Machines에서 단일 인스턴스 SAP HANA 수동 설치 | Microsoft Docs"
description: "Azure Virtual Machines에서 단일 인스턴스 SAP HANA를 수동으로 설치하기 위한 빠른 시작 가이드입니다."
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: c51a2a06-6e97-429b-a346-b433a785c9f0
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 57b58b8e07379eed5641f5f89d55b38f52c69e44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-manual-installation-of-single-instance-sap-hana-on-azure-vms"></a>빠른 시작: Azure VMs에서 단일 인스턴스 SAP HANA 수동 설치
## <a name="introduction"></a>소개
이 가이드는 SAP NetWeaver 7.5 및 SAP HANA 1.0 SP12를 수동으로 설치할 때 Azure VM(가상 컴퓨터)에서 단일 인스턴스 SAP HANA를 설정하는 데 유용합니다. 이 가이드의 초점은 hello Azure에서 SAP HANA 배포 켜져 있습니다. SAP 설명서를 대체하지는 않습니다. 

>[!Note]
>이 가이드에서는 Azure VM에 SAP HANA를 배포하는 방법에 대해 설명합니다. HANA 큰 인스턴스에 SAP HANA를 배포하는 방법에 대한 자세한 내용은 [Azure VM(가상 컴퓨터)에서 SAP 사용](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started)을 참조하세요.
 
## <a name="prerequisites"></a>필수 조건
여기서는 다음과 같은 IaaS(Infrastructure as a Service) 기본 사항에 대해 잘 알고 있다고 가정합니다.
 * 어떻게 toodeploy 가상 컴퓨터 또는 가상 네트워크를 통해 hello Azure 포털 또는 PowerShell입니다.
 * hello Azure 크로스 플랫폼 명령줄 인터페이스 (CLI) hello 옵션 toouse 개체 JSON (JavaScript Notation) 템플릿을 포함 하 합니다.

또한 다음에 대해서도 잘 알고 있다고 가정합니다.
* SAP HANA 및 SAP NetWeaver와 방법을 tooinstall 온 프레미스 합니다.
* Azure에서 SAP HANA 및 SAP 응용 프로그램 인스턴스 설치 및 조작
* 다음 개념 및 절차 hello:
   * Azure에서의 SAP 배포 계획(Azure Virtual Network 계획 및 Azure Storage 사용 포함) - [Azure VMs(Virtual Machines)에서 SAP NetWeaver - 계획 및 구현 가이드](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide) 참조
   * 배포 원리와 같은 방법으로 toodeploy Azure의 Vm입니다. [SAP용 Azure Virtual Machines 배포](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide) 참조
   * Azure의 SAP NetWeaver ASCS(ABAP SAP Central Services), SCS(SAP Central Services) 및 ERS(입고 기준 자동 정산)에 대한 고가용성 - [Azure VM에서 SAP NetWeaver에 대한 고가용성](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide) 참조
   * 자세한 방법은 tooimprove 효율성 ASCS/SCS Azure에서를 설치 하는 다중 SID를 활용 합니다. [SAP NetWeaver 다중 SID 구성 만들기](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid) 참조 
   * Azure에서 Linux 기반 VM에 기반한 SAP NetWeaver 실행 원칙 - [Microsoft Azure SUSE Linux VM에서 SAP NetWeaver 실행](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart) 참조. 이 가이드에서는 tooproperly Azure 저장소 디스크 tooLinux Vm을 연결 하는 방법에 Azure Vm 및 세부 정보에서 Linux에 대 한 특정 설정을 제공 합니다.

현재 Azure VM은 SAP HANA 강화 구성에 대해서만 SAP에서 인증되었습니다. SAP HANA 워크로드를 포함한 스케일 아웃 구성은 아직 지원되지 않습니다. 강화 구성 시의 SAP HANA 고가용성은 [Azure VMs(Virtual Machines)의 SAP HANA 고가용성](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability)을 참조하세요.

SAP HANA 인스턴스 또는 S/4HANA 또는 매우 빠른 시간에 배포 하는 BW/4HANA 시스템 tooget 찾고, 경우에 hello 사용을 고려해 야 [SAP 클라우드 어플라이언스에 라이브러리](http://cal.sap.com)합니다. 예를 들어 Azure에서 SAP CAL을 통해 S/4HANA 시스템을 배포하는 방법에 대한 설명서는 [이 가이드](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h)에서 찾을 수 있습니다. Azure 구독 및 SAP 클라우드 어플라이언스에 라이브러리와 함께 등록 될 수 있는 SAP 사용자 toohave 하면 됩니다.

## <a name="additional-resources"></a>추가 리소스
### <a name="sap-hana-backup"></a>SAP HANA 백업
Azure VM에서 SAP HANA 데이터베이스를 백업하는 방법에 대한 자세한 내용은 다음을 참조하세요.
* [Azure Virtual Machines의 SAP HANA 백업 가이드](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)
* [파일 수준의 SAP HANA Azure 백업](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level)
* [저장소 스냅숏에 기반한 SAP HANA 백업](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-storage-snapshots)

### <a name="sap-cloud-appliance-library"></a>SAP 클라우드 어플라이언스 라이브러리
SAP 클라우드 어플라이언스에 라이브러리 toodeploy S/4HANA 또는 BW/4HANA를 사용 하는 방법은 참조 하십시오. [SAP 배포 S/4HANA 또는 Microsoft Azure에서 BW/4HANA](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h)합니다.

### <a name="sap-hana-supported-operating-systems"></a>SAP HANA 지원 운영 체제
SAP HANA 지원 운영 체제에 대한 내용은 [SAP Support Note #2235581 - SAP HANA: 지원되는 운영 체제](https://launchpad.support.sap.com/#/notes/2235581/E)를 참조하세요. Azure VM은 이러한 운영 체제의 하위 집합만 지원합니다. hello 다음 운영 체제는 지원 되는 Azure에서 SAP HANA toodeploy: 

* SUSE Linux Enterprise Server 12.x
* Red Hat Enterprise Linux 7.2

SAP HANA 및 다른 Linux 운영 체제에 대한 SAP 추가 설명서는 다음을 참조하세요.

* [SAP Support Note #171356 – SAP Software on Linux: 일반 정보](https://launchpad.support.sap.com/#/notes/1984787)(영문)
* [SAP Support Note #1944799 – SLES 운영 체제 설치를 위한 SAP HANA 지침](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)(영문)
* [SAP Support Note #2205917 – SAP HANA DB: SLES 12 for SAP Applications를 위한 권장 OS 설정](https://launchpad.support.sap.com/#/notes/2205917/E)(영문)
* [SAP Support Note #1984787 – SUSE Linux Enterprise Server 12: 설치 참고](https://launchpad.support.sap.com/#/notes/1984787)(영문)
* [SAP Support Note #1391070 – Linux UUID 솔루션](https://launchpad.support.sap.com/#/notes/1391070)(영문)
* [SAP Support Note #2009879 – RHEL(Red Hat Enterprise Linux) 운영 체제에 대한 SAP HANA 지침](https://launchpad.support.sap.com/#/notes/2009879)
* [2292690 - SAP HANA DB: RHEL 7에 대한 권장 OS 설정](https://launchpad.support.sap.com/#/notes/2292690/E)

### <a name="sap-monitoring-in-azure"></a>Azure에서 SAP 모니터링
Azure에서 SAP를 모니터링하는 방법에 대한 내용은 다음을 참조하세요.

* [SAP Note 2191498](https://launchpad.support.sap.com/#/notes/2191498/E)(영문) - Azure에서 Linux VM을 사용한 SAP "고급 모니터링"에 대해 설명합니다. 
* [SAP Note 1102124](https://launchpad.support.sap.com/#/notes/1102124/E)(영문) - SAPOSCOL on Linux에 대해 설명합니다. 
* [SAP Note 2178632](https://launchpad.support.sap.com/#/notes/2178632/E)(영문) - Microsoft Azure의 SAP용 주요 모니터링 메트릭에 대해 설명합니다.

### <a name="azure-vm-types"></a>Azure VM 유형
SAP HANA와 함께 사용되는 Azure VM 유형 및 SAP 지원 워크로드 시나리오는 [SAP 인증 IaaS 플랫폼](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html)(영문)에서 설명하고 있습니다. 

SAP NetWeaver 용 SAP에 의해 인증 또는 S/4HANA 응용 프로그램 계층 환영 하 여 azure VM 유형을에 문서화 된 [SAP 참고 1928533-Azure의 SAP 응용 프로그램: 제품 지원 및 Azure VM 유형](https://launchpad.support.sap.com/#/notes/1928533/E)합니다.

>[!Note]
>SAP-Linux-Azure 통합은 Azure 리소스 관리자 및 하지 hello 클래식 배포 모델에 대해서만 지원 됩니다. 

## <a name="manual-installation-of-sap-hana"></a>SAP HANA 수동 설치
이 가이드에서는 toomanually 설치 어떻게 SAP HANA Azure Vm에서 두 가지 방법으로 설명 합니다.

* Hello "데이터베이스 인스턴스를 설치" 단계에서 분산된 NetWeaver 설치의 일환으로 SAP 소프트웨어 배포 관리자 SWPM ()를 사용 하 여
* SAP HANA hello를 사용 하 여 데이터베이스 수명 주기 관리자 도구, HDBLCM, 및 다음 NetWeaver 설치

사용할 수도 있습니다 SWPM tooinstall 하나의 단일 VM의 모든 구성 요소 (SAP HANA, hello SAP 응용 프로그램 서버 및 hello ASCS 인스턴스)에 설명 된 대로 [SAP HANA 블로그 알림을](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/)합니다. 이 옵션이 빠른 시작 가이드에 설명 되지 않습니다 되지만 고려해 야 하는 문제는 hello hello 동일 합니다.

설치를 시작 하기 전에 hello를 읽는 것이 좋습니다 "준비 Azure Vm에 대 한 SAP HANA의 수동 설치"이이 가이드의 뒷부분에 나오는 섹션. 이렇게 하면 기본 Azure VM 구성만 사용할 때 발생할 수 있는 몇 가지 기본적인 실수를 방지할 수 있습니다.

## <a name="key-steps-for-sap-hana-installation-when-you-use-sap-swpm"></a>SAP SWPM 사용 시 SAP HANA 설치를 위한 주요 단계
이 섹션 SAP SWPM tooperform 분산된 SAP NetWeaver 7.5 설치를 사용 하는 경우 수동, 단일 인스턴스 SAP HANA 설치에 대 한 hello 주요 단계를 나열 합니다. hello 개별 단계는이 가이드의 뒷부분에 나오는 스크린 샷에 보다 자세히 설명 되어 있습니다.

1. 2개 테스트 VM이 포함된 Azure 가상 네트워크를 만듭니다.
2. Toohello Azure 리소스 관리자 모델에 따라 두 hello Azure Vm (이 예제에서 SUSE Linux Enterprise Server (SLES) 및 SAP 응용 프로그램 12 s p 1 용 SLES), 운영 체제를 배포 합니다.
3. 두 Azure 표준 또는 프리미엄 저장소 디스크 (예를 들어 75 GB 또는 500GB 디스크) toohello 응용 프로그램 서버 VM에 연결 합니다.
4. 프리미엄 저장소 디스크 toohello HANA DB 서버 VM을 연결 합니다. 자세한 내용은이 가이드의 뒷부분에 나오는 hello "디스크 설치" 섹션을 참조 합니다.
5. 크기 또는 처리량 요구 사항에 따라 여러 디스크를 추가 하 고 hello OS 수준 hello VM 내에서 논리 볼륨 관리 또는 다중 장치 관리 도구 (MDADM)를 사용 하 여 스트라이프 볼륨을 만듭니다.
6. 연결 된 hello 디스크나 논리 볼륨에 XFS 파일 시스템을 만듭니다.
7. Hello 운영 체제 수준에서 hello 새 XFS 파일 시스템을 탑재 합니다. 모든 hello SAP 소프트웨어에 대해 하나의 파일 시스템을 사용 합니다. 사용 예를 들어 hello /sapmnt 디렉터리 및 백업에 대 한 다른 파일 시스템을 hello 합니다. SAP HANA DB 서버 hello에 /hana 및 /usr/sap hello 프리미엄 저장소 디스크에 hello XFS 파일 시스템을 탑재 합니다. 이 프로세스는 필요한 tooprevent hello 루트 파일 시스템을 채워지지 않도록 Linux Azure Vm에서 큰 되지 않습니다.
8. Hello/등/호스트 파일에 hello hello 테스트 Vm의 로컬 IP 주소를 입력 합니다.
9. Hello 입력 **nofail** hello/등/fstab 파일에서 매개 변수입니다.
10. 사용 중인 toohello Linux 운영 체제 버전에 따라 Linux 커널 매개 변수를 설정 합니다. 자세한 내용은 HANA 및 hello이이 가이드의 "커널 매개 변수" 섹션을 설명 하는 hello 적절 한 SAP 메모를 참조 하세요.
11. 교환 공간 추가
12. 필요에 따라 hello 테스트 Vm에는 그래픽 데스크톱을 설치 합니다. 그렇지 않은 경우 원격 SAPinst 설치 사용
13. SAP Service Marketplace hello에서 hello SAP 소프트웨어를 다운로드 합니다.
14. Hello 응용 프로그램 서버 VM에서 hello SAP ASCS 인스턴스를 설치 합니다.
15. Hello 간에 공유 hello /sapmnt 디렉터리 NFS를 사용 하 여 Vm을 테스트 합니다. hello 응용 프로그램 서버 VM는 hello NFS 서버입니다.
16. HANA를 포함 하 여 hello DB 서버 VM SWPM 사용 하 여 hello 데이터베이스 인스턴스를 설치 합니다.
17. Hello 응용 프로그램 서버 VM에 hello 기본 응용 프로그램 서버 (PA)를 설치 합니다.
18. SAP MC(SAP 관리 콘솔)를 시작합니다. 예를 들어 SAP GUI 또는 HANA Studio와 연결합니다.

## <a name="key-steps-for-sap-hana-installation-when-you-use-hdblcm"></a>HDBLCM 사용 시 SAP HANA 설치를 위한 주요 단계
이 섹션 SAP HDBLCM tooperform 분산된 SAP NetWeaver 7.5 설치를 사용 하는 경우 수동, 단일 인스턴스 SAP HANA 설치에 대 한 hello 주요 단계를 나열 합니다. hello 개별 단계는이 가이드 전체에서 스크린에 보다 자세히 설명 되어 있습니다.

1. 2개 테스트 VM이 포함된 Azure 가상 네트워크를 만듭니다.
2. 운영 체제 (이 예제에서 SLES 및 SAP 응용 프로그램 12 s p 1 용 SLES)와 두 개의 Azure Vm 배포 toohello Azure 리소스 관리자 모델에 따라 합니다.
3. 두 Azure 표준 또는 프리미엄 저장소 디스크 (예를 들어 75 GB 또는 500GB 디스크) toohello 응용 프로그램 서버 VM에 연결 합니다.
4. 프리미엄 저장소 디스크 toohello HANA DB 서버 VM을 연결 합니다. 자세한 내용은이 가이드의 뒷부분에 나오는 hello "디스크 설치" 섹션을 참조 합니다.
5. 크기 또는 처리량 요구 사항에 따라 여러 디스크를 추가 하 고 hello OS 수준 hello VM 내에서 논리 볼륨 관리 또는 다중 장치 관리 도구 (MDADM)를 사용 하 여 스트라이프 볼륨을 만듭니다.
6. 연결 된 hello 디스크나 논리 볼륨에 XFS 파일 시스템을 만듭니다.
7. Hello 운영 체제 수준에서 hello 새 XFS 파일 시스템을 탑재 합니다. 사용 예를 들어 hello /sapmnt 디렉터리 및 백업을 위한 hello 및 모든 hello SAP 소프트웨어에 대해 하나의 파일 시스템을 사용 합니다. SAP HANA DB 서버 hello에 /hana 및 /usr/sap hello 프리미엄 저장소 디스크에 hello XFS 파일 시스템을 탑재 합니다. 이 프로세스는 필요한 toohelp 채워지지 않도록 Linux Azure Vm에서 큰 없는 hello 루트 파일 시스템을 방지 합니다.
8. Hello/등/호스트 파일에 hello hello 테스트 Vm의 로컬 IP 주소를 입력 합니다.
9. Hello 입력 **nofail** hello/등/fstab 파일에서 매개 변수입니다.
10. 사용 중인 toohello Linux 운영 체제 버전에 따라 커널 매개 변수를 설정 합니다. 자세한 내용은 HANA 및 hello이이 가이드의 "커널 매개 변수" 섹션을 설명 하는 hello 적절 한 SAP 메모를 참조 하세요.
11. 교환 공간 추가
12. 필요에 따라 hello 테스트 Vm에는 그래픽 데스크톱을 설치 합니다. 그렇지 않은 경우 원격 SAPinst 설치 사용
13. SAP Service Marketplace hello에서 hello SAP 소프트웨어를 다운로드 합니다.
14. ID 1001 hello HANA DB 서버 VM의 그룹으로 sapsys, 그룹을 만듭니다.
15. HANA 데이터베이스 수명 주기 관리자 (HDBLCM)를 사용 하 여 hello DB 서버 VM에서 SAP HANA를 설치 합니다.
16. Hello 응용 프로그램 서버 VM에서 hello SAP ASCS 인스턴스를 설치 합니다.
17. Hello 간에 공유 hello /sapmnt 디렉터리 NFS를 사용 하 여 Vm을 테스트 합니다. hello 응용 프로그램 서버 VM는 hello NFS 서버입니다.
18. HANA를 포함 하 여 hello HANA DB 서버 VM SWPM 사용 하 여 hello 데이터베이스 인스턴스를 설치 합니다.
19. Hello 응용 프로그램 서버 VM에 hello 기본 응용 프로그램 서버 (PA)를 설치 합니다.
20. SAP MC를 시작합니다. SAP GUI 또는 HANA Studio를 통해 연결합니다.

## <a name="preparing-azure-vms-for-a-manual-installation-of-sap-hana"></a>SAP HANA 수동 설치를 위한 Azure VM 준비
이 섹션에서는 hello 다음 항목을 다룹니다.

* OS 업데이트
* 디스크 설정
* 커널 매개 변수
* 파일 시스템
* hello/등/호스트 파일
* hello/등/fstab 파일

### <a name="os-updates"></a>OS 업데이트
추가 소프트웨어를 설치하기 전에 먼저 Linux OS 업데이트 및 픽스가 있는지 확인합니다. 패치를 설치 하 여 수 tooavoid 호출 toohello 지원 센터 수도 있습니다.

다음을 사용하고 있는지 확인합니다.
* SUSE Linux Enterprise Server for SAP Applications
* Red Hat Enterprise Linux for SAP Applications 또는 Red Hat Enterprise Linux for SAP HANA 

아직 하지 않는 경우 hello OS 배포 hello Linux 공급 업체에서 Linux 구독에 등록 합니다. SUSE에는 이미 서비스를 포함하고 있고 자동으로 등록되는 SAP 응용 프로그램용 OS 이미지가 있습니다.

Hello를 사용 하 여 사용 가능한 패치 SUSE Linux에 대 한 확인 하는 예로 **zypper** 명령:

 `sudo zypper list-patches`

Hello에 따라 문제를 패치 범주 및 심각도 별로 분류 됩니다. 범주에 일반적으로 사용되는 값은 **security**, **recommended**, **optional**, **feature**, **document** 또는 **yast**입니다.
심각도에 일반적으로 사용되는 값은 **critical**, **important**, **moderate**, **low** 또는 **unspecified**입니다.

hello **zypper** 명령은 설치 된 패키지에 필요한 업데이트도 hello에 대 한만 찾습니다. 예를 들어 다음 명령은 사용할 수 있습니다.

`sudo zypper patch  --category=security,recommended --severity=critical,important`

Hello 매개 변수를 추가할 수 `--dry-run` 실제로 hello 시스템을 업데이트 하지 않고 tootest hello 업데이트 합니다.


### <a name="disk-setup"></a>디스크 설정
hello 루트 파일 시스템을 Azure에서 Linux VM의 크기 제한이 있습니다. 따라서 SAP를 실행 하는 데 필요한 tooattach 추가 디스크 공간 tooan Azure VM은. SAP 응용 프로그램 서버 Azure Vm에 대 한 표준 저장소를 Azure 디스크가 hello 사용 충분할 수 있습니다. 그러나 SAP HANA DBMS Azure Vm에 대 한 프로덕션 및 비프로덕션 구현에 대 한 Azure 프리미엄 저장소 디스크의 hello 사용은 필수입니다.

Hello에 따라 [SAP HANA TDI 저장소 요구 사항을](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html), 같은 Azure 프리미엄 저장소 구성이 hello 제안 됩니다. 

| VM SKU | RAM |  /hana/data 및 /hana/log <br /> (LVM 또는 MDADM으로 스트라이프됨) | /hana/shared | /root 볼륨 | /usr/sap |
| --- | --- | --- | --- | --- | --- |
| GS5 | 448GB | 2 x P30 | 1 x P20 | 1 x P10 | 1 x P10 | 

Hello 제안 된 디스크 구성에서 hello HANA 데이터 볼륨 및 로그 볼륨 hello LVM 또는 MDADM 스트라이프 Azure 프리미엄 저장소 디스크의 동일한 집합에 배치 됩니다. Azure 프리미엄 저장소에서는 hello에 대 한 디스크 중복 이미지가 3 개 유지 하므로 중복 RAID 수준 필요한 toodefine 않습니다. 충분 한 저장소를 구성 해야 toomake hello를 참조 하십시오. [SAP HANA TDI 저장소 요구 사항을](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) 및 [SAP HANA 서버 설치 및 업데이트 가이드](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm)합니다. 또한에 설명 된 대로 다른 Azure 프리미엄 저장소 디스크 hello 양의 다른 가상 하드 디스크 (VHD) 처리량 hello를 고려 [고성능 프리미엄 저장소 및 Vm에 대 한 관리 되는 디스크](https://docs.microsoft.com/azure/storage/storage-premium-storage)합니다. 

데이터베이스 또는 트랜잭션 로그 백업을 저장 하기 위한 toohello HANA DBMS Vm 디스크를 프리미엄 저장소를 더 추가할 수 있습니다.

Hello 사용 되는 두 가지 주요 도구 tooconfigure 스트라이프 하는 방법에 대 한 자세한 내용은 다음 문서는 hello 참조:

* [Linux에서 소프트웨어 RAID 구성](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure에서 Linux VM에 LVM 구성](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

연결에 대 한 자세한 내용은 게스트 OS로 Linux를 실행 하는 tooAzure Vm 디스크, 참조 [디스크 tooa Linux VM 추가](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

Azure 프리미엄 저장소 toodefine 디스크를 모드 캐싱 있습니다. /Hana/data 및 /hana/log 보유 hello 스트라이프 세트에 대 한 디스크 캐싱이 해제 되어야 합니다. Hello 다른 볼륨 (디스크) hello caching에 대 한 모드 설정할지 너무**ReadOnly**합니다.

자세한 내용은 [Premium Storage: Azure Virtual Machine 워크로드를 위한 고성능 저장소](../../../storage/common/storage-premium-storage.md)를 참조하세요.

Vm을 만들기 위한 샘플 JSON 템플릿이 toofind 너무 이동[Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates)합니다.
hello vm-단순-sles 서식 파일은 기본 템플릿입니다. 여기에는 100GB 추가 데이터 디스크가 포함된 저장소 섹션이 있습니다. 이 템플릿을 기반으로 사용할 수 있습니다. Hello 템플릿 tooyour 특정 구성을 적용할 수도 있습니다.

>[!Note]
>에 설명 된 대로 UUID를 사용 하 여 중요 한 tooattach hello Azure 저장소 디스크를은 [Microsoft Azure SUSE Linux Vm에서의 SAP NetWeaver 실행](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

Hello 테스트 환경에서 두 개의 Azure 표준 저장소 디스크 24 개가 hello 스크린 샷 뒤에 표시 된 대로 연결 된 toohello SAP 응용 프로그램 서버 VM을 했습니다. 설치에 대 한 모든 hello SAP 소프트웨어 (NetWeaver 7.5, SAP GUI 및 SAP HANA 포함)를 저장 하는 하나의 디스크. 두 번째 디스크 hello 추가 요구 사항 (예: 백업 및 테스트 데이터)을 사용할 수 있는 공간이 충분 하 고 동일한 SAP 지형이 hello /sapmnt 디렉터리 (즉, SAP 프로필) toobe toohello 속해 있는 모든 Vm 간에 공유에 대 한 보장 됩니다.

![2개 데이터 디스크 및 해당 크기를 보여 주는 SAP HANA 앱 서버 디스크 창](./media/hana-get-started/image003.jpg)


### <a name="kernel-parameters"></a>커널 매개 변수
SAP HANA hello 표준 Azure 갤러리 이미지의 일부분이 아닌 및 수동으로 설정 해야 하는 특정 Linux 커널 설정 해야 합니다. 사용 하는지에 따라 SUSE 또는 Red Hat, hello 매개 변수는 달라질 수 있습니다. hello SAP Note 앞에 나열 된 해당 매개 변수에 대 한 정보가 표시 됩니다. 표시 된 hello 스크린샷에서 SUSE Linux 12 s p 1이 사용 되었습니다. 

SAP 응용 프로그램 12 GA에 대 한 SLES 및 SLES SAP 응용 프로그램 12 s p 1에 대 한 새로운 도구는 **튜닝 adm**, 대체 hello 이전 **sapconf** 도구입니다. **tuned-adm**에 대한 특별한 SAP HANA 프로필을 사용할 수 있습니다. SAP HANA에 대해 tootune hello 시스템 루트 사용자로 hello 다음을 입력 합니다.

   `tuned-adm profile sap-hana`

에 대 한 자세한 내용은 **튜닝 adm**, hello 참조 [adm 튜닝에 대 한 설명서 SUSE](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip)합니다.

다음 스크린 샷 hello에서 볼 수 있습니다 어떻게 **튜닝 adm** 변경 된 hello `transparent_hugepage` 및 `numa_balancing` toohello에 따라 값을 필요한 SAP HANA 설정 합니다.

![toorequired SAP HANA 설정에 따라 값을 변경 하는 hello adm 튜닝 도구](./media/hana-get-started/image005.jpg)

영구적으로 적용 toomake hello SAP HANA 커널 설정을 사용 하 여 **grub2** SLES 12에 있습니다. 에 대 한 자세한 내용은 **grub2**, toohello 이동 [구성 파일 구조](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) hello SUSE 설명서의 섹션입니다.

hello 다음 스크린샷은 hello 커널 설정이 된 hello 구성 파일에서 변경 하 고 사용 하 여 컴파일된 다음 하는 방법을 **grub2 mkconfig**:

![커널 설정을 hello 구성 파일에서 변경 하 고 grub2 mkconfig를 사용 하 여 컴파일된](./media/hana-get-started/image006.jpg)

두 번째 방법은 toochange hello 설정을 YaST 및 hello를 사용 하 여 **부트 로더** > **커널 매개 변수** 설정:

![YaST 부트 로더의 hello 커널 매개 변수 설정 탭](./media/hana-get-started/image007.jpg)

### <a name="file-systems"></a>파일 시스템
hello 다음 스크린샷은 hello 두 개의 연결 된 Azure 표준 저장소 디스크를 기반으로 hello SAP 응용 프로그램 서버 VM에서 생성 된 두 개의 파일 시스템이 있습니다. 두 파일 시스템은 유형이 XFS 고 탑재 된 너무/sapdata 및 /sapsoftware 합니다.

것은 필수는 아니지만 toostructure 이러한 방식으로 파일 시스템입니다. Hello 디스크 공간 구성에 대 한 다른 옵션이 있습니다. hello 가장 중요 한 고려 사항은 tooprevent hello 루트 파일 시스템에서 사용 가능한 공간 부족입니다.

![Hello SAP 응용 프로그램 서버 VM에서 생성 하는 두 개의 파일 시스템](./media/hana-get-started/image008.jpg)

SAP HANA DB VM SAPinst SWPM ()를 사용 하는 경우 데이터베이스 설치 하는 동안 hello 및 hello에 대 한 **일반적인** 설치 옵션을 /hana 및 /usr/sap에서 모든 항목을 설치 합니다. hello SAP HANA 로그 백업에 대 한 hello 기본 위치에서 /usr/sap입니다. 다시, 중요 한 tooprevent hello 루트 파일 시스템의 저장소 공간이 부족에서 이기 때문에 충분 한 여유 공간이 있는지 /hana 및 /usr/sap SWPM를 사용 하 여 SAP HANA를 설치 하기 전에 있는지 확인 합니다.

SAP HANA의 표준 파일 시스템 레이아웃 hello에 대 한 참조 hello [SAP HANA 서버 설치 및 업데이트 가이드](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm)합니다.

![Hello SAP 응용 프로그램 서버 VM에서 만든 추가 파일 시스템](./media/hana-get-started/image009.jpg)

SAP 응용 프로그램 12 Azure 갤러리 이미지에 대 한 표준 SLES/SLES에 SAP NetWeaver를 설치할 때 hello 스크린 샷 뒤에 표시 된 대로 스왑 공간이 라는 메시지가 표시 됩니다. toodismiss이 메시지를 사용 하 여 스왑 파일을 수동으로 추가할 수 있습니다 **dd**, **mkswap**, 및 **swapon**합니다. 에 대 한 검색 방법, toolearn "hello에" 수동으로 스왑 파일 추가 [를 사용 하 여 hello YaST 파티 셔 너](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) hello SUSE 설명서의 섹션입니다.

두 번째 방법은 tooconfigure 스왑 공간 hello Linux VM 에이전트를 사용 하 여 합니다. 자세한 내용은 참조 hello [Azure Linux 에이전트 사용자 가이드](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

![교환 공간이 부족하다고 알리는 팝업 메시지](./media/hana-get-started/image010.jpg)


### <a name="hello-etchosts-file"></a>hello/등/호스트 파일
SAP tooinstall 시작 하기 전에 hello /etc/hosts 파일에 hello 호스트 이름 및 hello SAP Vm의 IP 주소를 포함 해야 합니다. 하나의 Azure 가상 네트워크 내에서 모든 hello SAP Vm을 배포 하 고 여기 표시 된 대로 다음 hello 내부 IP 주소를 사용 하 여:

![Hello /etc/hosts 파일에 나열 된 호스트 이름 및 hello SAP Vm의 IP 주소](./media/hana-get-started/image011.jpg)

### <a name="hello-etcfstab-file"></a>hello/등/fstab 파일

유용한 tooadd hello **nofail** 매개 변수 toohello fstab 파일입니다. 이러한 방식으로 hello 디스크에 문제가 발생 hello 부팅 프로세스에 hello VM 정지 하지 않습니다. 그러나 추가 디스크 공간을 사용할 수 있습니다 및 프로세스 hello 루트 파일 시스템을 가득 찰 수 있습니다. /hana가 누락되면 SAP HANA가 시작되지 않습니다.

![Hello nofail toohello fstab file 매개 변수를 추가 합니다.](./media/hana-get-started/image000c.jpg)

## <a name="graphical-gnome-desktop-on-sles-12sles-for-sap-applications-12"></a>SLES 12/SLES for SAP Applications 12의 그래픽 GNOME 데스크톱
이 섹션에서는 hello 다음 항목을 다룹니다.

* SAP 응용 프로그램 12 용 SLES 12/SLES hello GNOME 데스크톱과 xrdp 설치
* SLES 12/SLES for SAP Applications 12에서 Firefox를 사용하여 Java 기반 SAP MC 실행

Xterminal 또는 VNC와 같은 대안을 사용할 수도 있습니다(여기서는 설명하지 않음).

### <a name="installing-hello-gnome-desktop-and-xrdp-on-sles-12sles-for-sap-applications-12"></a>SAP 응용 프로그램 12 용 SLES 12/SLES hello GNOME 데스크톱과 xrdp 설치
Windows 배경을 설정한 경우 쉽게 hello Linux Vm의 SAP toorun Firefox, SAPinst, SAP GUI, SAP MC 또는 HANA Studio 내에서 직접 그래픽 데스크톱을 사용 하 고 연결할 수 toohello VM hello 프로토콜 RDP (원격 데스크톱)는 Windows 컴퓨터에서를 통해 합니다. 추가 대 한 회사 정책에 따라 달라 그래픽 사용자 인터페이스 tooproduction 및 비-프로덕션 Linux 기반 시스템, 서버에서 tooinstall GNOME 할 수 있습니다. SAP 응용 프로그램 12 VM에 대 한 Azure SLES 12/SLES에 tooinstall hello GNOME 데스크톱:

1. Hello 다음 (예를 들어 PuTTY 창)에서 명령을 입력 하 여 hello GNOME 데스크톱을 설치 합니다.

   `zypper in -t pattern gnome-basic`

2. Xrdp tooallow 연결 toohello RDP 통해 VM 설치 합니다.

   `zypper in xrdp`

3. /Etc/sysconfig/windowmanager, 편집 하 고 hello 기본 창 관리자 tooGNOME를 설정 합니다.

   `DEFAULT_WM="gnome"`

4. 실행 **chkconfig** toomake 해당 xrdp 다시 부팅 후 자동으로 시작 합니다.

   `chkconfig -level 3 xrdp on`

5. Hello RDP 연결에 문제가 있는 경우 (예: PuTTY 창)에서 toorestart 시도해 보십시오.

   `/etc/xrdp/xrdp.sh restart`

6. 단계가 작동 하지 않는 hello 이전에 언급 된 xrdp 다시 시작 되는,.pid 파일 확인.

   `check /var/run` 

   `xrdp.pid`를 찾아보세요. 를 찾을 경우 제거한 toorestart을 다시 시도 하십시오.

### <a name="starting-sap-mc"></a>SAP MC 시작
Hello GNOME 바탕 화면을 설치한 후 hello 그래픽 시작 SAP 응용 프로그램 12 VM에 대 한 Azure SLES 12/SLES에서 실행 하는 동안 Firefox에서 SAP MC Java 기반 표시 오류가 hello Java 브라우저 플러그 인을 누락으로 인해 됩니다.

SAP MC는 hello URL toostart hello `<server>:5<instance_number>13`합니다.

자세한 내용은 참조 [시작 hello SAP 관리 콘솔-웹 기반](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm)합니다.

hello 다음 스크린샷은 hello Java 브라우저 플러그 인 누락 된 경우 표시 되는 hello 오류 메시지:

![누락된 Java 브라우저 플러그 인을 나타내는 오류 메시지](./media/hana-get-started/image013.jpg)

한 가지 방법은 toosolve hello 문제는 hello 스크린 샷 뒤에 표시 된 대로 YaST를 사용 하 여 플러그 인 누락 tooinstall hello:

![YaST tooinstall 누락 플러그 인을 사용 하 여](./media/hana-get-started/image014.jpg)

Hello SAP 관리 콘솔 URL을 다시 입력 하면 메시지가 묻는 있습니다 tooactivate hello 플러그 인을 나타납니다.

![플러그 인 활성화를 요청하는 대화 상자](./media/hana-get-started/image015.jpg)

누락된 javafx.properties 파일에 대한 오류 메시지가 표시될 수도 있습니다. SAP GUI 7.4에 대 한 Oracle java 1.8 관련된 toohello 요구 사항입니다. ([SAP Note 2059429](https://launchpad.support.sap.com/#/notes/2059424) 참조) Hello IBM Java 버전도 아니고 SAP 응용 프로그램 12에 대 한 SLES/SLES 포함 된 hello openjdk 패키지 hello 필요한 javafx.properties 파일이 포함 됩니다. hello 솔루션 toodownload 이며 oracle에서 Java SE 8을 설치 합니다.

에 대 한 내용은 비슷한 문제가 openjdk openSUSE hello 토론 스레드를 참조 하십시오. [openSUSE 42.1에 대 한 sap Gui 7.4 Java Leap](https://scn.sap.com/thread/3908306)합니다.

## <a name="manual-installation-of-sap-hana-swpm"></a>SAP HANA 수동 설치: SWPM
hello 일련의이 섹션에 스크린 샷이 hello SWPM (SAPinst)를 사용 하면 SAP NetWeaver 7.5 및 SAP HANA SP12를 설치 하기 위한 주요 단계를 보여 줍니다. NetWeaver 7.5 설치의 일부로 SWPM 단일 인스턴스로 hello HANA 데이터베이스도 설치할 수 있습니다.

샘플 테스트 환경에서는 ABAP(Advanced Business Application Programming) 앱 서버 하나만 설치했습니다. Hello 사용 hello 다음 스크린 샷에서 같이 **분산 시스템** Azure VM에서 hello 데이터베이스 시스템으로 tooinstall hello ASCS 및 기본 응용 프로그램 서버 인스턴스를 하나의 Azure VM 및 SAP HANA 옵션입니다.

![ASCS 및 hello 분산 시스템 옵션을 사용 하 여 설치 하는 기본 응용 프로그램 서버 인스턴스](./media/hana-get-started/image012.jpg)

Hello ASCS 인스턴스 hello 응용 프로그램 서버 VM에 설치 되어 있으며 후 너무 "녹색"으로 SAP 관리 콘솔 (hello 스크린 샷 뒤에 표시), hello 설정 hello /sapmnt 디렉터리 (hello SAP 프로필 디렉터리가 포함)와 공유 해야 hello SAP HANA DB 서버 VM입니다. hello DB 설치 단계 toothis 정보에 액세스 해야 합니다. hello 가장 좋은 방법은 tooprovide 액세스가 toouse NFS YaST를 사용 하 여 구성할 수 있는 합니다.

![SAP 관리 콘솔 표시 된 hello ASCS 인스턴스 hello 응용 프로그램 서버 VM에 설치 하 고 너무 "녹색"으로 설정](./media/hana-get-started/image016.jpg)

Hello 응용 프로그램 서버 VM에서 hello/sapmnt 디렉터리 hello를 사용 하 여 NFS를 통해 공유 되지 않아야 **rw** 및 **no_root_squash** 옵션입니다. hello 기본값은 **ro** 및 **root_squash**, hello 데이터베이스 인스턴스를 설치 하는 tooproblems 발생할 수 있습니다.

![Hello rw 및 no_root_squash 옵션을 사용 하 여 NFS 통해 hello /sapmnt 디렉터리를 공유 합니다.](./media/hana-get-started/image017b.jpg)

Hello 응용 프로그램 서버 VM에서에서 hello /sapmnt 공유를 사용 하 여 hello SAP HANA DB 서버 VM에 구성 해야 hello 다음 스크린 샷에서 같이 **NFS 클라이언트** (및 YaST).

![NFS 클라이언트를 사용 하 여 구성 된 hello /sapmnt 공유](./media/hana-get-started/image018b.jpg)

tooperform 분산된 NetWeaver 7.5 설치 (**데이터베이스 인스턴스**), 스크린 샷 뒤에 표시 된 hello, toohello SAP HANA DB 서버 VM에에서 로그인 및 SWPM를 시작 합니다.

![Toohello SAP HANA DB 서버 VM에에서 로그인 하 SWPM를 시작 하 여 데이터베이스 인스턴스를 설치 합니다.](./media/hana-get-started/image019.jpg)

선택한 후 **일반적인** 설치 및 hello 경로 toohello 설치 미디어를 DB SID, hello 호스트 이름, hello 인스턴스 번호 및 hello DB 시스템 관리자 암호를 입력 합니다.

![hello SAP HANA 데이터베이스 시스템 관리자 로그인 페이지](./media/hana-get-started/image035b.jpg)

Hello DBACOCKPIT 스키마에 대 한 hello 암호를 입력 합니다.

![hello DBACOCKPIT 스키마에 대 한 hello 암호 입력 상자](./media/hana-get-started/image036b.jpg)

Hello SAPABAP1 스키마 암호에 대 한 질문을 입력 합니다.

![Hello SAPABAP1 스키마 암호에 대 한 질문을 입력 합니다.](./media/hana-get-started/image037b.jpg)

각 작업이 완료 되 면 녹색 확인 표시가 hello DB 설치 프로세스의 다음 tooeach 단계 표시 됩니다. hello 메시지 "실행 중... 인스턴스의 실행이 완료되었습니다."가 표시됩니다.

![확인 메시지가 표시된 작업 완료 창](./media/hana-get-started/image023.jpg)

설치 후 hello SAP 관리 콘솔도 hello DB 인스턴스 "녹색"으로 표시를 hello SAP HANA 프로세스 (hdbindexserver, hdbcompileserver, 등)의 전체 목록을 표시 합니다.

![SAP HANA 프로세스 목록을 보여 주는 SAP 관리 콘솔 창](./media/hana-get-started/image024.jpg)

hello 다음 스크린 샷에서 hello의 부분을 보여줍니다 SWPM hello HANA 설치 중에 생성 하는 hello /hana/shared 디렉터리 아래 hello 파일 구조입니다. 가 없는 옵션 toospecify 다른 경로 되므로 hello SAP HANA 설치 하기 전에 hello /hana 디렉터리 아래 중요 한 toomount 추가 디스크 공간이 SWPM를 사용 하 여 합니다. 이렇게 하면 hello 루트 파일 시스템을의 사용 가능한 공간 부족 않습니다.

![HANA 설치 중에 만들어진 hello /hana/shared 디렉터리 파일 구조](./media/hana-get-started/image025.jpg)

이 스크린샷에서 hello /usr/sap 디렉터리의 hello 파일 구조를 보여 줍니다.

![hello /usr/sap 디렉터리 파일 구조](./media/hana-get-started/image026.jpg)

hello distributed hello ABAP 설치의 마지막 단계는 tooinstall hello 기본 응용 프로그램 서버 인스턴스:

![Hello 마지막 단계로 ABAP 설치 보여 주는 기본 응용 프로그램 서버 인스턴스](./media/hana-get-started/image027b.jpg)

Hello를 사용 하 여 hello 기본 응용 프로그램 서버 인스턴스 및 SAP GUI를 설치한 후 **DBA Cockpit** SAP HANA 설치 hello 트랜잭션 tooconfirm 올바르게 완료:

![성공적인 설치를 확인하는 DBA Cockpit 창](./media/hana-get-started/image028b.jpg)

마지막 단계로 수도 toofirst 설치 HANA Studio hello SAP 응용 프로그램 서버 VM에에서 있으며 다음 연결 hello DB 서버 VM에서 실행 되는 toohello SAP HANA 인스턴스:

![Hello SAP 응용 프로그램 서버 VM에서에서 SAP HANA Studio 설치](./media/hana-get-started/image038b.jpg)

## <a name="manual-installation-of-sap-hana-hdblcm"></a>SAP HANA 수동 설치: HDBLCM
또한 tooinstalling SWPM를 사용 하 여 분산된 설치의 일환으로 SAP HANA에에서 HDBLCM를 사용 하 여 hello HANA 독립 실행형을 먼저 설치할 수 있습니다. 예를 들어 SAP NetWeaver 7.5를 설치할 수 있습니다. 이 섹션에서 hello 스크린 샷이이 프로세스가 작동 하는 방법을 보여 줍니다.

Hello HANA HDBLCM 도구에 대 한 자세한 내용은 다음을 참조 하세요.

* [선택 hello Your 작업에 대 한 SAP HANA HDBLCM 올바름](https://help.sap.com/saphelp_hanaplatform/helpdata/en/68/5cff570bb745d48c0ab6d50123ca60/content.htm)
* [SAP HANA Lifecycle Management Tools(SAP HANA 수명 주기 관리 도구)](http://saphanatutorial.com/sap-hana-lifecycle-management-tools/)
* [SAP HANA Server Installation and Update Guide(SAP HANA 서버 설치 및 업데이트 가이드)](http://help.sap.com/hana/SAP_HANA_Server_Installation_Guide_en.pdf)

기본값 tooavoid 문제 그룹 hello에 대 한 ID 설정 `\<HANA SID\>adm user` (hello HDBLCM 도구로 만든) 라는 새 그룹을 정의 `sapsys` 그룹 ID를 사용 하 여 `1001` HDBLCM 통해 SAP HANA를 설치 하기 전에:

![1001 그룹 ID를 사용하여 정의한 새로운 "sapsys" 그룹](./media/hana-get-started/image030.jpg)

HDBLCM hello를 처음 시작 하면 간단한 시작 메뉴가 표시 됩니다. 선택 항목 1, **새 시스템 설치**hello 스크린 샷 뒤에 나타난 것 처럼:

![Hello HDBLCM 시작 창에서 "새 시스템 설치" 옵션](./media/hana-get-started/image031.jpg)

hello 다음 스크린샷에 표시 이전에 선택한 모든 hello 키 옵션 합니다.

> [!IMPORTANT]
> HANA 로그 및 데이터 볼륨을 hello 설치 경로 (/ hana/개의이 샘플의 공유) 및 /usr/sap에 대 한 명명 된 디렉터리는 hello 루트 파일 시스템의 일부가 되지 않아야 합니다. 이러한 디렉터리에 연결 된 toohello (hello "디스크"설치 하는 섹션에 설명 된) VM 되었던 toohello Azure 데이터 디스크 속해 있습니다. 이 방법의 공간이 부족해 hello 루트 파일 시스템을 방지할 수 있습니다. Hello 다음 스크린 샷, 볼 수 있습니다는 HANA 시스템 관리자에 게 사용자 ID가 `1005` hello의 일부인 `sapsys` 그룹 (ID `1001`) hello 설치 하기 전에 정의 된입니다.

![이전에 선택한 주요 SAP HANA 구성 요소 전체 목록](./media/hana-get-started/image032.jpg)

Hello를 확인할 수 있습니다 `\<HANA SID\>adm user` (`azdadm` hello 스크린 샷 뒤에) 디렉터리 hello/등/암호에에서 대 한 세부 정보:

![HANA \<HANA SID\>디렉터리 hello/등/암호에에서 나열 된 adm 사용자 세부 정보](./media/hana-get-started/image033.jpg)

SAP HANA HDBLCM를 사용 하 여 설치한 후 hello 스크린 샷 뒤에 나와 있는 것 처럼 SAP HANA Studio에서 hello 파일 구조를 볼 수 있습니다. 모든 hello SAP NetWeaver 테이블을 포함 하는 hello SAPABAP1 스키마를 아직 사용할 수 없습니다.

![SAP HANA Studio의 SAP HANA 파일 구조](./media/hana-get-started/image034.jpg)

SAP HANA를 설치한 후에는 이를 기반으로 하여 SAP NetWeaver를 설치할 수 있습니다. 스크린 샷 뒤에 표시 된 hello,으로 hello 설치 SWPM (대로 hello 이전 섹션에서 설명)를 사용 하 여 분산된 설치로 수행 되었습니다. Hello 입력 SWPM를 사용 하 여 hello 데이터베이스 인스턴스를 설치할 때 HDBLCM (예: 호스트 이름, HANA SID 및 인스턴스 번호)을 사용 하 여 동일한 데이터입니다. 그런 다음 SWPM hello 기존 HANA 설치를 사용 하 고 더 많은 스키마를 추가 합니다.

![SWPM을 사용하여 수행한 분산 설치](./media/hana-get-started/image035b.jpg)

hello 다음 스크린샷은 hello SWPM 설치 단계 hello DBACOCKPIT 스키마에 대 한 데이터를 입력 하는 위치:

![DBACOCKPIT 스키마 데이터를 입력 한 hello SWPM 설치 단계](./media/hana-get-started/image036b.jpg)

Hello SAPABAP1 스키마에 대 한 데이터를 입력 합니다.

![Hello SAPABAP1 스키마에 대 한 데이터를 입력합니다.](./media/hana-get-started/image037b.jpg)

Hello SWPM 데이터베이스 인스턴스 설치가 완료 된 후에 SAP HANA Studio에서 hello SAPABAP1 스키마를 확인할 수 있습니다.

![SAP HANA Studio에서 hello SAPABAP1 스키마](./media/hana-get-started/image038b.jpg)

마지막으로, hello SAP 응용 프로그램 서버 및 SAP GUI 설치를 완료 한 후 확인할 수 있습니다 hello HANA DB 인스턴스 hello를 사용 하 여 **DBA Cockpit** 트랜잭션:

![DBA Cockpit 트랜잭션 hello를 사용 하 여 hello HANA DB 인스턴스 확인](./media/hana-get-started/image039b.jpg)


## <a name="sap-software-downloads"></a>SAP 소프트웨어 다운로드
다음 스크린 샷을 hello와 같이 hello SAP Service Marketplace에서에서 소프트웨어를 다운로드할 수 있습니다.

Linux/HANA용 NetWeaver 7.5 다운로드:

 ![NetWeaver 7.5를 다운로드하기 위한 SAP 서비스 설치 및 업그레이드 창](./media/hana-get-started/image001.jpg)

HANA SP12 Platform Edition 다운로드:

 ![HANA SP12 Platform Edition을 다운로드하기 위한 SAP 서비스 설치 및 업그레이드 창](./media/hana-get-started/image002.jpg)

