---
title: "aaaAzure 데이터 카탈로그 릴리스 정보 | Microsoft Docs"
description: "Azure Data Catalog에 대한 릴리스 정보입니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a>Azure 데이터 카탈로그 릴리스 정보
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a>Azure Data catalog hello 2015 년 11 월 20 일 릴리스에 대 한 정보
### <a name="opening-data-sources-in-power-bi-desktop"></a>Power BI Desktop에서 데이터 원본 열기
Hello에서 hello "열기에 Power BI Desktop" 옵션을 사용 하는 경우 **Azure Data Catalog** 포털에서 사용자가 발생할 수 hello Power BI Desktop 응용 프로그램의에서 두 가지 문제 중 하나:

* Hello 제목의 "없습니다 tooOpen 문서" 대화 상자가 표시 됩니다.
* Power BI Desktop 응용 프로그램 hello 열리지만 hello 파일이 빈 toobe 나타납니다.

각 상황에 대 한 hello 문제를 해결할 수 다운로드 하 여 hello에서 Power BI Desktop의 최신 버전을 설치 [PowerBI.com](https://powerbi.com)합니다.

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a>Azure Data catalog hello 2015 년 11 월 13 일 릴리스에 대 한 정보
### <a name="registering-and-connecting-tooteradata"></a>등록 하 고 tooTeradata 연결
TooTeradata hello 올바른 Teradata ODBC 드라이버 사용자가 설치 되어 있어야 하는 데이터 원본 사용 중인 hello 소프트웨어의 hello 비트 (32 비트 또는 64 비트)와 일치 연결할 때 합니다.

이 ADC를 기준으로 출시 날짜, 가장 최근의 hello [Teradata ODBC 드라이버 (버전 15.10) windows 용](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) 호환 되는 Office 2013 있고 Office 2016을 사용 하지 않습니다.

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a>Azure Data catalog hello 2015 년 7 월 13 일 릴리스에 대 한 정보
### <a name="registering-and-connecting-toooracle-database"></a>등록 하 고 tooOracle 데이터베이스 연결
때 tooOracle 데이터베이스 데이터 원본을 사용자 연결 설치 되어 있어야 사용 중인 hello 소프트웨어의 hello 비트 (32 비트 또는 64 비트)와 일치 하는 hello 올바른 Oracle 드라이버.

* Hello 32 비트 Oracle 드라이버가 32 비트 Windows를 실행 하는 컴퓨터에서 Oracle 데이터 소스를 등록할 때 사용 됩니다.
* Hello 64 비트 Oracle 드라이버가 64 비트 Windows를 실행 하는 컴퓨터에서 Oracle 데이터 소스를 등록할 때 사용 됩니다.
* Hello 32 비트 버전의 Microsoft Office를 실행 하는 컴퓨터에서 Excel을 사용 하 여 tooOracle 데이터 원본에 연결할 때 64 비트 Windows에 포함 하 여 hello 32 비트 Oracle 드라이버가 사용 됩니다.
* Hello 64 비트 Oracle 드라이버가 hello 64 비트 버전의 Microsoft Office를 실행 하는 컴퓨터에서 Excel을 사용 하 여 tooOracle 데이터 원본에 연결할 때 사용 됩니다.

### <a name="registering-and-connecting-toosql-server-reporting-services"></a>등록 하 고 tooSQL 서버 Reporting Services에 연결
SQL Server Reporting Services (SSRS) 데이터 원본에 대 한 지원은 현재 제한 tooNative 모드 서버에만 합니다. SharePoint 모드에서 SSRS 지원은 이후 릴리스에 추가됩니다.

### <a name="opening-data-assets-in-excel"></a>Excel에서 데이터 자산 열기
Hello에서 Microsoft Excel에서 데이터 자산을 열 때 **Azure Data Catalog** 포털에서 사용자가 표시 될 수도 있습니다는 **Microsoft Excel 보안 알림** 대화 상자. Standard,이 예상 된 동작이 며 사용자가 선택할 수 **사용** toocontinue 합니다.

자세한 내용은 [의심스러운 웹 사이트의 링크 및 파일에 대한 보안 경고 사용 또는 사용 안 함](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE)을 참조하세요.

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a>프록시 및 정책 구성과 데이터 원본 등록
사용자가 toohello Azure Data Catalog 포털에 있지만 toolog 로그온 수 없도록 하는 오류 메시지가 발생 하는 toohello 데이터 원본 등록 도구에서 시도할 때 로그인 수 할 상황이 발생할 수 있습니다.

이 문제 동작에는 다음과 같은 잠재적인 두 가지 원인이 있습니다.

**원인 1: Active Directory Federation Services 구성** hello 데이터 원본 등록 도구는 Active Directory에 대해 폼 인증 toovalidate 사용자 로그온을 사용 합니다. 성공적인 로그온에 대 한 Active Directory 관리자도 폼 인증 hello 전역 인증 정책에서에서 활성화 해야 합니다.

경우에 따라이 오류 동작 hello 사용자 hello 회사 네트워크에 있을 경우에 또는 hello 사용자가 외부 hello 회사 네트워크에서 연결 하는 경우에 발생할 수 있습니다. 전역 인증 정책 hello 인트라넷 및 익스트라넷 연결에 대해 별도로 사용 하는 인증 방법 toobe를 수 있습니다. 로그온 오류 hello 네트워크는 hello에서 사용자가 연결에 대 한 폼 인증을 사용 하지 않는 경우에 발생할 수 있습니다.

자세한 내용은 [인증 정책 구성](https://technet.microsoft.com/library/dn486781.aspx)을 참조하세요.

**2 원인: 네트워크 프록시 구성** hello 프록시를 통해 수 tooconnect tooAzure Active Directory hello 회사 네트워크에서 프록시 서버를 사용 하는 경우 hello 등록 도구 수 없습니다. 사용자가이 섹션 toohello 파일을 추가 해당 hello 등록 도구 hello 도구의 구성 파일을 편집 하 여 확인할 수 있습니다.

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


toolocate hello RegistrationTool.exe.config 파일 hello 등록 도구를 실행 한 다음 hello Windows 작업 관리자 유틸리티를 엽니다. Hello 세부 정보 탭에서 작업 관리자를 RegistrationTool.exe를 마우스 오른쪽 단추로 클릭 하 고 hello 팝업 메뉴에서 파일 위치 열기를 선택 합니다.
