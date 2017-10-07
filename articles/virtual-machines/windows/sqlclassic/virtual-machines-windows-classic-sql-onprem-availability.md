---
title: "aaaExtend 온-프레미스 Always On 가용성 그룹 tooAzure | Microsoft Docs"
description: "이 자습서는 hello 클래식 배포 모델을 사용 하 여 만든 리소스를 사용 하 고 어떻게 toouse hello 복제본 추가 마법사에서 SQL Server Management Studio (SSMS) tooadd Azure에서 Always On 가용성 그룹 복제본을 설명 합니다."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 7ca7c423-8342-4175-a70b-d5101dfb7f23
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: 51fe117b40d69706b35f30101538a7a36116e128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-on-premises-always-on-availability-groups-tooazure"></a>온-프레미스 Always On 가용성 그룹 tooAzure 확장
Always On 가용성 그룹은 보조 복제본 추가를 통해 데이터베이스 그룹에 고가용성을 제공합니다. 이러한 복제본은 오류 발생 시의 데이터베이스 장애 조치를 허용합니다. 또한 사용된 toooffload 작업 부하 또는 백업 작업을 읽을 수 있습니다.

SQL Server와 하나 이상의 Azure 가상 컴퓨터를 프로 비전 한 다음 복제본 tooyour 온-프레미스 가용성 그룹 추가 온-프레미스 가용성 그룹 tooMicrosoft Azure를 확장할 수 있습니다.

이 자습서에서는 hello 다음 있다고 가정 합니다.

* 활성 Azure 구독. [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.
* 기존 Always On 가용성 그룹 온-프레미스. 가용성 그룹에 대한 자세한 내용은 [Always On 가용성 그룹](https://msdn.microsoft.com/library/hh510230.aspx)을 참조하세요.
* Hello 간의 연결 온-프레미스 네트워크와 Azure 가상 네트워크. 이 가상 네트워크 만들기에 대 한 자세한 내용은 참조 [Azure 포털 (클래식) hello 사용 하 여 만들기는 사이트 및 사이트 간 연결](../../../vpn-gateway/vpn-gateway-howto-site-to-site-classic-portal.md)합니다.

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

## <a name="add-azure-replica-wizard"></a>Azure Replica Wizard 추가
이 섹션에서는 toouse hello **Azure 복제본 추가 마법사** tooextend Always On 가용성 그룹 솔루션 tooinclude Azure 복제본입니다.

> [!IMPORTANT]
> hello **Azure 복제본 추가 마법사** 만 hello 클래식 배포 모델을 사용 하 여 만든 가상 컴퓨터를 지원 합니다. 새 VM 배포 hello 최신 리소스 관리자 모델을 사용 해야 합니다. 사용 중인 경우 Vm 리소스 관리자와 TRANSACT-SQL commmands (여기 표시 되지 않음)를 사용 하 여 hello 보조 Azure 복제본을 수동으로 추가 해야 합니다. 이 마법사는 hello 리소스 관리자 시나리오에서 작동 하지 않습니다.

1. SQL Server Management Studio에서 **Always On 고가용성** > **가용성 그룹** > **[가용성 그룹 이름]**을 확장합니다.
2. 마우스 오른쪽 단추로 **가용성 복제본**을 클릭한 다음 **복제본 추가**를 클릭합니다.
3. 기본적으로 hello **Add Replica tooAvailability 그룹 마법사** 표시 됩니다. **다음**을 누릅니다.  Hello를 선택한 경우 **이 페이지를 다시 표시 안 함** 이 화면이이 마법사의 이전 시작 하는 동안 옵션 hello hello 페이지 맨 아래에 표시 되지 것입니다.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742861.png)
4. 필요한 tooconnect tooall 기존 보조 복제본이 됩니다. **연결…**을 클릭합니다. 화면 하단의 **모두 연결…**을 hello 화면 아래쪽에 hello 합니다. 인증을 받은 후 클릭 **다음** tooadvance toohello 다음 화면입니다.
5. Hello에 **복제본 지정** 페이지에서 여러 탭 hello 위쪽 나열 됩니다: **복제본**, **끝점**, **백업 기본 설정**, 및 **수신기**합니다. Hello에서 **복제본** 탭을 클릭 **Azure 복제본 추가...** toolaunch hello Azure 복제본 추가 마법사.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742863.png)
6. 설치 하기 전에 hello 로컬 Windows 인증서 저장소에서 기존 Azure 관리 인증서를 선택 합니다. 선택 하거나 전에 사용한 경우 hello Azure 구독 id를 입력 합니다. Toodownload 다운로드를 클릭 하 고 Azure 관리 인증서를 설치 및 Azure 계정을 사용 하 여 구독 hello 목록을 다운로드할 수 있습니다.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742864.png)
7. Hello 페이지에 사용 되는 toocreate hello Azure 가상 컴퓨터 (VM) hello 복제본을 호스팅할 수 있는 값이 포함 된 각 필드를 채웁니다.
   
   | 설정 | 설명 |
   | --- | --- |
   | **이미지** |Hello 원하는 조합의 OS와 SQL Server를 선택 합니다. |
   | **VM 크기** |비즈니스 요구에 가장 적합 한 VM의 hello 크기를 선택 합니다. |
   | **VM 이름** |Hello에 대 한 고유한 이름을 지정한 새 VM입니다. hello 이름은 3 자에서 15 자 사이의 문자를 포함, 수 문자, 숫자 및 하이픈을 포함 하 고 해야 시작 문자로 하 고 문자 또는 숫자로 끝나야 합니다. |
   | **VM 사용자 이름** |Hello 관리자 계정 hello VM에 사용할 사용자 이름을 지정 합니다. |
   | **VM 관리자 암호** |Hello 새 계정에 대 한 암호를 지정 합니다. |
   | **암호 확인** |Hello 새 계정의 hello 암호 확인 |
   | **Virtual Network** |Azure 가상 네트워크는 새 VM을 사용 해야 하는 hello hello를 지정 합니다. 가상 네트워크에 대한 자세한 내용은 [가상 네트워크 개요](../../../virtual-network/virtual-networks-overview.md)를 참조하세요. |
   | **가상 네트워크 서브넷** |새 VM을 사용 해야 하는 hello hello 가상 네트워크 서브넷 지정 |
   | **도메인** |Hello 도메인에 대 한 hello 미리 채워진된 값이 올바른지 확인 합니다. |
   | **도메인 사용자 이름** |Hello 로컬 클러스터 노드에서 hello 로컬 관리자 그룹에 해당 하는 계정을 지정 합니다. |
   | **암호** |Hello 도메인 사용자 이름에 대 한 hello 암호를 지정 합니다. |
