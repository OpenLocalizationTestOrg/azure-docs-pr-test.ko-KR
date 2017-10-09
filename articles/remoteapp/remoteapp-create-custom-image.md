---
title: "Azure RemoteApp에 대 한 사용자 지정 템플릿 이미지 aaaHow toocreate | Microsoft Docs"
description: "Azure RemoteApp에 대 한 사용자 지정 템플릿을 toocreate 이미지 하는 방법을 알아봅니다. 하이브리드 또는 클라우드 컬렉션에서 이 템플릿을 사용할 수 있습니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: b9ec5b51-f7cd-470b-8545-d0fd714c5982
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9e3a0b2d3cc56177ea51406e6cecfe19ff235340
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-custom-template-image-for-azure-remoteapp"></a>Azure RemoteApp에 대 한 사용자 지정 템플릿을 toocreate 이미지 방법
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure RemoteApp에서 사용자와 tooshare 되도록 모든 hello 프로그램 Windows Server 2012 R2 템플릿 이미지 toohost를 사용 합니다. RemoteApp 템플릿 이미지를 사용자 지정 toocreate을 기존 이미지 시작 하거나 새로 만들 수 있습니다. 

> [!TIP]
> Azure VM에서 이미지를 만들 수 있다는 것을 알고 있나요? True 스토리 하며의 수를 줄일 hello 기간 것은 tooimport hello 이미지입니다. 체크 아웃 hello 단계 [여기](remoteapp-image-on-azurevm.md)합니다.
> 
> 

에 Azure RemoteApp과 함께 사용 하기 위해 업로드할 수 있는 hello 이미지에 대 한 hello 요구 사항:

* hello 이미지 크기를 Mb의 배수 여야 합니다. Tooupload 정확한 배수가 아닌 이미지에서 하면 hello 업로드가 실패 합니다.
* hello 이미지 크기는 127GB 이어야 하거나 축소 합니다.
* VHD 파일에 있어야 합니다. VHDX 파일 [Hyper-V 가상 하드 드라이브]은 현재 지원되지 않습니다.
* hello VHD 2 세대 가상 컴퓨터 수 없습니다.
* hello VHD는 고정 크기 또는 동적 확장 될 수 있습니다. 크기가 고정 된 VHD 파일 보다 작은 시간 tooupload tooAzure 사용 하기 때문에 동적 확장 VHD 것이 좋습니다.
* hello 레코드 MBR (마스터 부트) 파티션 스타일을 사용 하 여 hello 디스크를 초기화 합니다. hello GUID 파티션 테이블 (GPT) 파티션 스타일을 사용 하는 것이 없습니다.
* hello VHD에는 Windows Server 2012 r 2를 설치 하는 단일 포함 해야 합니다. 여러 볼륨을 포함할 수 있지만 한 볼륨만 Windows의 설치를 포함합니다.
* hello RDSH 원격 데스크톱 세션 호스트 () 역할 및 hello 데스크톱 경험 기능을 설치 해야 합니다.
* hello 원격 데스크톱 연결 브로커 역할 해야 *하지* 설치할 수 있습니다.
* hello 암호화 EFS (파일 시스템) 사용 하지 않도록 설정 해야 합니다.
* hello 이미지 있어야 hello 매개 변수를 사용 하 여 SYSPREPed **/oobe /generalize /shutdown** (hello를 사용 하지 않는 **/mode: vm** 매개 변수).
* 스냅숏 체인으로부터의 VHD 업로드는 지원되지 않습니다.

**시작하기 전에**

Hello 서비스를 만들기 전에 toodo hello 다음이 필요 합니다.

