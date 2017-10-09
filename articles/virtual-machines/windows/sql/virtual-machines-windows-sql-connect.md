---
title: "SQL Server 가상 컴퓨터 (리소스 관리자) aaaConnect tooa | Microsoft Docs"
description: "자세한 내용은 방법 tooconnect tooSQL 서버 Azure에서 가상 컴퓨터에서 실행 합니다. 이 항목에서는 hello 클래식 배포 모델을 사용 합니다. hello 시나리오 hello 네트워킹 구성 및 hello 클라이언트의 hello 위치에 따라 다릅니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a>Tooa (리소스 관리자) Azure에서 SQL Server 가상 컴퓨터를 연결 합니다.
> [!div class="op_single_selector"]
> * [리소스 관리자](virtual-machines-windows-sql-connect.md)
> * [클래식](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>개요

이 항목에서는 tooconnect tooyour SQL Server 인스턴스는 Azure 가상 컴퓨터에서 실행 하는 방법을 설명 합니다. 여기서는 몇 가지 [일반 연결 시나리오](#connection-scenarios)를 다룬 다음 [Azure VM에서 SQL Server 연결을 구성하기 위한 상세 단계](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm)를 제공합니다.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

프로비저닝 및 연결의 전체 연습 과정을 확인하려면 [Azure에서 SQL Server 가상 컴퓨터 프로비전](virtual-machines-windows-portal-sql-server-provision.md)을 참조하세요.

## <a name="connection-scenarios"></a>연결 시나리오

hello 방식으로 클라이언트 tooSQL hello 클라이언트와 hello 네트워킹 구성의 hello 위치에 따라 달라 집니다 가상 컴퓨터에서 실행 중인 서버를 연결 합니다.

hello 형식 지정의 hello 옵션이 hello Azure 포털에서에서 SQL Server VM을 프로 비전 하는 경우 **SQL 연결**합니다.

![프로비전 중 공용 SQL 연결 옵션](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

연결에 대한 옵션은 다음과 같습니다.

| 옵션 | 설명 |
|---|---|
| **공용** | TooSQL 서버 hello 통해 연결 인터넷 |
| **개인** | 연결 tooSQL 서버 hello에 동일한 가상 네트워크 |
| **로컬** | TooSQL 서버 hello에 로컬로 연결 동일한 가상 컴퓨터 | 

hello 다음 섹션에 설명 hello **공용** 및 **개인** 자세히 옵션입니다.

## <a name="connect-toosql-server-over-hello-internet"></a>TooSQL 서버 hello 인터넷을 통해 연결

Tooconnect hello 인터넷에서에서 SQL Server 데이터베이스 엔진 tooyour 선택 **공용** hello에 대 한 **SQL 연결** 프로 비전 시 hello 포털의 유형입니다. 다음 단계는 자동으로 hello 포털 hello지 않습니다.

* SQL Server에 대 한 hello TCP/IP 프로토콜을 설정 합니다.
* 방화벽 규칙 tooopen hello SQL Server TCP 포트 (기본값 1433)를 구성합니다.
* 공용 액세스에 필요한 SQL Server 인증을 활성화합니다.
* SQL Server 포트 hello VM tooall TCP 트래픽 hello에 hello 네트워크 보안 그룹을 구성합니다.

> [!IMPORTANT]
> SQL Server Developer hello에 대 한 가상 컴퓨터 이미지 hello 및 Express edition 사용 하지 마십시오 자동으로 hello TCP/IP 프로토콜. 개발자 및 Express 버전만 사용 해야 SQL Server 구성 관리자 너무[수동으로 hello TCP/IP 프로토콜을 사용 하도록 설정](#manualtcp) hello VM을 만든 후 합니다.

인터넷에 연결 된 모든 클라이언트 hello hello 가상 컴퓨터의 공용 IP 주소 또는 toothat IP 주소를 할당 한 모든 DNS 레이블을 지정 하 여 toohello SQL Server 인스턴스에 연결할 수 있습니다. Toospecify 불필요 hello SQL Server 포트 1433 이면 hello 연결 문자열에 해당 합니다. 다음 연결 문자열 hello DNS 레이블이 tooa SQL VM 연결의 `sqlvmlabel.eastus.cloudapp.azure.com` (사용할 수도 있습니다 hello 공용 IP 주소)는 SQL 인증을 사용 하 여 합니다.

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

통해 클라이언트에 대 한 연결을 통해이 있지만 인터넷 hello, 것은 아닙니다 모든 사용자가 SQL Server tooyour 연결할 수 있습니다. 클라이언트 외부 toohello 올바른 사용자 이름 및 암호가 있어야 합니다. 그러나 추가 보안을 위해 hello 잘 알려진 포트 1433을 방지할 수 있습니다. 예를 들어 포트 1500에서 SQL Server toolisten 및 설정 된 적절 한 방화벽과 네트워크 보안 그룹 규칙을 구성한 경우 hello 포트 번호 toohello 서버 이름을 추가 하 여 연결할 수 있습니다. hello 다음 예제에서는 변경 hello 이전 쿼리와 사용자 지정 포트 번호를 추가 하 여 **1500**, toohello 서버 이름:

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> VM의 SQL Server를 통해 쿼리할 때 hello 인터넷, 보내는 데이터를 모두 hello Azure에서에서의 데이터 센터는 주체 toonormal [아웃 바운드 데이터 전송에 대 한 가격](https://azure.microsoft.com/pricing/details/data-transfers/)합니다.

## <a name="connect-toosql-server-within-a-virtual-network"></a>가상 네트워크 내에서 tooSQL 서버 연결

선택 하는 경우 **개인** hello에 대 한 **SQL 연결** 형식 hello 포털, Azure에서에서 구성 대부분의 동일한 hello 설정이 너무**공용**합니다. 한 가지 차이점 hello hello SQL Server 포트 (기본값 1433)에서 트래픽 밖에 없는 네트워크 보안 그룹 규칙 tooallow 된다는 점입니다.

> [!IMPORTANT]
> SQL Server Developer hello에 대 한 가상 컴퓨터 이미지 hello 및 Express edition 사용 하지 마십시오 자동으로 hello TCP/IP 프로토콜. 개발자 및 Express 버전만 사용 해야 SQL Server 구성 관리자 너무[수동으로 hello TCP/IP 프로토콜을 사용 하도록 설정](#manualtcp) hello VM을 만든 후 합니다.

개인 연결은 종종 여러 가지 시나리오를 활성화하는 [Virtual Network](../../../virtual-network/virtual-networks-overview.md)와 함께 사용됩니다. Hello 다른 리소스 그룹에 있는 동일한 가상 네트워크에서 이러한 경우에 Vm의에서 Vm에 연결할 수 있습니다. 또한 [사이트 간 VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)을 통해 온-프레미스 네트워크와 컴퓨터에 VM을 연결하는 하이브리드 아키텍처를 만들 수 있습니다.

가상 네트워크는 또한 toojoin 하면 Azure Vm tooa 도메인을 설정 합니다. 이 hello 유일한 방법은 toouse Windows 인증 tooSQL 서버입니다. hello 다른 연결 시나리오의 SQL 인증을 요구할 사용자 이름 및 암호.

가상 네트워크의 DNS 구성한 것 이라고 가정할 hello SQL Server VM 컴퓨터 이름 hello 연결 문자열에 지정 하 여 tooyour SQL Server 인스턴스에 연결할 수 있습니다. 다음 예에서는 또한 hello Windows 인증도 구성 되어 있고 해당 hello 사용자 액세스 toohello SQL Server 인스턴스에 부여 받았는지 가정 합니다.

```
Server=mysqlvm;Integrated Security=true
```

## <a id="change"></a> SQL 연결 설정 변경

Hello Azure 포털의에서 SQL Server 가상 컴퓨터에 대 한 hello 연결 설정을 변경할 수 있습니다.

1. Hello Azure 포털에서에서 선택 **가상 컴퓨터**합니다.

2. SQL Server VM을 선택합니다.

3. **설정** 아래에서 **SQL Server 구성**을 클릭합니다.

4. 변경 hello **SQL 연결 수준을** tooyour 필요한 설정 합니다. 필요에 따라이 SQL Server 포트 영역 toochange hello 또는 hello SQL 인증 설정을 사용할 수 있습니다.

   ![SQL 연결 변경](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. Hello 업데이트 toocomplete 몇 분 동안 기다립니다.

   ![SQL VM 업데이트 알림](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <a id="manualtcp"></a> Developer 및 Express 버전에 대해 TCP/IP 사용

SQL Server 연결 설정을 변경 하는 경우 Azure는 자동으로 사용 되지 hello TCP/IP 프로토콜 SQL Server Developer 및 Express 버전에 대 한 합니다. 다음 hello 단계 IP 주소를 통해 원격으로 연결할 수 있도록 toomanually TCP/IP를 설정 하는 방법을 설명 합니다.

먼저, toohello SQL Server 컴퓨터와 원격 데스크톱 연결 합니다.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

다음으로 hello TCP/IP 프로토콜을 사용 하도록 설정 **SQL Server 구성 관리자**합니다.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a>SSMS로 연결

hello 다음 단계 어떻게 toocreate 선택적 DNS는 Azure vm을 레이블을 표시 하 고 SQL Server Management Studio (SSMS)와 연결 합니다.

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>다음 단계

이러한 연결 단계와 함께 프로 비전 방법은 toosee 확인 [Azure에서 SQL Server 가상 컴퓨터를 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.

다른 항목은 서로 관련 toorunning Azure Vm에서 SQL Server에 대 한 참조 [Azure 가상 컴퓨터에 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)합니다.
