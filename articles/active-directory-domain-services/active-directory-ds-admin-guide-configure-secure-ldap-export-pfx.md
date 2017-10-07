---
title: "Azure AD 도메인 서비스에서 LDAP (LDAPS) Secure aaaConfigure | Microsoft Docs"
description: "Azure AD 도메인 서비스 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Azure AD Domain Services 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성

## <a name="before-you-begin"></a>시작하기 전에
[작업 1: 보안 LDAP를 위한 인증서 가져오기](active-directory-ds-admin-guide-configure-secure-ldap.md)를 완료했는지 확인합니다.


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a>작업 2-hello 보안 LDAP 인증서 tooa 내보냅니다. PFX 파일
이 작업을 시작 하기 전에 hello 보안 LDAP 인증서 공용 인증 기관에서 얻은 하거나 만든 자체 서명 된 인증서를 확인 합니다.

Tooexport hello LDAPS 인증서 tooa, hello 다음 단계를 수행 합니다. PFX 파일입니다.

1. 키를 눌러 hello **시작** 단추 및 형식 **R**합니다. Hello에 **실행** 대화 상자에서 형식 **mmc** 클릭 **확인**합니다.

    ![Hello MMC 콘솔을 시작 합니다.](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. Hello에 **사용자 계정 컨트롤** 확인을 클릭 **예** toolaunch 관리자 권한으로 MMC (Microsoft Management Console)입니다.
3. Hello에서 **파일** 메뉴를 클릭 하 여 **스냅인 추가/제거...** .

    ![콘솔의 스냅인 tooMMC 추가](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. Hello에 **추가 또는 제거 스냅인** 대화 상자에서 선택 hello **인증서** 스냅인 hello 클릭 **추가 >** 단추입니다.

    ![인증서 스냅인 tooMMC 콘솔 추가](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. Hello에 **인증서 스냅인** 선택 마법사 **컴퓨터 계정** 클릭 **다음**합니다.

    ![컴퓨터 계정에 대한 인증서 스냅인 추가](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. Hello에 **컴퓨터 선택** 페이지 **로컬 컴퓨터: (hello이이 콘솔이 실행 되 고)** 클릭 **마침**합니다.

    ![인증서 스냅인 추가 - 컴퓨터 선택](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. Hello에 **추가 또는 제거 스냅인** 대화 상자를 클릭 하 여 **확인** tooadd hello 인증서 스냅인 tooMMC 합니다.

    ![인증서 스냅인 tooMMC-완료를 추가 합니다.](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. Hello MMC 창에서 클릭 tooexpand **콘솔 루트**합니다. Hello 인증서 스냅인을 로드 하는 것이 나타납니다. 클릭 **인증서 (로컬 컴퓨터)** tooexpand 합니다. Tooexpand hello 클릭 **개인** 노드, hello **인증서** 노드.

    ![개인 인증서 저장소 열기](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. 만든 자체 서명 된 인증서를 hello 표시 되어야 합니다. Hello 인증서 tooensure hello 지문이 일치 항목의 hello 인증서를 만들 때 PowerShell windows hello에서 보고 하는 hello 속성을 검사할 수 있습니다.
10. 선택 hello 자체 서명 된 인증서 및 **마우스 오른쪽 단추로 클릭**합니다. Hello 오른쪽 클릭 메뉴에서 선택 **모든 작업** 선택 **내보내기...** .

    ![인증서 내보내기](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. Hello에 **인증서 내보내기 마법사**, 클릭 **다음**합니다.

    ![인증서 내보내기 마법사](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. Hello에 **개인 키 내보내기** 페이지에서 **예, hello 개인 키 내보내기**를 클릭 하 고 **다음**합니다.

    ![인증서 개인 키 내보내기](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > Hello hello 인증서와 함께 개인 키를 내보내야 합니다. Hello hello 인증서 개인 키를 포함 하지 않는 PFX를 제공 하는 경우 관리 되는 도메인에 대 한 보안 LDAP를 사용 하면 실패 합니다.
    >
    >
13. Hello에 **파일 내보내기 형식** 페이지에서 **개인 정보 교환-PKCS #12 (합니다. PFX)** 내보낸 인증서의 hello에 대 한 hello 파일 형식으로 합니다.

    ![인증서 내보내기 파일 형식](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > Hello만 합니다. PFX 파일 형식을 사용할 수 있습니다. Hello 인증서 toohello를 내보내지 않습니다. CER 파일 형식입니다.
    >
    >
14. Hello에 **보안** 페이지, 선택 hello **암호** 옵션과 암호 tooprotect hello 입력 합니다. PFX 파일입니다. Hello 다음 작업에 필요 하므로이 암호를 기억해 둡니다. 클릭 **다음** tooproceed 합니다.

    ![인증서 내보내기에 대한 암호 ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > 이 암호를 기록해 둡니다. 이 관리 되는 도메인에 대 한 보안 LDAP를 사용 하도록 설정 하는 동안 필요한 [작업 3-hello 관리 되는 도메인에 대 한 보안 LDAP를 사용 하도록 설정](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
    >
    >
15. Hello에 **파일 tooExport** 페이지 hello 파일 이름 및 원하는 사이트로 tooexport hello 인증서 위치를 지정 합니다.

    ![인증서 내보내기에 대한 경로](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. Hello에서 다음 페이지에서 클릭 **마침** tooexport hello 인증서 tooa PFX 파일입니다. Hello 인증서를 내보낸 경우 확인 대화 상자를 표시 됩니다.

    ![인증서 내보내기 완료](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a>다음 단계
[작업 3-hello 관리 되는 도메인에 대 한 보안 LDAP를 사용 하도록 설정](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
