---
title: "StorSimple 8000 시리즈에 대 한 지원 티켓 aaaLog | Microsoft Docs"
description: "Toocreate 한 지원 요청 하는 방법을 알아보려면 StorSimple 장치에서 지원 세션을 시작 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a>StorSimple의 Microsoft 지원에 문의
Microsoft Azure StorSimple 솔루션에 문제가 발생하는 경우 기술 지원을 위해 서비스 요청을 할 수 있습니다. 지원 엔지니어와 온라인 세션에서 StorSimple 장치에서 지원 세션 toostart를 할 수도 있습니다. 이 문서에서는 다음을 안내합니다.

* 어떻게 toocreate 기술 지원 요청 합니다.
* 어떻게 지원 세션을 toostart hello StorSimple 장치의 Windows PowerShell 인터페이스입니다.

검토 hello [StorSimple 8000 시리즈 지원 Sla 및 정보](https://msdn.microsoft.com/library/mt433077.aspx) 지원 요청을 만들어야 합니다.

## <a name="create-a-support-request"></a>지원 요청 만들기
Hello 단계 toocreate 지원 요청에 다음을 수행 합니다.

#### <a name="toocreate-a-support-request"></a>toocreate 지원 요청
1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/)hello 오른쪽 위 모서리로에서 계정 이름을 클릭 한 다음 클릭 **Microsoft 지원에 문의**합니다.
   
    ![ManagementPortal을 통한 MS 지원 문의](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. 리디렉션된 toohello 새 Azure 포털 (portal.azure.com) 됩니다. Hello 클릭 **새로운 지원 요청** 바둑판식으로 배열입니다.
   
    ![새 포털을 통한 MS 지원 문의](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    Hello 오른쪽에 hello 화면, hello **새로운 지원 요청** 창이 나타납니다. 
   
    ![새 지원 요청 창](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. Hello에 **기본 사항** 대화 상자에서 다음 전체 hello:                                
   
   1. Hello에서 **종류를 발급** 드롭 다운 목록 **기술**합니다.
   2. 선택 된 **구독** hello 드롭 다운 목록에서 합니다.
   3. Hello에서 **서비스** 드롭 다운 목록 **StorSimple**합니다. 
   4. 선택 된 **지원 플랜** hello 드롭 다운 목록에서 합니다. 기술 지원 서비스 유료 지원 계획이 tooenable가 필요합니다.
4. **다음**을 누릅니다. hello **문제** 대화 상자가 나타납니다.
   
    ![새 지원 요청 창](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. Hello에 **문제** 대화 상자에서 다음 전체 hello:
   
   1. 선택 된 **심각도** hello 드롭 다운 목록에서 수준입니다.
   2. 선택 된 **문제 유형** hello 드롭 다운 목록에서 합니다.
   3. 선택 된 **범주** hello 드롭 다운 목록에서 합니다. 
   4. Hello에 **세부 정보** 상자 문제에 간략하게 설명 합니다.
   5. Hello에 **시간 프레임** 상자에서, hello 날짜, 시간 및 해당 문제의 가장 최근에 발생 toohello는 시간대를 표시 합니다.
   6. 아래 **파일 업로드**, hello 폴더 아이콘 toobrowse tooyour 지원 패키지를 클릭 합니다.
   7. 선택 hello **진단 정보를 공유** 확인란 합니다.
6. **다음**을 누릅니다. hello **연락처 정보** 대화 상자가 나타납니다.
   
    ![새 지원 요청 창](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. 연락처 정보를 입력하고 연락 방법(전화 또는 전자 메일)을 선택합니다. 
8. 선택 hello **이후 지원 요청에 대 한 연락처 변경 내용을 저장** 확인란 합니다.
9. **만들기**를 클릭합니다.

요청을 제출 하 고 나면 지원 엔지니어 연락을 드릴 가능한 한 빨리 tooproceed 요청 합니다.

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a>StorSimple용 Windows PowerShell에서 지원 세션 시작
hello StorSimple 장치 발생할 수 있는 문제를 tootroubleshoot, tooengage hello Microsoft 지원 팀과 함께 필요 합니다. Microsoft 지원 toouse tooyour 장치의 지원 세션 toolog 해야 합니다. 

Hello 다음이 수행 지원 세션 toostart 단계:

#### <a name="toostart-a-support-session"></a>지원 세션 toostart
1. 액세스 hello 직렬 콘솔을 사용 하 여 직접 또는 원격 컴퓨터에서 텔넷 세션을 통해 hello 장치입니다. toodo hello 단계에서 수행이, [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)합니다.
2. 열린 hello 세션에서 hello를 눌러 **Enter** 키 tooget 명령 프롬프트입니다.
3. Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다.
4. Hello 프롬프트 hello 다음 암호를 입력 합니다. 
   
    `Password1`
5. Hello 프롬프트에서 다음 명령을 hello를 입력 합니다.
   
    `Enable-HcsSupportAccess`
6. 암호화 된 문자열이 tooyou를 표시 됩니다. 메모장과 같은 텍스트 편집기에 이 문자열을 복사합니다.
7. 이 문자열을 저장해 전자 메일 메시지 tooMicrosoft 지원에에서 보냅니다. 

> [!IMPORTANT]
> `Disable-HcsSupportAccess`를 실행하여 지원 액세스를 비활성화할 수 있습니다. hello StorSimple 장치 toodisable 지원 액세스 hello 세션이 시작 된 후 8 시간이 시도 합니다. 지원 세션을 초기화 한 후 StorSimple 장치 자격 증명 모범 사례 toochange 이며
> 
> 

