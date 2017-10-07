---
title: "aaaHow toogenerate 및 전송 HSM 보호 키 Azure 키 자격 증명 모음에 대 한 | Microsoft Docs"
description: "이 문서 toohelp 계획을 생성 및 다음 Azure 키 자격 증명 모음 HSM 보호 키 toouse 직접 전송 사용 합니다. BYOK, 즉 Bring Your Own Key라고도 합니다."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a>어떻게 toogenerate 및 전송 HSM 보호 키를 Azure 키 자격 증명 모음
## <a name="introduction"></a>소개
추가 된 보증에 대 한 Azure 키 자격 증명 모음을 사용 하는 경우 수 가져오거나 hello HSM 경계를 벗어날 하드웨어 보안 모듈 (Hsm)의 키를 생성 합니다. 이 시나리오는 종종 참조 tooas *고유한 키를 가져올*, byok 합니다. hello Hsm은 FIPS 140-2 수준 2 유효성을 검사 합니다. Azure 키 자격 증명 모음은 Thales nShield Hsm tooprotect 제품군 키를 사용합니다.

이 항목 toohelp 계획을 생성 및 다음 Azure 키 자격 증명 모음 HSM 보호 키 toouse 직접 전송의 hello 정보를 사용 합니다.

이 기능은 Azure 중국에 사용할 수 없습니다.

> [!NOTE]
> Azure 주요 자격 증명 모음에 대한 자세한 내용은 [Azure 주요 자격 증명 모음이란?](key-vault-whatis.md)  
>
> HSM 보호된 키를 위해 주요 자격 증명 모음 만들기가 포함된 자습서를 시작하려면 [Azure 주요 자격 증명 모음 시작](key-vault-get-started.md)을 참조하세요.
>
>

생성 하 고 hello 인터넷을 통해 HSM 보호 키를 전송 하는 방법에 대 한 자세한 정보:

* Hello 공격 노출 영역을 줄일 수 있는 오프 라인 워크스테이션에서 hello 키를 생성 합니다.
* hello 키와는 키 KEK (키 교환), 암호화 상태를 유지 전송된 toohello Azure 키 자격 증명 모음 Hsm 될 때까지 암호화 됩니다. 키의 암호화 된 버전 hello만 hello 원래 워크스테이션을 벗어납니다.
* hello 도구 집합 키 toohello Azure 키 자격 증명 모음 보안 권역에 바인딩하는 테 넌 트 키에 속성을 설정 합니다. 따라서 후 hello Azure 키 자격 증명 모음 Hsm를 받아 암호를 해독 키만 이러한 Hsm 사용할 수 있습니다. 키는 내보낼 수 없습니다. 이 바인딩은 Thales Hsm hello로 적용 됩니다.
* hello 키 교환 KEK (키)를 사용 하는 tooencrypt 키 hello Azure 키 자격 증명 모음 Hsm 내부에서 생성 되며 되며 내보낼 수 없습니다. hello Hsm 적용 hello Hsm 외부 hello KEK의 일반 버전이 있을 수 있습니다. 또한 hello 도구 집합 되지 하 고 KEK가 Thales에서 제조한 정품 HSM 내부에서 생성 하는 hello 나타내는 Thales 로부터의 증명이 포함 되어 있습니다.
* hello 도구 집합에는 Azure 키 자격 증명 모음 보안 권역도 Thales에서 제조한 정품 HSM에서 생성 하는 hello 나타내는 Thales 로부터의 증명이 포함 되어 있습니다. 이 증명 증명 tooyou는 Microsoft가 정품 하드웨어를 사용 합니다.
* Microsoft는 각 지역별로 별도의 보안 권역과 별도의 KEK를 사용합니다. 이러한 분리는 암호화 된 hello 지역의 데이터 센터 에서만에서 키를 사용할 수 있는지 확인 합니다. 예를 들어 유럽 고객의 키는 북아메리카 또는 아시아의 데이터 센터에서 사용할 수 없습니다.

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a>Thales HSM 및 Microsoft 서비스에 대한 추가 정보
Thales e-보안은 데이터 암호화 및 사이버 보안 솔루션 toohello 금융 서비스, 첨단 기술, 제조, 정부 및 기술 부문에는 선도적인 글로벌 기업입니다. 40 년 역사가 보호 회사 및 정부 정보를 Thales 솔루션은 hello 5 명의 가장 큰 에너지 및 항공 우주 회사의 4/에서 사용 됩니다. 또한 22개 NATO 국가에서 사용되고 있으며 전세계 지불 거래의 80퍼센트 이상의 보안을 담당하고 있습니다.

