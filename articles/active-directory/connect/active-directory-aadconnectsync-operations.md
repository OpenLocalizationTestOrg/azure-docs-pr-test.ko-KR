---
title: "Azure AD Connect Sync: 운영 작업 및 고려 사항 | Microsoft Docs"
description: "이 항목에서는 Azure AD Connect 동기화를 위한 운영 작업을 설명 및 방법을이 구성 요소를 운영 하기 위한 tooprepare 합니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a>Azure AD Connect Sync: 운영 작업 및 고려 사항
이 항목의 hello 목표에는 Azure AD Connect 동기화를 위한 toodescribe 운영 작업입니다.

## <a name="staging-mode"></a>스테이징 모드
다음을 비롯한 여러 시나리오에 스테이징 모드를 사용할 수 있습니다.

* 고가용성.
* 새 구성 변경 내용을 테스트하고 배포합니다.
* 새 서버를 소개 하 고 이전 hello를 서비스 해제 합니다.

준비 모드에서 서버와 수 변경 toohello 구성 및 미리 보기 hello 변경 하면 hello 서버를 활성화 하기 전에 됩니다. 또한 있습니다 toorun 전체 가져오기 및 전체 동기화 tooverify 프로덕션 환경으로 변경 하기 전에 이러한 모든 변경 내용이 예상 됩니다.

설치 중에 서버 toobe hello를 선택할 수 있습니다 **준비 모드**합니다. 이 이렇게 하면 hello 서버 가져오기 및 동기화에 대 한 활성 하지만 모든 내보내기와 실행 되지 않습니다. 설치 중에 이러한 기능을 선택하더라도 스테이징 모드에 있는 서버는 암호 동기화 또는 비밀번호 쓰기 저장을 실행하지 않습니다. 준비 모드를 해제 하면 hello 서버 내보내기를 시작, 암호 동기화를 사용 하도록 설정 및 암호 쓰기 저장을 사용 하도록 설정 합니다.

Hello 동기화 서비스 관리자를 사용 하 여 내보내기를 하도록 할 수 있습니다.

준비 모드의 서버에에서 Active Directory와 Azure AD에서 tooreceive 변경 내용을 계속 됩니다. 항상 다른 서버 hello 책임을 통해 hello 최신 변경 내용 및 수 매우 빠르게 수행의 복사본을 가집니다. 구성 변경 내용을 tooyour 주 서버를 설정한 경우 책임 toomake hello 준비 모드의 동일한 변경 내용을 toohello 서버입니다.

이전 동기화 기술 알고 있는 사용자를 위해 준비 모드 hello 이므로 다른 hello 서버에 자체 SQL 데이터베이스입니다. 이 구조는 준비 모드 서버 toobe 다른 데이터 센터에 있는 hello를 사용 합니다.

### <a name="verify-hello-configuration-of-a-server"></a>서버 hello 구성 확인
tooapply이이 메서드를 다음이 단계를 수행 합니다.

