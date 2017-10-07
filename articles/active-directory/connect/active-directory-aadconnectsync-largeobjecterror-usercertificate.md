---
title: "Azure AD Connect 동기화: userCertificate 특성으로 인한 LargeObject 오류 처리 | Microsoft Docs"
description: "이 항목 userCertificate 특성에 의해 발생 하는 LargeObject 오류에 대 한 hello 수정 단계를 제공 합니다."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 146ad5b3-74d9-4a83-b9e8-0973a19828d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e547fb5f601b92f6f5154de9997651b1f28c51b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-handling-largeobject-errors-caused-by-usercertificate-attribute"></a>Azure AD Connect 동기화: userCertificate 특성으로 인한 LargeObject 오류 처리

Azure AD에는 최대 제한을 적용 **15** hello에 대 한 값을 인증서 **userCertificate** 특성입니다. Azure AD Connect 15 개 이상의 값 tooAzure AD 가진 개체를 내보내는 경우 Azure AD에서 반환 된 **LargeObject** 메시지에 오류가 발생 했습니다:

>*"hello 프로 비전 된 개체가 너무 큽니다. 특성 값이이 개체에 hello 개수를 자릅니다. hello 작업을 다시 시도 됩니다 hello 다음 동기화 주기... "*

다른 AD 속성별로 hello LargeObject 오류가 발생할 수 있습니다. hello 또는 hello 개체에서 온-프레미스 AD에 대해 tooverify 해야 tooconfirm hello userCertificate 특성으로 인해 실제로, [동기화 서비스 관리자 메타 버스 검색](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-mvsearch)합니다.

