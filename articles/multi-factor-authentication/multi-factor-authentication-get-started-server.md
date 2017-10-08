---
title: "aaaGetting Azure Multi-factor Authentication 서버를 시작 | Microsoft Docs"
description: "Tooget Azure MFA 서버를 시작 하는 방법을 설명 하는 hello Azure multi-factor authentication 페이지입니다."
services: multi-factor-authentication
keywords: "인증 서버, Azure Multi Factor Authentication 앱 활성화 페이지, 인증 서버 다운로드"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: e94120e4-ed77-44b8-84e4-1c5f7e186a6b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 92a6a586eb96375e92a9455ad64e67221001db81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-multi-factor-authentication-server"></a>Azure Multi-factor Authentication 서버 hello로 시작

<center>![MFA 온-프레미스](./media/multi-factor-authentication-get-started-server/server2.png)</center>

Toouse 온-프레미스 Multi-factor Authentication 서버를 결정 했으므로 출발 합니다. 이 페이지에서는 hello 서버와 온-프레미스 Active directory 설정의 새 설치에 설명 합니다. Hello MFA 서버 설치 이미 있고 tooupgrade 확인 하려는 경우 참조 [toohello 업그레이드 최신 Azure Multi-factor Authentication 서버](multi-factor-authentication-server-upgrade.md)합니다. 방금 hello 웹 서비스 설치에 대 한 내용은 찾고 있는 경우 참조 [배포 hello Azure Multi-factor Authentication 서버 모바일 앱 웹 서비스](multi-factor-authentication-get-started-server-webservice.md)합니다.

## <a name="plan-your-deployment"></a>배포 계획

Hello Azure Multi-factor Authentication 서버를 다운로드 하기 전에 부하 및 고가용성 요구 사항 이란에 대해 생각 합니다. 이 정보 toodecide 위치와 방법을 사용 하 여 toodeploy 합니다.

좋은 지침은 정기적으로 tooauthenticate 원하는 hello 필요한 메모리 양은 사용자 수가 hello에 대 한 합니다.

| 사용자 | RAM |
| ----- | --- |
| 1-10,000 | 4GB |
| 10,001-50,000 | 8GB |
| 50,001-100,000 | 12GB |
| 100,000-200,001 | 16GB |
| 200,001+ | 32GB |

고가용성을 위해 여러 서버를 tooset 필요 하거나 부하 분산 수행 했습니까? 이 구성을 Azure MFA 서버와 같은 방법으로 tooset의 여러 가지가 있습니다. 첫 번째 Azure MFA 서버를 설치 하면 hello 마스터 됩니다. 서버를 더 하위 수준 해지고 hello 마스터와 사용자 및 구성 작업을 자동으로 동기화 합니다. 그런 다음 주 서버를 구성할 수 있으며 역할 hello rest는 백업 또는 있습니다 모든 hello 서버 간의 부하 분산을 설정할 수 있습니다.

Azure MFA 서버 마스터 되 면 오프 라인, 하위 서버 hello 계속 프로세스 2 단계 확인 요청 수입니다. 그러나 추가할 수 없는 새 사용자 및 기존 사용자 hello 마스터는 온라인 또는 하위 항목이 승격 될 때까지 해당 설정을 업데이트할 수 없습니다.

### <a name="prepare-your-environment"></a>환경 준비

Azure Multi-factor Authentication을 사용 하는 hello 서버 hello 요구 사항을 준수를 충족 해야 합니다.

| Azure Multi-Factor Authentication 서버 요구 사항 | 설명 |
|:--- |:--- |
| 하드웨어 |<li>200MB의 하드 디스크 공간</li><li>x32 또는 x64 지원 프로세서</li><li>1GB 이상 RAM</li> |
| 소프트웨어 |<li>Windows Server 2008 이상이 hello 호스트 서버인 경우 운영 체제</li><li>Windows 7 또는 hello 호스트는 클라이언트 OS 증가 하면</li><li>Microsoft .NET 4.0 Framework</li><li>IIS 7.0 또는 설치 하는 경우 큰 hello 사용자 포털 또는 웹 서비스 SDK</li> |

### <a name="azure-mfa-server-components"></a>Azure MFA 서버 구성 요소

Azure MFA 서버를 구성하는 세 가지 웹 구성 요소가 있습니다.