Microsoft는 Hsm에 대 한 아트 Thales tooenhance hello 상태와 함께 합니다. 이러한 향상 된이 기능을 사용 하면 tooget hello 프로그램은 키에 대 한 제어권을 포기 하지 않고 호스팅된 서비스의 일반적인 이점을 있습니다. 특히, 이러한 향상 된 고객이 Microsoft가를 보유 하지 않는 hello Hsm을 관리 합니다. 클라우드 서비스, Azure 주요 자격 증명 모음 없이 소집 toomeet 수직 확장로 조직의 사용 급증 합니다. At hello 동일 time, Microsoft Hsm 내부에서 사용자의 키 보호 됩니다: hello 키를 생성 하 고 tooMicrosoft의 Hsm을 전송 했으므로 hello 키 수명 주기에 대 한 제어권을 유지 합니다.

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a>Azure 주요 자격 증명 모음에 대한 BYOK(Bring Your Own Key) 구현
사용 하 여 hello HSM 보호 키 생성 되며, 주요 자격 증명 모음 tooAzure 전송 하는 경우 정보 및 절차를 따라-hello bring 키 (BYOK) 하는 시나리오입니다.

## <a name="prerequisites-for-byok"></a>BYOK에 대한 필수 조건
다음 표를 위한 필수 구성 요소의 목록에 대 한 hello (byok)를 통해 Azure 키 자격 증명 모음을 참조 하십시오.

