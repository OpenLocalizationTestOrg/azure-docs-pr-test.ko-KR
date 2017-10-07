---
title: 'Azure Active Directory Connect: FAQ - | Microsoft Docs'
description: "이 페이지에는 Azure AD Connect에 대해 자주 묻는 질문과 대답이 있습니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a>Azure Active Directory Connect에 대한 질문과 대답

## <a name="general-installation"></a>일반 설치
**Q:는 설치 hello Azure AD 전역 관리자에 사용 하도록 설정 하는 2FA 유지 됩니까?**  
2016 년 2 월에서에서 hello 빌드와이 지원 됩니다.

**Q: 방식으로 tooinstall 무인된 Azure AD Connect는 무엇입니까?**  
지원 되는 tooinstall Azure AD Connect는 hello 설치 마법사를 사용 하 여 합니다. 무인 및 자동 설치는 지원되지 않습니다.

**Q: 하나의 도메인에 연결할 수 없는 포리스트가 있습니다. Azure AD Connect를 설치하려면 어떻게 하나요?**  
2016 년 2 월에서에서 hello 빌드와이 지원 됩니다.

**Q:는 server core에 AD DS 상태 에이전트 작업 hello?**  
예. Hello 에이전트를 설치한 후 다음 PowerShell cmdlet hello를 사용 하 여 hello 등록 프로세스를 완료할 수 있습니다. 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a>네트워크
**Q: 방화벽, 네트워크 장치 또는 내 네트워크 상의 열려 유지 될 수 있는 hello 최대 타임 연결을 제한 하는 다른 것입니다. Azure AD Connect를 사용하는 경우 클라이언트 쪽 기간 내 클라이언트 쪽 시간 제한 임계값은 얼마나 길어야 합니까?**  
모든 네트워킹 소프트웨어, 물리적 장치 라도 연결을 열어 둘 수 있는 최대 시간을 hello 사이의 연결을 위한 임계값이 적어도 5 분 (300 초)를 사용 해야 하는 제한 hello hello Azure AD Connect 클라이언트를 설치한 서버는 와 Azure Active Directory 합니다. 또한 이전에 출시 된 tooall Microsoft Id 동기화 도구의 적용 됩니다.

**Q: SLD(단일 레이블 도메인)가 지원되나요?**  
아니요 Azure AD Connect는 SLD를 사용하는 온-프레미스 포리스트/도메인을 지원하지 않습니다.

**Q: "마침표"를 포함하는 NetBios 이름이 지원되나요?**  
아니요, Azure AD Connect는 온-프레미스 포리스트/도메인이 hello NetBios 이름에 마침표가 있는 지원 하지 않는 "." hello 이름에서입니다.

## <a name="federation"></a>페더레이션
**Q: 어떻게 하나요 전자 메일을 내게 toorenew 요청 나타나는 경우 내 Office 365 인증서**  
Hello에 설명 된 hello 지침을 사용 하 여 [인증서 갱신](active-directory-aadconnect-o365-certs.md) toorenew 인증서 hello 하는 방법에 대 한 항목입니다.

**Q: O365 신뢰 당사자에 대해 "신뢰 당사자 자동 업데이트"를 설정했습니다. 용량은 tootake 조치 내 토큰 서명 인증서를 자동으로 위로 가져가면**  
Hello 문서에서 설명 하는 hello 지침을 사용 하 여 [인증서 갱신](active-directory-aadconnect-o365-certs.md)합니다.

## <a name="environment"></a>Environment
**Q: Azure AD Connect가 설치 된 후 it 지원 toorename hello 서버 인가요?**  
아니요. Hello 서버 이름 변경 원인을 hello 동기화 엔진 toonot 수 tooconnect toohello SQL 데이터베이스 수 및 hello 서비스 수 toostart 수 없습니다.

## <a name="identity-data"></a>ID 데이터
**Q: hello UPN (userPrincipalName) 특성을 Azure AD에 맞지 않는 온-프레미스 UPN-이유 hello?**  
아래 문서를 참조하세요.

