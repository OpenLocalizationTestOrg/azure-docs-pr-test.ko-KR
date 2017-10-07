---
title: "Azure Active Directory Domain Services: Kerberos 제한 위임 활성화 | Microsoft Docs"
description: "Azure Active Directory Domain Services 관리되는 도메인에서 Kerberos 제한 위임 활성화"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d32547c8018dd1f99c992e95a01d2711d460a261
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a>관리되는 도메인에서 Kerberos 제한 위임(KCD) 구성
대부분의 응용 프로그램에는 hello 사용자의 hello 컨텍스트에서 tooaccess 리소스가 필요 합니다. Active Directory는 이 사용 사례가 가능한 Kerberos 위임이라고 하는 메커니즘을 지원합니다. 또한 hello 사용자의 hello 컨텍스트에서 특정 리소스에 액세스할 수 있도록 위임을 제한할 수 있습니다. Azure AD Domain Services 관리되는 도메인은 더 안전하게 잠겨 있으므로 기존의 Active Directory 도메인과는 다릅니다.

이 문서에서는 tooconfigure kerberos 제한 된 하는 Azure AD 도메인 서비스 관리 되는 도메인에 위임 합니다.

## <a name="kerberos-constrained-delegation-kcd"></a>Kerberos 제한 위임(KCD)
Kerberos 위임 계정 tooimpersonate 다른 보안 주체 (사용자)와 같은 tooaccess 리소스가 수 있습니다. 웹 응용 프로그램을 사용자의 hello 컨텍스트에서 백 엔드 웹 API에 액세스 하는 것이 좋습니다. 이 예제에서는 hello (hello 컨텍스트의 서비스 계정 또는 컴퓨터/시스템 계정에서 실행) 하는 웹 응용 프로그램 사용자를 가장 hello hello 리소스 (백 엔드 웹 API)에 액세스할 때. Kerberos 위임을 안전 하지 않으므로 hello 계정을 가장 하는 리소스 hello hello 사용자의 hello 컨텍스트에서 액세스할 수를 제한 하지 않습니다.

Kerberos 제한 위임 KCD ()는 서비스/리소스 toowhich hello에 대 한 지정된 서버 hello 사용자를 대신 하 여 작업할 수 있는 hello를 제한 합니다. 기존의 KCD는 서비스에 대 한 도메인 관리자 권한이 tooconfigure 도메인 계정에 필요 하 고 hello 계정 tooa 단일 도메인을 제한 합니다.

또한 기존의 KCD에는 이것과 관련된 몇 가지 문제가 있습니다. 도메인 관리자에 게 hello 서비스를 구성한 이전 운영 체제, 서비스 관리자에 게 없는 유용한 방법은 tooknow 되는 프런트 엔드 서비스 이들이 소유 toohello 리소스 서비스로 위임 해야 합니다. 와 tooa 리소스 서비스로 위임 될 수 있는 프런트 엔드 서비스에 잠재적 공격 지점이 표현 합니다. 프런트 엔드 서비스를 호스팅하는 서버의 보안이 손상 된, 되었으며 구성된 toodelegate tooresource 서비스 하는 경우 리소스 서비스 hello도 손상 될 수 있습니다.

> [!NOTE]
> Azure AD Domain Services 관리되는 도메인에서 도메인 관리자 권한이 없습니다. 따라서 **관리되는 도메인에 기존 KCD를 구성할 수 없습니다**. 이 문서에 설명된 대로 리소스 기반 KCD를 사용합니다. 또한 이 메커니즘은 더 안전합니다.
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a>리소스 기반 Kerberos 제한 위임
Windows Server 2012 R2 및 Windows Server 2012의 hello 서비스에 대 한 hello 기능 tooconfigure 제한 된 위임에서 도메인 관리자 toohello 서비스 관리자에 게 이전 되었습니다. 이러한 방식으로 백 엔드 서비스 관리자에 게 허용 하거나 프런트 엔드 서비스를 거부할 수 있습니다. 이 모델은 **리소스 기반 Kerberos 제한 위임**으로 알려져 있습니다.

리소스 기반 KCD는 PowerShell을 사용하여 구성됩니다. Hello Set-adcomputer 또는 컴퓨터 계정이 나 사용자 계정/서비스 계정의 계정을 가장 하는 hello 인지에 따라 Set-aduser cmdlet를 사용 합니다.

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a>관리되는 도메인에서 컴퓨터 계정에 대한 리소스 기반 KCD 구성
Hello 컴퓨터에서 실행 되는 웹 응용 프로그램 사용 한다고 가정 ' contoso100-webapp.contoso100.com'. 필요한 tooaccess hello 리소스 (에서 실행 되는 web API ' contoso100-api.contoso100.com') 도메인 사용자의 hello 컨텍스트에서 합니다. 이 시나리오에서 리소스 기반 KCD를 설정하는 방법은 다음과 같습니다.

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a>관리되는 도메인에서 사용자 계정에 대한 리소스 기반 KCD 구성
서비스 계정 'appsvc'으로 실행 되는 웹 앱이 있는 도메인 사용자의 hello 컨텍스트에서 tooaccess hello 리소스 ('backendsvc'-서비스 계정으로 실행 하는 웹 API) 필요한 가정 합니다. 이 시나리오에서 리소스 기반 KCD를 설정하는 방법은 다음과 같습니다.

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a>관련 콘텐츠
* [Azure AD Domain Services - 시작 가이드](active-directory-ds-getting-started.md)
* [Kerberos 제한 위임 개요](https://technet.microsoft.com/library/jj553400.aspx)
