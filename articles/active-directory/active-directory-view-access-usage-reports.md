---
title: "aaaView 액세스 및 사용 보고서 | Microsoft Docs"
description: "Tooview 액세스 및 사용 보고 toogain 통찰력 조직 디렉터리의 hello 무결성 및 보안 방법에 대해 설명 합니다."
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: a074bc4e-cf3f-4ad1-8cc6-4199d2e09ce4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 1c18fd2a327ae8b67f62ce2754f643bdb03514a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="view-your-access-and-usage-reports"></a>액세스 및 사용 보고서 보기
*이 설명서는 hello의 일부 [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)합니다.*

Azure Active Directory의 액세스 및 조직 디렉터리의 hello 무결성 및 보안에 대 한 사용 현황 보고서 toogain 가시성을 사용할 수 있습니다. 이 정보를 사용 하면 디렉터리 관리자 수 보다 잘 결정 있는 가능한 보안 위험이 발생할 수 있습니다 적절 하 게 될 수 toomitigate 이러한 위험.

Hello Azure 관리 포털에서에서 보고서는 다음 방법으로 hello로 분류 됩니다.

* 비정상 보고서-Contain 로그인 이벤트가 있음을 toobe 비정상적인 합니다. 목표는 toomake 이러한 활동을 인식 하 고 toobe 수 toomake 의심 스러운 이벤트 인지에 대 한 결정을 사용 합니다.
* 통합 응용 프로그램 보고서 – 클라우드 응용 프로그램이 조직에서 사용되는 방식을 파악할 수 있게 해 줍니다. Azure Active Directory는 수천 개의 클라우드 응용 프로그램과 통합을 제공합니다.
* 오류 보고서 – 계정 tooexternal 응용 프로그램을 프로 비전 할 때 발생할 수 있는 오류를 나타냅니다.
* 사용자별 보고서 – 특정 사용자에 대한 장치/로그인 활동 데이터를 표시합니다.
* 활동 로그-Contain hello 내에서 모든 감사 된 이벤트의 레코드가 지난 24 시간, 최근 7 일 또는 30 일 이내 뿐만 아니라 그룹 활동 변경 사항 및 암호 재설정 및 등록 활동 합니다.