1. [준비](#prepare)
2. [구성](#configuration)
3. [가져오기 및 동기화](#import-and-synchronize)
4. [Verify](#verify)
5. [활성 서버 전환](#switch-active-server)

#### <a name="prepare"></a>준비
1. Azure AD Connect를 설치, 선택 **준비 모드**을 선택 취소 **동기화를 시작** hello hello 설치 마법사의 마지막 페이지에 있습니다. 이 모드에서는 toorun hello 동기화 엔진이 수동으로 있습니다.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)
2. Off/로그인 기호와 시작 메뉴 선택 hello에서 **동기화 서비스**합니다.

#### <a name="configuration"></a>구성
사용자 지정 변경 내용 toohello 주 서버와 원하는 toocompare hello 구성으로 만든 서버를 준비 하는 hello를 사용 하 여 [Azure AD Connect 구성 데이터베이스 구조](https://github.com/Microsoft/AADConnectConfigDocumenter)합니다.

#### <a name="import-and-synchronize"></a>가져오기 및 동기화
1. 선택 **커넥터**, 선택 hello hello 형식과 첫 번째 커넥터 및 **Active Directory 도메인 서비스**합니다. **실행**을 클릭하고 **전체 가져오기** 및 **확인**을 선택합니다. 이 형식인 모든 커넥터에 해당 단계를 수행합니다.
2. 형식과 선택 hello 커넥터 **Azure Active Directory (Microsoft)**합니다. **실행**을 클릭하고 **전체 가져오기** 및 **확인**을 선택합니다.
3. Hello 탭 커넥터가 선택 되어 있는지 확인 합니다. **Active Directory Domain Services** 형식인 각 커넥터의 경우 **실행**을 클릭하고 **델타 동기화** 및 **확인**을 선택합니다.
4. 형식과 선택 hello 커넥터 **Azure Active Directory (Microsoft)**합니다. **실행**을 클릭하고 **델타 동기화** 및 **확인**을 차례로 선택합니다.

준비 된 내보내기 변경 tooAzure AD 및 온-프레미스 AD (Exchange 하이브리드 배포를 사용 하는 경우) 하는 경우 이제 해야 합니다. hello 다음 단계를 사용 하면 실제로 hello 내보내기 toohello 디렉터리를 시작 하기 전에 toochange의 내용을 tooinspect 있습니다.

#### <a name="verify"></a>Verify
1. Cmd 프롬프트를 시작 하 고 너무 이동`%ProgramFiles%\Microsoft Azure AD Sync\bin`
2. 실행: `csexport "Name of Connector" %temp%\export.xml /f:x` hello 이름 hello 커넥터의 동기화 서비스에서 확인할 수 있습니다. 에 이름이 비슷한 too"contoso.com – AAD" Azure AD에 대 한 합니다.
3. Hello 섹션에서 hello PowerShell 스크립트를 복사 [CSAnalyzer](#appendix-csanalyzer) 라는 tooa 파일 `csanalyzer.ps1`합니다.
4. PowerShell 창을 열고 toohello 폴더 hello PowerShell 스크립트를 만들 위치를 이동 합니다.
5. `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`을 실행합니다.
6. 이제 Microsoft Excel에서 검사할 수 있는 **processedusers1.csv**라는 파일이 있습니다. 모든 준비 된 변경 내용을 내보낼 toobe tooAzure AD이이 파일에 있습니다.
7. 필요한 변경 toohello 데이터 나 구성을 만들고 hello 된 내보낸 toobe에 대 한 변경 내용을 반환 될 때까지 이러한 단계 다시 (가져오기 및 동기화 및 확인)를 실행 합니다.

#### <a name="switch-active-server"></a>활성 서버 전환
1. Hello 현재 활성 서버에서 AD tooAzure 내보내지 하므로 hello 서버 (DirSync/FIM/Azure AD 동기화)를 해제 하거나 준비 모드 (Azure AD Connect)에 설정 합니다.
2. Hello 설치 마법사에 대 한 hello 서버에서 실행 **준비 모드** 사용 하지 않도록 설정 하 고 **준비 모드**합니다.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)

## <a name="disaster-recovery"></a>재해 복구
hello 구현 디자인 부분은 tooplan 어떤 toodo에 대 한 경우에 재해 hello 동기화 서버를 잃게 됩니다. 서로 다른 모델 toouse 및 어느 한 toouse 등 여러 가지 요소에 따라 달라 집니다 가지가 있습니다.

* Hello 가동 중지 시간 중에 Azure AD에서 tooobjects 변경 수 확인 되 고 있지에 대 한 허용 범위는 무엇입니까?
* 암호 동기화를 사용 하는 경우 수행 hello 사용자가 수락 온-프레미스 변경 하는 경우 Azure AD에서 toouse hello 이전 암호 권한이 있는 무엇 인가요?
* 비밀번호 쓰기 저장 등의 실시간 작업에 대한 종속성이 있습니까?

Hello 답변 toothese 질문 및 조직의 정책에 따라 hello 다음 전략 중 하나 구현할 수 있습니다.

* 필요할 때 다시 작성합니다.
* **스테이징 모드**라고 하는 예비 대기 서버가 있습니다.
* 가상 컴퓨터를 사용합니다.

Hello 기본 제공 SQL Express 데이터베이스를 사용 하지 않는 경우 hello도 검토 해야 [SQL 고가용성](#sql-high-availability) 섹션.

### <a name="rebuild-when-needed"></a>필요할 때 다시 작성
실행 가능한 전략은 필요할 때 서버 다시 작성에 대 한 tooplan입니다. 일반적으로 hello 동기화 엔진 설치 및 초기 가져오기 hello 수행 하 고 몇 시간 이내에 동기화를 완료할 수 있습니다. 사용 가능한 예비 서버 없는 경우 가능한 tootemporarily 사용 하 여 도메인 컨트롤러 toohost hello 동기화 엔진입니다.

Active Directory와 Azure AD의 hello 데이터에서 hello 데이터베이스를 다시 빌드할 수 있도록 hello 동기화 엔진 서버 hello 개체에 대 한 모든 상태를 저장 하지 않습니다. hello **sourceAnchor** 특성은 사용 되는 toojoin hello 개체를 온-프레미스 및 클라우드 hello 합니다. 다시 빌드하면 기존 개체와 서버 hello 온-프레미스 및 hello 클라우드 다음 hello 엔진 일치 재설치에 다시 해당 개체를 동기화 합니다. hello toodocument 필요 하 고 저장 사항은 필터링 및 동기화 규칙이 같은 toohello 서버에 대 한 hello 구성 변경 합니다. 동기화를 시작하기 전에 해당 사용자 지정 구성을 다시 적용해야 합니다.

### <a name="have-a-spare-standby-server---staging-mode"></a>스테이징 모드라는 예비 대기 서버가 있습니다.
더 복잡한 환경을 사용하는 경우 하나 이상의 대기 서버가 있는 것이 좋습니다. 설치 중에 서버 toobe를 설정할 수 있습니다 **준비 모드**합니다.

자세한 내용은 [스테이징 모드](#staging-mode)를 참조하세요.

### <a name="use-virtual-machines"></a>가상 컴퓨터 사용
일반 및 지원 되는 메서드는 가상 컴퓨터에서 toorun hello 동기화 엔진입니다. Hello 호스트에는 문제, 경우에 대비 hello 동기화 엔진 서버를 사용 하 여 hello 이미지 마이그레이션된 tooanother 서버일 수 있습니다.

### <a name="sql-high-availability"></a>SQL 고가용성
Azure AD Connect와 함께 제공 하는 SQL Server Express hello를 사용 하지 않는 경우 다음 SQL Server에 대 한 고가용성도 고려할 수 있습니다. hello 고가용성 솔루션을 지 원하는 SQL 클러스터링 및 AOA (Always On 가용성 그룹)에 포함 됩니다. 지원되지 않는 솔루션은 미러링을 포함합니다.

SQL AOA에 대 한 지원 추가 tooAzure AD 1.1.524.0 버전에 연결 합니다. Azure AD Connect를 설치하기 전에 SQL AOA를 사용하도록 설정해야 합니다. Azure AD Connect를 설치 하는 동안 SQL AOA에 대 한 제공 된 hello SQL 인스턴스 사용 되는지 여부를 검색 합니다. SQL AOA 사용 하는 경우 Azure AD Connect를 더 이상를 알아 SQL AOA 구성된 toouse 동기 복제 또는 비동기 복제 인지 합니다. Hello 가용성 그룹 수신기를 설정할 때는 hello RegisterAllProvidersIP 속성 too0를 설정 하는 것이 좋습니다. 이 SQL Native Client tooconnect tooSQL에 현재 사용 하 여 Azure AD Connect SQL Native Client MultiSubNetFailover 속성의 hello 사용을 지원 하지 않는 때문입니다.

## <a name="appendix-csanalyzer"></a>Appendix CSAnalyzer
Hello 섹션을 참조 [확인](#verify) 방법은 toouse이이 스크립트입니다.

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have hello basics, go get hello details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a>다음 단계
**개요 항목**  

* [Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정](active-directory-aadconnectsync-whatis.md)  
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)  
