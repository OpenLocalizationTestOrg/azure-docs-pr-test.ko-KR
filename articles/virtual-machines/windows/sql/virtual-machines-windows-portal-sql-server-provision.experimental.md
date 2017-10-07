---
title: "SQL Server 가상 컴퓨터 aaaProvision | Microsoft Docs"
description: "만들고 hello 포털을 사용 하 여 Azure에서 tooa SQL Server 가상 컴퓨터를 연결 합니다. 이 자습서에서는 hello Resource Manager 모드를 사용 합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
editor: 
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: jroth
experimental_id: a641df96-f27d-40
ms.openlocfilehash: aaad422d6ed47f5ca00b1ef484ac270a58e24f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a>Hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 프로 비전
> [!div class="op_single_selector"]
> * [포털](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

이 종단 간 자습서에서는 어떻게 toouse hello Azure 포털 tooprovision SQL Server를 실행 하는 가상 컴퓨터를 보여 줍니다.

hello (VM) Azure 가상 컴퓨터 갤러리에 Microsoft SQL Server가 포함 된 몇 가지 이미지가 있습니다. 몇 번의 클릭 hello hello 갤러리에서 SQL VM 이미지 중 하나를 선택 하 고 프로 비전 할 Azure 환경에서 사용할 수 있습니다.

이 자습서에서는 다음을 수행합니다.

* [Hello 갤러리에서 SQL VM 이미지를 선택 합니다.](#select-a-sql-vm-image-from-the-gallery)
* [구성 및 hello VM 만들기](#configure-the-vm)
* [원격 데스크톱으로 hello VM을 열으십시오](#open-the-vm-with-remote-desktop)
* [TooSQL 서버를 원격으로 연결](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a>Hello 갤러리에서 SQL VM 이미지를 선택 합니다.
1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정을 사용 합니다.

   > [!NOTE]
   > Azure 계정이 없는 경우 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 방문하십시오.

2. Hello Azure 포털에서 클릭 **새로**합니다. hello 포털이 열립니다 hello **새로** 블레이드입니다. hello SQL Server VM 리소스는 hello에서 **계산** hello Marketplace의 그룹입니다.
3. Hello에 **새로** 블레이드에서 클릭 **계산** 클릭 하 고 **스크롤하게**합니다.
4. Hello에 **필터** 텍스트 상자에 SQL Server를 입력 하 고 hello ENTER 키를 누릅니다.

   ![Azure Virtual Machines 블레이드](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. Hello 제공 되는 SQL Server 이미지를 검토 합니다. 각 이미지는 SQL Server 버전 및 운영 체제를 식별합니다. 
6. Windows Server 2016에서 SQL Server 2016 SP1 개발자에 대 한 hello 이미지를 선택 합니다.

   > [!TIP]
   > hello Developer edition은 테스트 목적으로 개발에 대 한 무료 SQL Server의 모든 기능을 갖춘 버전 이기 때문에이 자습서에 사용 됩니다. Hello 실행 비용을 hello VM에 대해서만 지불 합니다.

   > [!NOTE]
   > SQL VM 이미지 SQL Server 라이선스 비용 hello hello hello 개발자 및 Express 버전만) (제외 만드는 VM의 hello 분 당 가격에 포함 합니다. SQL Server Developer는 개발/테스트(비 프로덕션)를 위한 평가판이며, SQL Express는 간단한 워크로드(1GB 미만 메모리, 10GB 미만 저장소)를 위한 평가판입니다.
   > 다른 옵션 toobring your-소유-라이선스 (BYOL) 고 hello VM에 대해서만 지불 됩니다. 이러한 이미지 이름에는 접두사 {BYOL}이 붙습니다. 이러한 옵션에 대한 자세한 내용은 [SQL Server Azure VM에 대한 가격 책정 지침](virtual-machines-windows-sql-server-pricing-guidance.md)을 참조하세요.

7. **배포 모델 선택**에서 **리소스 관리자**가 선택되어 있는지 확인합니다. 리소스 관리자는 새 가상 컴퓨터에 대 한 배포 모델을 권장 하는 hello입니다. **만들기**를 클릭합니다.

    ![리소스 관리자로 SQL VM 만들기](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>Hello VM 구성
SQL Server 가상 컴퓨터를 구성하기 위한 5개의 블레이드가 있습니다.

| 단계 | 설명 |
| --- | --- |
| **기본 사항** |[기본 설정 구성](#1-configure-basic-settings) |
| **크기** |[가상 컴퓨터 크기 선택](#2-choose-virtual-machine-size) |
| **설정** |[선택적 기능 구성](#3-configure-optional-features) |
| **SQL 서버 설정** |[SQL Server 설정 구성](#4-configure-sql-server-settings) |
| **요약** |[요약 검토 hello](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. 기본 설정 구성
Hello에 **기본 사항** 블레이드에서 hello 다음 정보를 제공 합니다.

* 고유한 가상 컴퓨터 **이름**을 입력합니다.
* 지정 된 **사용자 이름** hello hello VM 로컬 관리자 계정에 대 한 합니다. 이 계정은 SQL Server toohello도 추가 **sysadmin** 고정된 서버 역할입니다.
* 강력한 **암호**를 제공합니다.
* Hello 구독에 대해 올바른지 확인 하는 여러 구독이 있는 경우에 새 VM hello 합니다.
* Hello에 **리소스 그룹** 상자에 새 리소스 그룹에 대 한 이름을 입력 합니다. 또는 toouse 기존 리소스 그룹 클릭 **기존 항목 사용**합니다. 리소스 그룹은 Azure 내 관련 리소스의 컬렉션입니다(가상 컴퓨터, 저장소 계정, 가상 네트워크 등).
  
  > [!NOTE]
  > 새 리소스 그룹을 사용하면 Azure에서 SQL Server 배포를 테스트하거나 알아보는 경우에 유용합니다. 테스트와 완료 된 후 hello 리소스 그룹 tooautomatically delete hello VM 및 해당 리소스 그룹에 연결 된 모든 리소스를 삭제 합니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../../azure-resource-manager/resource-group-overview.md)를 참조하세요.
  > 
  > 
* 이 배포의 **위치** 를 선택합니다.
* 클릭 **확인** toosave hello 설정 합니다.
  
    ![SQL 기본 블레이드](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2. 가상 컴퓨터 크기 선택
Hello에 **크기** 단계, hello에 가상 컴퓨터 크기 선택 **크기 선택** 블레이드입니다. hello 블레이드는 처음 선택한 hello 이미지에 따라 권장된 컴퓨터 크기를 표시 합니다.

> [!IMPORTANT]
> hello 예상 hello에 표시 되는 월별 비용 **크기 선택** 블레이드 SQL Server 라이선스 비용을 다루지 않습니다. 이 예상된 월별 비용 hello 단독 VM의 hello 비용이입니다. SQL Server의 hello Express 및 Developer 버전에서 hello 총 예상된 비용입니다. 다른 버전에 대 한 참조 hello [Windows 가상 컴퓨터 가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) 하 고 SQL Server의 대상 버전을 선택 합니다. 또한 hello 참조 [SQL Server Azure Vm에 대 한 지침을 가격](virtual-machines-windows-sql-server-pricing-guidance.md)합니다.

![SQL VM 크기 옵션](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

프로덕션 워크로드에는, [Premium Storage](../../../storage/storage-premium-storage.md)를 지원하는 가상 컴퓨터 크기를 선택하는 것이 좋습니다. Hello를 사용 하 여 해당 수준의 성능 필요 하지 않은 경우 **모든 보기** 단추를 모든 컴퓨터 크기 옵션을 보여 줍니다. 예를 들어, 개발 또는 테스트 환경을 위해 더 작은 컴퓨터 크기를 사용할 수 있습니다.

> [!NOTE]
> 가상 컴퓨터 크기에 대한 자세한 내용은 [가상 컴퓨터 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요. SQL Server VM 크기에 대한 고려 사항은 [Azure Virtual Machines의 SQL Server에 대한 성능 모범 사례](virtual-machines-windows-sql-performance.md)를 참조하세요.

컴퓨터 크기를 선택한 다음 **선택**을 클릭합니다.

## <a name="3-configure-optional-features"></a>3. 선택적 기능 구성
Hello에 **설정을** 블레이드를 Azure 저장소, 네트워킹, 및 hello 가상 컴퓨터에 대 한 모니터링을 구성 합니다.

* **Storage**에서 **디스크 유형**으로 표준 또는 프리미엄(SSD)을 지정합니다. 프리미엄 저장소는 프로덕션 워크로드용으로 권장됩니다.

> [!NOTE]
> Premium Storage를 지원하지 않는 컴퓨터 크기에 대해 프리미엄(SSD)을 선택하면, 컴퓨터 크기가 자동으로 변경됩니다.  
> 
> 

* 아래 **저장소 계정**, hello 자동으로 프로 비전 된 저장소 계정 이름을 사용할 수 있습니다. 또한 클릭할 수 **저장소 계정** toochoose 기존 계정 및 hello 저장소 계정 유형을 구성 합니다. 기본적으로 Azure에서는 로컬 중복 저장소로 새 저장소 계정을 만듭니다. 저장소 옵션에 대한 자세한 내용은 [Azure Storage 복제](../../../storage/storage-redundancy.md)를 참조하세요.
* 아래 **네트워크**를 자동으로 채울 hello 값을 사용할 수 있습니다. 각 기능을 클릭할 수도 있습니다 toomanually hello 구성 **가상 네트워크**, **서브넷**, **공용 IP 주소**, 및 **네트워크보안그룹**. 이 자습서의 hello 위해 hello 기본값을 유지 합니다.
* Azure 사용 **모니터링** hello VM에 대해 동일한 저장소 계정을 지정 하는 hello로 기본적으로 합니다. 여기에서 이러한 설정을 변경할 수 있습니다.
* **가용성 집합**아래에서 가용성 집합을 지정합니다. 이 자습서의 hello 위해 선택할 수 있습니다 **none**합니다. SQL AlwaysOn 가용성 그룹을 tooset 하려는 경우 hello 가용성 tooavoid 다시 만들고 hello 가상 컴퓨터를 구성 합니다.  자세한 내용은 참조 [가상 컴퓨터의 가용성 관리 hello](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

이러한 설정 구성을 완료한 후 **확인**을 클릭합니다.

## <a name="4-configure-sql-server-settings"></a>4. SQL Server 설정 구성
Hello에 **SQL Server 설정을** 블레이드에서 특정 설정 및 SQL Server에 대 한 최적화를 구성 합니다. SQL Server에 대해 구성할 수 있는 hello 설정 hello 설정을 다음을 포함 합니다.

| 설정 |
| --- |
| [연결](#connectivity) |
| [인증](#authentication) |
| [Storage 구성](#storage-configuration) |
| [자동화된 패치](#automated-patching) |
| [자동화된 Backup](#automated-backup) |
| [Azure Key Vault 통합](#azure-key-vault-integration) |
| [R 서비스](#r-services) |

### <a name="connectivity"></a>연결
**SQL 연결**, hello 유형을 지정 하려는이 VM의 SQL Server 인스턴스에 toohello 액세스 합니다. 이 자습서의 hello 위해서 선택 **공개 (인터넷)** tooallow 연결 tooSQL 서버 컴퓨터 또는 서비스를 통해 인터넷 hello 합니다. 이 옵션을 선택 하면 Azure에서 자동으로 구성 hello 방화벽 및 네트워크 보안 그룹 tooallow 트래픽 hello 포트 1433입니다.  

![SQL 연결 옵션](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

tooconnect tooSQL 서버 hello 통해 인터넷을도 인증을 활성화 해야 SQL Server, hello 다음 섹션에 설명 되어 있습니다.

> [!NOTE]
> 것은 가능한 tooadd hello 네트워크 통신 tooyour SQL Server VM에 대 한 더 많은 제한이 있습니다. Hello VM을 만든 후 더 많은 제한이 편집 hello 네트워크 보안 그룹으로 추가할 수 있습니다. 자세한 내용은 [NSG(네트워크 보안 그룹)란?](../../../virtual-network/virtual-networks-nsg.md)
> 
> 

Toonot enable 연결 toohello 데이터베이스 엔진을 사용 하도록 하려는 경우를 통해 인터넷 hello, hello 다음 옵션 중 하나를 선택 합니다.

* **VM에만 해당) (내 로컬** tooallow 연결 tooSQL 에서만 서버 hello VM 내에서.
* **(가상 네트워크 내에서) 개인** tooallow 연결 tooSQL 서버 hello의 서비스 또는 컴퓨터에서 동일한 가상 네트워크입니다.

> [!NOTE]
> SQL Server Express edition에 대 한 가상 컴퓨터 이미지 hello hello TCP/IP 프로토콜을 자동으로 허용 하지 않습니다. 이 hello 공용 및 전용 연결에도 적용 옵션입니다. Express edition을 사용 해야 SQL Server 구성 관리자 너무[수동으로 hello TCP/IP 프로토콜을 사용 하도록 설정](#configure-sql-server-to-listen-on-the-tcp-protocol) hello VM을 만든 후 합니다.
> 
> 

일반적으로 시나리오에서 허용 하는 hello 가장 제한적인 연결을 선택 하 여 보안을 향상 합니다. 하지만 모든 hello 옵션은 네트워크 보안 그룹 규칙 및 SQL/Windows 인증을 통해 보안 개체입니다.

**포트** too1433 기본값입니다. 다른 포트 번호를 지정할 수 있습니다.
자세한 내용은 참조 [tooa SQL Server 가상 컴퓨터 (리소스 관리자)에 연결 | Microsoft Azure](virtual-machines-windows-sql-connect.md)합니다.

### <a name="authentication"></a>인증
SQL Server 인증이 필요하도록 지정하려면 **사용** under **사용**을 방문하십시오.

![SQL Server 인증](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> 통해 tooaccess SQL Server를 계획 하는 경우 hello 인터넷 (즉, hello 공용 연결 옵션), 여기에 SQL 인증을 사용 하도록 설정 해야 합니다. 공용 액세스 toohello SQL Server에는 SQL 인증 hello 사용을 해야합니다.
> 
> 

SQL Server 인증을 사용하도록 설정하는 경우 **로그인 이름** 및 **암호**를 지정합니다. 이 사용자 이름은 SQL Server 인증 로그인 및 hello의 구성원으로 구성 된 **sysadmin** 고정된 서버 역할입니다. 인증 모드에 대한 자세한 내용은 [인증 모드 선택](http://msdn.microsoft.com/library/ms144284.aspx) 을 참조하세요.

SQL Server 인증을 사용 하지 않도록 하는 경우 로컬 관리자 계정을 hello hello VM tooconnect toohello SQL Server 인스턴스에서 사용할 수 있습니다.

### <a name="storage-configuration"></a>Storage 구성
클릭 **저장소 구성** toospecify hello에 대 한 저장소 요구 사항입니다.

![SQL Storage 구성](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> 표준 저장소를 선택하면, 이 옵션을 사용할 수 없습니다. 자동 저장소 최적화는 Premium Storage에서만 사용할 수 있습니다.
> 
> 

초당 입/출력 작업(IOPs), 처리량(MB/s) 및 총 저장소 크기로 요구 사항을 지정할 수 있습니다. Hello 슬라이딩 눈금을 사용 하 여 이러한 값을 구성 합니다. hello 포털 hello 수의 이러한 요구 사항에 따라 디스크를 자동으로 계산 합니다.

기본적으로 Azure 5,000 IOPs, 200mb의 디스크 및 저장소 공간의 1TB hello 저장소를 최적화 합니다. 워크로드에 따라 이러한 저장소 설정을 변경할 수 있습니다. 아래 **저장소에 대 한 액세스에 최적화 된**, hello 다음 옵션 중 하나를 선택 합니다.

* **일반** hello 기본 설정 이며 대부분의 워크 로드를 지원 합니다.
* **트랜잭션** 처리 일반 데이터베이스 OLTP 워크 로드에 대 한 hello 저장소를 최적화 합니다.
* **데이터 웨어하우징** 분석 및 보고 작업에 대 한 hello 저장소를 최적화 합니다.

> [!NOTE]
> hello 상한값 hello 슬라이더에서 선택한 가상 컴퓨터 크기에 따라 달라 집니다.
> 
> 

### <a name="automated-patching"></a>자동화된 패치
**Automated patching**이 사용됩니다. 자동화 된 패치 적용 Azure tooautomatically 패치 hello 및 SQL Server 운영 체제 수 있습니다. 요일을 한 hello 주, 시간 및 유지 관리 기간에 대 한 기간을 지정 합니다. Azure에서 유지 관리 기간에 패치를 수행합니다. hello 유지 관리 창 일정 시간에 대 한 hello VM 로캘을 사용합니다. Azure tooautomatically 패치 hello 및 SQL Server 운영 체제 하지 않으려면 클릭 **사용 하지 않도록 설정**합니다.  

![SQL 자동화된 패치](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

자세한 내용은 [Azure Virtual Machines에서 SQL Server의 자동화된 패치](virtual-machines-windows-sql-automated-patching.md)를 참조하세요.

### <a name="automated-backup"></a>자동화된 백업
**자동화된 백업**에서 모든 데이터베이스에 대해 자동 데이터베이스 백업을 사용하도록 설정합니다. 자동화된 백업은 기본적으로 사용하지 않도록 설정됩니다.

SQL 자동화 된 백업을 사용 하도록 설정 하면 hello 다음 설정을 구성할 수 있습니다.

* 백업에 대한 보존 기간(일)
* 백업에 대 한 저장소 계정 toouse
* 백업을 위한 암호화 옵션 및 암호
* 시스템 데이터베이스 백업
* 백업 일정 구성

tooencrypt hello 백업, 클릭 **사용**합니다. 그런 다음 hello 지정 **암호**합니다. Azure 인증서 tooencrypt hello 백업을 만들고 사용 하 여 hello 암호 tooprotect 해당 인증서를 지정 합니다.

![SQL 자동화된 Backup](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 자세한 내용은 [Azure Virtual Machines에서 SQL Server에 대한 자동화된 Backup](virtual-machines-windows-sql-automated-backup.md)을 참조하세요.

### <a name="azure-key-vault-integration"></a>Azure Key Vault 통합
암호화를 위해 Azure의 보안 암호 toostore 클릭 **Azure 키 자격 증명 모음 통합** 클릭 **사용**합니다.

![SQL Azure Key Vault 통합](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

hello 다음 표에 나열 hello 매개 변수가 필요한 tooconfigure Azure 키 자격 증명 모음 통합 합니다.

| 매개 변수 | 설명 | 예제 |
| --- | --- | --- |
| **주요 자격 증명 모음 URL** |hello 위치 hello 주요 자격 증명 모음입니다. |https://contosokeyvault.vault.azure.net/ |
| **주체 이름** |Azure Active Directory 서비스 주체 이름. 이 이름은 이기도 하며 tooas hello 클라이언트 id입니다. |fde2b411-33d5-4e11-af04eb07b669ccf2 |
| **주체 암호** |Azure Active Directory 서비스 주체 암호입니다. 이 암호는 또한 참조 tooas hello 클라이언트 암호입니다. |9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= |
| **자격 증명 이름** |**자격 증명 이름**: AKV 통합 hello VM toohave 액세스 toohello 주요 자격 증명 모음을 허용 하는 SQL Server 내에서 자격 증명을 만듭니다. 이 자격 증명의 이름을 선택하세요. |mycred1 |

자세한 내용은 [Azure VM에서 SQL Server에 대한 Azure Key Vault 통합 구성](virtual-machines-windows-ps-sql-keyvault.md)을 참조하세요.

SQL Server 설정 구성을 마치면 **확인**을 클릭합니다.

### <a name="r-services"></a>R 서비스
[SQL Server R 서비스](https://msdn.microsoft.com/library/mt604845.aspx)를 사용하도록 설정할 수 있습니다. SQL Server R Services는 SQL Server 2016으로 고급 toouse 분석이 가능 합니다. 클릭 **사용** hello에 **SQL Server 설정** 블레이드입니다.

![SQL Server R 서비스 사용](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)


## <a name="5-review-hello-summary"></a>5. 요약 검토 hello
Hello에 **요약** 블레이드에서 검토 hello 요약 하 고 클릭 **확인** 이 VM에 대해 지정 된 SQL Server toocreate, 리소스 그룹 및 리소스.

Hello azure 포털에서 hello 배포를 모니터링할 수 있습니다. hello **알림** hello hello 화면 위쪽에 단추를 클릭 hello 배포의 기본 상태를 표시 합니다.

> [!NOTE]
> tooprovide 시간이 배포에 대해 예측 하기 SQL VM toohello 미국 동부 지역 기본 설정으로 배포 하려면. 이 테스트 배포 환경에서는 총 26 분 toocomplete의 걸렸습니다. 사용자의 지역 및 선택한 설정에 따라서 배포 시간이 더 빠르거나 늦을 수 있습니다.
> 
> 

## <a name="open-hello-vm-with-remote-desktop"></a>원격 데스크톱으로 hello VM을 열으십시오
다음 단계 tooconnect toohello 가상 컴퓨터 원격 데스크톱을 사용 하는 hello를 사용 합니다.

1. Hello Azure VM 작성 되 면 hello에 대 한 hello 아이콘 후 VM에서 Azure 대시보드에 나타납니다. 기존 가상 컴퓨터를 검색하여 찾을 수도 있습니다. 새 SQL 가상 컴퓨터를 클릭합니다. **가상 컴퓨터** 블레이드에 가상 컴퓨터 세부 정보가 표시됩니다.
2. Hello의 hello 위쪽 **가상 컴퓨터** 블레이드에서 클릭 **연결**합니다.
3. hello 브라우저 hello VM에 대 한 RDP 파일을 다운로드합니다. 열기 hello RDP 파일입니다.
    ![원격 데스크톱 tooSQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)
4. 원격 데스크톱 연결 hello가 알려줍니다 해당 hello이 원격 연결의 게시자를 식별할 수 없습니다. 클릭 **연결** toocontinue 합니다.
5. Hello에 **Windows 보안** 대화 상자를 클릭 하 여 **다른 계정을 사용 하 여**합니다.
6. 에 대 한 **사용자 이름** 형식  **\<사용자 이름 >**여기서 <user name> hello VM을 구성할 때 지정한 hello 사용자 이름입니다. Tooadd hello 이름 앞에 초기 백슬래시를 해야합니다.
7. 형식 hello **암호** 이전에이 vm을 구성을 클릭 한 다음 **확인** tooconnect 합니다.
8. 다른 경우 **원격 데스크톱 연결** 대화 묻는 여부 tooconnect, 클릭 **예**합니다.

Toohello SQL Server 가상 컴퓨터를 연결한 후에 SQL Server Management Studio 실행 수 있으며 로컬 관리자 자격 증명을 사용 하 여 Windows 인증을 사용 하 여 연결 수 있습니다. SQL Server 인증을 설정한 경우 SQL 인증 hello SQL 로그인 및 프로 비전 하는 동안 구성 된 암호를 사용 하 여 연결할 수 있습니다.

액세스 toohello 컴퓨터 toodirectly 변경 컴퓨터 및 요구 사항에 따라 SQL Server 설정을 사용 하면 됩니다. 예를 들어 hello 방화벽 설정을 구성 하거나 SQL Server 구성 설정을 변경할 수 있습니다.

## <a name="connect-toosql-server-remotely"></a>TooSQL 서버를 원격으로 연결
이 자습서에서는 선택한 **공용** hello 가상 컴퓨터에 대 한 액세스 및 **SQL Server 인증**합니다. 이러한 설정을 자동으로 구성 된 hello 가상 컴퓨터 tooallow SQL Server 연결을 통해 모든 클라이언트에서 hello 인터넷 (hello 올바른 SQL 로그인에 게 이러한 가정).

> [!NOTE]
> 선택 하지 않은 Public이 프로 비전 하는 동안 추가 단계는 필요한 tooaccess를 통해 SQL Server 인스턴스 하는 경우 인터넷 hello 합니다. 자세한 내용은 참조 [tooa SQL Server 가상 컴퓨터를 연결](virtual-machines-windows-sql-connect.md)합니다.
> 
> 

다음 섹션 hello tooconnect tooyour SQL Server 인스턴스를 통해 다른 컴퓨터에서 VM에 인터넷 hello 하는 방법을 보여 줍니다.

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]
> 
> 

## <a name="next-steps"></a>다음 단계
Azure에서 SQL Server를 사용 하는 방법에 대 한 기타 정보를 참조 하십시오. [Azure 가상 컴퓨터에 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) 및 hello [질문과 대답](virtual-machines-windows-sql-server-iaas-faq.md)합니다.

SQL Server를 Azure 가상 컴퓨터의 비디오 개요를 감시 [Azure VM은 SQL Server 2016 용 hello 기능이 뛰어난](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016)합니다.

[Hello 학습 경로 탐색](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) Azure 가상 컴퓨터에 SQL Server에 대 한 합니다.

