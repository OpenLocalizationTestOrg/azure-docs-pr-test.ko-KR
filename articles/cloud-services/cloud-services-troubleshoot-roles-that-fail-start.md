---
title: "toostart 못하는 aaaTroubleshoot 역할 | Microsoft Docs"
description: "클라우드 서비스 역할 toostart 못할 이유 몇 가지 일반적인 원인은 다음과 같습니다. 솔루션 toothese 문제 제공 됩니다."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a>Toostart 실패 하는 클라우드 서비스 역할 문제 해결
다음은 몇 가지 일반적인 문제와 toostart 실패 하는 솔루션 관련된 tooAzure 클라우드 서비스 역할입니다.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a>DLL 또는 종속성 누락
응답하지 않는 역할 및 **초기화 중**, **사용 중** 및 **중지** 상태를 반복하는 역할은 누락된 DLL 또는 어셈블리 때문에 발생할 수 있습니다.

누락된 DLL 또는 어셈블리의 증상은 다음과 같을 수 있습니다.

* 역할 인스턴스가 **초기화 중**, **사용 중** 및 **중지** 상태를 반복하고 있습니다.
* 역할 인스턴스에 너무 이동**준비** 하지만 tooyour 웹 응용 프로그램을 이동 하는 경우 hello 페이지가 표시 되지 않습니다.

이러한 문제를 조사하기 위해 권장되는 여러 가지 방법이 있습니다.

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a>웹 역할에서 누락된 DLL 문제 진단
웹 역할에 배포 된 tooa 웹 사이트를 탐색 하 고 hello 브라우저 표시 서버 오류와 비슷한 toohello 다음을를 DLL이 누락 된 나타낼 수 있습니다.