8. 클릭 **확인** toovalidate hello 배포 설정 합니다.
9. 약관이 다음에 표시됩니다. 읽고 클릭 **확인** toothese 동의 하는 경우 용어입니다.
10. hello **복제본 지정** 페이지가 다시 표시 됩니다. Hello hello에 새 Azure 복제본에 대 한 hello 설정을 확인 **복제본**, **끝점**, 및 **백업 기본 설정** 탭 합니다. 비즈니스 요구 사항 설정 toomeet를 수정 합니다.  이러한 탭에 포함 된 hello 매개 변수에 대 한 자세한 내용은 참조 하십시오. [복제본 페이지 지정 (새 가용성 그룹 마법사/복제본 추가 마법사)](https://msdn.microsoft.com/library/hh213088.aspx)합니다. 수신기 Azure 복제본이 포함 된 가용성 그룹에 대 한 hello 수신기 탭을 사용 하 여 만들 수 없음을 note 합니다. 또한 수신기가 이미 생성 되어 이전 toolaunching hello 마법사 하는 경우 Azure에서 지원 되지 않음을 나타내는 메시지가 나타납니다. 방법을 살펴볼 toocreate 수신기 hello에 **가용성 그룹 수신기를 만드는** 섹션.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742865.png)
11. **다음**을 누릅니다.
12. Hello에 toouse 원하는 hello 데이터 동기화 방법 선택 **초기 데이터 동기화 선택** 페이지 클릭 하 여 **다음**합니다. 대부분의 시나리오에서 **전체 데이터 동기화**를 선택합니다. 데이터 동기화 방법에 대한 자세한 내용은 [최초 데이터 동기화 선택 페이지(Always On 가용성 그룹 마법사)](https://msdn.microsoft.com/library/hh231021.aspx)를 참조하세요.
13. Hello에 hello 결과 검토 **유효성 검사** 페이지. 미해결 문제를 수정 하 고 필요한 경우 hello 유효성 검사를 다시 실행 합니다. **다음**을 누릅니다.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742866.png)
14. Hello에서 hello 설정을 검토 **요약** 클릭 한 다음 페이지 **마침**합니다.
15. hello를 프로 비전 프로세스를 시작 합니다. Hello 마법사가 성공적으로 완료 되 면 클릭 **닫기** tooexit hello 마법사.

> [!NOTE]
> hello Azure 복제본 추가 마법사 로그 파일을 만듭니다 Users\User Name\AppData\Local\SQL Server\AddReplicaWizard에 있습니다. 이 로그 파일에 사용 되는 tootroubleshoot 하지 못했습니다 Azure 복제본 배포 될 수 있습니다. Hello 마법사에 실패 하면 모든 작업을 실행 하는 경우 모든 이전 작업이 롤백됩니다, 그리고 hello 삭제를 포함 하 여 VM을 프로 비전 합니다.
> 
> 

## <a name="create-an-availability-group-listener"></a>가용성 그룹 수신기 만들기
Hello 가용성 그룹을 만든 후 toohello 복제본 tooconnect 클라이언트에 대 한 수신기를 만들 해야 있습니다. 수신기는 들어오는 연결 tooeither hello 주 또는 읽기 전용 보조 복제본에 전달 합니다. 수신기에 대한 자세한 내용은 [Azure에서 Always On 가용성 그룹에 대한 ILB 수신기 구성](../classic/ps-sql-int-listener.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
또한 toousing hello에 **Azure 복제본 추가 마법사** tooextend 프로그램 Always On 가용성 그룹 tooAzure 일부 SQL Server 작업 부하를 이동할 수 있습니다 완전히 tooAzure 합니다. 시작 tooget 참조 [Azure에서 SQL Server 가상 컴퓨터를 프로 비전](../sql/virtual-machines-windows-portal-sql-server-provision.md)합니다.

다른 항목은 서로 관련 toorunning Azure Vm에서 SQL Server에 대 한 참조 [Azure 가상 컴퓨터에 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)합니다.

