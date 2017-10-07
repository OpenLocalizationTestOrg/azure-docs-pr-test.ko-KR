---
title: "Configuration Manager tooLog 분석 aaaConnect | Microsoft Docs"
description: "이 문서에서는 분석 및 데이터 분석 시작 hello 단계 tooconnect Configuration Manager tooLog를 보여 줍니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f2298bd7-18d7-4371-b24a-7f9f15f06d66
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: dc50ebc46020a806d99d1a3e3d0e91fd09ad2c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-configuration-manager-toolog-analytics"></a>Configuration Manager tooLog 분석 연결
System Center Configuration Manager tooLog 분석 toosync 장치 컬렉션 데이터를 OMS에 연결할 수 있습니다. 이 경우 OMS에서 구성 관리자 계층 구조의 데이터를 사용할 수 있습니다.

## <a name="prerequisites"></a>필수 조건

Log Analytics는 System Center Configuration Manager 현재 분기, 1606 이상 버전을 지원합니다.  

## <a name="configuration-overview"></a>구성 개요
단계를 수행 하는 hello hello 프로세스 tooconnect Configuration Manager tooLog 분석 요약 되어 있습니다.  

1. Hello Azure 관리 포털에서에서 웹 응용 프로그램 및/또는 Web API 응용 프로그램으로 Configuration Manager에 등록 하 고 hello 클라이언트 ID와 클라이언트 암호 키에서 Azure Active Directory에서 hello 등록 했는지 확인 합니다. 참조 [포털 toocreate Active Directory 응용 프로그램 및 리소스에 액세스할 수 있는 서비스 보안 주체를 사용 하 여](../azure-resource-manager/resource-group-create-service-principal-portal.md) 방법에 대 한 자세한 내용은이 단계를 수행 합니다.
2. Hello Azure 관리 포털에서에서 [권한 tooaccess OMS에 Configuration Manager (hello 등록 된 웹 응용 프로그램)를 제공](#provide-configuration-manager-with-permissions-to-oms)합니다.
3. Configuration Manager에서 [hello OMS 연결 추가 마법사를 사용 하 여 연결을 추가할](#add-an-oms-connection-to-configuration-manager)합니다.
4. Configuration Manager에서 [hello 연결 속성을 업데이트](#update-oms-connection-properties) hello 암호 또는 클라이언트 비밀 키도 만료 되거나 손실 된 경우.
5. Hello OMS 포털의 정보와 함께 [다운로드 하 여 hello Microsoft Monitoring Agent 설치](#download-and-install-the-agent) hello Configuration Manager 서비스 연결을 실행 하는 hello 컴퓨터에서 지점 사이트 시스템 역할입니다. hello 에이전트에는 Configuration Manager 데이터 tooOMS 보냅니다.
6. Log Analytics에서 컴퓨터 그룹으로 [구성 관리자의 컬렉션을 가져옵니다](#import-collections).
7. Log Analytics에서 [컴퓨터 그룹](log-analytics-computer-groups.md)으로 구성 관리자에서 데이터를 봅니다.

자세한 내용은 Configuration Manager tooOMS에 연결 하는 방법에 대 한 [Configuration Manager toohello Microsoft Operations Management Suite에서 데이터 동기화](https://technet.microsoft.com/library/mt757374.aspx)합니다.

## <a name="provide-configuration-manager-with-permissions-toooms"></a>구성 관리자 사용 권한 tooOMS에 제공
hello 다음 절차에서는 사용 권한 tooaccess OMS와 hello Azure 관리 포털. Hello를 부여 해야 하는 구체적으로, *참가자 역할* toousers 순서 tooallow hello 리소스 그룹에 Azure 관리 포털 tooconnect Configuration Manager tooOMS hello 합니다.

> [!NOTE]
> 구성 관리자의 OMS에 사용 권한을 지정해야 합니다. 그렇지 않으면 받게 됩니다 오류 메시지가 hello 구성 마법사를 사용 하면 Configuration Manager에서.
>
>

1. 열기 hello [Azure 포털](https://portal.azure.com/) 클릭 **찾아보기** > **로그 분석 (OMS)** tooopen hello 로그 분석 (OMS) 블레이드입니다.  
2. Hello에 **로그 분석 (OMS)** 블레이드에서 클릭 **추가** tooopen hello **OMS 작업 영역** 블레이드입니다.  
   ![OMS 블레이드](./media/log-analytics-sccm/sccm-azure01.png)
3. Hello에 **OMS 작업 영역** 블레이드에서 hello 다음 정보를 제공 하 고 클릭 **확인**합니다.

   * **OMS 작업 영역**
   * **구독**
   * **리소스 그룹**
   * **위치**:
   * **가격 책정 계층**  
     ![OMS 블레이드](./media/log-analytics-sccm/sccm-azure02.png)  

     > [!NOTE]
     > 위의 hello 예제는 새 리소스 그룹을 만듭니다. hello 리소스 그룹에만 사용 되는 tooprovide Configuration Manager이 예에서 사용 권한 toohello OMS 작업 영역입니다.
     >
     >
4. 클릭 **찾아보기** > **리소스 그룹** tooopen hello **리소스 그룹** 블레이드입니다.
5. Hello에 **리소스 그룹** 블레이드에서 tooopen hello 위에서 만든 hello 리소스 그룹을 클릭 &lt;리소스 그룹 이름은&gt; 설정 블레이드에서 합니다.  
   ![리소스 그룹 설정 블레이드](./media/log-analytics-sccm/sccm-azure03.png)
6. Hello에 &lt;리소스 그룹 이름은&gt; 설정 블레이드에서 액세스 제어 (IAM) tooopen hello 클릭 &lt;리소스 그룹 이름은&gt; 사용자 블레이드입니다.  
   ![리소스 그룹 사용자 블레이드](./media/log-analytics-sccm/sccm-azure04.png)  
7. Hello에 &lt;리소스 그룹 이름은&gt; 사용자 블레이드 클릭 **추가** tooopen hello **액세스 추가** 블레이드입니다.
8. Hello에 **액세스 추가** 블레이드에서 클릭 **역할을 선택**를 클릭 한 hello **참가자** 역할입니다.  
   ![역할 선택](./media/log-analytics-sccm/sccm-azure05.png)  
9. 클릭 **사용자 추가**hello Configuration Manager 사용자 선택, 클릭, **선택**, 클릭 하 고 **확인**합니다.  
   ![사용자 추가](./media/log-analytics-sccm/sccm-azure06.png)  

## <a name="add-an-oms-connection-tooconfiguration-manager"></a>OMS 연결 tooConfiguration 관리자 추가
Configuration Manager 환경의 순서 tooadd OMS 연결에에서 있어야는 [서비스 연결 지점](https://technet.microsoft.com/library/mt627781.aspx) 온라인 모드에 대해 구성 합니다.

1. Hello에 **관리** 작업 영역 구성 관리자의 선택 **OMS 커넥터**합니다. Hello 열립니다 **OMS 연결 추가 마법사**합니다. **다음**을 선택합니다.
2. Hello에 **일반** 화면에서 확인 하 고 작업을 수행 하는 hello를 수행한 각 항목에 대 한 정보 포함 하 고 다음 선택 있습니다 **다음**합니다.

   1. Hello Azure 관리 포털에서 웹 응용 프로그램 및/또는 Web API 응용 프로그램으로 Configuration Manager에 등록 한 및 hello가 있는 [hello 등록에서 클라이언트 ID](../active-directory/active-directory-integrating-applications.md)합니다.
   2. Azure 관리 포털 hello hello Azure Active Directory에 등록 된 앱에 대 한 앱 암호 키를 만들었습니다.  
   3. Hello Azure 관리 포털에서에서 권한 tooaccess OMS와 hello 등록 된 웹 응용 프로그램을 제공 했습니다.  
      ![연결 tooOMS 마법사의 일반 페이지](./media/log-analytics-sccm/sccm-console-general01.png)
3. Hello에 **Azure Active Directory** 화면에서 제공 하 여 연결 설정 tooOMS 구성 프로그램 **테 넌 트** , **클라이언트 ID** , 및 **클라이언트 암호 키**  을 선택한 후 **다음**합니다.  
   ![연결 tooOMS 마법사 Azure Active Directory 페이지](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)
4. 하면 모든 hello 다른 프로시저가 성공적으로 수행, 하는 경우 다음 hello에 대 한 정보를 hello **OMS 연결 구성** 화면에 자동으로이 페이지에 나타납니다. 에 대 한 hello 연결 설정에 대 한 정보를 표시할지 프로그램 **Azure 구독** , **Azure 리소스 그룹** , 및 **Operations Management Suite 작업 영역**합니다.  
   ![연결 tooOMS 마법사 OMS 연결 페이지](./media/log-analytics-sccm/sccm-wizard-configure04.png)
5. hello 마법사 입력 한 hello 정보를 사용 하 여 toohello OMS 서비스를 연결 합니다. OMS와 함께 toosync 원하고 클릭 hello 장치 컬렉션 선택 **추가**합니다.  
   ![컬렉션 선택](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)
6. Hello에 연결 설정을 확인 **요약** 화면에서 선택한 다음 선택 **다음**합니다. hello **진행률** 화면 hello 연결 상태를 표시 한 후 해야 **완료**합니다.

> [!NOTE]
> OMS toohello 최상위 계층 사이트 계층 구조에 연결 해야 합니다. OMS tooa 독립 실행형 기본 사이트를 연결 하 고 중앙 관리 사이트 tooyour 환경을 추가 toodelete가 하 고 hello 새 계층 구조 내에서 hello OMS 연결을 다시 만드십시오.
>
>

Configuration Manager tooOMS에 연결한 후 추가 하 고 또는 컬렉션을 제거 하 고, hello OMS 연결의 hello 속성을 볼 수 있습니다.

## <a name="update-oms-connection-properties"></a>OMS 연결 속성 업데이트
암호 또는 클라이언트 비밀 키도 만료 되거나 손실 된 경우 toomanually hello OMS 연결 속성 업데이트 해야 합니다.

1. 구성 관리자에서 너무 이동**클라우드 서비스** 을 선택한 후 **OMS 커넥터** tooopen hello **OMS 연결 속성** 페이지.
2. 이 페이지에서 클릭 hello **Azure Active Directory** tooview 탭 프로그램 **테 넌 트**, **클라이언트 ID**, **클라이언트 비밀 키 만료**합니다. **클라이언트 비밀 키**가 만료되었는지 **확인**합니다.

## <a name="download-and-install-hello-agent"></a>Hello 에이전트 다운로드 및 설치
1. Hello OMS 포털에서 [OMS에서 hello 에이전트 설치 파일 다운로드](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms)합니다.
2. Hello tooinstall 메서드를 다음 중 하나를 사용 하 고 hello Configuration Manager 서비스 연결 지점 사이트 시스템 역할을 실행 하는 hello 컴퓨터에서 hello 에이전트를 구성 합니다.
   * [설치 프로그램을 사용 하 여 hello 에이전트 설치](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [Hello 명령줄을 사용 하는 hello 에이전트 설치](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [Azure 자동화에 DSC를 사용 하 여 hello 에이전트 설치](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a>컬렉션 가져오기
OMS 연결 tooConfiguration 관리자를 추가 하 고 hello 에이전트 설치 후 hello Configuration Manager 서비스 연결을 실행 하는 hello 컴퓨터에서 지점 사이트 시스템 역할, hello 다음 단계는 Configuration Manager에서 OMS에서 tooimport 컬렉션 컴퓨터 그룹입니다.

Hello 컬렉션 멤버 자격 정보를 검색할 가져오기를 활성화 된 후 모든 3 시간 tookeep hello 컬렉션 멤버 자격 현재 합니다. 언제 든 지 toodisable 가져오기를 선택할 수 있습니다.

1. Hello OMS 포털에서 클릭 **설정을**합니다.
2. Hello 클릭 **컴퓨터 그룹** 탭 클릭 한 후 hello **SCCM** 탭 합니다.
3. **구성 관리자 컬렉션 멤버 자격 가져오기**를 선택한 다음 **저장**을 클릭합니다.  
   ![컴퓨터 그룹 - SCCM 탭](./media/log-analytics-sccm/sccm-computer-groups01.png)

## <a name="view-data-from-configuration-manager"></a>구성 관리자의 데이터 보기
OMS 연결 tooConfiguration 관리자를 추가 하 고 hello Configuration Manager 서비스 연결 지점 사이트 시스템 역할을 실행 하는 hello 컴퓨터에 hello 에이전트를 설치, tooOMS hello 에이전트에서 데이터 전송 됩니다. OMS에서 구성 관리자 컬렉션이 [컴퓨터 그룹](log-analytics-computer-groups.md)으로 나타납니다. Hello에서 hello 그룹을 볼 수 **Configuration Manager** 페이지 **컴퓨터 그룹** 에 **설정을**합니다.

컬렉션은 가져온 hello, 후에 컬렉션 구성원 자격 컴퓨터 수를 검색을 볼 수 있습니다. Hello 가져온 컬렉션 수를 볼 수 있습니다.

![컴퓨터 그룹 - SCCM 탭](./media/log-analytics-sccm/sccm-computer-groups02.png)

둘 중 하나를 검색 열립니다를 클릭할 때 그룹 또는 tooeach 그룹에 속한 모든 컴퓨터를 가져온의 hello: 모두 표시 합니다. [로그 검색](log-analytics-log-searches.md)을 사용하여 구성 관리자 데이터의 자세한 분석을 시작할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* 사용 하 여 [로그 검색](log-analytics-log-searches.md) tooview Configuration Manager 데이터에 대 한 정보를 자세히 설명 합니다.