> [!NOTE]
> * 일부 고급 비정상 보고서 및 리소스 사용 보고서는 [Azure Active Directory Premium](active-directory-get-started-premium.md)을 사용하도록 설정하는 경우에만 사용할 수 있습니다. 고급 보고서 toopotential 위협 응답 액세스 보안을 개선 하 고 장치 액세스 및 응용 프로그램 사용에 대해 액세스 tooanalytics 도움이 됩니다.
> * Azure Active Directory Premium 및 Basic edition은 중국 고객의 사용 가능한 Azure Active Directory의 전세계 인스턴스 hello를 사용 하 여 합니다. Azure Active Directory Premium 및 Basic edition 중국의 21vianet이 운영 하는 hello Microsoft Azure 서비스에서 현재 지원 되지 않습니다. 자세한 내용은 주소로 문의 hello [Azure Active Directory 포럼](https://feedback.azure.com/forums/169401-azure-active-directory/)합니다.
> 
> 

## <a name="reports"></a>보고서
| 보고서 | 설명 |
| --- | --- |
| **비정상적인 작업 보고서** | |
| [알 수 없는 원본에서 로그인](active-directory-reporting-sign-ins-from-unknown-sources.md) |에 시도 toosign 추적 되지 않고 나타낼 수 있습니다. |
| [여러 번의 실패 후 로그인](active-directory-reporting-sign-ins-after-multiple-failures.md) |성공적인 무작위 공격을 나타낼 수 있습니다. |
| [여러 지역에서의 로그인](active-directory-reporting-sign-ins-from-multiple-geographies.md) |수 여러 사용자가 로그인 했음을 나타낼 hello를 사용 하 여 동일한 계정입니다. |
| [의심스러운 활동을 포함하는 IP 주소의 로그인](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |지속적인된 침입 시도 후에 성공적인 로그인을 나타낼 수 있습니다. |
| [감염 가능성이 있는 장치에서의 로그인](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |감염된 된 장치에는 시도 toosign를 나타낼 수 있습니다. |
| [비정상적인 로그인 활동](active-directory-reporting-irregular-sign-in-activity.md) |로그인 이벤트가 비정상 toousers' 패턴을 나타낼 수 있습니다. |
| [비정상적인 로그인 활동을 포함하는 사용자 보고서](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |손상된 계정을 가진 사용자를 나타냅니다. |
| 자격 증명이 손실된 사용자 |자격 증명이 손실된 사용자 |
| **활동 로그** | |
| 감사 보고서 |디렉토리에서 감사된 이벤트 |
| 암호 재설정 활동 |조직에서 발생하는 암호 재설정의 세부 정보 보기를 제공합니다. |
| 암호 재설정 등록 활동 |조직에서 발생하는 암호 재설정 등록의 세부 정보 보기를 제공합니다. |
| 셀프 서비스 그룹 활동 |활동 로그 tooall 제공 그룹 디렉터리에 셀프 서비스 활동 |
| **통합된 응용 프로그램** | |
| 응용 프로그램 사용 현황 |디렉토리와 통합하는 모든 SaaS 응용 프로그램에 대한 사용 현황 요약을 제공합니다. |
| 계정 프로비전 활동 |시도 기록을 tooprovision 계정 tooexternal 응용 프로그램을 제공합니다. |
| 암호 롤오버 상태 |SaaS 응용 프로그램의 자동 암호 롤오버 상태의 자세한 개요를 제공합니다. |
| 계정 프로비전 오류 |영향 toousers' 액세스 tooexternal 응용 프로그램을 나타냅니다. |
| **권한 관리** | |
| RMS 사용 현황 |권한 관리 사용 현황에 대한 요약을 제공합니다. |
| 가장 활동적인 RMS 사용자 |RMS로 보호된 파일에 액세스하는 상위 1000명의 활성 사용자를 나열합니다. |
| RMS 장치 사용 |RMS로 보호된 파일에 액세스하는 데 사용된 장치를 나열합니다. |
| RMS 사용 응용 프로그램 사용 현황 |RMS 사용 응용 프로그램의 사용 현황을 제공합니다. |

## <a name="report-editions"></a>보고서 버전
| 보고서 | 무료 | Basic | Premium |
| --- | --- | --- | --- |
| **비정상적인 작업 보고서** | | | |
| 알 수 없는 원본에서 로그인 |✓ |✓ |✓ |
| 여러 번의 실패 후 로그인 |✓ |✓ |✓ |
| 여러 지역에서의 로그인 |✓ |✓ |✓ |
| 의심스러운 활동을 포함하는 IP 주소의 로그인 | | |✓ |
| 감염 가능성이 있는 장치에서의 로그인 | | |✓ |
| 비정상적인 로그인 활동 | | |✓ |
| 비정상적인 로그인 활동을 포함하는 사용자 보고서 | | |✓ |
| 자격 증명이 손실된 사용자 | | |✓ |
| **활동 로그** | | | |
| 감사 보고서 |✓ |✓ |✓ |
| 암호 재설정 활동 | | |✓ |
| 암호 재설정 등록 활동 | | |✓ |
| 셀프 서비스 그룹 활동 | | |✓ |
| **통합된 응용 프로그램** | | | |
| 응용 프로그램 사용 현황 | | |✓ |
| 계정 프로비전 활동 |✓ |✓ |✓ |
| 암호 롤오버 상태 | | |✓ |
| 계정 프로비전 오류 |✓ |✓ |✓ |
| **권한 관리** | | | |
| RMS 사용 현황 | | |RMS만 해당 |
| 가장 활동적인 RMS 사용자 | | |RMS만 해당 |
| RMS 장치 사용 | | |RMS만 해당 |
| RMS 사용 응용 프로그램 사용 현황 | | |RMS만 해당 |

## <a name="anomalous-activity-reports"></a>비정상적인 활동 보고서
<p>hello 비정상적인 로그인 활동 보고서 활동 tooOffice365, Azure 관리 포털, Azure AD 액세스 패널, Sharepoint Online, Dynamics CRM Online 및 다른 Microsoft 온라인 서비스에 의심 스러운 로그인 플래그 합니다.</p>

<p>모든이 보고서, 보고서 "여러 번 실패 후 로그인" hello 점을 제외 하 고 또한 플래그 의심 스러운 <i>페더레이션</i> hello 페더레이션 공급자에 관계 없이 기능 toohello 앞에서 언급 한 서비스를 등록 합니다. </p>

<p>보고서를 다음 hello 사용할 수 있습니다. </p><ul>

<li>[알 수 없는 원본에서 로그인](active-directory-reporting-sign-ins-from-unknown-sources의 일부입니다.md)의 일부입니다.</li>

<li>[여러 번의 실패 후 로그인](active-directory-reporting-sign-ins-after-multiple-failures의 일부입니다.md)의 일부입니다.</li>

<li>[여러 지역에서의 로그인](active-directory-reporting-sign-ins-from-multiple-geographies의 일부입니다.md)의 일부입니다.</li>

<li>[의심스러운 활동을 포함하는 IP 주소의 로그인](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity의 일부입니다.md)의 일부입니다.</li>

<li>[비정상적인 로그인 활동](active-directory-reporting-irregular-sign-in-activity의 일부입니다.md)의 일부입니다.</li>

<li>[감염 가능성이 있는 장치에서의 로그인](active-directory-reporting-sign-ins-from-possibly-infected-devices의 일부입니다.md)의 일부입니다.</li>

<li>[비정상적인 로그인 활동을 포함하는 사용자 보고서](active-directory-reporting-users-with-anomalous-sign-in-activity.md)의 일부입니다.</li>

<li>자격 증명이 손실된 사용자</li></ul>

## <a name="activity-logs"></a>활동 로그
### <a name="audit-report"></a>감사 보고서
| 설명 | 보고서 위치 |
|:--- |:--- |
| Hello 지난 24 시간, 최근 7 일 또는 최근 30 일 내에 감사 된 모든 이벤트의 레코드를 표시합니다. <br /> 자세한 내용은 [Azure Active Directory 감사 보고서 이벤트](active-directory-reporting-audit-events.md) |디렉터리 > 보고서 탭 |

![감사 보고서](./media/active-directory-view-access-usage-reports/auditReport.PNG)

### <a name="password-reset-activity"></a>암호 재설정 활동
| 설명 | 보고서 위치 |
|:--- |:--- |
| 조직 내에서 발생한 모든 암호 재설정 시도를 보여 줍니다. |디렉터리 > 보고서 탭 |

![암호 재설정 활동](./media/active-directory-view-access-usage-reports/passwordResetActivity.PNG)

### <a name="password-reset-registration-activity"></a>암호 재설정 등록 활동
| 설명 | 보고서 위치 |
|:--- |:--- |
| 조직 내에서 발생한 모든 암호 재설정 등록을 보여 줍니다. |디렉터리 > 보고서 탭 |

![암호 재설정 등록 활동](./media/active-directory-view-access-usage-reports/passwordResetRegistrationActivity.PNG)

### <a name="self-service-groups-activity"></a>셀프 서비스 그룹 활동
| 설명 | 보고서 위치 |
|:--- |:--- |
| 디렉터리의 hello 셀프 서비스 관리 그룹에 대 한 모든 활동을 보여 줍니다. |디렉터리 > 사용자 > <i>사용자</i> > 장치 탭 |

![셀프 서비스 그룹 활동](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a>통합된 응용 프로그램 보고서
### <a name="application-usage-summary"></a>응용 프로그램 사용: 요약
| 설명 | 보고서 위치 |
|:--- |:--- |
| 디렉터리의 모든 hello SaaS 응용 프로그램에 대 한 toosee 사용 하려는 경우이 보고서를 사용 합니다. 이 보고서는 hello 횟수 hello 액세스 패널에에서 hello 응용 프로그램을 클릭을 기반으로 합니다. |디렉터리 > 보고서 탭 |

이 보고서에 포함 되어 너무 로그인*모든* 디렉터리에는 응용 프로그램에 대 한 액세스를 사전 통합 된 Microsoft 응용 프로그램을 포함 하 여 합니다.

사전 통합 된 Microsoft 응용 프로그램에는 Office 365, Sharepoint, hello Azure 관리 포털 있습니다.

![응용 프로그램 사용 요약](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a>응용 프로그램 사용: 세부
| 설명 | 보고서 위치 |
|:--- |:--- |
| 얼마나 많은 특정 SaaS 응용 프로그램을 사용 하 되 고 toosee 하려는 경우이 보고서를 사용 합니다. 이 보고서는 hello 횟수 hello 액세스 패널에에서 hello 응용 프로그램을 클릭을 기반으로 합니다. |디렉터리 > 보고서 탭 |

### <a name="application-dashboard"></a>응용 프로그램 대시보드
| 설명 | 보고서 위치 |
|:--- |:--- |
| 이 보고서는 선택한 시간 간격 동안 조직 사용자가 누적 기호 기능 toohello 응용 프로그램을 나타냅니다. hello 차트 hello 대시보드 페이지에서 해당 응용 프로그램의 모든 사용 추세를 식별 하는 데 도움이 됩니다. |디렉터리 > 응용 프로그램 > 대시보드 탭 |

## <a name="error-reports"></a>오류 보고서
### <a name="account-provisioning-errors"></a>계정 프로비전 오류
| 설명 | 보고서 위치 |
|:--- |:--- |
| SaaS 응용 프로그램 tooAzure Active Directory에서에서의 계정 hello 동기화 중에 발생 하는이 toomonitor 오류를 사용 합니다. |디렉터리 > 보고서 탭 |

![계정 프로비전 오류](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a>사용자별 보고서
### <a name="devices"></a>장치
| 설명 | 보고서 위치 |
|:--- |:--- |
| Toosee hello IP 주소 및 특정 사용자가 Azure Active Directory tooaccess를 사용 하는 장치의 지리적 위치를 원하는 경우이 보고서를 사용 합니다. |디렉터리 > 사용자 > <i>사용자</i> > 장치 탭 |

### <a name="activity"></a>작업
| 설명 | 보고서 위치 |
|:--- |:--- |
| 사용자에 대 한 활동의 hello 기호를 보여 줍니다. hello 보고서에는 hello 응용 프로그램에 로그인, 사용 되는 장치, IP 주소 및 위치와 같은 정보가 포함 됩니다. Microsoft 계정으로 로그인 하는 사용자에 대 한 hello 기록이 수집 하지 않습니다. |디렉터리 > 사용자 > <i>사용자</i> > 활동 탭 |

#### <a name="sign-in-events-included-in-hello-user-activity-report"></a>Hello 사용자 작업 보고서에에서 포함 된 이벤트에 로그인
특정 유형의 로그인 이벤트가 hello 사용자 작업 보고서에에서 표시 됩니다.

| 이벤트 유형 | 포함 여부 |
| --- | --- |
| 기능 toohello 서명 [액세스 패널](http://myapps.microsoft.com/) |예 |
| 기능 toohello 서명 [Azure 관리 포털](https://manage.windowsazure.com/) |예 |
| 기능 toohello 서명 [Microsoft Azure 포털](https://portal.azure.com/) |예 |
| 기능 toohello 서명 [Office 365 포털](http://portal.office.com/) |예 |
| 기능 tooa 네이티브 응용 프로그램에 서명, Outlook 같은 (아래 예외 참조) |예 |
| Hello Salesforce와 같은 액세스 패널을 통해 기능 tooa 페더레이션/프로 비전 된 앱에 서명 |예 |
| Hello Twitter와 같은 액세스 패널을 통해 기능 tooa 암호 기반 앱에 서명 |예 |
| Toohello 디렉터리 추가 된 기능 tooa 사용자 지정 비즈니스 앱에 서명 |아니요(포함 예정) |
| Toohello 디렉터리 추가 된 기능 tooan Azure AD 응용 프로그램 프록시 앱에 서명 |아니요(포함 예정) |

> 참고: tooreduce hello 양을 노이즈가이 보고서에 로그인 하 여 hello [Microsoft Online Services 로그인 도우미](http://community.office365.com/en-us/w/sso/534.aspx) 표시 되지 않습니다.
> 
> 

## <a name="things-tooconsider-if-you-suspect-security-breach"></a>보안 위반이 의심 되는 경우 작업 tooconsider
않았다고 의심 될 경우 사용자 계정이 손상 또는 모든 종류의 hello 클라우드에서 디렉터리 데이터의 tooa 보안 위반을 야기할 수 있는 의심 스러운 사용자 작업 하나 이상의 작업을 수행 하는 hello tooconsider을 할 수 있습니다.

* 연락처 hello 사용자 tooverify hello 활동
* Hello 사용자의 암호를 다시 설정
* [다단계 인증](../multi-factor-authentication/multi-factor-authentication-get-started.md) 사용

## <a name="view-or-download-a-report"></a>보고서 보기 또는 다운로드
1. Hello Azure 클래식 포털에서에서 클릭 **Active Directory**조직 디렉터리의 hello 이름을 클릭 하 고 클릭 **보고서**합니다.
2. Hello 보고서 페이지에서 tooview hello 보고서를 클릭 합니다. 다운로드 및/또는 합니다.
   
   > [!NOTE]
   > Azure Active Directory의 기능을 보고 하는 hello를 사용 하는 hello 이것이에서 메시지 tooOpt 표시 됩니다. 동의 하면 hello 확인 표시 아이콘 toocontinue를 클릭 합니다.
   > 
   > 
3. Hello 드롭 다운 메뉴 다음 tooInterval 누르고 hello이이 보고서를 생성할 때 사용 해야 하는 시간 범위를 다음 중 하나를 선택 합니다.
   
   * 최근 24시간
   * 최근 7일
   * 최근 30일
4. Hello 확인 표시 아이콘 toorun hello 보고서를 클릭 합니다.
   * Too1000를 이벤트 hello Azure 클래식 포털에에서 표시 됩니다.
5. 해당 하는 경우 클릭 **다운로드** toodownload hello 보고서 tooa 형식의 압축된 파일로 쉼표로 구분 된 값 (CSV) 오프 라인으로 보거나 보관 하기 위해 합니다.
   * too75, 000 이벤트 hello 다운로드 한 파일에 포함 됩니다.
   * 더 많은 데이터에 대 한 체크 아웃 hello [Azure AD Reporting API](active-directory-reporting-api-getting-started.md)합니다.

## <a name="ignore-an-event"></a>이벤트 무시
비정상 보고서를 본다면 관련 보고서에 표시된 다양한 이벤트를 무시할 수 있다는 것을 알 수 있습니다. 이벤트, tooignore hello 이벤트 hello 보고서에서 강조 표시 하 고 클릭 **무시**합니다. hello **무시** 단추 hello 보고서에서 강조 표시 한 이벤트가 hello를 영구적으로 제거 됩니다와 허가 받은 전역 관리자만 사용할 수 있습니다.

## <a name="automatic-email-notifications"></a>자동 전자 메일 알림
Azure AD의 보고 알림에 대한 자세한 내용은 [Azure Active Directory Reporting 알림](active-directory-reporting-notifications.md)을 확인하세요.

## <a name="whats-next"></a>다음 단계
* [Azure Active Directory Premium 시작](active-directory-get-started-premium.md)
* [회사 브랜딩 tooyour 로그인 및 액세스 패널 페이지 추가](active-directory-add-company-branding.md)

