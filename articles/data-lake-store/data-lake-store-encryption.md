---
title: "Azure 데이터 레이크 저장소의 aaaEncryption | Microsoft Docs"
description: "Azure Data Lake Store에서 암호화 및 키 회전의 작동 방식 이해"
services: data-lake-store
documentationcenter: 
author: yagupta
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 4/14/2017
ms.author: yagupta
ms.openlocfilehash: a9f3a2dce8232deba93005594d1e6a21e9c0cbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encryption-of-data-in-azure-data-lake-store"></a>Azure Data Lake Store의 데이터 암호화

Azure Data Lake Store의 암호화를 통해 데이터를 보고하고 엔터프라이즈 보안 정책을 구현하고 규정 준수 요구 사항을 충족할 수 있습니다. 이 문서는 hello 디자인의 개요를 제공 하 고 구현의 기술적인 측면도 hello 중 일부에 대해 설명 합니다.

Data Lake Store는 미사용 또는 전송 중인 데이터의 암호화를 지원합니다. Data Lake Store는 미사용 데이터에 대해 기본적으로 투명한 암호화를 지원합니다. 이러한 용어의 의미를 좀 더 자세히 알아보겠습니다.

* **기본적으로**: hello 기본 설정은 새 데이터 레이크 저장소 계정을 만들 때 암호화를 사용 합니다. 이제 데이터 레이크 저장소에 저장 된 데이터를 영구 미디어에 이전 암호화 된 toostoring 항상 합니다. 이것은 모든 데이터에 대 한 hello 동작 하 고 계정을 만든 후 변경할 수 없습니다.
* **투명 한**: 데이터 레이크 저장소에서 자동으로 toopersisting을 이전 하는 데이터를 암호화 하 고 이전 tooretrieval 데이터를 해독 합니다. hello 암호화 구성 되 고 hello 데이터 레이크 저장소 수준에서 관리자가 관리 합니다. 변경 내용이 없는 toohello 데이터 Api에 액세스 합니다. 따라서 암호화 때문에 Data Lake Store와 상호 작용하는 응용 프로그램 및 서비스를 변경할 필요가 없습니다.

전송되는 데이터(즉, 동작 중인 데이터)는 항상 Data Lake Store에서 암호화됩니다. 또한 tooencrypting 데이터 사전 toostoring toopersistent 미디어 hello 데이터는 항상 전송에 보호 HTTPS를 사용 하 여 합니다. HTTPS는 hello hello 데이터 레이크 저장소 REST 인터페이스에 지원 되는 유일한 프로토콜입니다. hello 다음 그림에 데이터 레이크 저장소의 데이터 암호화 되는 방법을:

![Data Lake Store의 데이터 암호화 다이어그램](./media/data-lake-store-encryption/fig1.png)


## <a name="set-up-encryption-with-data-lake-store"></a>Data Lake Store를 사용하여 암호화 설정

Data Lake Store 암호화는 계정을 만드는 동안 설정되며, 항상 기본적으로 사용됩니다. Hello 키를 직접 관리 하거나 데이터 레이크 저장소 toomanage 허용 ç (이것이 hello 기본) 있습니다.

자세한 내용은 [시작](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal)을 참조하세요.

## <a name="how-encryption-works-in-data-lake-store"></a>Data Lake Store에서 암호화가 작동하는 방법

hello 다음 정보에 설명 어떻게 toomanage 마스터 암호화 키를 설명 hello 세 가지 유형의 키 데이터 레이크 저장소에 대 한 데이터 암호화에서 사용할 수 있습니다.

### <a name="master-encryption-keys"></a>마스터 암호화 키

Data Lake Store는 MEK(마스터 암호화 키)를 관리하는 두 가지 모드를 제공합니다. 지금은 해당 hello 마스터 암호화 키가 hello 최상위 수준 키를 가정 합니다. 액세스 toohello 마스터 암호화 키가 필요한 toodecrypt 데이터 레이크 저장소에 저장 된 데이터.

hello 마스터 암호화 키를 관리 하기 위한 hello 두 모드는 다음과 같습니다.

*   서비스 관리 키
*   고객 관리 키