!['/' 응용 프로그램의 서버 오류.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a>사용자 지정 오류를 해제하여 문제 진단
Hello 웹 역할 tooset hello 사용자 지정 오류 모드 tooOff에 대 한 hello web.config를 구성 하 고 hello 서비스를 다시 배포 하 여 자세한 오류 정보를 볼 수 있습니다.

더 tooview 원격 데스크톱을 사용 하지 않고 오류를 완료 합니다.

1. Microsoft Visual Studio에서 hello 솔루션을 엽니다.
2. Hello에 **솔루션 탐색기**을 hello web.config 파일을 찾아서 엽니다.
3. Hello web.config 파일에서 hello system.web 섹션을 찾아서 hello 다음 줄 추가:

    ```xml
    <customErrors mode="Off" />
    ```
4. Hello 파일을 저장 합니다.
5. 패키지에 포함 시키고 hello 서비스를 다시 배포 합니다.

Hello 서비스를 다시 배포 되 면 hello 누락 된 어셈블리 또는 DLL의 hello 이름으로 오류 메시지가 표시 됩니다.

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a>원격으로 hello 오류를 확인 하 여 문제를 진단 합니다.
원격 데스크톱 tooaccess hello 역할을 사용 하 고 자세한 오류 정보를 원격으로 볼 수 있습니다. 원격 데스크톱을 사용 하 여 다음 단계 tooview hello 오류 hello를 사용 합니다.

1. Azure SDK 1.3 이상이 설치되어야 합니다.
2. Visual Studio를 사용 하 여 hello 솔루션의 hello 배포 하는 동안 선택 너무 "원격 데스크톱 연결 구성...". Hello 원격 데스크톱 연결 구성에 대 한 자세한 내용은 참조 하십시오. [Azure 역할과 함께 원격 데스크톱 사용 하 여](../vs-azure-tools-remote-desktop-roles.md)합니다.
3. Hello Microsoft Azure 클래식 포털에서 hello 인스턴스 상태가 표시 되 면 **준비**, hello 역할 인스턴스 중 하나를 클릭 합니다.
4. Hello 클릭 **연결** hello 아이콘 **원격 액세스** hello 리본 메뉴의 영역입니다.
5. Hello 원격 데스크톱 구성 중에 지정 된 hello 자격 증명을 사용 하 여 toohello 가상 컴퓨터에 로그인 합니다.
6. 명령 창을 엽니다.
7. `IPconfig`을 입력합니다.
8. 참고 hello IPV4 주소 값입니다.
9. Internet Explorer를 엽니다.
10. Hello 주소와 hello hello 웹 응용 프로그램 이름을 입력 합니다. 예: `http://<IPV4 Address>/default.aspx`.

웹 사이트를 탐색 toohello 하 더 구체적인 오류 메시지가 이제 반환 합니다.

* '/' 응용 프로그램의 서버 오류.
* 설명: hello 현재 웹 요청 hello 실행 하는 동안 처리 되지 않은 예외가 발생 했습니다. Hello 오류에 대 한 자세한 내용은 hello 스택 추적 및 hello 코드에서 발생 한 위치를 검토 하십시오.
* 예외 세부 정보: System.IO.FIleNotFoundException: 파일이나 어셈블리를 로드할 수 없습니다 'Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ 또는 해당 종속성 중 하나입니다. hello 시스템 지정 된 hello 파일을 찾을 수 없습니다.

예:

!['/' 응용 프로그램의 명시적 서버 오류](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a>Hello 계산 에뮬레이터를 사용 하 여 문제를 진단 합니다.
Microsoft Azure 계산 에뮬레이터 toodiagnose hello를 사용 하 여 수 있으며의 누락 된 종속성 및 web.config 오류 문제를 해결할 수 있습니다.

이 진단 방법을 사용하여 최상의 결과가 발생한 경우 Windows 새로 설치한 컴퓨터 또는 가상 컴퓨터를 사용해야 합니다. toobest은 hello Azure 환경을 시뮬레이션, Windows Server 2008 R2 x64 사용 합니다.

1. 독립 실행형 버전의 hello hello 설치 [Azure SDK](https://azure.microsoft.com/downloads/)합니다.
2. Hello 개발 컴퓨터에서 hello 클라우드 서비스 프로젝트를 빌드하십시오.
3. Windows 탐색기에서 hello 클라우드 서비스 프로젝트의 toohello bin\debug 폴더를 이동 합니다.
4. Hello.csx 폴더와.cscfg 파일 toohello 컴퓨터 toodebug hello 문제를 사용 하 고 있는지를 복사 합니다.
5. 클린 컴퓨터 hello에서 유형과 Azure SDK 명령 프롬프트 창을 엽니다 `csrun.exe /devstore:start`합니다.
6. Hello 명령 프롬프트에서 입력 `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`합니다.
7. Hello 역할 시작 될 때 Internet Explorer에 자세한 오류 정보가 표시 됩니다. 표준 Windows 문제 해결 도구를 사용할 수도 있습니다 toofurther hello 문제를 진단 합니다.

## <a name="diagnose-issues-by-using-intellitrace"></a>IntelliTrace를 사용하여 문제 진단
.NET Framework 4를 사용하는 작업자 및 웹 역할의 경우 Microsoft Visual Studio Enterprise에서 사용 가능한 [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx)를 사용할 수 있습니다.

사용 하도록 설정 하는 IntelliTrace에서 이러한 단계 toodeploy hello 서비스를 수행 합니다.

1. Azure SDK 1.3 이상이 설치되었는지 확인합니다.
2. Visual Studio를 사용 하 여 hello 솔루션을 배포 합니다. 배포 하는 동안 확인 hello **.NET 4 역할에 대해 IntelliTrace 사용** 확인란 합니다.
3. Hello 인스턴스가 시작 되 면 hello 열어 **서버 탐색기**합니다.
4. Hello 확장 **Azure\\클라우드 서비스** 노드 hello 배포를 찾습니다.
5. Hello 배포를 확장 하 고 hello 역할 인스턴스를 참조 하십시오. Hello 인스턴스 중 하나를 오른쪽 단추로 클릭 합니다.
6. **IntelliTrace 로그 보기**를 선택합니다. hello **IntelliTrace 요약** 열립니다.
7. Hello 요약의 hello 예외 섹션을 찾습니다. Hello 섹션 표시 되는 예외가 있으면 **예외 데이터**합니다.
8. Hello 확장 **예외 데이터** 를 찾아서 **System.IO.FileNotFoundException** 비슷한 toohello 다음 오류:

![예외 데이터, 파일 또는 어셈블리 누락](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a>누락된 DLL 및 어셈블리 주소 지정
DLL 및 어셈블리 오류 누락 tooaddress 다음이 단계를 따르십시오.

1. Visual Studio에서 hello 솔루션을 엽니다.
2. **솔루션 탐색기**개방형 hello **참조** 폴더입니다.
3. Hello 오류에서 확인 된 hello 어셈블리를 클릭 합니다.
4. Hello에 **속성** 창 찾기 **로컬 복사 속성** 너무 hello 값을 설정 하 고**True**합니다.
5. Hello 클라우드 서비스를 다시 배포 합니다.

모든 오류가 오류를 확인 한 후 hello를 검사 하지 않고 hello 서비스를 배포할 수 있습니다 **.NET 4 역할에 대해 IntelliTrace 사용** 확인란 합니다.

## <a name="next-steps"></a>다음 단계
클라우드 서비스에 대한 [문제해결 문서](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 를 더 봅니다.

Azure PaaS 컴퓨터 진단 데이터를 사용 하 여 tootroubleshoot 클라우드 서비스 역할을 발급 하는 방법을 toolearn 참조 [Kevin Williamson 블로그 시리즈](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)합니다.
