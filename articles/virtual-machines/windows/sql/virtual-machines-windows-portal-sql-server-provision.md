---
title: "SQL Server 가상 컴퓨터 aaaProvision | Microsoft Docs"
description: "만들고 hello 포털을 사용 하 여 Azure에서 tooa SQL Server 가상 컴퓨터를 연결 합니다. 이 자습서에서는 hello Resource Manager 모드를 사용 합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: acb52b180103d83715b51b46e2519211c8f0e362
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

2. Hello Azure 포털에서 클릭 **새로**합니다. hello 포털이 열립니다 hello **새로** 창.

3. Hello에 **새로** 창 클릭 **계산** 클릭 하 고 **스크롤하게**합니다.

   ![새 계산 창](./media/virtual-machines-windows-portal-sql-server-provision/azure-new-compute-blade.png)

4. Hello 검색 필드에 입력 **SQL Server**, ENTER 키를 누릅니다.

5. Hello 클릭 **필터** 아이콘과 선택 **Microsoft** hello 게시자에 대 한 합니다. 클릭 **수행** tooMicrosoft hello 필터 toofilter hello 결과 창에 SQL Server 이미지를 게시 합니다.

   ![Azure Virtual Machines 창](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. Hello 제공 되는 SQL Server 이미지를 검토 합니다. 각 이미지는 SQL Server 버전 및 운영 체제를 식별합니다.

6. 라는 선택 hello 이미지 **무료 라이선스: Windows Server 2016에서 SQL Server 2016 SP1 Developer**합니다.

   > [!TIP]
   > hello Developer edition은 테스트 목적으로 개발에 대 한 무료 SQL Server의 모든 기능을 갖춘 버전 이기 때문에이 자습서에 사용 됩니다. Hello 실행 비용을 hello VM에 대해서만 지불 합니다. 하지만 무료 toochoose는이 자습서에서는 hello 이미지 toouse 중 하나입니다.

   > [!TIP]
   > SQL VM 이미지 SQL Server 라이선스 비용 hello hello hello 개발자 및 Express 버전만) (제외 만드는 VM의 hello 분 당 가격에 포함 합니다. SQL Server Developer는 개발/테스트(비 프로덕션)에 대해 무료이며 SQL Express는 간단한 작업(1GB 미만의 메모리, 10GB 미만의 저장소)에 대해 무료입니다. 다른 옵션 toobring your-소유-라이선스 (BYOL) 고 hello VM에 대해서만 지불 됩니다. 이러한 이미지 이름에는 접두사 {BYOL}이 붙습니다. 
   >
   > 이러한 옵션에 대한 자세한 내용은 [SQL Server Azure VM에 대한 가격 책정 지침](virtual-machines-windows-sql-server-pricing-guidance.md)을 참조하세요.

7. **배포 모델 선택**에서 **리소스 관리자**가 선택되어 있는지 확인합니다. 리소스 관리자는 새 가상 컴퓨터에 대 한 배포 모델을 권장 하는 hello입니다. 

8. **만들기**를 클릭합니다.

    ![리소스 관리자로 SQL VM 만들기](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>Hello VM 구성
SQL Server 가상 컴퓨터를 구성하기 위한 5개의 창이 있습니다.

| 단계 | 설명 |
| --- | --- |
| **기본 사항** |[기본 설정 구성](#1-configure-basic-settings) |
| **크기** |[가상 컴퓨터 크기 선택](#2-choose-virtual-machine-size) |
| **설정** |[선택적 기능 구성](#3-configure-optional-features) |
| **SQL 서버 설정** |[SQL Server 설정 구성](#4-configure-sql-server-settings) |
| **요약** |[요약 검토 hello](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. 기본 설정 구성

Hello에 **기본 사항** 창의 hello 다음 정보를 제공 합니다.

* 고유한 가상 컴퓨터 **이름**을 입력합니다.

* 최적의 성능을 위해 VM 디스크 유형에 **SSD**를 선택합니다.

* 지정 된 **사용자 이름** hello hello VM 로컬 관리자 계정에 대 한 합니다. 이 계정은 SQL Server toohello도 추가 **sysadmin** 고정된 서버 역할입니다.

* 강력한 **암호**를 제공합니다.

* Hello 구독에 대해 올바른지 확인 하는 여러 구독이 있는 경우에 새 VM hello 합니다.

* Hello에 **리소스 그룹** 상자에 새 리소스 그룹에 대 한 이름을 입력 합니다. 또는 toouse 기존 리소스 그룹 클릭 **기존 항목 사용**합니다. 리소스 그룹은 Azure 내 관련 리소스의 컬렉션입니다(가상 컴퓨터, 저장소 계정, 가상 네트워크 등).

  > [!NOTE]
  > 새 리소스 그룹을 사용하면 Azure에서 SQL Server 배포를 테스트하거나 알아보는 경우에 유용합니다. 테스트와 완료 된 후 hello 리소스 그룹 tooautomatically delete hello VM 및 해당 리소스 그룹에 연결 된 모든 리소스를 삭제 합니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../../azure-resource-manager/resource-group-overview.md)를 참조하세요.

* 선택 된 **위치** hello이이 배포를 호스팅하는 Azure 지역에 대 한 합니다.

* 클릭 **확인** toosave hello 설정 합니다.

    ![SQL 기본 창](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2. 가상 컴퓨터 크기 선택

Hello에 **크기** 단계, hello에 가상 컴퓨터 크기 선택 **크기 선택** 창. hello 창은 선택한 hello 이미지에 따라 권장된 컴퓨터 크기를 나타냅니다.

> [!IMPORTANT]
> hello 예상 hello에 표시 되는 월별 비용 **크기를 선택** 창에 SQL Server 라이선스 비용 포함 되지 않습니다. 이 hello 단독 VM의 hello 비용입니다. SQL Server의 hello Express 및 Developer 버전에서 hello 총 예상된 비용입니다. 다른 버전에 대 한 참조 hello [Windows 가상 컴퓨터 가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) 하 고 SQL Server의 대상 버전을 선택 합니다. 또한 hello 참조 [SQL Server Azure Vm에 대 한 지침을 가격](virtual-machines-windows-sql-server-pricing-guidance.md)합니다.

![SQL VM 크기 옵션](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

프로덕션 작업에 대 한 hello 컴퓨터 크기 및 구성에서 권장을 보려면 [Azure 가상 컴퓨터의 SQL Server에 대 한 성능 모범 사례](virtual-machines-windows-sql-performance.md)합니다. 나열 되지 않은 컴퓨터 크기를 해야 하는 경우 클릭 hello **모든 보기** 단추입니다.

> [!NOTE]
> 가상 컴퓨터 크기에 대한 자세한 내용은 [가상 컴퓨터 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

컴퓨터 크기를 선택한 다음 **선택**을 클릭합니다.

## <a name="3-configure-optional-features"></a>3. 선택적 기능 구성

Hello에 **설정을** 창에서 Azure 저장소, 네트워킹, 및 hello 가상 컴퓨터에 대 한 모니터링을 구성 합니다.

* **Storage**의 **Managed Disks**에서 **예**를 선택합니다.

   > [!NOTE]
   > SQL Server에 Managed Disks를 사용하는 것이 좋습니다. Hello 백그라운드 핸들 저장소 디스크를 관리합니다. 또한 관리 되는 디스크와 가상 컴퓨터에에서 있는 경우 hello 동일한 가용성 집합에 Azure hello 저장소 리소스 tooprovide 적절 한 중복 배포 합니다. 자세한 내용은 [Azure Managed Disks 개요](../../../storage/storage-managed-disks-overview.md)를 참조하세요. 가용성 집합의 Managed Disks에 대한 구체적인 내용을 보려면 [가용성 집합에서 VM에 Managed Disks 사용](../manage-availability.md)을 참조하세요.

* 아래 **네트워크**를 자동으로 채울 hello 값을 사용할 수 있습니다. 각 기능을 클릭할 수도 있습니다 toomanually hello 구성 **가상 네트워크**, **서브넷**, **공용 IP 주소**, 및 **네트워크보안그룹**. 이 자습서의 hello 위해 hello 기본값을 유지 합니다.

* Azure 사용 **모니터링** hello VM에 대해 동일한 저장소 계정을 지정 하는 hello로 기본적으로 합니다. 여기에서 이러한 설정을 변경할 수 있습니다.

* 아래 **가용성 집합**, hello 기본값은 그대로 두면 **none** 이 자습서에 대 한 합니다. SQL AlwaysOn 가용성 그룹을 tooset 하려는 경우 hello 가용성 tooavoid 다시 만들고 hello 가상 컴퓨터를 구성 합니다.  자세한 내용은 참조 [가상 컴퓨터의 가용성 관리 hello](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

이러한 설정 구성을 완료한 후 **확인**을 클릭합니다.

## <a name="4-configure-sql-server-settings"></a>4. SQL Server 설정 구성
Hello에 **SQL Server 설정을** 창에서 특정 설정 및 SQL Server에 대 한 최적화를 구성 합니다. SQL Server에 대해 구성할 수 있는 hello 설정을 hello 다음과 같습니다.

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

> [!TIP]
> 기본적으로 SQL Server는 잘 알려진 포트 **1433**에서 수신 대기합니다. 보안 향상된을 위해 1401 등의 기본이 아닌 포트에서 이전 대화 toolisten hello에에서 hello 포트를 변경 합니다. 이 작업을 수행할 경우 SSMS와 같이 모든 클라이언트 도구의 해당 포트를 사용하여 연결해야 합니다.

tooconnect tooSQL 서버 hello 통해 인터넷을도 인증을 활성화 해야 SQL Server, hello 다음 섹션에 설명 되어 있습니다.

Toonot enable 연결 toohello 데이터베이스 엔진을 사용 하도록 하려는 경우를 통해 인터넷 hello, hello 다음 옵션 중 하나를 선택 합니다.

* **VM에만 해당) (내 로컬** tooallow 연결 tooSQL 에서만 서버 hello VM 내에서.
* **(가상 네트워크 내에서) 개인** tooallow 연결 tooSQL 서버 hello의 서비스 또는 컴퓨터에서 동일한 가상 네트워크입니다.

일반적으로 시나리오에서 허용 하는 hello 가장 제한적인 연결을 선택 하 여 보안을 향상 합니다. 하지만 모든 hello 옵션은 네트워크 보안 그룹 규칙 및 SQL/Windows 인증을 통해 보안 개체입니다. Hello VM이 생성 한 후 네트워크 보안 그룹을 편집할 수 있습니다. 자세한 내용은 [Azure Virtual Machines의 SQL Server에 대한 보안 고려 사항](virtual-machines-windows-sql-security.md)을 참조하세요.

> [!NOTE]
> SQL Server Express edition에 대 한 가상 컴퓨터 이미지 hello hello TCP/IP 프로토콜을 자동으로 허용 하지 않습니다. 이 hello 공용 및 전용 연결에도 적용 옵션입니다. Express edition을 사용 해야 SQL Server 구성 관리자 너무[수동으로 hello TCP/IP 프로토콜을 사용 하도록 설정](#configure-sql-server-to-listen-on-the-tcp-protocol) hello VM을 만든 후 합니다.

### <a name="authentication"></a>인증

SQL Server 인증이 필요하도록 지정하려면 **사용** under **사용**을 방문하십시오.

![SQL Server 인증](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> 통해 tooaccess SQL Server를 계획 하는 경우 hello 인터넷 (예: hello 공용 연결 옵션), 여기에 SQL 인증을 사용 하도록 설정 해야 합니다. 공용 액세스 toohello SQL Server에는 SQL 인증 hello 사용을 해야합니다.
> 
> 

SQL Server 인증을 사용하도록 설정하는 경우 **로그인 이름** 및 **암호**를 지정합니다. 이 사용자 이름은 SQL Server 인증 로그인 및 hello의 구성원으로 구성 된 **sysadmin** 고정된 서버 역할입니다. 인증 모드에 대한 자세한 내용은 [인증 모드 선택](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode)을 참조하세요.

SQL Server 인증을 사용 하지 않도록 하는 경우 로컬 관리자 계정을 hello hello VM tooconnect toohello SQL Server 인스턴스에서 사용할 수 있습니다.

### <a name="storage-configuration"></a>Storage 구성

클릭 **저장소 구성** toospecify hello에 대 한 저장소 요구 사항입니다.

![SQL Storage 구성](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> VM toouse 표준 저장소를 수동으로 구성한 경우이 옵션은 사용할 수 없습니다. 자동 저장소 최적화는 Premium Storage에서만 사용할 수 있습니다.

> [!TIP]
> 위치의 hello 수 및 각 슬라이더의 상한값 hello 선택한 VM의 hello 크기에 따라 달라 집니다. 더 큰 효율적이 고 VM이 더 수 tooscale 합니다.

초당 입/출력 작업(IOPs), 처리량(MB/s) 및 총 저장소 크기로 요구 사항을 지정할 수 있습니다. Hello 슬라이딩 눈금을 사용 하 여 이러한 값을 구성 합니다. 워크로드에 따라 이러한 저장소 설정을 변경할 수 있습니다. 디스크 tooattach 수가 hello 및 구성에 자동으로 hello 포털 계산 이러한 요구 사항을 고려 합니다.

아래 **저장소에 대 한 액세스에 최적화 된**, hello 다음 옵션 중 하나를 선택 합니다.

* **일반** hello 기본 설정 이며 대부분의 워크 로드를 지원 합니다.
* **트랜잭션** 처리 일반 데이터베이스 OLTP 워크 로드에 대 한 hello 저장소를 최적화 합니다.
* **데이터 웨어하우징** 분석 및 보고 작업에 대 한 hello 저장소를 최적화 합니다.

### <a name="automated-patching"></a>자동화된 패치

**Automated patching**이 사용됩니다. 자동화 된 패치 적용 Azure tooautomatically 패치 hello 및 SQL Server 운영 체제 수 있습니다. 요일을 한 hello 주, 시간 및 유지 관리 기간에 대 한 기간을 지정 합니다. Azure에서 유지 관리 기간에 패치를 수행합니다. hello 유지 관리 창 일정 시간에 대 한 hello VM 로캘을 사용합니다. Azure tooautomatically 패치 hello 및 SQL Server 운영 체제 하지 않으려면 클릭 **사용 하지 않도록 설정**합니다.  

![SQL 자동화된 패치](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

자세한 내용은 [Azure Virtual Machines에서 SQL Server의 자동화된 패치](virtual-machines-windows-sql-automated-patching.md)를 참조하세요.

### <a name="automated-backup"></a>자동화된 백업

**자동화된 백업**에서 모든 데이터베이스에 대해 자동 데이터베이스 백업을 사용하도록 설정합니다. 자동화된 백업은 기본적으로 사용하지 않도록 설정됩니다.

SQL 자동화 된 백업을 사용 하도록 설정 하면 hello 다음을 구성할 수 있습니다.

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

### <a name="r-services"></a>R 서비스

Hello 옵션 tooenable 있는 [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)합니다. 이렇게 하면 SQL Server 2016 toouse 고급 분석 합니다. 클릭 **사용** hello에 **SQL Server 설정** 창.

> [!NOTE]
> SQL Server 2016 Developer Edition에 대 한이 옵션은 hello 포털에서 하지 사용할 정확 합니다. Developer 버전의 경우 VM을 생성한 후 R 서비스를 수동으로 활성화해야 합니다.

![SQL Server R 서비스 사용](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)

SQL Server 설정 구성을 마치면 **확인**을 클릭합니다.

## <a name="5-review-hello-summary"></a>5. 요약 검토 hello

Hello에 **요약** 검토 요약 hello 창과 클릭 **구매** 이 VM에 대해 지정 된 SQL Server toocreate, 리소스 그룹 및 리소스.

Hello Azure 포털에서에서 hello 배포를 모니터링할 수 있습니다. hello **알림** hello hello 화면 위쪽에 단추를 클릭 hello 배포의 기본 상태를 표시 합니다.

> [!NOTE]
> tooprovide 시간이 배포에 대해 예측 하기 SQL VM toohello 미국 동부 지역 기본 설정으로 배포 하려면. 이 테스트 배포 환경에서는 총 26 분 toocomplete의 걸렸습니다. 사용자의 지역 및 선택한 설정에 따라서 배포 시간이 더 빠르거나 늦을 수 있습니다.

## <a name="open-hello-vm-with-remote-desktop"></a>원격 데스크톱으로 hello VM을 열으십시오

다음 단계 tooconnect toohello SQL Server 가상 컴퓨터 원격 데스크톱을 사용 하는 hello를 사용 합니다.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

Toohello SQL Server 가상 컴퓨터를 연결한 후에 SQL Server Management Studio 실행 수 있으며 로컬 관리자 자격 증명을 사용 하 여 Windows 인증을 사용 하 여 연결 수 있습니다. SQL Server 인증을 설정한 경우 SQL 인증 hello SQL 로그인 및 프로 비전 하는 동안 구성 된 암호를 사용 하 여 연결할 수 있습니다.

액세스 toohello 컴퓨터 toodirectly 변경 컴퓨터 및 요구 사항에 따라 SQL Server 설정을 사용 하면 됩니다. 예를 들어 hello 방화벽 설정을 구성 하거나 SQL Server 구성 설정을 변경할 수 있습니다.

## <a name="enable-tcpip-for-developer-and-express-editions"></a>개발자 및 Express 버전에 대해 TCP/IP 사용

새 SQL Server VM을 프로 비전 할 때 Azure는 자동으로 사용 되지 hello TCP/IP 프로토콜 SQL Server Developer 및 Express 버전에 대 한 합니다. 다음 hello 단계 IP 주소를 통해 원격으로 연결할 수 있도록 toomanually TCP/IP를 설정 하는 방법을 설명 합니다.

다음 단계 사용 하 여 hello **SQL Server 구성 관리자** SQL Server Developer 및 Express 버전에 대 한 tooenable hello TCP/IP 프로토콜입니다.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-toosql-server-remotely"></a>TooSQL 서버를 원격으로 연결

이 자습서에서는 선택한 **공용** hello 가상 컴퓨터에 대 한 액세스 및 **SQL Server 인증**합니다. 이러한 설정을 자동으로 구성 된 hello 가상 컴퓨터 tooallow SQL Server 연결을 통해 모든 클라이언트에서 hello 인터넷 (hello 올바른 SQL 로그인에 게 이러한 가정).

> [!NOTE]
> 프로 비전 중에 공용을 선택 하지 않은 hello 포털을 통해 SQL 연결 설정을 프로 비전 한 후 변경할 수 있습니다. 자세한 내용은 [SQL 연결 설정 변경](virtual-machines-windows-sql-connect.md#change)을 참조하세요.

다음 섹션 hello tooconnect tooyour SQL Server 인스턴스를 통해 다른 컴퓨터에서 VM에 인터넷 hello 하는 방법을 보여 줍니다.

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>다음 단계

Azure에서 SQL Server를 사용 하는 방법에 대 한 기타 정보를 참조 하십시오. [Azure 가상 컴퓨터에 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) 및 hello [질문과 대답](virtual-machines-windows-sql-server-iaas-faq.md)합니다.