* [사용자 이름에 Office 365, Azure 또는 Intune 일치 하지 않으면 hello 온-프레미스 UPN 또는 대체 로그인 ID](https://support.microsoft.com/en-us/kb/2523192)
* [Hello 사용자 계정 toouse 다른 페더레이션된 도메인의 UPN을 변경한 후 변경 내용은 hello Azure Active Directory 동기화 도구에서 동기화 되지 않습니다.](https://support.microsoft.com/en-us/kb/2669550)

에 설명 된 대로 Azure AD tooallow hello 동기화 엔진 tooupdate hello userPrincipalName 구성할 수도 있습니다 [Azure AD Connect 동기화 서비스 기능](active-directory-aadconnectsyncservice-features.md)합니다.

**Q: 기존 Azure AD 그룹/연락처 개체를 사용 하 여 AD 그룹/연락처 개체를 it 지원 toosoft 일치 온-프레미스 인가요?**  
아니요. 현재는 지원되지 않습니다.

**Q: ImmutableId 특성을 설정 하는 it 지원 toomanually은에 기존 Azure AD 그룹/연락처 개체 toohard 일치 tooon 온-프레미스 AD 그룹/연락처 개체?**  
아니요. 현재는 지원되지 않습니다.



## <a name="custom-configuration"></a>사용자 지정 구성
**Q: 문서화 하는 Azure AD Connect에 대 한 hello PowerShell cmdlet을 어디 입니까?**  
이 사이트에 설명 된 hello cmdlet의 hello 예외를 통해 Azure AD Connect에 다른 PowerShell cmdlet 사용 하 여 고객에 대 한 지원 되지 않습니다.

**Q:를 사용할 수 있습니까 "서버 내보내기/서버 가져오기"에서 찾을 *동기화 서비스 관리자* 서버 간에 toomove 구성?**  
아니요. 이 옵션은 모든 구성 설정을 가져오는 것이 아니므로 사용하지 말아야 합니다. 대신 두 번째 서버 hello에 hello 마법사 toocreate hello 기본 구성을 사용 하 고 hello 동기화 규칙 편집기 toogenerate PowerShell 스크립트 toomove 서버 간의 모든 사용자 지정 규칙을 사용 해야 합니다. [스윙 마이그레이션](active-directory-aadconnect-upgrade-previous-version.md#swing-migration)을 참조하세요.

**Q: hello Azure 로그인 페이지에 대 한 암호를 캐시할 수 및이 방지 hello 자동 완성 기능으로 암호 input 요소를 포함 하 고 있으므로 = 특성을 "false"?**</br>
현재 hello 암호 입력된 필드의 hello 자동 완성 태그를 포함 하 여 hello HTML 특성 수정을 지원 하지 않습니다. 현재 작업에서 사용자 지정 Javascript tooadd 있게 됩니다에 허용 하는 기능 특성 toohello 암호 필드입니다. 이 기능은 2017년 하반기에 제공될 예정입니다.

**Q: hello Azure 로그인 페이지에 이전에 성공적으로 로그인 하는 사용자에 대 한 사용자 이름이 표시 됩니다.  이 동작을 끌 수 있나요?**</br>
현재 hello 로그인 페이지의 hello HTML 특성 수정을 지원 하지 않습니다. 현재 작업에서 사용자 지정 Javascript tooadd 있게 됩니다에 허용 하는 기능 특성 toohello 암호 필드입니다. 이 기능은 2017년 하반기에 제공될 예정입니다.

**Q:는 방식으로 tooprevent 동시 세션 무엇입니까?**</br>
아니요.



## <a name="troubleshooting"></a>문제 해결
**Q: Azure AD Connect에 대한 도움을 받으려면 어떻게 합니까?**

[Hello Microsoft 기술 자료 (KB)를 검색 합니다.](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* Azure AD Connect에 대 한 지원에 대 한 기술 솔루션 toocommon 장애 수리 문제에 대 한 hello Microsoft 기술 자료 (KB)를 검색 합니다.

[Microsoft Azure Active Directory 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* 검색 하 고 기술 질문 및 답변 hello 커뮤니티에서 또는 사용자 고유의 질문을 클릭 하 여 찾아보려면 [여기](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required)합니다.

[Azure AD Connect 고객 지원](https://manage.windowsazure.com/?getsupport=true)

* Hello Azure 포털을 통해이 링크 tooget 지원을 사용 합니다.

