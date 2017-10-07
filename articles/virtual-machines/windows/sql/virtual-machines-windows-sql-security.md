---
title: "Azure의 SQL Server에 대 한 고려 사항 aaaSecurity | Microsoft Docs"
description: "이 항목에서는 Azure Virtual Machine에서 실행되는 SQL Server 보안에 대한 일반적인 지침을 제공합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 14c3d828fa87446da67beea6d28886de254afe15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a>Azure 가상 컴퓨터의 SQL Server에 대한 보안 고려 사항

이 항목에는 Azure 가상 컴퓨터 (VM)에 대 한 보안 액세스 tooSQL 서버 인스턴스를 설정 하는 데 도움이 되는 전반적인 보안 지침이 포함 되어 있습니다.

Azure는 몇 가지 산업 규정 및 표준을 사용할 수 있는 호환 되는 솔루션 toobuild 가상 컴퓨터에서 실행 중인 SQL Server를 준수 합니다. Azure 규정 준수에 대한 자세한 내용은 [Azure 보안 센터](https://azure.microsoft.com/support/trust-center/)를 참조하세요.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-toohello-sql-vm"></a>컨트롤 액세스 toohello SQL VM

SQL Server 가상 컴퓨터를 만들면 사용자 액세스 toohello 컴퓨터와 서버 tooSQL 누가 toocarefully을 제어 하는 방법을 고려 합니다. 일반적으로 수행 해야 hello 다음:

- 액세스 tooSQL 서버 tooonly hello 응용 프로그램 및 필요로 하는 클라이언트를 제한 합니다.
- 사용자 계정 및 암호를 관리하는 모범 사례를 따릅니다.

hello 다음 섹션에 이러한 요소를 고려 제안을 제공 합니다.

## <a name="secure-connections"></a>보안 연결

갤러리 이미지를 사용 하는 SQL Server 가상 컴퓨터를 만들 때 hello **SQL Server 연결** 옵션은 다양 한 hello **(VM) 내부의 로컬**, **개인 (가상 네트워크 내에서)** , 또는 **공개 (인터넷)**합니다.

![SQL Server 연결](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

Hello 최상의 보안을 위해 사용자의 시나리오에 대 한 hello 가장 제한적인 옵션을 선택 합니다. 예를 들어 SQL Server에 액세스 하는 응용 프로그램을 실행 하는 경우 hello 동일한 VM 다음 **로컬** 는 hello 가장 안전한 선택 합니다. 다음 액세스 toohello SQL Server를 필요로 하는 Azure 응용 프로그램을 실행 하는 경우 **개인** 통신 tooSQL 서버 hello 지정 내 에서만 보호 [Azure 가상 네트워크](../../../virtual-network/virtual-networks-overview.md)합니다. 필요한 경우 **공용** (internest) 액세스 toohello SQL Server VM을 확인 한 다음 있는지 toofollow 공격 노출 영역에서이 항목 tooreduce 다른 모범 사례입니다.

hello hello 포털에서 선택 된 옵션 사용 하 여 인바운드 보안 규칙 hello Vm에 [네트워크 보안 그룹](../../../virtual-network/virtual-networks-nsg.md) tooallow (NSG) 또는 네트워크 트래픽 tooyour 가상 컴퓨터를 거부 합니다. 수정 하거나 새 인바운드 NSG 규칙 tooallow 트래픽 toohello SQL Server 포트 (기본값 1433)를 만들 수 있습니다. 허용 되는 toocommunicate이이 포트를 통해 특정 IP 주소를 지정할 수 있습니다.

![네트워크 보안 그룹 규칙](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

또한 tooNSG 규칙 toorestrict 네트워크 트래픽, hello 가상 컴퓨터에서 Windows 방화벽 hello를 사용할 수도 있습니다.

끝점 hello 클래식 배포 모델을 사용 하는 경우 사용 하지 않는 경우 hello 가상 컴퓨터 끝점을 모두 제거 합니다. 끝점 Acl을 사용 하 여, 참조 [끝점에서 ACL 관리 hello](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)합니다. 이 작업이 hello 리소스 관리자를 사용 하는 Vm에 대 한 필요 하지 않습니다.

마지막으로, Azure 가상 컴퓨터에 SQL Server 데이터베이스 엔진 hello의 hello 인스턴스에 대 한 암호화 된 연결을 사용 하는 것이 좋습니다. 서명된 인증서로 SQL server 인스턴스를 구성합니다. 자세한 내용은 참조 [암호화 연결 사용 toohello 데이터베이스 엔진](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) 및 [연결 문자열 구문](https://msdn.microsoft.com/library/ms254500.aspx)합니다.

## <a name="use-a-non-default-port"></a>기본 포트가 아닌 포트 사용

기본적으로 SQL Server는 잘 알려진 포트 1433에서 수신 대기합니다. 보안 향상된을 위해 SQL Server toolisten에서 1401 같은 기본이 아닌 포트를 구성 합니다. Hello Azure 포털에에서는 SQL Server 갤러리 이미지를 프로 비전 하는 경우 hello에서이 포트를 지정할 수 있습니다 **SQL Server 설정을** 블레이드입니다.

tooconfigure이에서 프로 비전 후 두 가지 옵션이 있습니다.

- 리소스 관리자 Vm에 대해 선택할 수 있습니다 **SQL Server 구성** hello VM 개요 블레이드에서 합니다. Toochange hello 포트는 옵션 제공합니다.

  ![포털에서 TCP 포트 변경](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- 클래식 Vm 또는 포털 hello로 프로 비전 되지 않은 SQL Server Vm에 대 한 VM toohello 원격으로 연결 하 여 hello 포트를 수동으로 구성할 수 있습니다. Hello 구성 단계를 참조 하십시오. [서버 tooListen 특정 TCP 포트로 구성](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)합니다. 이 수동 방법을 사용 하는 경우 해당 TCP 포트에서 Windows 방화벽 규칙 tooallow 들어오는 트래픽이 tooadd가 있어야 합니다.

> [!IMPORTANT]
> 기본이 아닌 포트를 지정 하는 SQL Server 포트가 열려 toopublic 인터넷 연결 하는 경우에 것이 좋습니다.

SQL Server를 기본이 아닌 포트에서 수신 하는 경우에 연결할 때 hello 포트를 지정 해야 합니다. 예를 들어 hello 서버 IP 주소가 13.55.255.255 고 1401 포트에서 SQL Server가 수신 하는 시나리오를 고려 하십시오. tooconnect tooSQL 서버를 지정 하는 경우 `13.55.255.255,1401` hello 연결 문자열에 있습니다.

## <a name="manage-accounts"></a>계정 관리

공격자가 tooeasily 추측 계정 이름이 나 암호를 되기를 원하지 않습니다. 다음 팁 toohelp hello를 사용 합니다.

- 로컬 관리자 계정의 이름을 **Administrator**가 아닌 다른 이름으로 만듭니다.

- 모든 계정에 복잡하고 강력한 암호를 사용합니다. 방법에 대 한 자세한 내용은 강력한 암호를 toocreate 참조 [강력한 암호를 만드는](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) 문서.

- 기본적으로 Azure는 SQL Server 가상 컴퓨터를 설치하는 동안 Windows 인증을 선택합니다. 따라서 hello **SA** 로그인이 해제 되며 설치 프로그램에서 암호를 할당 합니다. 해당 hello 권장 **SA** 로그인 사용 되거나 사용 하도록 설정 되지 않아야 합니다. SQL 로그인 해야 할 경우 hello 다음 전략 중 하나를 사용 합니다.

  - **sysadmin** 멤버 자격이 있는 고유한 이름을 가진 SQL 계정을 만듭니다. 사용 하 여 hello 포털에서 이렇게 하려면 **SQL 인증** 프로 비전 중입니다.

    > [!TIP] 
    > 프로 비전 하는 동안 SQL 인증을 사용 하지 않도록 하는 경우 너무 hello 인증 모드를 수동으로 변경 해야 하면**SQL Server 및 Windows 인증 모드**합니다. 자세한 내용은 [서버 인증 모드 변경](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode)을 참조하세요.

  - Hello를 사용 해야 할 경우 **SA** 로그인을 프로 비전 하 고 강력한 새 암호를 할당 한 후 hello 로그인을 사용 하도록 설정 합니다.

## <a name="follow-on-premises-best-practices"></a>온-프레미스 모범 사례 따르기

검토 하 고 해당 되는 hello 기존의 온-프레미스 보안 방법을 구현 하는 또한 권장 toohello이이 항목에 설명 합니다. 자세한 내용은 [SQL Server 설치에 대한 보안 고려 사항](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)을 참조하세요.

## <a name="next-steps"></a>다음 단계

성능에 대한 모범 사례에도 관심이 있으면 [Azure Virtual Machines의 SQL Server에 대한 성능 모범 사례](virtual-machines-windows-sql-performance.md)를 참조하세요.

다른 항목은 서로 관련 toorunning Azure Vm에서 SQL Server에 대 한 참조 [SQL Server에 대 한 Azure 가상 컴퓨터 개요](virtual-machines-windows-sql-server-iaas-overview.md)합니다.

