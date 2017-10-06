---
title: "프록시 서비스에 대 한 App Discovery 레지스트리 설정 aaaCloud | Microsoft Docs"
description: "hello이이 항목에서는 tooprovide hello로 사용자의 단계 필요한 tooperform tooset hello 필요한 포트 hello Cloud App Discovery 에이전트를 실행 하는 hello 컴퓨터에 있어야 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>프록시 서비스용 클라우드 앱 검색 레지스트리 설정
Hello Cloud App Discovery 에이전트는 기본적으로 구성 된 toouse만 hello 포트 80 또는 443입니다. 사용자 지정 포트 (80 또는 443)를 사용 하는 프록시 서버는 환경에서 Cloud App Discovery를 설치 하려는 경우 필요한 tooconfigure 에이전트 toouse이이 포트입니다. hello 구성 레지스트리 키를 기반으로 합니다.

hello이이 항목에서는 tooprovide hello로 사용자의 단계 필요한 tooperform tooset hello 필요한 포트 hello Cloud App Discovery 에이전트를 실행 하는 hello 컴퓨터에 있어야 합니다.

**toomodify hello 포트 hello Cloud App Discovery 에이전트를 실행 하는 hello 컴퓨터에서 사용 하는 hello 다음 단계를 수행 합니다.**

1. Hello 레지스트리 편집기를 시작 합니다. <br> ![실행](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. 탐색 tooor hello 다음 레지스트리 키를 만듭니다. <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint** 
3. **포트**라고 불리는 새 **다중 문자열**을 만듭니다. ![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. tooopen hello **다중 문자열 편집** 대화 상자에서 hello 포트 값을 두 번 클릭 합니다.
5. Hello 값 데이터 입력란 hello 다음 값을 입력 하 고 조직에서 사용 되는 모든 사용자 지정 포트를 추가 합니다. 키를 누릅니다. <br><br>
   **80** <br>
   **8080** <br>
   **8118** <br>
   **8888** <br>
   **81** <br>
   **12080** <br>
   **6999** <br>
   **30606** <br>
   **31595** <br>
   **4080** <br>
   **443** <br>
   **1110** <br><br>
   ![다중 문자열 편집](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)
6. 클릭 **확인** tooclose hello **다중 문자열 편집** 대화 상자.

**추가 리소스**

* [조직 내에서 사용되고 있는 허용되지 않은 클라우드 앱을 검색하는 방법](active-directory-cloudappdiscovery-whatis.md) 

