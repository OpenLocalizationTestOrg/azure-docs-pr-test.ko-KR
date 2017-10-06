---
title: 'FAQ: Azure AD SSPR | Microsoft Docs'
description: "Azure AD 셀프 서비스 암호 재설정에 대해 자주 묻는 질문과 대답"
services: active-directory
keywords: "Active Directory 암호 관리, 암호 관리, Azure AD 셀프 서비스 암호 재설정"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a>암호 관리 질문과 대답

모든 것 관련 toopassword 다시 설정에 대 한 hello 다음은 몇 가지 질문과 대답된 질문 합니다.

Azure AD에 대 한 일반적인 질문이 있는 경우 및 셀프 서비스 암호 재설정 응답이 여기는 hello 커뮤니티 지원에 요청 hello [Azure Ad 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD)합니다. Hello 커뮤니티 구성원 엔지니어, 제품 관리자, Mvp 및 친구 IT 전문가 포함합니다.

이 FAQ는 hello 다음 섹션으로 분할 됩니다.

* [**암호 재설정 등록에 대한 질문**](#password-reset-registration)
* [**암호 재설정에 대한 질문**](#password-reset)
* [**암호 변경에 대한 질문**](#password-change)
* [**암호 관리 보고서에 대한 질문**](#password-management-reports)
* [**비밀번호 쓰기 저장에 대한 질문**](#password-writeback)

## <a name="password-reset-registration"></a>암호 재설정 등록
* **Q: 내 사용자가 자신의 암호 재설정 데이터를 등록할 수 있습니까?**

  > **A:** 예, 암호 재설정이 활성화 되 고 사용이 허가 됩니다, 것 toohello 암호 재설정 등록 포털 http://aka.ms/ssprsetup tooregister에 해당 인증 정보입니다. Hello 프로필 탭을 클릭 하 고 암호 재설정 옵션에 대 한 hello 레지스터를 클릭 하면 사용자가 http://myapps.microsoft.com, toohello 액세스 패널로 이동 하 여 등록할 수도 있습니다.
  >
  >
* **Q: 내 사용자 대신 암호 재설정 데이터를 정의할 수 있습니까?**

  > **A:** 예, 이렇게 하려면 Azure AD Connect PowerShell hello로 [Azure 포털](https://portal.azure.com), 또는 hello Office 관리 포털. 자세한 내용은 hello 문서 참조 [Azure AD 셀프 서비스 암호 재설정 사용 되는 데이터](active-directory-passwords-data.md)합니다.
  >
  >
* **Q: 온-프레미스에서 보안 질문에 대한 데이터를 동기화 할 수 있습니까?**

  > **A:** 현재 불가능합니다.
  >
  >
* **Q: 내 사용자가 다른 사용자가 이 데이터를 볼 수 없는 방식으로 데이터를 등록할 수 있습니까?**

  > **A:** 예, 사용자 에게만 전역 관리자 및 hello 사용자가 표시 되는 개인 인증 필드에 암호 재설정 등록 포털로 저장 된 hello를 사용 하 여 데이터를 등록 합니다.
    >
    > [!NOTE]
    > 경우는 **Azure 관리자 계정** hello 휴대폰 필드에 채워집니다도 표시 되 고 인증 전화 번호를 등록 합니다.
    >
  >
  >
* **Q: 내 사용자가 암호 재설정을 사용 하기 전에 등록 toobe를 있습니까?**

  > **A:** 아니요, 대신에 충분 한 인증 정보를 정의 하면 사용자가 없는 tooregister 합니다. 암호 재설정이 작동 하는 상태로 제대로 hello hello 디렉터리에 적절 한 필드에 저장 된 데이터의 서식을 지정 했습니다.
  >
  >
* **Q: 동기화 하거나 내 사용자를 대신 하 여 hello 인증 전화, 인증 전자 메일 또는 대체 인증 전화 필드를 설정 합니다. 수 있습니까?**

  > **A:** 현재 불가능합니다.
  >
  >
* **Q: 어떻게는 hello 등록 포털 알 수 있는 옵션 tooshow 내 사용자가?**

  > **A:** hello 암호 재설정 등록 포털에서는 사용자에 대해 설정한 옵션 hello만 합니다. 이러한 옵션은 디렉터리의 구성 탭의 사용자 암호 재설정 정책 섹션 hello 있습니다. 예를 들어,이 보안 질문을 사용 하지 않도록 하는 경우 다음 사용자가 없으면 수 tooregister 해당 옵션에 대 한 의미 합니다.
  >
  >
* **Q: 사용자가 등록된 것으로 간주되는 경우는 언제입니까?**

  > **A:** 등록 한 경우 SSPR에 등록 된 것으로 간주 이상 hello **메서드 필요한 tooreset 수가** hello에 설정 된 [Azure 포털](https://portal.azure.com)합니다.
  >
  >
## <a name="password-reset"></a>암호 재설정
* **Q:는 전자 메일, SMS 또는 전화 통화 암호 재설정에서 tooreceive를 대기 해야는 시간**

  > **A:** 전자 메일, SMS 메시지가 고 전화 통화 5-20 초 동안 hello 일반적인 경우와 1 분 미만에 도착 해야 합니다.
    >이 시간 내에 hello 알림을 나타나지 않습니다.
        > * 정크 메일 폴더를 확인합니다.
        > * Hello 수 확인 또는 연결할 수 없거나 전자 메일은 hello 예상 하나입니다.
        > * Hello 디렉터리의 hello 인증 데이터 형식이 올바로 확인 합니다.
                >     * 예: "+1 4255551234" 또는 "user@contoso.com"
  >
  >
* **Q: 암호 재설정에서 지원되는 언어는 무엇입니까?**

  > **A:** 암호 재설정 UI, SMS 메시지 및 음성 hello 호출 hello로 지역화 된 Office 365에서 지원 되는 동일한 언어입니다.
  >
  >
* **Q: 조직 내 디렉터리에 대 한 브랜딩 설정 하는 경우 hello 암호 재설정 환경의 어떤 부분 브랜드 가져오기의 구성 탭?**

  > **A:** hello 암호 재설정 포털에서 조직 로고를 보여주며 tooconfigure hello 연락처 관리자 링크 toopoint tooa 사용자 지정 메일 또는 URL 있습니다. 암호 재설정에서 보내는 전자 메일 hello 전자 메일의 hello 본문에 조직 로고, 색상, 이름이 포함 및 이름에서 사용자 지정 합니다.
  >
  >
* **Q: 어떻게 수 합니까 내 사용자에 게 교육 where toogo tooreset 암호?**

  > **A:** 사용자 toohttps://passwordreset.microsoftonline.com를 직접 보내거나 tooclick hello 지시할 수 **계정 링크에 액세스할 수 없습니다** 페이지에 있는 모든 회사 또는 학교에 로그인 합니다. 전체 tooyour 쉽게 액세스할 수 있는 사용자가 이러한 링크를 게시할 수도 있습니다.
  >
  >
* **Q: 모바일 장치에서 이 페이지를 사용할 수 있습니까?**

  > **A:** 예, 이 페이지는 모바일 장치에서 작동합니다.
  >
  >
* **Q: 사용자가 암호를 재설정할 때 로컬 활성 디렉터리 계정 잠금해제를 지원합니까?**

  > **A:** 예, 사용자가 자신의 암호를 재설정하고 Azure AD Connect를 사용하여 비밀번호 쓰기 저장을 배포한 경우 암호를 재설정할 때 해당 사용자의 계정은 자동으로 잠금이 해제됩니다.
  >
  >
* **Q: 암호 재설정을 내 사용자의 데스크톱 로그인 환경으로 직접 통합하려면 어떻게 해야 합니까?**

  > **A:** Azure AD Premium 고객 인 경우 추가 비용 없이 Microsoft Identity Manager를 설치 하 고 hello 온-프레미스 암호 다시 설정 솔루션 toomeet이 요구이 사항을 배포할 수 있습니다.
  >
  >
* **Q: 서로 다른 로캘로 다른 보안 질문을 설정할 수 있습니까?**

  > **A:** 현재 불가능합니다.
  >
  >
* **Q: 몇 개의 질문 hello 보안 질문 인증 옵션에 대해 구성할 수 있습니다?**

  > **A:** hello에 too20 사용자 지정 보안 질문을 구성할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다.
  >
  >
* **Q: 질문의 길이는 어떻게 설정할 수 있습니까?**

  > **A:** 보안 질문은 3자에서 200자 사이일 수 있습니다.
  >
  >
* **Q: 얼마나 답변 toosecurity 질문 수? 있습니다.**

  > **A:** 대답이 3 too40 자 수 있습니다.
  >
  >
* **Q: 중복 된 답변 toosecurity 질문 거부?**

  > **A:** 예, 중복 된 답변 toosecurity 질문 거부 합니다.
  >
  >
* **Q: 월 사용자 레지스터 hello 동일한 보안 질문에 두 번 이상?**

  > **A:** 아니요, 사용자가 특정 질문을 등록하면 해당 질문을 두 번 등록할 수 없습니다.
  >
  >
* **Q: 가능한 tooset 등록 및 재설정에 대 한 보안 질문의 최소 제한을 입니까?**

  > **A:** 예, 등록에 대해 하나의 제한, 재설정에 대해 또 하나의 제한을 설정할 수 있습니다. 3-5개의 보안 질문을 등록해야 하며 3-5개 질문은 재설정을 위해 필요할 수 있습니다.
  >
  >
* **Q: 사용자가 질문 필요한 tooreset hello 최대 개수 보다 많은 등록 경우 보안 질문 선택 방법을 재설정 하는 동안?**

  > **A:** N 보안 질문은 hello 총 사용자 질문 수 중 임의로 선택 하기 위해 등록, 여기서 N은 hello **질문 필요한 tooreset 수가**합니다. 예를 들어 사용자에 게 5 개의 보안 질문을 등록 하는 경우 3 개만 필요 tooreset는 hello 5의 3 임의로 선택 되어 표시 됩니다 다시 설정에서 합니다. Hello 사용자 가져오는 hello 답변 toohello 질문 잘못 된 경우 hello 선택 프로세스 tooprevent 질문 공세 다시 발생 합니다.
  >
  >
* **Q: 사용자가 짧은 기간 내에 여러 번 암호 재설정을 시도하지 못합니까?**

  > **A:** 예, 잘못 사용 되지 않도록에서 암호 재설정 tooprotect에 기본 제공 보안 기능이 있습니다. 사용자가 24시간 동안 잠그기 전에 한 시간 내에 5번만 암호 재설정을 시도할 수 있습니다. 사용자가 toovalidate 전화 번호를 24 시간 동안 계정이 잠깁니다 하기 전에 1 시간 내에 5 번 시도 될 수 있습니다. 사용자가 24시간 동안 잠그기 전에 한 시간 내에 5번만 단일 인증 방법을 시도할 수 있습니다.
  >
  >
* **Q:는 얼마나 hello 전자 메일 및 SMS 일회용 암호가 유효?**

  > **A:** hello 되 암호 재설정을 위해 세션 수명은 105 분입니다. 암호 재설정 작업 hello hello부터에서, hello 사용자에 게 자신의 암호 105 분 tooreset 합니다. hello 전자 메일 및 SMS 일회용 암호가 유효 하지 않습니다이 기간이 만료 된 후.
  >
  >

## <a name="password-change"></a>암호 변경
* **Q: 해야 사용자가 어디에 toochange 암호 있습니까?**

  > **A:** 사용자가 자신의 암호를 변경할 수 자신의 프로필 사진 또는 아이콘 참조 위치 (hello의 오른쪽 상단 모서리에서와 같이 해당 [Office 365](https://portal.office.com) 또는 [액세스 패널](https://myapps.microsoft.com) 발생 합니다. Hello에서 사용자가 자신의 암호를 변경할 수 [액세스 패널 프로필 페이지](https://account.activedirectory.windowsazure.com/r#/profile)합니다. 사용자가 수도 있습니다의 암호가 만료 되었다고 경우 toochange hello Azure AD 로그인 화면에 자동으로 해당 암호를 요청 합니다. 마지막으로, 사용자가 toohello를 탐색할 수 있습니다 [Azure AD 암호 변경 포털](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) 직접 암호 toochange 만들려는 경우.
  >
  >
* **Q: 내 사용자가 알림을 받을 수 hello Office 포털에서에서 자신의 온-프레미스 암호 만료 되 면?**

  > **A:** 이것이 가능 오늘 여기 hello 지침에 따라 ad FS를 사용 하는 경우: [adfs 암호 정책 클레임 보내기](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396)합니다. 암호 해시 동기화를 사용하는 경우에는 불가능합니다. 에서는 동기화 온-프레미스에서 암호 정책 때문에 이것이, toopost 만료 알림 toocloud 환경을 불가능 되기 때문입니다. 두 경우 모두 것도 가능 너무[암호를 가진 tooexpire에 대 한 PowerShell을 사용 하 여 사용자에 게 알림](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx)합니다.
  >
  >

## <a name="password-management-reports"></a>암호 관리 보고서
* **Q: 어떻게 것 시간이를 hello 암호 관리 보고서에 데이터 tooshow?**

  > **A:** 데이터 5-10 분 내 hello 암호 관리 보고서에 표시 됩니다. 이 경우에 따라 tooan 시간 tooappear를 차지할 수 있습니다.
  >
  >
* **Q: hello 암호 관리 보고서는 어떻게 필터링 할 수 있습니까?**

  > **A:** hello 작은 돋보기 toohello (오른쪽) hello 열 레이블이 hello 보고서의 hello 위쪽을 클릭 하 여 hello 암호 관리 보고서를 필터링 할 수 있습니다. Toodo 다양 한 필터링을 원하는 경우 hello 보고서 tooexcel 다운로드 하 고 피벗 테이블을 만들 수 있습니다.
  >
  >
* **Q: 이란 hello 최대 이벤트 수 hello 암호 관리 보고서에 저장 되는 방법**

  > **A:** too75, 위로 000 암호 재설정 또는 암호 재설정 등록 이벤트 too30 일 백업 스패닝 hello 암호 관리 보고서에 저장 됩니다.  Tooexpand이 작업 하는 더 많은 이벤트 tooinclude 번호입니다.
  >
  >
* **Q: 얼마나 다시 어떤 hello 암호 관리 보고서도?**

  > **A:** hello 암호 관리 보고서 표시 작업 hello 내 지난 30 일 이내에 발생 합니다. 지금은 tooarchive이이 데이터를 유지 해야 하는 경우 hello 보고서를 주기적으로 다운로드할 수 있고 별도 위치에 저장 합니다.
  >
  >
* **Q: hello 암호 관리 보고서에 표시할 수 있는 행의 최대 수는 없는 입니까?**

  > **A:** 예, 최대 사람들이 75000 행 hello 암호 관리 보고서 중 하나에 나타날 수 있습니다에 표시 되 고 여부 hello UI 또는 다운로드 되 고 있습니다.
  >
  >
* **Q:는 API tooaccess hello 암호 재설정 또는 등록 보고 데이터 무엇입니까?**

  > **A:** 예, hello 참조 설명서 toolearn 다음 보고 데이터 스트림을 재설정 어떻게 hello 암호에 액세스할 수 있습니다.  [Tooaccess 암호 다시 설정 방법 보고 이벤트 프로그래밍 방식으로 알아봅니다](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent)합니다.
  >
  >

## <a name="password-writeback"></a>비밀번호 쓰기 저장
* **Q: 암호 쓰기 저장 hello 백그라운드 어떻게 작동 합니까?**

  > **A:** 참조 [암호 쓰기 저장의 작동 원리](active-directory-passwords-writeback.md) 에 암호 쓰기 저장 및 데이터 흐름 hello 시스템을 통해 온-프레미스 환경으로 다시 사용 하도록 설정 하면 발생 하는 기능에 대해 설명 합니다.
  >
  >
* **Q: 암호 쓰기 저장 toowork를 수행 하는 시간  암호 해시 동기화와 같이 동기화 지연이 있습니까?**

  > **A:** 비밀번호 쓰기 저장은 인스턴트입니다. 암호 해시 동기화와는 근본적으로 다르게 작동하는 동기 파이프라인입니다. 암호 쓰기 저장에는 사용자를 암호의 hello 성공에 대 한 실시간 피드백 tooget 다시 설정 또는 변경 작업 수 있습니다. 성공적인 암호 쓰기 저장에 대 한 평균 시간 hello 0.5 초 미만입니다.
  >
  >
* **Q: 온-프레미스 계정을 사용하지 않으면 클라우드 계정/액세스에 어떤 영향을 주나요?**

  > **A:** 온-프레미스 ID를 사용 하지 않도록 설정 하는 경우 클라우드 byt 기본 AAD Connect를 통해 다음 동기화 간격 hello에 i D/액세스도 비활성화 됩니다이 30 분 마다.
  >
  >
* **Q: 경우 온-프레미스 Active Directory 암호 정책에 따라 내 온-프레미스 계정 메모리가 제한지 않습니다 SSPR 준수이 정책을 hello 암호를 변경 합니까?**

  > **A:** 예, SSPR에 의존 하 고 관련 하 여 hello 온-프레미스도 일반적인 AD 도메인 암호 정책을 비롯 한 AD 암호 정책에 정의 된 모든 세분화 된 암호 정책을 대상 tooa 사용자를 지정 합니다.
  >
  >
* **Q: 비밀번호 쓰기 저장에 대해 어떤 유형의 계정이 작동합니까?**

  > **A:** 페더레이션 및 암호 해시 동기화된 사용자에 대한 비밀번호 쓰기 저장이 작동합니다.
  >
  >
* **Q: 비밀번호 쓰기 저장을 내 도메인 암호 정책에 적용합니까?**

  > **A:** 예, 비밀번호 쓰기 저장을 암호 사용 기간, 기록, 복잡성, 필터 및 로컬 도메인의 암호에 대해 시행할 다른 제한 사항에 적용합니다.
  >
  >
* **Q: 비밀번호 쓰기 저장은 안전합니까?  해킹을 당하지 않는다고 어떻게 확신할 수 있습니까?**

  > **A:** 예, 비밀번호 쓰기 저장은 안전합니다. hello 4 단계 보안 계층이 대해 자세히 tooread hello 암호 쓰기 저장 서비스에 의해 구현, 체크 아웃 hello [암호 쓰기 저장 보안 모델](active-directory-passwords-writeback.md#password-writeback-security-model) 암호 쓰기 저장의 작동 방식에 섹션입니다.
  >
  >

## <a name="next-steps"></a>다음 단계

링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.

* [**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작 
* [**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성
* [**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법
* [**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자
* [**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.
* [**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색
* [**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정
* [**비밀번호 쓰기 저장**](active-directory-passwords-writeback.md) - 비밀번호 쓰기 저장이 온-프레미스 디렉터리와 함께 작동 하는 원리
* [**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법
* [**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다
