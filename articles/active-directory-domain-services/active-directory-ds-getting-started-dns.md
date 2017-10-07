---
title: "Azure Active Directory 도메인 서비스: 업데이트 hello Azure 가상 네트워크에 대 한 DNS 설정을 | Microsoft Docs"
description: "Azure Active Directory Domain Services 시작"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a>Azure Active Directory Domain Services 활성화(미리 보기)

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>작업 4: hello Azure 가상 네트워크에 대 한 DNS 설정을 업데이트합니다
Hello 구성 작업 앞에에서 성공적으로 사용 하도록 설정한 디렉터리에 대 한 Azure Active Directory 도메인 서비스. hello 다음 작업은 tooensure hello 가상 네트워크 내에서 컴퓨터 연결 하 고 이러한 서비스를 사용할 수 있습니다. 이 문서에서는 사용자 가상 네트워크 toopoint toohello 두 IP 주소에 대해 Azure Active Directory 도메인 서비스를 hello 가상 네트워크에서 사용할 수 있는 hello DNS 서버 설정을 업데이트 합니다.

tooupdate hello DNS 서버 설정을 hello 가상 네트워크를 사용 하도록 설정한 Azure Active Directory 도메인 서비스, 단계를 수행 하는 전체 hello:

1. hello **개요** 탭 집합을 나열 **구성 단계를 필요한** toobe 관리 되는 도메인 완전히 프로 비전 한 후 수행 합니다. hello 첫 번째 구성 단계는 **가상 네트워크에 대 한 업데이트 DNS 서버 설정을**합니다.

    ![Domain Services - 완전히 프로비전한 후 개요 탭](./media/getting-started/domain-services-provisioned-overview.png)

2. 도메인이 완전히 프로비전되면 두 개의 IP 주소가 이 타일에 표시됩니다. 이들 IP 주소 각각은 관리되는 도메인에 대한 도메인 컨트롤러를 나타냅니다.

3. toocopy hello 첫 번째 IP 주소 tooclipboard를 hello 복사 다음 tooit 단추를 클릭 합니다. Hello 클릭 **DNS 구성 서버** 단추입니다.

4. Hello에 hello 첫 번째 IP 주소를 붙여 **추가 DNS 서버** hello 텍스트 상자로 **DNS 서버** 블레이드입니다. Toocopy hello 두 번째 IP 주소를 왼쪽 toohello 가로로 스크롤될를 hello에 붙여 넣습니다 **추가 DNS 서버** 텍스트 상자에 붙여넣습니다.

    ![Domain Services - DNS 업데이트](./media/getting-started/domain-services-update-dns.png)

5. 클릭 **저장** tooupdate hello DNS 서버 hello 가상 네트워크를 완료 합니다.

> [!NOTE]
> Hello 네트워크의 가상 컴퓨터만 다시 시작한 후에 새로운 DNS 설정을 hello를 가져옵니다. 필요할 경우 tooget 업데이트 hello DNS 설정을 바로, hello 포털, PowerShell 또는 CLI hello에 의해 다시 시작을 트리거하십시오.
>
>

## <a name="next-step"></a>다음 단계
[태스크 5: 암호 동기화 tooAzure Active Directory 도메인 서비스를 사용 하도록 설정](active-directory-ds-getting-started-password-sync.md)
