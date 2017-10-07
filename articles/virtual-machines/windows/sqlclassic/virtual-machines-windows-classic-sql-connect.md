---
title: "aaaConnect tooa (클래식) Azure에서 SQL Server 가상 컴퓨터 | Microsoft Docs"
description: "자세한 내용은 방법 tooconnect tooSQL 서버 Azure에서 가상 컴퓨터에서 실행 합니다. 이 항목에서는 hello 클래식 배포 모델을 사용 합니다. hello 시나리오 hello 네트워킹 구성 및 hello 클라이언트의 hello 위치에 따라 다릅니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
experimental_id: d51f3cc6-753b-4e
ms.openlocfilehash: 4fff3936ad0bcfd3a56855a8436991e19b92522b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-classic-deployment"></a>Tooa (클래식 배포) Azure에서 SQL Server 가상 컴퓨터를 연결 합니다.
> [!div class="op_single_selector"]
> * [리소스 관리자](../sql/virtual-machines-windows-sql-connect.md)
> * [클래식](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>개요
이 항목에서는 tooconnect tooyour SQL Server 인스턴스는 Azure 가상 컴퓨터에서 실행 하는 방법을 설명 합니다. 여기서는 몇 가지 [일반 연결 시나리오](#connection-scenarios)를 다룬 다음 [Azure VM에서 SQL Server 연결을 구성하기 위한 상세 단계](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)를 제공합니다.

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 리소스 관리자 Vm을 사용 하는 경우 참조 [tooa 리소스 관리자를 사용 하 여 Azure에서 SQL Server 가상 컴퓨터를 연결](../sql/virtual-machines-windows-sql-connect.md)합니다.

## <a name="connection-scenarios"></a>연결 시나리오
hello 방식으로 클라이언트 tooSQL hello 클라이언트와 hello 컴퓨터/네트워킹 구성의 hello 위치에 따라 달라 집니다 가상 컴퓨터에서 실행 중인 서버를 연결 합니다. 이 시나리오에는 다음이 포함됩니다.

* [연결 tooSQL 서버 hello에 동일한 클라우드 서비스](#connect-to-sql-server-in-the-same-cloud-service)
* [TooSQL 서버 hello 통해 연결 인터넷](#connect-to-sql-server-over-the-internet)
* [연결 tooSQL 서버 hello에 동일한 가상 네트워크](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> 이러한 메서드를 사용 하 여 연결 하기 전에 hello 따라야 [이 문서 tooconfigure 연결의 단계를](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)합니다.
> 
> 

### <a name="connect-toosql-server-in-hello-same-cloud-service"></a>연결 tooSQL 서버 hello에 동일한 클라우드 서비스
여러 가상 컴퓨터에서에서 만들 수 있습니다 hello 동일한 클라우드 서비스입니다. toounderstand이 가상 컴퓨터 시나리오에서는 참조 [어떻게 tooconnect 가상 컴퓨터 가상 네트워크 또는 클라우드 서비스와](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service)합니다. 이 시나리오는 하나의 가상 컴퓨터에서 실행 중인 tooconnect tooSQL 서버 시도 하면 hello에 다른 가상 컴퓨터에서 동일한 클라우드 서비스입니다.

이 시나리오에서는 연결할 수 있습니다 VM hello를 사용 하 여 **이름** (표시 **컴퓨터 이름** 또는 **호스트 이름** hello 포털에서). 만드는 동안 hello VM에 대해 제공한 hello 이름입니다. 예를 들어, SQL VM의 이름을 **mysqlvm**, hello 동일한 클라우드 서비스를 사용할 수 있는 클라이언트 VM 다음 연결 문자열 tooconnect hello:

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-toosql-server-over-hello-internet"></a>TooSQL 서버 hello 인터넷을 통해 연결
원하는 tooconnect tooyour SQL Server 데이터베이스 엔진 hello 인터넷에서에서 들어오는 TCP 통신에 대 한 가상 컴퓨터 끝점을 만들어야 합니다. 이 Azure 구성 단계에서는 들어오는 TCP 포트 트래픽을 tooa TCP 포트를 액세스할 수 있는 toohello 가상 컴퓨터가 안내 합니다.

통해 tooconnect hello 인터넷 hello VM의 DNS 이름 및 hello VM 끝점 포트 번호 (이 문서의 뒷부분에 나오는 구성)를 사용 해야 합니다. toofind hello DNS 이름 toohello Azure 포털에서 선택한 탐색 **가상 컴퓨터 (클래식)**합니다. 그런 다음 가상 컴퓨터를 선택합니다. hello **DNS 이름** hello에 보여집니다 **개요** 섹션.

예를 들어 이름이 **mysqlvm**, DNS 이름이 **mysqlvm7777.cloudapp.net**이고 VM 끝점이 **57500**인 클래식 가상 컴퓨터를 고려해보세요. 올바르게 구성 된 연결을 가정할 hello 연결 문자열 뒤에 있을 수 어디에서 나 사용된 tooaccess hello 가상 컴퓨터 인터넷 hello:

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

통해 클라이언트에 대 한 연결을 통해이 있지만 인터넷 hello, 것은 아닙니다 모든 사용자가 SQL Server tooyour 연결할 수 있습니다. 클라이언트 외부 toohello 올바른 사용자 이름 및 암호가 있어야 합니다. 추가 보안을 위해 hello 공용 가상 컴퓨터 끝점에 대 한 hello 잘 알려진 포트 1433 사용 하지 마십시오. 및 가능한 경우 허용할 끝점 toorestrict 트래픽만 toohello 클라이언트에는 ACL을 추가 하는 것이 좋습니다. 끝점 Acl을 사용 하 여, 참조 [끝점에서 ACL 관리 hello](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)합니다.

> [!NOTE]
> 이 SQL Server와 함께이 기술을 toocommunicate를 사용할 때 모든 보내는 데이터를 hello Azure 데이터 센터 toonote 주체 toonormal 중요 [아웃 바운드 데이터 전송에 대 한 가격](https://azure.microsoft.com/pricing/details/data-transfers/)합니다.
> 
> 

### <a name="connect-toosql-server-in-hello-same-virtual-network"></a>연결 tooSQL 서버 hello에 동일한 가상 네트워크
[가상 네트워크](../../../virtual-network/virtual-networks-overview.md) 에서는 추가적인 시나리오가 가능합니다. Hello 서로 다른 클라우드 서비스에 있는 동일한 가상 네트워크에서 이러한 경우에 Vm의에서 Vm에 연결할 수 있습니다. 또한 [사이트 간 VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)을 통해 온-프레미스 네트워크와 컴퓨터에 VM을 연결하는 하이브리드 아키텍처를 만들 수 있습니다.

가상 네트워크는 또한 toojoin 하면 Azure Vm tooa 도메인이 있습니다. 이 hello 유일한 방법은 toouse Windows 인증 tooSQL 서버입니다. hello 다른 연결 시나리오의 SQL 인증을 요구할 사용자 이름 및 암호.

Tooconfigure 도메인 환경 및 Windows 인증 하려는 경우에이 문서 tooconfigure hello 공용 끝점 또는 hello SQL 인증 로그인의 toouse hello 단계를 설치할 필요가 없습니다. 이 시나리오에서는 hello 연결 문자열에 hello SQL Server VM 이름을 지정 하 여 tooyour SQL Server 인스턴스에 연결할 수 있습니다. 다음 예에서는 hello Windows 인증도 구성 되어 있고 해당 hello 사용자 액세스 toohello SQL Server 인스턴스에 부여 받았는지 가정 합니다.

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a>Azure VM에서 SQL Server 연결을 구성하기 위한 단계
단계를 수행 하는 hello tooconnect toohello SQL Server 인스턴스를 통해 SQL Server Management Studio (SSMS)를 사용 하 여 인터넷 hello 하는 방법을 보여 줍니다. 그러나 hello 동일한 단계 적용 toomaking Azure 및 온-프레미스를 실행 중인 응용 프로그램에 액세스할 수 있는 SQL Server 가상 컴퓨터.

다른 VM에서 SQL Server 인스턴스의 toohello 연결 하거나 인터넷 hello 하려면, 먼저 다음 hello 섹션에 설명 된 대로 작업을 수행 하는 hello를 완료 해야 합니다.

* [Hello 가상 컴퓨터에 대 한 TCP 끝점 만들기](#create-a-tcp-endpoint-for-the-virtual-machine)
* [Hello Windows 방화벽에서 TCP 포트를 열어야 합니다.](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [SQL Server toolisten hello TCP 프로토콜에서 구성](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [혼합된 모드 인증에 대한 SQL Server 구성](#configure-sql-server-for-mixed-mode-authentication)
* [SQL Server 인증 로그인 만들기](#create-sql-server-authentication-logins)
* [Hello 가상 컴퓨터의 DNS 이름을 hello 결정](#determine-the-dns-name-of-the-virtual-machine)
* [다른 컴퓨터에서 toohello 데이터베이스 엔진 연결](#connect-to-the-database-engine-from-another-computer)

hello 연결 경로 hello 다이어그램을 다음으로 요약 되어 있습니다.

![Tooa SQL Server 가상 컴퓨터 연결](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect tooSQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect tooSQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect tooSQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a>다음 단계
고가용성 및 재해 복구를 위한 toouse AlwaysOn 가용성 그룹에도 계획 하는 경우 수신기를 구현 하는 것이 좋습니다. 데이터베이스 클라이언트 toohello 수신기 하지 않고 직접 tooone hello SQL Server 인스턴스를 연결합니다. hello 수신기 경로 클라이언트 toohello 기본 hello 가용성 그룹의 복제본입니다. 자세한 내용은 [Azure에서 AlwaysOn 가용성 그룹에 대한 ILB 수신기 구성](../classic/ps-sql-int-listener.md)을 참조하세요.

모든 hello 보안 모범 사례는 Azure 가상 컴퓨터에서 실행 되는 SQL Server에 대 한 중요 한 tooreview 이며 자세한 내용은 [Azure Virtual Machines의 SQL Server에 대한 보안 고려 사항](../sql/virtual-machines-windows-sql-security.md)을 참조하세요.

[Hello 학습 경로 탐색](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) Azure 가상 컴퓨터에 SQL Server에 대 한 합니다. 

다른 항목은 서로 관련 toorunning Azure Vm에서 SQL Server에 대 한 참조 [Azure 가상 컴퓨터에 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)합니다.