두 모드에서 Azure 키 자격 증명 모음에 저장 하 여 hello 마스터 암호화 키 보호 됩니다. 주요 자격 증명 모음에 사용 되는 toosafeguard 암호화 키 일 수 있는 Azure에서 완벽 하 게 관리 되 고, 보안 수준이 높은 서비스입니다. 자세한 내용은 [Key Vault](https://azure.microsoft.com/services/key-vault)를 참조하세요.

다음은 hello hello MEKs 관리의 두 가지 모드에서 제공 하는 기능의 간략 한 비교입니다.

|  | 서비스 관리 키 | 고객 관리 키 |
| --- | --- | --- |
|데이터가 어떻게 저장되나요?|항상 암호화 된 이전 toobeing 저장 합니다.|항상 암호화 된 이전 toobeing 저장 합니다.|
|Hello 마스터 암호화 키 저장 위치|키 자격 증명 모음|키 자격 증명 모음|
|키 자격 증명 모음 외부에서 hello에 저장 된 키의 선택을 취소 하는 모든 암호화? |아니요|아니요|
|키 자격 증명 모음에서 검색할 수 MEK hello?|아니요. MEK 주요 자격 증명 모음에 저장 된 hello, 후만 사용할 수 있습니다 암호화 및 암호 해독 합니다.|아니요. MEK 주요 자격 증명 모음에 저장 된 hello, 후만 사용할 수 있습니다 암호화 및 암호 해독 합니다.|
|소유자, 주요 자격 증명 모음 인스턴스와 hello MEK hello?|hello 데이터 레이크 저장소 서비스|Azure 구독에 속한 hello 주요 자격 증명 모음 인스턴스를 소유 합니다. 키 자격 증명 모음의 MEK hello 소프트웨어 또는 하드웨어에서 관리할 수 있습니다.|
|Hello Data Lake 저장소 서비스에 대 한 액세스 toohello MEK를 해지할 수 있습니까?|아니요|예. 주요 자격 증명에 대 한 액세스 제어 목록을 관리할 수 있으며 hello Data Lake 저장소 서비스에 대 한 액세스 제어 항목 toohello 서비스 id를 제거할 수 있습니다.|
|영구적으로 hello MEK를 삭제할 수 있습니다.|아니요|예. 주요 자격 증명 모음에서 MEK hello를 삭제 하면 hello 데이터 레이크 저장소 서비스를 포함 하 여 모든 사용자가 hello hello Data Lake 저장소 계정에에서는 데이터를 해독할 수 없습니다. <br><br> 명시적으로 백업한 hello MEK 이전 toodeleting 것 키 자격 증명 모음에서 hello MEK 복원할 수 및 hello 데이터 복구할 수 있습니다. 그러나 있습니다 백업 되지 않은 hello MEK 이전 toodeleting 것 키 자격 증명 모음에서 경우 hello 데이터 hello Data Lake 저장소 계정에서에서 되지 해독할 수 이후 합니다.|


이러한 차이 외에도 관리 하는 사람 MEK hello 및 hello 키 자격 증명 모음 인스턴스에 구문이 있는 hello 나머지 hello 디자인 모드에서 모두 동일 hello 됩니다.

Hello에 대 한 hello 모드 마스터 암호화 키를 선택 하는 경우 것이 중요 한 tooremember hello 다음 합니다.

*   여부 toouse 고객 관리 되는 키 또는 관리 서비스 키 데이터 레이크 저장소 계정 프로 비전 할 때 선택할 수 있습니다.
*   데이터 레이크 저장소 계정이 프로 비전 되 면 hello 모드를 변경할 수 없습니다.

### <a name="encryption-and-decryption-of-data"></a>데이터 암호화 및 암호 해독

세 가지 방법으로 데이터 암호화의 hello 디자인에 사용 되는 키의 수입니다. 다음 표에서 hello 요약을 제공 합니다.

| 키                   | 약어 | 연결 대상 | 저장 위치                             | 형식       | 참고 사항                                                                                                   |
|-----------------------|--------------|-----------------|----------------------------------------------|------------|---------------------------------------------------------------------------------------------------------|
| 마스터 암호화 키 | MEK          | Data Lake Store 계정 | 키 자격 증명 모음                              | 비대칭 | Data Lake Store 또는 사용자가 관리할 수 있습니다.                                                              |
| 데이터 암호화 키   | DEK          | Data Lake Store 계정 | 영구 저장소, Data Lake Store 서비스에서 관리 | 대칭  | DEK hello MEK hello로 암호화 됩니다. 암호화 된 DEK는 영구 미디어에 저장 된 항목 번호입니다. |
| 블록 암호화 키  | BEK          | 데이터 블록 | 없음                                         | 대칭  | hello BEK DEK hello 및 hello 데이터 블록에서 파생 됩니다.                                                      |

hello 다음 다이어그램에서는 이러한 개념을 보여 줍니다.

![데이터 암호화의 키](./media/data-lake-store-encryption/fig2.png)

#### <a name="pseudo-algorithm-when-a-file-is-toobe-decrypted"></a>파일을 암호 해독 toobe 때 의사 알고리즘:
1.  Hello DEK hello Data Lake 저장소 계정에 대 한 캐시 된 고 사용 준비가 인지 확인 합니다.
    - 그렇지 않은 경우 다음 읽을 hello 영구 저장소에서 DEK를 암호화 하 고 해독 tooKey 자격 증명 모음 toobe 보냅니다. 캐시 hello 메모리에 DEK를 해독 합니다. 준비 toouse 되었습니다.
2.  Hello 파일에 데이터의 모든 블록에 대 한:
    - 읽기 hello 영구 저장소에서 데이터 블록을 암호화 합니다.
    - DEK hello에서 BEK hello 및 hello 암호화 된 데이터 블록을 생성 합니다.
    - Hello BEK toodecrypt 데이터를 사용 합니다.


#### <a name="pseudo-algorithm-when-a-block-of-data-is-toobe-encrypted"></a>데이터 블록을 암호화 toobe 때 의사 알고리즘:
1.  Hello DEK hello Data Lake 저장소 계정에 대 한 캐시 된 고 사용 준비가 인지 확인 합니다.
    - 그렇지 않은 경우 다음 읽을 hello 영구 저장소에서 DEK를 암호화 하 고 해독 tooKey 자격 증명 모음 toobe 보냅니다. 캐시 hello 메모리에 DEK를 해독 합니다. 준비 toouse 되었습니다.
2.  Hello 블록의 데이터에 대 한 고유 BEK hello DEK에서 생성 합니다.
3.  Aes-256 암호화를 사용 하 여 hello BEK 사용 하 여 hello 데이터 블록을 암호화 합니다.
4.  영구 저장소에 hello 암호화 된 데이터 블록의 데이터를 저장 합니다.

> [!NOTE] 
> 성능상의 이유로 hello에 DEK의 선택을 취소 하는 hello 짧은 시간에 대 한 메모리에 캐시 된 하 고 나중에 즉시 지워집니다. 영구 미디어에는 항상 MEK hello로 암호화 된 저장 됩니다.

## <a name="key-rotation"></a>키 회전

고객이 관리 하는 키를 사용 하는 hello MEK 회전할 수 있습니다. tooset 고객이 관리 하는 키가 있는 데이터 레이크 저장소 계정을 참조 하는 방법을 toolearn [시작](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal)합니다.

### <a name="prerequisites"></a>필수 조건

Hello Data Lake 저장소 계정 연결을 설정할 때 사용자 고유의 키 toouse 선택 했습니다. Hello 계정이 생성 된 다음에이 옵션을 변경할 수 없습니다. hello 다음 단계에서는 가정 고객이 관리 하는 키를 사용 하는 (즉, 키 자격 증명 모음에서 사용자 고유의 키를 선택 했습니다).

암호화에 대 한 hello 기본 옵션을 사용 하는 경우 데이터가 항상 암호화 데이터 레이크 저장소에서 관리 되는 키를 사용 하 여 note 합니다. 이 옵션에서는 없는 hello 기능 toorotate 키 데이터 레이크 저장소에서 관리 하는 합니다.

### <a name="how-toorotate-hello-mek-in-data-lake-store"></a>Toorotate는 데이터 레이크 저장소의 MEK hello 하는 방법

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 데이터 레이크 저장소 계정에 연결 된 키를 저장 하는 toohello 주요 자격 증명 모음 인스턴스를 찾습니다. **키**를 선택합니다.

    ![Key Vault의 스크린샷](./media/data-lake-store-encryption/keyvault.png)

3.  데이터 레이크 저장소 계정과 연결 된 hello 키를 선택 하 고이 키의 새 버전을 만듭니다. 데이터 레이크 저장소 현재 지원함을 키의 키를 회전 tooa 새 버전을 참고 합니다. Tooa 다른 키를 회전을 지원 하지 않습니다.

   ![강조 표시된 새 버전에서 키 창의 스크린샷](./media/data-lake-store-encryption/keynewversion.png)

4.  Toohello 데이터 레이크 저장소 저장소 계정 이름을 찾아 선택 **암호화**합니다.

    ![강조 표시된 암호화에서 Data Lake Store 저장소 계정 창의 스크린샷](./media/data-lake-store-encryption/select-encryption.png)

5.  새 키 버전의 hello 키를 사용할 수 있는지는 메시지가 표시 됩니다. 클릭 **키 회전** tooupdate hello 키 toohello 새 버전입니다.

    ![강조 표시된 메시지와 회전 키에서 Data Lake Store 창의 스크린샷](./media/data-lake-store-encryption/rotatekey.png)

이 작업에는 2 분 미만 취해야 되며 tookey 회전 인해 예상된 가동 중지 시간이 없습니다. Hello 작업이 완료 되 면 hello hello 키의 새 버전 사용 중인 경우