테 넌 트에 LargeObject 오류로 hello 메서드를 다음 중 하나를 사용 하는 개체의 tooobtain hello 목록:

 * 동기화에 대 한 Azure AD Connect Health에 테 넌 트을 사용할 경우 toohello을 참조할 수 있습니다 [동기화 오류 보고서](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-sync#object-level-synchronization-error-report-preview) 제공 합니다.
 
 * 각 동기화 주기 hello 끝날 때 전송 되는 디렉터리 동기화 오류에 대 한 hello 알림 메일에 hello LargeObject 오류가 있는 개체 목록이 있습니다. 
 * hello [Synchronization Service Manager 작업 탭](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-operations) hello 최신 내보내기 tooAzure AD 작업을 클릭 하면 hello LargeObject 오류가 있는 개체 목록이 표시 됩니다.
 
## <a name="mitigation-options"></a>해결 방법 옵션
Hello LargeObject 오류가 해결 될 때까지 동일한 개체가 될 수 없으므로 다른 특성 변경 내용 toohello tooAzure AD 내보냅니다. tooresolve hello 오류 hello 다음 옵션을 고려할 수 있습니다.

 * Azure AD Connect toobuild 1.1.524.0 업그레이드 후 또는 합니다. Hello 기본 제공 동기화 규칙에 업데이트 된 toonot 내보내기 특성 userCertificate 고 된 userSMIMECertificate hello 특성 15 개 이상의 값이 있는 경우, Azure AD Connect에서 1.1.524.0 빌드입니다. 방법에 대 한 자세한 내용은 Azure AD Connect tooupgrade 참조 tooarticle [Azure AD Connect:는 이전 버전 toohello 최신 버전에서 업그레이드](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version)합니다.

 * 구현 된 **아웃 바운드 동기화 규칙** 내보내는 Azure AD Connect에는 **null 15 개 이상의 인증서 값을 가진 개체에 대 한 hello 실제 값 대신 값**합니다. 이 옵션은 필요 하지 않은 모든 hello 인증서 값 내보낸 toobe tooAzure AD 15 개 이상의 값이 있는 개체에 대 한 경우 적합 합니다. 방법에 대 한 자세한 내용은이 동기화 규칙을 toonext 섹션을 참조 하는 tooimplement [구현 동기화 규칙 toolimit 내보내기를 userCertificate 특성의](#implementing-sync-rule-to-limit-export-of-usercertificate-attribute)합니다.

 * Hello hello에 대 한 인증서 값 수를 줄일 온-프레미스 AD 개체 (15 개이 하)로 더 이상 조직에서 사용 중인 값을 제거 합니다. 이것은 만료 되거나 사용 하지 않는 인증서에 의해 hello 특성 팽창이 발생 하는 경우 적절 합니다. Hello를 사용할 수 있습니다 [PowerShell 스크립트 사용 가능한 여기](https://gallery.technet.microsoft.com/Remove-Expired-Certificates-0517e34f) 백업 및 온-프레미스에서 만료 된 인증서 삭제 toohelp 찾을 AD 합니다. Hello 인증서를 삭제 하기 전에 조직에서 hello 공개 키 인프라 관리자에 게 확인 하는 것이 좋습니다.

 * 구성 Azure AD Connect tooexclude hello userCertificate 특성에서 내보낸 tooAzure AD 합니다. 일반적으로 권장 하지는 않습니다이 옵션 이후 hello 특성 Microsoft 온라인 서비스 tooenable 특정 시나리오에서 사용할 수 있습니다. 특히 다음과 같습니다.
    * hello 사용자 개체에 hello userCertificate 특성은 메시지 서명 및 암호화에 대 한 Exchange Online 및 Outlook 클라이언트에서 사용 됩니다. 이 기능에 대해 자세히 toolearn 참조 tooarticle [S/MIME 메시지 서명 및 암호화에 대 한](https://technet.microsoft.com/library/dn626158(v=exchg.150).aspx)합니다.

    * hello 컴퓨터 개체에 hello userCertificate 특성은 Azure AD Windows 10 tooallow 온-프레미스 도메인에 가입 된 장치 tooconnect tooAzure AD에서 사용 됩니다. 이 기능에 대해 자세히 toolearn tooarticle를 참조 하십시오 [발생 하는 Windows 10에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy)합니다.

## <a name="implementing-sync-rule-toolimit-export-of-usercertificate-attribute"></a>동기화 규칙 toolimit 내보내기를 userCertificate 특성의 구현
tooresolve hello LargeObject hello userCertificate 특성에 의해 발생 한 오류를 내보내는 Azure AD Connect에서 아웃 바운드 동기화 규칙을 구현할 수 있습니다는 **null인증서값이15개이상의개체에대한hello실제값대신값**. 이 섹션에서는 hello 단계 필요한 tooimplement hello 동기화 규칙에 대 한 설명 **사용자** 개체입니다. hello 단계에 적용할 수 **연락처** 및 **컴퓨터** 개체입니다.

> [!IMPORTANT]
> Null 값을 내보내면 값 이전에 성공적으로 내보냈습니다. tooAzure AD 인증서를 제거 합니다.

hello 단계는 다음과 같이 요약할 수 있습니다.

1. 동기화 스케줄러를 비활성화하고 진행 중인 동기화가 없는지 확인합니다.
3. UserCertificate 특성에 대 한 아웃 바운드 동기화 규칙을 읽었습니다 hello를 찾습니다.
4. 필요한 hello 아웃 바운드 동기화 규칙을 만듭니다.
5. LargeObject 오류와 함께 기존 개체에 hello 새 동기화 규칙을 확인 합니다.
6. Hello 새 동기화 규칙 tooremaining 개체 LargeObject 오류와 함께 적용 됩니다.
7. 예기치 않은 변경 된 사항이 없습니다 내보낸 toobe tooAzure AD 대기를 확인 합니다.
8. Hello 변경 tooAzure AD 내보냅니다.
9. 동기화 스케줄러를 다시 활성화합니다.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>1단계. 동기화 스케줄러를 비활성화하고 진행 중인 동기화가 없는지 확인합니다.
새 동기화 구현의 hello 중간에 있는 동안 발생 하는 동기화 확인 규칙 tooavoid 의도 하지 않은 변경 되 고 AD tooAzure 내보낸 합니다. toodisable hello 기본 제공 동기화 스케줄러:
1. Hello Azure AD Connect 서버에서 PowerShell 세션을 시작 합니다.

2. cmdlet을 실행하여 예약된 동기화 비활성화: `Set-ADSyncScheduler -SyncCycleEnabled $false`

> [!Note]
> hello 앞 단계는 적용 가능한 toonewer의 버전에만 (1.1.xxx.x) 기본 제공 스케줄러 hello와 Azure AD Connect 합니다. Toodisable 해야 Windows 작업 스케줄러를 사용 하 여 Azure AD Connect의 이전 버전 (1.0.xxx.x)를 사용 하는 사용자 고유의 사용자 지정 스케줄러 (일반적으로 되지) tootrigger 정기 동기화를 사용 하는 경우에 적절 하 게 합니다.

3. Hello 시작 **동기화 서비스 관리자** tooSTART → 라인으로 전환 하 여 동기화 서비스입니다.

4. Toohello 이동 **작업** 탭 및 상태는 작업이 확인 *"에서"진행 중입니다.*

### <a name="step-2-find-hello-existing-outbound-sync-rule-for-usercertificate-attribute"></a>2단계. UserCertificate 특성에 대 한 아웃 바운드 동기화 규칙을 읽었습니다 hello 찾기
사용 하 고 사용자 개체 tooAzure AD에 대 한 tooexport userCertificate 특성을 구성 하는 기존 동기화 규칙이 있어야 합니다. 이 동기화 규칙 toofind 아웃를 찾아 해당 **선행** 및 **범위 지정 필터** 구성:

1. Hello 시작 **동기화 규칙 편집기** tooSTART → 라인으로 전환 하 여 동기화 규칙 편집기입니다.

2. 다음 값에는 hello로 hello 검색 필터를 구성 합니다.

    | 특성 | 값 |
    | --- | --- |
    | 방향 |**Outbound** |
    | MV 개체 유형 |**Person** |
    | 커넥터 |*Azure AD 커넥터의 이름* |
    | 커넥터 개체 유형 |**user** |
    | MV 특성 |**userCertificate** |

3. OOB (기본적으로) 동기화 규칙 tooAzure AD 커넥터 tooexport userCertficiate 특성 사용자 개체를 사용 하는 경우 되돌려야 hello *tooAAD 사용자 ExchangeOnline"Out"* 규칙입니다.
4. Hello 기록해 **선행** 이 동기화 규칙의 값입니다.
5. Hello 동기화 규칙을 선택 하 고 클릭 **편집**합니다.
6. Hello에 *"예약 된 규칙 확인 편집"* 팝업 대화 상자에서 클릭 **아니요**합니다. (스 러 하지 하겠습니다 toomake toothis 동기화 규칙을 변경 하는).
7. Hello 편집 화면에서 선택 hello **범위 지정 필터** 탭 합니다.
8. 필터 구성의 범위를 지정 하는 hello 아래로 note 합니다. Hello OOB 동기화 규칙을 사용 하는 경우 정확 하 게 있을 것 **두 개의 절을 포함 하 한 범위 지정 필터 그룹**를 포함 하 여:

    | 특성 | 연산자 | 값 |
    | --- | --- | --- |
    | sourceObjectType | EQUAL | 사용자 |
    | cloudMastered | NOTEQUAL | True |

### <a name="step-3-create-hello-outbound-sync-rule-required"></a>3단계. 필요한 hello 아웃 바운드 동기화 규칙 만들기
hello 새 동기화 규칙 해야가 hello 동일 **범위 지정 필터** 및 **우선 순위가 높은** 보다 hello 동기화 규칙을 읽었습니다. 이렇게 하면 해당 hello 새 동기화 규칙 개체의 동기화 규칙을 읽었습니다 hello 및 hello userCertificate 특성에 대 한 재정의 hello 기존 동기화 규칙 집합이 동일한 toohello 적용 됩니다. toocreate hello 동기화 규칙:
1. 동기화 규칙 편집기 hello 클릭 hello **새 규칙 추가** 단추입니다.
2. Hello에서 **설명 탭**, 같은 구성이 hello를 제공 합니다.

    | 특성 | 값 | 세부 정보 |
    | --- | --- | --- |
    | 이름 | *이름 제공* | 예: *"tooAAD – 아웃 사용자 지정 재정의 userCertificate에 대 한"* |
    | 설명 | *설명 제공* | 예: *“userCertificate 특성에 15개 이상의 값이 있는 경우 NULL을 내보냅니다.”* |
    | 연결된 시스템 | *Hello Azure AD 커넥터를 선택 합니다.* |
    | 연결된 시스템 개체 유형 | **user** | |
    | 메타버스 개체 유형 | **person** | |
    | 링크 형식 | **Join** | |
    | 우선 순위 | *1 ~ 99 사이의 숫자 선택* | hello 숫자 선택한 기존 동기화 규칙에서 사용 하면 안 있고 더 낮은 값 (및 따라서 우선 순위가 높은) hello 기존 동기화 규칙 보다 합니다. |

3. Toohello 이동 **범위 지정 필터** 탭 하 고 동일한 범위 지정 필터 hello 기존 동기화 규칙을 사용 하 여 hello를 구현 합니다.
4. Skip hello **조인 규칙** 탭 합니다.
5. Toohello 이동 **변환** tooadd는 새 변환 다음 사용 하 여 구성 탭:

    | 특성 | 값 |
    | --- | --- |
    | 흐름 형식 |**Expression** |
    | 대상 특성 |**userCertificate** |
    | 원본 특성 |*다음 식은 사용 하 여 hello*:`IIF(IsNullOrEmpty([userCertificate]), NULL, IIF((Count([userCertificate])> 15),AuthoritativeNull,[userCertificate]))` |
    
6. Hello 클릭 **추가** 단추 toocreate hello 동기화 규칙입니다.

### <a name="step-4-verify-hello-new-sync-rule-on-an-existing-object-with-largeobject-error"></a>4단계. LargeObject 오류와 함께 기존 개체에 hello 새 동기화 규칙을 확인
이 동기화 hello tooverify 규칙이 만들어졌습니다.이 제대로 작동 LargeObject 오류와 함께 기존 AD 개체에 tooother 개체 적용 하기 전에:
1. Toohello 이동 **작업** hello 동기화 서비스 관리자에서에서 탭 합니다.
2. Hello 가장 최근의 내보내기 tooAzure AD 작업을 선택 하 고 LargeObject 오류를 사용 하 여 hello 개체 중 하나를 클릭 합니다.
3.  Hello 커넥터 공간 개체 속성 팝업 화면 hello 클릭 **미리 보기** 단추입니다.
4. Hello 미리 보기 팝업 화면에서 선택 **전체 동기화** 클릭 **커밋 미리 보기**합니다.
5. Hello 미리 보기 화면 및 hello 커넥터 공간 개체 속성 화면을 닫습니다.
6. Toohello 이동 **커넥터** hello 동기화 서비스 관리자에서에서 탭 합니다.
7. Hello를 마우스 오른쪽 단추로 클릭 **Azure AD** 커넥터 및 선택 **실행...**
8. Hello 커넥터 실행 팝업에 선택 **내보내기** 단계를 클릭 하 여 **확인**합니다.
9. 내보내기 tooAzure AD toocomplete 기다렸다가 확인이 특정 개체에 대 한 자세한 LargeObject 오류입니다.

### <a name="step-5-apply-hello-new-sync-rule-tooremaining-objects-with-largeobject-error"></a>5단계. Hello 새 동기화 규칙 tooremaining 개체 LargeObject 오류로 적용
Hello 동기화 규칙 추가 되 면 hello AD 커넥터에서 전체 동기화 단계 toorun이 필요 합니다.
1. Toohello 이동 **커넥터** hello 동기화 서비스 관리자에서에서 탭 합니다.
2. Hello를 마우스 오른쪽 단추로 클릭 **AD** 커넥터 및 선택 **실행...**
3. Hello 커넥터 실행 팝업에 선택 **전체 동기화** 단계를 클릭 하 여 **확인**합니다.
4. Hello 전체 동기화 단계 toocomplete 될 때까지 기다립니다.
5. AD 커넥터 AD 커넥터가 하나 이상 있는 경우 나머지 hello에 대 한 hello 단계를 반복 합니다. 일반적으로 여러 온-프레미스 디렉터리가 있으면 여러 커넥터가 필요합니다.

### <a name="step-6-verify-there-are-no-unexpected-changes-waiting-toobe-exported-tooazure-ad"></a>6단계. 내보낸 toobe tooAzure AD 대기 중인 예기치 않은 변경 확인
1. Toohello 이동 **커넥터** hello 동기화 서비스 관리자에서에서 탭 합니다.
2. Hello를 마우스 오른쪽 단추로 클릭 **Azure AD** 커넥터 및 선택 **커넥터 공간 검색**합니다.
3. Hello 커넥터 공간 검색 팝업에:
    1. 범위를 너무 설정**보류 중인 내보내기**합니다.
    2. **추가**, **수정** 및 **삭제**를 포함하여 확인란 3개를 모두 선택합니다.
    3. 클릭 **검색** 단추 tooreturn 모든 개체 변경 내용이 내보낸 toobe tooAzure AD와 함께 합니다.
    4. 예기치 않은 변경 사항이 없는지 확인합니다. 지정된 된 개체에 대 한 tooexamine hello 변경 hello 개체에 두 번 클릭 합니다.

### <a name="step-7-export-hello-changes-tooazure-ad"></a>7단계. Hello 변경 tooAzure AD 내보내기
tooexport hello 변경 tooAzure AD:
1. Toohello 이동 **커넥터** hello 동기화 서비스 관리자에서에서 탭 합니다.
2. Hello를 마우스 오른쪽 단추로 클릭 **Azure AD** 커넥터 및 선택 **실행...**
4. Hello 커넥터 실행 팝업에 선택 **내보내기** 단계를 클릭 하 여 **확인**합니다.
5. 내보내기 tooAzure AD toocomplete 기다렸다가 자세한 LargeObject 오류가 없는지 확인 합니다.

### <a name="step-8-re-enable-sync-scheduler"></a>8단계: 동기화 스케줄러를 다시 활성화합니다.
Hello 문제를 해결 했으므로 hello 기본 제공 동기화 스케줄러 다시 설정 합니다.
1. PowerShell 세션을 시작합니다.
2. cmdlet을 실행하여 예약된 동기화 다시 활성화: `Set-ADSyncScheduler -SyncCycleEnabled $true`

> [!Note]
> hello 앞 단계는 적용 가능한 toonewer의 버전에만 (1.1.xxx.x) 기본 제공 스케줄러 hello와 Azure AD Connect 합니다. Toodisable 해야 Windows 작업 스케줄러를 사용 하 여 Azure AD Connect의 이전 버전 (1.0.xxx.x)를 사용 하는 사용자 고유의 사용자 지정 스케줄러 (일반적으로 되지) tootrigger 정기 동기화를 사용 하는 경우에 적절 하 게 합니다.

## <a name="next-steps"></a>다음 단계
[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.