| 요구 사항 | 자세한 정보 |
| --- | --- |
| 구독 tooAzure |Azure 구독이 필요 toocreate Azure 키 자격 증명 모음: [무료 평가판에 등록](https://azure.microsoft.com/pricing/free-trial/) |
| hello Azure 키 자격 증명 모음 Premium 서비스 계층 toosupport HSM 보호 키 |Azure 키 자격 증명 모음에 대 한 hello 서비스 계층과 기능에 대 한 자세한 내용은 참조 hello [Azure 키 자격 증명 모음 가격](https://azure.microsoft.com/pricing/details/key-vault/) 웹 사이트입니다. |
| Thales HSM, 스마트 카드 및 지원 소프트웨어 |있어야 tooa Thales 하드웨어 보안 모듈 및 Thales Hsm의 기본적인 작동 지식이 액세스 합니다. 참조 [Thales 하드웨어 보안 모듈](https://www.thales-esecurity.com/msrms/buy) 호환 모델 또는 toopurchase 하지 않은 경우 하나 HSM hello 목록에 대 한 합니다. |
| 다음 하드웨어 및 소프트웨어 hello:<ol><li>Windows 운영 체제 Windows 7 이상 및 Thales nShield 소프트웨어 버전 11.50 이상이 설치된 오프라인 x64 워크스테이션.<br/><br/>이 워크스테이션에서 Windows 7을 실행하는 경우 [Microsoft.NET Framework 4.5를 설치](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe)해야 합니다.</li><li>연결 된 toohello 인터넷 이며 최소 Windows 운영 체제의 Windows 7 인 워크스테이션 및 [Azure PowerShell](/powershell/azure/overview) **최소 버전 1.1.0** 설치 합니다.</li><li>여유 공간이 16MB 이상인 USB 드라이브 또는 기타 휴대용 저장 장치 </li></ol> |보안상의 이유로 hello 첫 번째 워크스테이션의 연결 된 tooa 네트워크 않습니다 것이 좋습니다. 그러나 이 권고는 프로그램 방식으로 강제 적용되지는 않습니다.<br/><br/>뒤에 나오는 hello 지침에서이 워크스테이션은 참조 tooas hello 연결이 끊어진 워크스테이션 note 합니다.</p></blockquote><br/>또한 테 넌 트 키가 프로덕션 네트워크용, 별도 두 번째 워크스테이션 toodownload hello 도구 집합 및 업로드 hello 테 넌 트 키를 사용 하는 것이 좋습니다. 테스트를 위해 사용할 수 있습니다 하지만 첫 번째 hello 처럼 동일한 워크스테이션을 hello 합니다.<br/><br/>뒤에 나오는 hello 지침에서이 두 번째 워크스테이션은 참조 tooas hello 인터넷에 연결 된 워크스테이션 note 합니다.</p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a>생성 및 사용자 키 tooAzure 자격 증명 모음 HSM 키를 전송 합니다.
5 단계 toogenerate 다음 hello를 사용 하 고 키 tooan Azure 키 자격 증명 모음 HSM에 전송 됩니다.

* [1단계: 인터넷에 연결된 워크스테이션 준비](#step-1-prepare-your-internet-connected-workstation)
* [2단계: 연결이 끊어진 워크스테이션 준비](#step-2-prepare-your-disconnected-workstation)
* [3단계: 키 생성](#step-3-generate-your-key)
* [4단계: 전송할 키 준비](#step-4-prepare-your-key-for-transfer)
* [5 단계: 키 자격 증명 모음에 키 tooAzure 전송](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a>1단계: 인터넷에 연결된 워크스테이션 준비
이 첫 번째 단계 수행 hello 있는 연결 된 toohello 인터넷 워크스테이션에서 다음 절차를 수행 합니다.

### <a name="step-11-install-azure-powershell"></a>1.1단계: Azure PowerShell 설치
Hello 인터넷에 연결 된 워크스테이션에서 다운로드 하 고 hello cmdlet toomanage Azure 키 자격 증명 모음을 포함 하는 hello Azure PowerShell 모듈을 설치 합니다. 이를 위해 0.8.13 이상 버전이 필요합니다.

설치 지침을 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

### <a name="step-12-get-your-azure-subscription-id"></a>1.2단계: Azure 구독 ID 얻기
Azure PowerShell 세션을 시작 하 고 다음 명령을 hello를 사용 하 여 tooyour Azure 계정에에서 로그인 합니다.

        Add-AzureAccount
Hello 팝업 브라우저 창에서 Azure 계정 사용자 이름 및 암호를 입력 합니다. 그런 다음 사용 하는 hello [Get-azuresubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) 명령:

        Get-AzureSubscription
Hello 출력에서 Azure 키 자격 증명 모음에 사용할 hello 구독에 대 한 hello ID를 찾습니다. 이 구독 ID는 나중에 필요합니다.

Hello Azure PowerShell 창을 닫지 마십시오.

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a>1.3 단계: Azure 키 자격 증명 모음에 대 한 hello BYOK 도구 집합 다운로드
Microsoft 다운로드 센터 toohello 이동 및 [hello Azure 키 자격 증명 모음 BYOK 도구 집합 다운로드](http://www.microsoft.com/download/details.aspx?id=45345) 지역 또는 Azure의 인스턴스에 대 한 합니다. Hello 다음을 사용 하 여 정보 tooidentify hello 패키지 이름 toodownload 및 해당 해당 s h A-256 패키지 해시:

- - -
**미국:**

KeyVault-BYOK-Tools-UnitedStates.zip

760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B

- - -
**유럽:**

KeyVault-BYOK-Tools-Europe.zip

7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D

- - -
**아시아:**

KeyVault-BYOK-Tools-AsiaPacific.zip

813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8

- - -
**라틴 아메리카:**

KeyVault-BYOK-Tools-LatinAmerica.zip

3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0

- - -
**일본:**

KeyVault-BYOK-Tools-Japan.zip

453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90

- - -
**한국:**

KeyVault-BYOK-Tools-Korea.zip

C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A

- - -
**오스트레일리아:**

KeyVault-BYOK-Tools-Australia.zip

4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B

- - -
[**Azure Government:**](https://azure.microsoft.com/features/gov/)

KeyVault-BYOK-Tools-USGovCloud.zip

3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64

- - -
**미국 정부 DOD:**

KeyVault-BYOK-Tools-USGovernmentDoD.zip

A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D

- - -
**캐나다:**

KeyVault-BYOK-Tools-Canada.zip

30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7

- - -
**독일:**

KeyVault-BYOK-Tools-Germany.zip

5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261

- - -
**인도:**

KeyVault-BYOK-Tools-India.zip

136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7

- - -
**영국:**

KeyVault-BYOK-Tools-UnitedKingdom.zip

ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268

- - -

Azure PowerShell 세션을 사용 하 여 hello에서 프로그램 다운로드 한 BYOK 도구 집합의 toovalidate hello 무결성 [Get-filehash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.

    Get-FileHash KeyVault-BYOK-Tools-*.zip

hello 도구 집합 hello 다음이 포함 됩니다.

* 이름이 **BYOK-KEK-pkg-**
* 이름이 **BYOK-SecurityWorld-pkg-**
* 이름이 **verifykeypackage.py**인 python 스크립트
* 이름이 **KeyTransferRemote.exe** 인 명령줄 실행 파일 및 관련 DLL
* 이름이 **vcredist_x64.exe**인 Visual C++ 재배포 가능 패키지

Hello 패키지 tooa USB 드라이브 또는 기타 휴대용 저장소에 복사 합니다.

## <a name="step-2-prepare-your-disconnected-workstation"></a>2단계: 연결이 끊어진 워크스테이션 준비
이 두 번째 단계에 대 한 않습니다 hello (hello 인터넷 또는 내부 네트워크) 연결 된 tooa 네트워크 하지 않은 hello 워크스테이션에서 다음 절차를 수행 합니다.

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a>2.1 단계: Thales HSM에 hello 연결이 끊어진 워크스테이션 준비
Windows 컴퓨터에 hello nCipher (Thales) 지원 소프트웨어를 설치 하 고 Thales HSM toothat 컴퓨터를 연결 합니다.

Thales 도구 hello 해당 경로에 있는지 확인 하십시오 (**%nfast_home%\bin**). 예를 들어 hello 다음을 입력 합니다.

        set PATH=%PATH%;"%nfast_home%\bin"

자세한 내용은 hello Thales HSM에 포함 된 hello 사용자 가이드를 참조 하세요.

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a>2.2 단계: 설치 hello BYOK 도구 집합 hello 연결이 끊어진 워크스테이션에서
Hello USB 드라이브 또는 기타 휴대용 저장소에서 hello BYOK 도구 집합 패키지를 복사 하 고 수행가 다음를 hello 다음:

1. Hello 다운로드 패키지에서 임의 폴더로 hello 파일을 추출 합니다.
2. 해당 폴더에서 vcredist_x64.exe를 실행합니다.
3. Visual Studio 2013 용 hello Visual c + + 런타임 구성 요소를 설치 하는 toohello hello 지침을 따릅니다.

## <a name="step-3-generate-your-key"></a>3단계: 키 생성
이 세 번째 단계에 대해 수행 hello hello 연결이 끊어진 워크스테이션에서 다음 절차를 수행 합니다. toocomplete이이 단계 HSM 초기화 모드에 있어야 합니다. 


### <a name="step-31-change-hello-hsm-mode-tooi"></a>3.1 단계: hello HSM 모드 too'I 변경 '
Thales nShield 경계 면 toochange hello 모드를 사용 하는 경우: 1입니다. Hello 모드 단추 toohighlight hello 필요한 모드를 사용 합니다. 2. 몇 초 안에 hello 지우기 단추를 누르고 몇 초 정도입니다. Hello 모드 변경 되 면 hello 새로운 모드 LED 깜박임 멈추고 켜져 됩니다. hello 상태 LED 몇 초간 불규칙 한 플래시 수 및 다음 hello 장치를 준비 하는 경우에 정기적으로 깜박입니다. 그렇지 않으면 hello 장치 남아 있으며 hello 적절 한 모드 LED hello 현재 모드 켜 졌습니다.

### <a name="step-32-create-a-security-world"></a>3.2단계: 보안 영역 만들기
명령 프롬프트를 시작 하 고 hello Thales new-world 프로그램을 실행 합니다.

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

이 프로그램을 만듭니다는 **보안 권역** % NFAST_KMDATA%\local\world toohello C:\ProgramData\nCipher\Key Management Data\local 폴더에 해당 하는 파일입니다. Hello 쿼럼에 대 한 다른 값을 사용할 수 있습니다 하는데이 예제에서는 있습니다 증명된 tooenter 3 개의 빈 카드와 핀 각각에 대 한 합니다. 그런 다음 임의의 두 카드에 대 한 모든 권한을 toohello 보안 권역을 제공 합니다. 이러한 카드 될 hello **관리자 카드 집합** hello 새 보안 권역의 합니다.

그런 다음 않습니다 다음 hello:

* Hello world 파일을 백업 합니다. 보안을 설정 하 고 hello world 파일, hello 관리자 카드 및 해당 핀을 보호 한 사람이 액세스 toomore 보다 카드 하나에 있는지 확인 합니다.

### <a name="step-33-change-hello-hsm-mode-tooo"></a>3.3 단계: hello HSM 모드 too'O 변경 '
Thales nShield 경계 면 toochange hello 모드를 사용 하는 경우: 1입니다. Hello 모드 단추 toohighlight hello 필요한 모드를 사용 합니다. 2. 몇 초 안에 hello 지우기 단추를 누르고 몇 초 정도입니다. Hello 모드 변경 되 면 hello 새로운 모드 LED 깜박임 멈추고 켜져 됩니다. hello 상태 LED 몇 초간 불규칙 한 플래시 수 및 다음 hello 장치를 준비 하는 경우에 정기적으로 깜박입니다. 그렇지 않으면 hello 장치 남아 있으며 hello 적절 한 모드 LED hello 현재 모드 켜 졌습니다.


### <a name="step-34-validate-hello-downloaded-package"></a>3.4 단계: hello 다운로드 한 패키지 유효성 검사
이 단계는 선택 사항 이지만 hello 다음을 확인할 수 있도록 권장.

* hello hello 도구 집합에 포함 된 키 교환 키가 정품 Thales HSM에서 생성 되었습니다.
* hello hello 도구 집합에 포함 된 보안 권역의 hello 해시가 정품 Thales HSM에서 생성 되었습니다.
* hello 키 교환 키를 내보낼 수 있습니다.

> [!NOTE]
> toovalidate hello 패키지를 다운로드 한, hello HSM 연결 되어 있어야, 전원이 켜져 방금 만든 하나 hello) (예: 보안 권역에 있어야 합니다.
>
>

toovalidate hello 다운로드 한 패키지:

1. Azure의 인스턴스 나 지리적 지역에 따라 hello 다음 중 하나를 입력 하 여 hello verifykeypackage.py 스크립트를 실행 합니다.

   * 북아메리카:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * 유럽:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * 아시아:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * 라틴 아메리카:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * 일본:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * 한국:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * 오스트레일리아:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * 에 대 한 [Azure Government](https://azure.microsoft.com/features/gov/), Azure의 hello 미국 정부 인스턴스를 사용 하 여:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * 미국 정부 DOD:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * 캐나다:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * 독일:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * 인도:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > hello Thales 소프트웨어는 %NFAST_HOME%\python\bin에 python 포함
     >
     >
2. 유효성 검사 성공을 나타냄 hello 다음 표시 되는지 확인 합니다: **결과: 성공**

이 스크립트에는 toohello Thales 루트 키를 hello 서명자 체 이닝 되는지를 확인 합니다. 이 루트 키의 해시 hello hello 스크립트에 포함 되어 있으며 해당 값 **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**합니다. Hello를 방문 하 여이 값을 개별적으로 확인할 수도 있습니다 [Thales 웹 사이트](http://www.thalesesec.com/)합니다.

이제 새 키를 준비 toocreate 것입니다.

### <a name="step-35-create-a-new-key"></a>3.5단계: 새 키 만들기
Thales hello를 사용 하 여 키를 생성 **generatekey** 프로그램.

다음 명령은 toogenerate hello 키 hello를 실행 합니다.

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

이 명령을 실행할 때 다음 지침을 사용합니다.

* 매개 변수를 hello *보호* toohello 값을 설정 해야 **모듈**표시 된 것 처럼 합니다. 이렇게 하면 모듈 보호 키가 만들어집니다. hello BYOK 도구 집합 OCS 보호 키는 지원 하지 않습니다.
* Hello 값의 대체 *contosokey* hello에 대 한 **ident** 및 **plainname** 임의의 문자열 값으로. 관리 오버 헤드가 toominimize hello 위험을 줄이고 오류의 hello 둘 다에 대해 같은 값을 사용 하는 권장 합니다. hello **ident** 값 숫자, 대시 및 소문자만 포함 해야 합니다.
* hello pubexp은 비워 뒀 지만 (기본값)이 예제에서는 하지만 특정 값을 지정할 수 있습니다. 자세한 내용은 Thales 문서 hello 합니다.

이 명령은으로 이름을 시작 하 여 %NFAST_KMDATA%\local 폴더에 토큰화 된 키 파일을 만들고 **key_simple_**hello와 **ident** hello 명령에 지정 된 합니다. 예들 들어 **key_simple_contosokey**입니다. 이 파일은 암호화된 키를 포함합니다.

안전한 위치에 이 토큰화된 키 파일을 백업합니다.

> [!IMPORTANT]
> 나중에 키 자격 증명 모음에 키 tooAzure를 전송할 때 Microsoft는 것이 매우 중요 한를 백업 하는 키와 보안 권역 안전 하 게이 키 백 tooyou를 내보낼 수 없습니다. 키 백업에 대한 지침 및 모범 사례는 Thales에 문의하세요.
>
>

사용자는 이제 준비 tootransfer 주요 자격 증명 모음에 키 tooAzure 합니다.

## <a name="step-4-prepare-your-key-for-transfer"></a>4단계: 전송할 키 준비
이 네 번째 단계에 대해 수행 hello hello 연결이 끊어진 워크스테이션에서 다음 절차를 수행 합니다.

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a>4.1단계: 축소된 권한을 가진 키의 복사본을 만듭니다.

새 명령 프롬프트를 열고 hello 현재 디렉터리 toohello 위치 hello BYOK zip 파일의 압축을 푼 변경 합니다. 명령 프롬프트에서 사용자의 키에 대 한 hello 권한을 tooreduce 인스턴스의 Azure 나 지리적 지역에 따라 hello 다음 중 하나를 실행합니다.

* 북아메리카:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* 유럽:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* 아시아:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* 라틴 아메리카:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* 일본:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* 한국:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* 오스트레일리아:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* 에 대 한 [Azure Government](https://azure.microsoft.com/features/gov/), Azure의 hello 미국 정부 인스턴스를 사용 하 여:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* 미국 정부 DOD:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* 캐나다:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* 독일:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* 인도:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

이 명령을 실행할 때 *contosokey* hello와 같은 값에서 지정한 **단계 3.5: 새 키 만들기** hello에서 [트 키 생성](#step-3-generate-your-key) 단계입니다.

사용자 보안 권역 관리자 카드에서 tooplug는 단계가 있습니다.

Hello 명령이 완료 되 면 표시 **결과: SUCCESS** 있으며 권한이 낮춰 키의 hello 복사본이 key_xferacId_ 라는 hello 파일에서<contosokey>합니다.

Hello ACL 검사 수 Thales 유틸리티를 hello 다음 명령을 사용 하 여 사용 하 여:

* aclprint.py:

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* kmfile-dump.exe:

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  이러한 명령을 실행할 때 contosokey hello에 지정한 같은 값으로 대체 **단계 3.5: 새 키 만들기** hello에서 [트 키 생성](#step-3-generate-your-key) 단계입니다.

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a>4.2단계: Microsoft의 키 교환 키를 사용하여 키 암호화
Hello 명령을 Azure 인스턴스의 나 지리적 지역에 따라 다음 중 하나를 실행 합니다.

* 북아메리카:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 유럽:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 아시아:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 라틴 아메리카:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 일본:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 한국:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 오스트레일리아:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 에 대 한 [Azure Government](https://azure.microsoft.com/features/gov/), Azure의 hello 미국 정부 인스턴스를 사용 하 여:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 미국 정부 DOD:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 캐나다:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 독일:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 인도:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

이 명령을 실행할 때 다음 지침을 사용합니다.

* 대체 *contosokey* 에 toogenerate hello 키를 사용 하는 hello 식별자를 가진 **단계 3.5: 새 키 만들기** hello에서 [트 키 생성](#step-3-generate-your-key) 단계입니다.
* 대체 *SubscriptionID* hello hello 주요 자격 증명 모음을 포함 하는 Azure 구독 ID로 합니다. 이 값을 검색에서 이전에 **1.2 단계: Azure 구독 ID를 가져올** hello에서 [인터넷에 연결 된 워크스테이션 준비](#step-1-prepare-your-internet-connected-workstation) 단계입니다.
* *ContosoFirstHSMKey*를 출력 파일 이름에 사용할 레이블로 바꿉니다.

이 성공적으로 완료 되 면 표시 **결과: 성공** hello 이름 뒤에 있는 hello 현재 폴더에 새 파일 이며: KeyTransferPackage-*ContosoFirstHSMkey*.byok

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a>4.3 단계: 키 전송 패키지 toohello 인터넷에 연결 된 워크스테이션을 복사
Hello 이전 단계 (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour 인터넷에 연결 된 워크스테이션에서 USB 드라이브 또는 기타 휴대용 저장소 toocopy hello 출력 파일을 사용 합니다.

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a>5 단계: 키 자격 증명 모음에 키 tooAzure 전송
이 마지막 단계에 대 한 hello 인터넷에 연결 된 워크스테이션에서 사용 하 여 hello [Add-azurekeyvaultkey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) hello에서 복사한 cmdlet tooupload hello 키 전송 패키지 끊긴 워크스테이션 toohello Azure 키 자격 증명 모음 HSM:

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

Hello 업로드에 성공한 경우 방금 추가한 hello 키의 표시 된 hello 속성 참조입니다.

## <a name="next-steps"></a>다음 단계
이제 주요 자격 증명 모음에서 이 HSM 보호된 키를 사용할 수 있습니다. 자세한 내용은 참조 hello **toouse 하드웨어 보안 모듈 (HSM) 하려는 경우** hello에 대 한 섹션 [Azure 키 자격 증명 모음 시작 하기](key-vault-get-started.md) 자습서입니다.