* [등록](https://azure.microsoft.com/services/remoteapp/) 합니다.
* Active Directory toouse에서 사용자 계정을 hello RemoteApp 서비스 계정으로 만듭니다. 컴퓨터 toohello 도메인을만 연결할 수 있도록이 계정에 대 한 hello 권한을 제한 합니다. 자세한 내용은 [RemoteApp에 대해 Azure Active Directory 구성](remoteapp-ad.md) 을 참조하세요.
* 온-프레미스 네트워크에 대한 정보 수집: IP 주소 정보 및 VPN 장치 세부 정보입니다.
* Hello 설치 [Azure PowerShell](/powershell/azure/overview) 모듈입니다.
* 에 액세스 하려면 toogrant hello 사용자에 대 한 정보를 수집 합니다. 이 정보는 사용자의 Microsoft 계정 정보나 Active Directory 작업 계정 정보가 될 수 있습니다.

## <a name="create-a-template-image"></a>템플릿 이미지 만들기
다음은 hello 상위 수준 단계 toocreate 처음부터 새 템플릿 이미지입니다.

1. Windows Server 2012 R2 Update DVD 또는 ISO 이미지를 찾습니다.
2. VHD 파일을 만듭니다.
3. Windows Server 2012 R2를 설치합니다.
4. Hello RDSH 원격 데스크톱 세션 호스트 () 역할과 hello 데스크톱 경험 기능을 설치 합니다.
5. 응용 프로그램에 필요한 추가 기능을 설치합니다.
6. 응용 프로그램을 설치하고 구성합니다. 응용 프로그램 또는 tooshare toohello 프로그램 toomake 공유 앱을 쉽게 추가 **시작** **%systemdrive%\ProgramData\Microsoft\Windows\Start 메뉴 \ 프로그램에서 특히 hello 이미지의 메뉴.
7. 응용 프로그램에 필요한 추가 Windows 구성을 수행합니다.
8. Hello 암호화 EFS (파일 시스템)를 사용 하지 않도록 설정 합니다.
9. **방법:** tooWindows 업데이트를 이동 하 고 모든 중요 업데이트를 설치 합니다.
10. SYSPREP hello 이미지입니다.

hello 새 이미지를 만드는 자세한 단계는

1. Windows Server 2012 R2 Update DVD 또는 ISO 이미지를 찾습니다.
2. 디스크 관리를 사용하여 VHD 파일을 만듭니다.
   
   1. 디스크 관리(diskmgmt.msc)를 실행합니다.
   2. 40GB 크기의 동적으로 확장되는 VHD를 만듭니다. (Windows, 응용 프로그램 및 사용자 지정 항목에 필요한 공간의 hello 크기를 예측 합니다. 데스크톱 경험 기능이 설치 및 hello RDSH 역할과 함께 Windows Server에서는 약 10GB 공간의) 합니다.
      
      1. **작업 > VHD 만들기**를 클릭합니다.
      2. Hello 위치, 크기 및 VHD 형식을 지정 합니다. **동적 확장**을 선택한 다음 **확인**을 클릭합니다.
      
      그러면 몇 초 정도 실행됩니다. VHD 만들기 hello 완료 되 면 새 디스크를 드라이브 문자 없이 hello 디스크 관리 콘솔에 "초기화 되지 않았습니다" 상태로 표시 됩니다.
      
      * Hello 디스크 (하지: hello 할당 되지 않은 공간)을 마우스 오른쪽 단추로 누른 **디스크 초기화**합니다. 선택 **MBR** (마스터 부트 레코드) hello 파티션 형식을, 및 클릭 **확인**합니다.
      * 새 볼륨을 만든: hello 할당 되지 않은 공간을 마우스 오른쪽 단추로 누른 **새 단순 볼륨**합니다. Hello 마법사에서 hello 기본값을 적용 수 있지만 hello 템플릿 이미지를 업로드 하는 경우 드라이브 문자 tooavoid 잠재적 문제를 할당 해야 합니다.
      * Hello 디스크를 마우스 오른쪽 단추로 누른 **VHD 분리**합니다.
3. Windows Server 2012 R2 설치:
   
   1. 새 가상 컴퓨터를 만듭니다. Hello 클라이언트 Hyper-v 또는 Hyper-v 관리자에서 새 가상 컴퓨터 마법사를 사용 합니다.
      1. Hello 세대 지정 페이지에서 선택 **1 세대**합니다.
      2. Hello 가상 하드 디스크 연결 페이지에서 선택 **기존 가상 하드 디스크를 사용 하 여**, toohello hello 이전 단계에서 만든 VHD를 찾습니다.
      3. Hello 설치 옵션 페이지에서 선택 **부팅 CD/DVD_ROM에서에서 운영 체제 설치**, 한 다음 Windows Server 2012 R2 설치 미디어의 hello 위치를 선택 합니다.
      4. Windows hello 마법사 필요한 tooinstall에서 다른 옵션 및 응용 프로그램을 선택 합니다. Hello 마법사를 완료 합니다.
   2. Hello 마법사를 완료 한 후 hello 가상 컴퓨터의 hello 설정을 편집 하 고 필요한 tooinstall 창과 hello 가상 프로세서 수와 같이, 프로그램 기타 변경을 수행 하 고 클릭 **확인**합니다.
   3. Toohello 가상 컴퓨터에 연결 하 고 Windows Server 2012 r 2를 설치 합니다.
4. Hello RDSH 원격 데스크톱 세션 호스트 () 역할과 hello 데스크톱 경험 기능을 설치 합니다.
   1. 서버 관리자를 실행합니다.
   2. 클릭 **역할 및 기능 추가** hello 시작 화면 또는 hello **관리** 메뉴.
   3. 클릭 **다음** hello 시작 하기 전에 페이지입니다.
   4. **역할 기반 또는 기능 기반 설치**를 선택하고 **다음**을 클릭합니다.
   5. Hello 목록에서 hello 로컬 컴퓨터를 선택한 다음 클릭 **다음**합니다.
   6. **원격 데스크톱 서비스**를 선택하고 **다음**을 클릭합니다.
   7. **사용자 인터페이스 및 인프라**를 확장하고 **데스크톱 환경**을 선택합니다.
   8. **기능 추가**를 클릭하고 **다음**을 클릭합니다.
   9. Hello 원격 데스크톱 서비스 페이지에서 클릭 **다음**합니다.
   10. **원격 데스크톱 세션 호스트**를 클릭합니다.
   11. **기능 추가**를 클릭하고 **다음**을 클릭합니다.
   12. Hello 설치 선택 확인 페이지를 선택 **필요한 경우 자동으로 hello 대상 서버 다시 시작**, 클릭 하 고 **예** hello에 경고를 다시 시작 합니다.
   13. **Install**을 클릭합니다. hello 컴퓨터 다시 시작 됩니다.
5. .NET Framework 3.5 hello 등의 응용 프로그램에 필요한 추가 기능을 설치 합니다. tooinstall hello 기능을 역할에 추가 하는 hello 및 기능 마법사를 실행 합니다.
6. 설치 하 고 hello 프로그램과 toopublish RemoteApp 통해 원하는 응용 프로그램을 구성 합니다.

> [!IMPORTANT]
> Hello RDSH 역할을 설치 tooensure 응용 프로그램을 설치 하기 전에 tooRemoteApp 업로드 이전 hello 이미지는 응용 프로그램 호환성에 문제가 있는지 검색 합니다.
> 
> 바로 가기 tooyour 응용 프로그램이 있는지 확인 (**.lnk** 파일) hello에 표시 **시작** 모든 사용자 (%systemdrive%\ProgramData\Microsoft\Windows\Start 메뉴 \ 프로그램)에 대 한 메뉴입니다. 또한 hello에 나와 있는 해당 hello 아이콘을 확인 **시작** 메뉴는 원하는 대로 사용자 toosee 합니다. 그렇지 않으면 변경합니다. (이렇게 하지 않으면 *가* tooadd hello 응용 프로그램 toohello 시작 메뉴, 하지만 훨씬 더 쉽게 toopublish hello 응용 프로그램에서에서 있도록 RemoteApp 합니다. 그렇지 않으면 한 tooprovide hello 응용 프로그램에 대 한 설치 경로 hello hello 앱을 게시 하면 됩니다.)
> 
> 

1. 응용 프로그램에 필요한 추가 Windows 구성을 수행합니다.
2. Hello 암호화 EFS (파일 시스템)를 사용 하지 않도록 설정 합니다. 다음 명령을 관리자 권한 명령 창을 hello를 실행 합니다.
   
     Fsutil behavior set disableencryption 1
   
   또는 설정 하거나 hello 다음 hello 레지스트리에서 DWORD 값을 추가할 수 있습니다.
   
     HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1
3. Azure 가상 컴퓨터 내 이미지를 작성 하는 경우 이름 바꾸기 hello  **\%windir%\Panther\Unattend.xml** 파일, hello 업로드 스크립트 작업에서 나중에 사용 되는 차단 됩니다. Toorevert를 배포 해야 할 경우 hello 파일을 계속 할 수 있도록이 파일 tooUnattend.old의 hello 이름을 변경 합니다.
4. 업데이트 tooWindows 이동한 다음 모든 중요 업데이트를 설치 합니다. Windows Update 여러 번 tooget toorun 모든 업데이트를 할 수 있습니다. (경우에 따라 업데이트를 설치하며 자체 해당 업데이트는 업데이트 해야합니다.)
5. SYSPREP hello 이미지입니다. 관리자 권한 명령 프롬프트에서 다음 명령을 hello를 실행 합니다.
   
   **C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /shutdown**
   
   **참고:** hello를 사용 하지 않는 **/mode: vm** 스위치의 가상 컴퓨터는 SYSPREP 명령을 hello 합니다.

## <a name="next-steps"></a>다음 단계
사용자 지정 템플릿 이미지를가지고 해당 이미지 tooyour RemoteApp 컬렉션 tooupload 할 수 있습니다. 컬렉션 hello 정보에 아티클을 toocreate 다음 hello 사용 합니다.

* [어떻게 toocreate RemoteApp의 하이브리드 컬렉션](remoteapp-create-hybrid-deployment.md)
* [어떻게 toocreate RemoteApp의 클라우드 컬렉션](remoteapp-create-cloud-deployment.md)