* 웹 서비스 SDK-통신할 때 다른 구성 요소를 hello 및 hello Azure MFA 응용 프로그램 서버에 설치 되어 사용 하도록 설정
* 사용자 포털-사용자가 tooenroll Azure Multi-factor Authentication (MFA)를 허용 하 고 자신의 계정을 관리할 수 있는 IIS 웹 사이트입니다.
* 모바일 앱 웹 서비스-2 단계 인증에 대 한 hello Microsoft Authenticator 앱 처럼 모바일 앱을 사용할 수 있습니다.

Hello에 모든 세 가지 구성 요소를 설치할 수 있습니다 동일한 서버 hello 서버는 인터넷에 연결 하는 경우. 웹 서비스 SDK hello hello Azure MFA 응용 프로그램 서버에 설치 된 hello 구성 요소를 해제 하는 경우 및 hello 사용자 포털 및 모바일 앱 웹 서비스는 인터넷 연결 서버에 설치 됩니다.

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a>Azure Multi-Factor Authentication 방화벽 요구 사항

각 MFA 서버 포트 443 아웃 바운드 toohello 주소 다음에 수 toocommunicate 해야 합니다.

* https://pfd.phonefactor.net
* https://pfd2.phonefactor.net
* https://css.phonefactor.net

포트 443에서 아웃 바운드 방화벽이 제한 된, hello 다음 IP 주소 범위를 엽니다.

| IP 서브넷 | 네트워크 마스크 | IP 범위 |
|:---: |:---: |:---: |
| 134.170.116.0/25 |255.255.255.128 |134.170.116.1 – 134.170.116.126 |
| 134.170.165.0/25 |255.255.255.128 |134.170.165.1 – 134.170.165.126 |
| 70.37.154.128/25 |255.255.255.128 |70.37.154.129 – 70.37.154.254 |

Hello 이벤트 확인 기능을 사용 하지 않는 경우 사용자가 장치에서 모바일 앱 tooverify를 hello 회사 네트워크에서 사용 하지 않는 hello 범위를 수행 하면 됩니다.

| IP 서브넷 | 네트워크 마스크 | IP 범위 |
|:---: |:---: |:---: |
| 134.170.116.72/29 |255.255.255.248 |134.170.116.72 – 134.170.116.79 |
| 134.170.165.72/29 |255.255.255.248 |134.170.165.72 – 134.170.165.79 |
| 70.37.154.200/29 |255.255.255.248 |70.37.154.201 – 70.37.154.206 |

