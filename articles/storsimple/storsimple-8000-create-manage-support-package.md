---
title: "지원 패키지 aaaCreate StorSimple 8000 시리즈 | Microsoft Docs"
description: "Toocreate, 암호를 해독 하면 및 StorSimple 8000 시리즈 장치에 대 한 지원 패키지 편집 방법에 대해 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 857555b6ba31b1527f8f00d19818ebbec6005d0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a>StorSimple 8000 시리즈용 지원 패키지 만들기 및 관리

## <a name="overview"></a>개요

StorSimple 지원 패키지는 StorSimple 장치 문제 해결에 모든 관련 로그 tooassist Microsoft 기술 지원 서비스를 수집 하는 사용 하기 쉬운 메커니즘입니다. hello 수집 된 로그 암호화 되 고 압축 합니다.

이 자습서는 toocreate 단계별 지침을 포함 하 고 StorSimple 8000 시리즈 장치에 대 한 hello 지원 패키지를 관리 합니다. StorSimple 가상 배열을 사용 하는 경우 너무 이동[로그 패키지를 생성할](storsimple-ova-web-ui-admin.md#generate-a-log-package)합니다.

## <a name="create-a-support-package"></a>지원 패키지 만들기

경우에 따라 해야 toomanually StorSimple 용 Windows PowerShell을 통해 hello 지원 패키지를 만듭니다. 예:

* 로그에서 tooremove 중요 한 정보가 필요한 경우 Microsoft 지원에 이전 toosharing 파일.
* Tooconnectivity 문제 인해 hello 패키지를 업로드 하는 데 어려움이 발생 하는 경우 있습니다.

전자 메일을 통해 Microsoft 지원에 수동으로 생성된 지원 패키지를 공유할 수 있습니다. Hello StorSimple 용 Windows PowerShell에서 지원 패키지 단계 toocreate 다음을 수행 합니다.

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a>StorSimple 용 Windows PowerShell에서 지원 패키지 toocreate

1. 가 tooconnect tooyour StorSimple 장치를 사용 하는 hello 원격 컴퓨터에서 관리자 권한으로 Windows PowerShell 세션 toostart hello 다음 명령을 입력 합니다.
   
    `Start PowerShell`
2. Hello Windows PowerShell 세션에서 장치의 SSAdmin 콘솔 toohello 연결:
   
   1. Hello 명령 프롬프트에서 다음을 입력 합니다.
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. Hello 대화 상자가 열리면 장치 관리자 암호를 입력 합니다. hello 기본 암호는 _Password1_합니다.
     
      ![PowerShell 자격 증명 대화 상자](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. **확인**을 선택합니다.
   4. Hello 명령 프롬프트에서 다음을 입력 합니다.
     
      `Enter-PSSession $MS`
3. 열린 hello 세션 hello 적절 한 명령을 입력 합니다.
   
   * 암호로 보호된 네트워크 공유에 다음을 입력합니다.
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       메시지가 표시 됩니다는 암호, 경로 toohello 네트워크 공유 폴더 및 암호화의 암호를 (hello 지원 패키지가 암호화 되기) 때문입니다. 그런 다음 지원 패키지 hello 지정 된 폴더에 생성 됩니다.
   * 암호로 보호 되지 않은 공유에 대 한 불필요 hello `-Credential` 매개 변수입니다. Hello 다음을 입력 합니다.
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       hello 지정 된 네트워크 공유 폴더에 있는 두 컨트롤러에 대 한 hello 지원 패키지가 생성 됩니다. 문제 해결에 대 한 지원 tooMicrosoft 보낼 수 있는 암호화, 압축 된 파일입니다. 자세한 내용은 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)를 참조하세요.

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a>hello Export-hcssupportpackage cmdlet 매개 변수

Hello hello Export-hcssupportpackage cmdlet과 함께 매개 변수 뒤에 사용할 수 있습니다.

| 매개 변수 | 필수/선택 | 설명 |
| --- | --- | --- |
| `-Path` |필수 |지원 패키지가 배치 되는 hello hello 네트워크 공유 폴더의 tooprovide hello 위치를 사용 합니다. |
| `-EncryptionPassphrase` |필수 |사용 하 여 tooprovide 암호 toohelp hello 지원 패키지를 암호화 합니다. |
| `-Credential` |옵션 |Hello 네트워크 공유 폴더에 대 한 toosupply 액세스 자격 증명을 사용 합니다. |
| `-Force` |옵션 |Tooskip hello 암호화 암호 확인 단계를 사용 합니다. |
| `-PackageTag` |옵션 |Toospecify에서 디렉터리를 사용 *경로* 는 hello 지원 패키지가 배치 됩니다. hello 기본값은 [장치 이름]-[현재 날짜 및 시간: yyyy-mm-dd-hh-mm-ss]. |
| `-Scope` |옵션 |으로 지정 **클러스터** (기본값) toocreate 두 컨트롤러 모두에 대 한 지원 패키지 합니다. 현재 컨트롤러 hello에 대 한 패키지 toocreate 하려는 지정 **컨트롤러**합니다. |

## <a name="edit-a-support-package"></a>지원 패키지 편집

지원 패키지를 생성 한 후에 tooedit hello 패키지 tooremove 중요 한 정보가 필요할 수 있습니다. 이 볼륨 이름, 장치 IP 주소 및 hello 로그 파일에서 백업 이름에 포함할 수 있습니다.

> [!IMPORTANT]
> StorSimple용 Windows PowerShell을 통해 생성된 지원 패키지를 편집할 수 있습니다. Hello StorSimple 장치 관리자 서비스와 Azure 포털에서에서 만든 패키지를 편집할 수 없습니다.

tooedit 지원 패키지 hello Microsoft 지원 사이트에 업로드 하기 전에 먼저 hello 지원 패키지 암호를 해독 hello 파일을 편집한 다음 다시 암호화 합니다. Hello 다음 단계를 수행 합니다.

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a>StorSimple 용 Windows PowerShell에서 지원 패키지 tooedit

1. 에 이전에 설명 된 대로 지원 패키지 생성 [toocreate StorSimple 용 Windows PowerShell에서 지원 패키지](#to-create-a-support-package-in-windows-powershell-for-storsimple)합니다.
2. [Hello 스크립트 다운로드](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) 클라이언트에서 로컬로 합니다.
3. Hello Windows PowerShell 모듈을 가져옵니다. Hello 경로 toohello 로컬 폴더를 다운로드 한 hello 스크립트를 지정 합니다. tooimport hello 모듈 입력:
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. 모든 hello 파일이 *.aes* 압축 및 암호화 하는 파일입니다. toodecompress 및 암호 해독 파일을 입력 합니다.
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    Note hello 실제 파일 확장명 모든 hello 파일에 대해 표시 됩니다.
   
    ![지원 패키지 편집](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. Hello 암호화의 암호에 대 한 메시지가 면 hello 지원 패키지를 만들 때 사용한 hello 암호를 입력 합니다.
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. Hello 로그 파일이 있는 toohello 폴더를 찾습니다. Hello 로그 파일은 이제 압축을 풀 고 암호 해독 하기 때문에 이러한 원래 파일 확장명 갖습니다. 이러한 파일 tooremove 볼륨 이름, 장치 IP 주소 등의 모든 고객 관련 정보를 수정 하 고 hello 파일을 저장 합니다.
7. 닫기 hello 파일 toocompress gzip을 사용 하 여 AES 256으로 암호화 합니다. 이 네트워크를 통해 hello 지원 패키지를 전송에서 보안 성능 및 속도입니다. toocompress 파일을 암호화 하 고 hello 다음을 입력 합니다.
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![지원 패키지 편집](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. 메시지가 표시 되 면 hello 수정 된 지원 패키지에 대 한 암호화의 암호를 제공 합니다.
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. Microsoft 기술 지원 요청 될 때와 공유할 수 있도록 hello 새 암호를 적어 둡니다.

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a>예: 암호로 보호된 공유에 대한 지원 패키지에서 파일 편집

다음 예제는 hello toodecrypt, 편집 하 고 다시 지원 패키지를 암호화 하는 방법을 보여 줍니다.

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a>다음 단계

* Hello에 대 한 자세한 내용은 [hello 지원 패키지에서 수집 된 정보](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)
* 너무 방법에 대해 알아봅니다[사용 하 여 지원 패키지 및 장치 tootroubleshoot 장치 배포를 기록](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting)합니다.
* 너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.