## <a name="download-hello-azure-multi-factor-authentication-server"></a>Hello Azure Multi-factor Authentication 서버 다운로드

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.
2. Hello 왼쪽에서 선택 **Active Directory**
3. **사용자 및 그룹**을 클릭합니다.
4. **모든 사용자**를 클릭합니다.
5. **Multi-Factor Authentication**을 클릭합니다.
6. **Multi-Factor Authentication** 섹션 아래에서 **서비스 설정**을 선택합니다.

   ![서비스 설정 페이지](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. Hello 서비스 설정 페이지에서 클릭에 hello hello 화면 맨 아래에 **Go toohello 포털**합니다. 새 페이지가 열립니다.
7. **다운로드**를 클릭합니다.
8. Hello 클릭 **다운로드** 연결 하 고 hello 설치 관리자를 저장 합니다.

   ![MFA 서버 다운로드](./media/multi-factor-authentication-get-started-server/download4.png)

9. 이 페이지 하므로 계속 열어둡니다 tooit hello 설치 관리자를 실행 한 후 이라고 합니다.

## <a name="install-and-configure-hello-azure-multi-factor-authentication-server"></a>설치 하 고 hello Azure Multi-factor Authentication 서버를 구성 합니다.

다운로드 한 hello 서버를 설치 하 고 구성할 수 있습니다. 해당 hello 서버에 설치 하는 hello 계획 섹션에에서 나열 된 요구 사항을 충족 해야 합니다.

1. Hello 실행 파일을 두 번 클릭 합니다.
2. Hello 설치 폴더 선택 화면에서 해당 hello 폴더가 올바른지 확인 하 고 클릭 **다음**합니다.
3. Hello 설치가 완료 되 면 클릭 **마침**합니다.  hello 구성 마법사를 시작합니다.
4. Hello 구성 마법사 시작 화면에서 확인 **Skip을 사용 하 여 hello 인증 구성 마법사** 클릭 **다음**합니다.  hello 마법사가 닫히고 hello 서버를 시작 합니다.

   ![클라우드](./media/multi-factor-authentication-get-started-server/skip2.png)

5. 다시 hello 페이지 hello 서버에서 다운로드 한 म 클릭 hello **활성화 자격 증명 생성** 단추입니다. 제공 된 hello 상자에 Azure MFA 서버 hello에이 정보를 복사 하 고 클릭 **Activate**합니다.

## <a name="send-users-an-email"></a>사용자에게 전자 메일 보내기

tooease 롤아웃, 사용자와 MFA 서버 toocommunicate 허용 합니다. MFA 서버에서 전자 메일 tooinform를 보낼 수에 2 단계 인증에 등록 되어 있습니다.

hello 전자 메일을 보내는 2 단계 인증에 대 한 사용자가 구성 하는 방법가 확인 해야 합니다. 예를 들어 hello 회사 디렉터리에서 전화 번호 수 tooimport 인 경우 사용자가 어떤 tooexpect 알 수 있도록 hello 전자 메일 hello 기본 전화 번호를 포함 되어야 합니다. 전화 번호를 가져오지 않으면 또는 사용자가 toouse hello 모바일 응용 프로그램 의도 보냅니다 toocomplete 안내 전자 메일 계정 등록. Hello 전자 메일에 하이퍼링크 toohello Azure Multi-factor Authentication 사용자 포털을 포함 합니다.

hello 전자 메일의 hello 콘텐츠 hello 사용자 (전화 통화, SMS 또는 모바일 앱)에 대해 설정 된 확인의 hello 방법에 따라 달라 집니다.  예를 들어 hello에서 사용자가 경우 필요한 toouse PIN 인증 시 hello 전자 메일 ¿ë à ú으로 어떤 초기 PIN 설정 되었습니다.  사용자가 해당 첫 번째 확인 하는 동안 필요한 toochange PIN 됩니다.

### <a name="configure-email-and-email-templates"></a>전자 메일 및 전자 메일 템플릿 구성

이러한 전자 메일을 보내기 위한 hello 설정이 왼쪽된 tooset hello에 hello 전자 메일 아이콘을 클릭 합니다. 이 페이지는 hello를 확인 하 여 메일 서버와 송신 전자 메일의 SMTP hello 정보를 입력할 수 있는 **송신 toousers 전자 메일로** 확인란 합니다.

![MFA 서버 전자 메일 구성](./media/multi-factor-authentication-get-started-server/email1.png)

Hello 전자 메일 내용 탭에서 사용할 수 있는 toochoose 있는 hello 전자 메일 템플릿을 볼 수 있습니다. 사용자가 한 tooperform 2 단계 확인을 구성 방식에 따라 하기에 가장 적합 한 hello 템플릿을 선택 합니다.

![MFA 서버 전자 메일 템플릿](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a>Active Directory에서 사용자 가져오기

해당 hello 서버가 설치 되어 이제 tooadd 사용자 해야 합니다. Toocreate 수동으로 Active Directory에서 사용자 가져오기 또는 Active Directory와 자동된 동기화를 구성할 수 있습니다.

### <a name="manual-import-from-active-directory"></a>Active Directory에서 수동 가져오기

1. Azure MFA 서버 hello hello 왼쪽에서 선택 **사용자**합니다.
2. Hello 맨 아래에 선택 **Active Directory에서 가져오기**합니다.
3. 이제 검색할 수 있습니다 하거나 개별 사용자 또는 검색 hello AD 디렉터리에 대 한 Ou에 대 한 해당 사용자와.  이 경우 hello 사용자 OU 지정합니다.
4. Hello 오른쪽에 있는 모든 hello 사용자를 강조 표시 하 고 클릭 **가져오기**합니다.  성공했음을 알려주는 팝업 메시지가 나타납니다.  닫기 hello 가져오기 창입니다.

   ![MFA 서버 사용자 가져오기](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a>Active Directory와 자동 동기화

1. Azure MFA 서버 hello hello 왼쪽에서 선택 **디렉터리 통합**합니다.
2. Toohello 이동 **동기화** 탭 합니다.
3. Hello 맨 아래에 선택 **추가**
4. Hello에 **동기화 항목 추가** 나타나는 상자 선택 hello 도메인 OU **또는** 보안 그룹, 설정, 방법 기본값 및이 동기화에 대 한 기본 언어는 작업 및 클릭**추가**합니다.
5. 레이블이 hello 확인란 **Active Directory와 동기화 사용** 선택 하 고는 **동기화 간격** 1 분에서 24 시간 사이입니다.

## <a name="how-hello-azure-multi-factor-authentication-server-handles-user-data"></a>Hello Azure Multi-factor Authentication 서버에서 사용자 데이터를 처리 하는 방법

Hello Multi-factor Authentication (MFA) 서버 온-프레미스를 사용 하면 사용자의 데이터는 hello 온-프레미스 서버에 저장 됩니다. 영구 사용자 데이터가 없으며 hello 클라우드에 저장 됩니다. Hello 사용자 2 단계 인증을 수행 하는 경우 MFA 서버 hello 데이터 toohello Azure MFA 클라우드 서비스 tooperform hello 확인을 보냅니다. 이러한 인증 요청 toohello 클라우드 서비스를 보내면 hello 다음 필드 보내집니다 hello 요청 및 로그 hello 고객의 인증/사용 현황 보고서에 사용할 수 있도록 합니다. Hello 필드 중 일부는 선택 사항 이므로 사용 하도록 설정 하거나 hello Multi-factor Authentication 서버 내에서 사용 하지 않도록 설정 수 있습니다. 포트 443 아웃 바운드 통한 SSL/TLS를 사용 하는 hello와 MFA 서버 toohello MFA 클라우드 서비스에서에서 hello 통신 합니다. 이러한 필드는 다음과 같습니다.

* 고유 ID - 사용자 이름 또는 내부 MFA 서버 ID 
* 이름과 성(선택 사항)
* 메일 주소(선택 사항)
* 전화 번호 - 음성 통화 또는 SMS 인증을 수행할 때
* 장치 토큰 - 모바일 앱 인증을 수행할 때
* 인증 모드
* 인증 결과
* MFA 서버 이름
* MFA 서버 IP
* 클라이언트 IP - 사용 가능한 경우

또한 toohello 위의 필드 hello 확인 결과 (성공/거부) 및 사유 hello 인증 데이터로 저장 되 고 hello 인증/사용 보고서를 통해 사용 가능한도 됩니다.

## <a name="back-up-and-restore-azure-mfa-server"></a>Azure MFA 서버 백업 및 복원

양호한 백업 한지 확인 하는 모든 시스템으로는 중요 한 단계 tootake입니다.

Azure MFA 서버를 설치한 tooback hello의 복사본을가지고 있는지 확인 하십시오. **C:\Program Files\multi-factor Authentication Server\Data** hello를 포함 하 여 폴더 **PhoneFactor.pfdata** 파일입니다. 

경우에는 복원에는 필요한 전체 hello 다음 단계:

1. 새 서버에 Azure MFA 서버를 다시 설치합니다.
2. 활성화 새 Azure MFA 서버 hello 합니다.
3. Stop hello **MultiFactorAuth** 서비스입니다.
4. Hello 덮어쓰기 **PhoneFactor.pfdata** 복사본을 백업 하는 hello로 합니다.
5. Hello 시작 **MultiFactorAuth** 서비스입니다.

새 서버 hello 지금 실행 되 고 hello 원래 백업 구성 및 사용자 데이터를 사용 합니다.

## <a name="next-steps"></a>다음 단계

- 설정 및 구성 hello [사용자 포털](multi-factor-authentication-get-started-portal.md) 셀프 서비스 사용자에 대 한 합니다.
- 설정 및 구성 Azure MFA 서버 함께 사용 hello [Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md), [RADIUS 인증](multi-factor-authentication-get-started-server-radius.md), 또는 [LDAP 인증](multi-factor-authentication-get-started-server-ldap.md)합니다.
- [RADIUS를 사용하여 원격 데스크톱 게이트웨이 및 Azure Multi-Factor Authentication 서버](multi-factor-authentication-get-started-server-rdg.md)를 설정 및 구성합니다.
- [Hello Azure Multi-factor Authentication 서버 모바일 앱 웹 서비스를 배포](multi-factor-authentication-get-started-server-webservice.md)합니다.
- [Azure Multi-Factor Authentication 및 타사 VPN을 사용한 고급 시나리오](multi-factor-authentication-advanced-vpn-configurations.md)
