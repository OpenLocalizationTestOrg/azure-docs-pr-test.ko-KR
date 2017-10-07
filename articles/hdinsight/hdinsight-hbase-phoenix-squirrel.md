---
title: "Apache 피닉스 aaaUse 및 Windows 기반 Azure HDInsight와 스 쿼 럴 | Microsoft Docs"
description: "자세한 방법을 toouse, HDInsight의 Apache 피닉스 방법과 tooinstall 스 쿼 럴 HDInsight에서 워크스테이션 tooconnect tooan HBase 클러스터에 구성 합니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a>HDInsight에서 Windows 기반 HBase 클러스터와 함께 Apache Phoenix 및 SQuirreL 사용
자세한 방법을 toouse [Apache 피닉스](http://phoenix.apache.org/) , HDInsight의 방법과 tooinstall 스 쿼 럴 HDInsight에서 워크스테이션 tooconnect tooan HBase 클러스터에 구성 합니다. Phoenix에 대한 자세한 내용은 [15분 이내의 Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)를 참조하세요. Hello 피닉스 문법에 대 한 참조 [피닉스 문법](http://phoenix.apache.org/language/index.html)합니다.

> [!NOTE]
> HDInsight의 버전 정보 피닉스 hello에 대 한 참조 [HDInsight에서 제공 하는 hello Hadoop 클러스터 버전의 새로운 기능?](hdinsight-component-versioning.md)합니다.
>

> [!IMPORTANT]
> hello 단계에서 Windows 기반 HDInsight 클러스터에 대 한이 문서 에서만 작동 합니다. HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요. Linux 기반 HDInsight에서 Phoenix 사용 방법에 대한 자세한 내용은 [HDInsight의 Linux 기반 HBase 클러스터와 함께 Apache Phoenix 사용](hdinsight-hbase-phoenix-squirrel-linux.md)을 참조하세요.
>



## <a name="use-sqlline"></a>SQLLine 사용
[SQLLine](http://sqlline.sourceforge.net/) 명령줄 유틸리티 tooexecute SQL 됩니다.

### <a name="prerequisites"></a>필수 조건
SQLLine를 사용 하려면 먼저 hello 다음이 있어야 합니다.

* **HDInsight의 HBase 클러스터**. HBase 클러스터 프로비전에 대한 자세한 내용은 [HDInsight에서 Apache HBase 시작][hdinsight-hbase-get-started]을 참조하세요.
* **Hello 원격 데스크톱 프로토콜을 통해 toohello HBase 클러스터를 연결**합니다. 자세한 내용은 [hello Azure 클래식 포털을 사용 하 여 HDInsight의 Hadoop 관리 클러스터][hdinsight-manage-portal]합니다.

**toofind hello 호스트 이름**

1. 열기 **Hadoop 명령줄** hello 바탕 화면에서.
2. Hello 명령 tooget hello DNS 접미사를 다음을 실행 합니다.

        ipconfig

    **연결별 DNS 접미사**를 적어 둡니다. 예를 들면 *myhbasecluster.f5.internal.cloudapp.net*과 같습니다. Tooan HBase 클러스터를 연결 하면의 FQDN을 사용 하 여 hello 사육 tooconnect tooone가 필요 합니다. 각 HDInsight 클러스터에는 3개의 Zookeeper, *zookeeper0*, *zookeeper1* 및 *zookeeper2*가 있습니다. hello FQDN 됩니다 다음과 같이 *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*합니다.

**toouse SQLLine**

1. 열기 **Hadoop 명령줄** hello 바탕 화면에서.
2. 다음 명령을 tooopen SQLLine hello를 실행 합니다.

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    hello 샘플에 사용 된 hello 명령:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

자세한 내용은 [SQLLine 설명서](http://sqlline.sourceforge.net/#manual) 및 [Phoenix 문법](http://phoenix.apache.org/language/index.html)을 참조하세요.

## <a name="use-squirrel"></a>SQuirrel 사용
[SQL 클라이언트 스 쿼 럴](http://squirrel-sql.sourceforge.net/) 됩니다 tooview hello 구조의 JDBC 규격 데이터베이스를 사용 하면 hello 테이블의에서 데이터를 찾아보고 등 SQL 명령을 실행 하는 그래픽 Java 프로그램입니다. 사용 되는 tooconnect tooApache HDInsight의 피닉스 수 있습니다.

이 섹션에서는 tooinstall 스 쿼 럴 VPN 통해 HDInsight에서 워크스테이션 tooconnect tooan HBase 클러스터에 구성 합니다.

### <a name="prerequisites"></a>필수 조건
Hello 절차를 수행 하기 전에 hello 다음이 필요 합니다.

* HBase 클러스터 tooan Azure 가상 네트워크 DNS 가상 컴퓨터를 배포합니다.  자세한 내용은 [Azure Virtual Network에 HBase 클러스터 만들기][hdinsight-hbase-provision-vnet]를 참조하세요.

* Hello HBase 클러스터 클러스터 연결별 DNS 접미사를 가져옵니다. tooget 것 hello 클러스터에 RDP 다음 IPConfig를 실행 합니다.  hello DNS 접미사는 유사 합니다.

        myhbase.b7.internal.cloudapp.net
* 워크스테이션에서 [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx)을 다운로드하여 설치합니다. Makecert hello 패키지 toocreate에서 인증서가 필요 합니다.  
* 워크스테이션에서 [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) 을 다운로드하여 설치합니다.  SQuirreL SQL Client 버전 3.0 이상에는 JRE 버전 1.6 이상이 필요합니다.  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a>지점-사이트 VPN 연결 toohello Azure 가상 네트워크 구성
지점 및 사이트 간 VPN 연결을 구성하는 단계는 3단계로 구성됩니다.

1. [가상 네트워크 및 동적 라우팅 게이트웨이 구성](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [인증서 만들기](#Create-your-certificates)
3. [VPN 클라이언트 구성](#Configure-your-VPN-client)

참조 [지점-사이트 VPN 연결 tooan Azure 가상 네트워크 구성](../vpn-gateway/vpn-gateway-point-to-site-create.md) 자세한 정보에 대 한 합니다.

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a>가상 네트워크 및 동적 라우팅 게이트웨이 구성
Azure 가상 네트워크에서 HBase 클러스터를 프로 비전을 위해 (이 섹션에 대 한 hello 필수 구성 요소 참조). hello 다음 단계는 tooconfigure 지점 및 사이트 간 연결입니다.

**tooconfigure hello 지점 및 사이트 연결**

1. Toohello 로그인 [Azure 클래식 포털][azure-portal]합니다.
2. Hello 왼쪽에서 클릭 **네트워크**합니다.
3. 만든 hello 가상 네트워크를 클릭 합니다. (참조 [Azure 가상 네트워크에서 프로 비전 HBase 클러스터][hdinsight-hbase-provision-vnet]).
4. 클릭 **구성** hello 위에서 합니다.
5. Hello에 **지점 및 사이트 연결** 섹션에서 **지점 및 사이트 연결을 구성**합니다.
6. 구성 **시작 IP** 및 **CIDR** toospecify hello IP 주소 범위를 VPN 클라이언트가 수신할 IP 주소 연결 된 경우. 온-프레미스에 있는 범위 네트워크 및 Azure 가상 네트워크에 연결 hello hello를 사용 하 여 hello 범위 겹칠 수 없습니다. 예를 들어 모바일 서비스는 스크립트 실행 간에 상태를 유지하지 않으므로 스크립트 실행 간에 지속되어야 하는 모든 데이터를 테이블에 저장해야 합니다. 10.0.0.0/20 hello 가상 네트워크를 선택한 경우에 hello 클라이언트 주소 공간에 대 한 10.1.0.0/24를 선택할 수 있습니다. Hello 참조 [지점 및 사이트 연결] [ vnet-point-to-site-connectivity] 자세한 내용을 보려면 페이지입니다.
7. Hello 가상 네트워크 주소 공간 섹션에서 클릭 **게이트웨이 서브넷 추가**합니다.
8. 클릭 **저장** hello hello 페이지 아래쪽에 있습니다.
9. 클릭 **예** tooconfirm hello 변경 합니다. Hello 시스템에서 변경할 toohello 다음 절차를 계속 하기 전에 hello 만들기를 완료할 때까지 기다립니다.

**동적 라우팅 게이트웨이 toocreate**

1. Hello Azure 클래식 포털에서에서 클릭 **대시보드** hello hello 페이지 위쪽에서 합니다.
2. 클릭 **게이트웨이 만들기** hello hello 페이지 아래에서 합니다.
3. 클릭 **예** tooconfirm 합니다. Hello 게이트웨이 만들어질 때까지 기다립니다.
4. 클릭 **대시보드** hello 위에서 합니다.  Hello 가상 네트워크의 시각적 다이어그램을 볼 수 있습니다.

    ![Azure 가상 네트워크 지점 및 사이트 간 가상 다이어그램][img-vnet-diagram]

    hello 다이어그램 0 클라이언트 연결을 표시합니다. 연결 toohello 가상 네트워크를 변경한 후 hello 번호가 업데이트 된 tooone 됩니다.

#### <a name="create-your-certificates"></a>인증서 만들기
사용 하 여 X.509 인증서는 한 가지 방법은 toocreate hello 인증서 작성 도구 (makecert.exe)와 함께 제공 되 [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx)합니다.

**toocreate 자체 서명 된 루트 인증서**

1. 워크스테이션에서 명령 프롬프트 창을 엽니다.
2. Toohello Visual Studio tools 폴더로 이동 합니다.
3. 다음 명령을 아래의 hello 예에서 hello 및 워크스테이션에서 hello 개인 인증서 저장소에 루트 인증서를 설치 만들고 toohello Azure 클래식 포털을 나중에 업로드 합니다 해당.cer 파일을 만들 수도 합니다.

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    .Cer 파일 toobe 여기서 HBaseVnetVPNRootCertificate은 hello 인증서에 대 한 toouse 되도록 hello 이름에 있는 hello 원하는 toohello 디렉터리를 변경 합니다.

    Hello 명령 프롬프트를 닫지 마십시오.  Hello 다음 절차에서 할 수 있습니다.

   > [!NOTE]
   > 클라이언트 인증서가 만들어집니다 루트 인증서를 만들었으므로 tooexport이이 인증서의 개인 키와 함께 사용할 하 고 tooa 안전한 위치에 복구 될 수 있습니다 저장 될 수 있습니다.
   >
   >

**toocreate 클라이언트 인증서**

* 동일한 명령 프롬프트에서 hello (toobe hello에 hello 루트 인증서를 만든 동일한 컴퓨터. hello 클라이언트 인증서를 생성 해야 hello 루트 인증서에서)를 실행 hello 다음 명령을:

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    HBaseVnetVPNRootCertificate은 hello 루트 인증서 이름입니다.  과 toomatch hello 루트 인증서 이름입니다.  

    Hello 루트 인증서와 hello 클라이언트 인증서는 컴퓨터에 개인 인증서 저장소에 저장 됩니다. Certmgr.msc tooverify를 사용 합니다.

    ![Azure Virtual Network 지점 및 사이트 간 VPN 인증서][img-certificate]

    클라이언트 인증서 tooconnect toohello 가상 네트워크를 지정 하는 각 컴퓨터에 설치 합니다. 인증서를 만드는 고유한 클라이언트는 각 컴퓨터에 대 한 tooconnect toohello 가상 네트워크를 지정 하는 것이 좋습니다. tooexport hello 클라이언트 인증서 certmgr.msc를 사용 합니다.

**tooupload hello 루트 인증서 toohello Azure 클래식 포털**

1. Hello Azure 클래식 포털에서에서 클릭 **네트워크** hello 왼쪽에 있습니다.
2. 이때 HBase 클러스터에 배포 하는 hello 가상 네트워크를 클릭 합니다.
3. 클릭 **인증서** hello 위에서 합니다.
4. 클릭 **업로드** hello에서 아래쪽 및 마지막 하기 전에 hello 절차에서 만든 hello 루트 인증서 파일을 지정 합니다. 가져온 hello 인증서를 가져올 때까지 기다립니다.
5. 클릭 **대시보드** hello 위에 표시 합니다.  hello 가상 다이어그램 hello 상태가 표시 됩니다.

#### <a name="configure-your-vpn-client"></a>VPN 클라이언트 구성
**hello 클라이언트 VPN 패키지 toodownload 및 설치**

1. Hello 빠른 보기 섹션의 hello 가상 네트워크의 hello 대시보드 페이지에서 하나를 클릭 **다운로드 hello 64 비트 클라이언트 VPN 패키지** 또는 **다운로드 hello 32 비트 클라이언트 VPN 패키지** 기반 사용자 워크스테이션 운영 체제 버전입니다.
2. 클릭 **실행** tooinstall hello 패키지 합니다.
3. Hello 보안 프롬프트 클릭 **자세한 정보**, 클릭 하 고 **그래도 실행**합니다.
4. **예** 를 두 번 클릭합니다.

**tooconnect tooVPN**

1. 워크스테이션의 hello 바탕 화면에서 hello 작업 표시줄에서 hello 네트워크 아이콘을 클릭 합니다. 가상 네트워크 이름과 함께 VPN 연결이 표시됩니다.
2. Hello VPN 연결 이름을 클릭 합니다.
3. **Connect**를 클릭합니다.

**tootest hello VPN 연결 및 도메인 이름 확인**

* Hello 워크스테이션에서 명령 프롬프트를 열고 이며 hello hello HBase 클러스터의 DNS 접미사를 지정 하는 이름 다음의 하나를 ping myhbase.b7.internal.cloudapp.net:

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a>워크스테이션에서 SQuirreL 설치 및 구성
**스 쿼 럴 tooinstall**

1. Hello 스 쿼 럴 SQL 클라이언트 jar 파일을 다운로드 [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation)합니다.
2. 열기/실행 hello jar 파일입니다. Hello 필요 [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html)합니다.
3. **다음** 를 두 번 클릭합니다.
4. Hello 쓰기 권한, 클릭 하 고 있는 경우 경로 지정 **다음**합니다.

  > [!NOTE]
  > hello 기본 설치 폴더는 hello C:\Program Files\squirrel sql 3.6 폴더에 있습니다.  순서 toowrite toothis 경로에 hello installer hello 관리자 권한이 부여 되어야 합니다. 관리자 권한으로 명령 프롬프트를 열고 지정, tooJava의 bin 폴더 탐색을 실행 합니다.
  >
  >     java.exe-jar [hello hello 스 쿼 럴 jar 파일의 경로]
5. 클릭 **확인** tooconfirm hello 대상 디렉터리를 만드는 중입니다.
6. hello 기본 설정은 tooinstall hello 기본 및 표준 패키지입니다.  **다음**을 누릅니다.
7. **다음**을 두 번 클릭한 후 **완료**를 클릭합니다.

**tooinstall hello 피닉스 드라이버**

hello 피닉스 드라이버 jar 파일은 hello HBase 클러스터에 있습니다. hello 경로 hello 버전에 따라 유사한 toohello 다음과 같습니다.

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
Toocopy 필요한 것 hello [스 쿼 럴 설치 폴더] 아래에서 tooyour 워크스테이션 /lib 경로입니다.  hello 가장 쉬운 방법은 hello 클러스터 변환한 다음 사용 하 여 파일 복사/붙여넣기 (CTRL + C 및 CTRL + V) toocopy tooRDP 것 tooyour 워크스테이션.

**tooadd 피닉스 드라이버 tooSQuirreL**

1. 워크스테이션에서 SQuirreL SQL Client를 엽니다.
2. Hello 클릭 **드라이버** hello 왼쪽에 탭 합니다.
3. Hello에서 **드라이버** 메뉴를 클릭 하 여 **새 드라이버**합니다.
4. Hello 다음 정보를 입력 합니다.

   * **이름**: Phoenix
   * **예제 URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net
   * **클래스 이름**: org.apache.phoenix.jdbc.PhoenixDriver

     > [!WARNING]
     > 사용자 hello 예를 들어 URL에에서 모든 소문자로 변환 합니다. 그 중 하나가 다운된 경우 전체 zookeeper 쿼럼을 사용할 수 있습니다.  hello hostnames은 zookeeper0, zookeeper1, 및 zookeeper2입니다.
     >
     >

     ![HDInsight HBase Phoenix SQuirreL 드라이버][img-squirrel-driver]
5. **확인**을 클릭합니다.

**toocreate 별칭 toohello HBase 클러스터**

1. 스 쿼 럴, 클릭 hello **별칭** hello 왼쪽에 탭 합니다.
2. Hello에서 **별칭** 메뉴를 클릭 하 여 **새 별칭**합니다.
3. Hello 다음 정보를 입력 합니다.

   * **이름**: hello 이름 hello HBase 클러스터 또는 원하는 모든 이름입니다.
   * **드라이버**: Phoenix.  이 hello 마지막 절차에서 만든 hello 드라이버 이름은 일치 해야 합니다.
   * **URL**: hello URL 드라이버 구성에서 복사 됩니다. 모든 소문자 toouser 있는지를 확인 합니다.
   * **사용자 이름**: 모든 텍스트일 수 있습니다.  여기서 VPN 연결을 사용 하므로 hello 사용자 이름이 전혀 사용 되지 않습니다.
   * **암호**: 모든 텍스트일 수 있습니다.

     ![HDInsight HBase Phoenix SQuirreL 드라이버][img-squirrel-alias]
4. **테스트**를 클릭합니다.
5. **Connect**를 클릭합니다. Hello 연결 하면 스 쿼 럴이 같습니다.

    ![HBase Phoenix SQuirreL][img-squirrel]

**toorun 테스트**

1. Hello 클릭 **SQL** 바로 다음 toohello 탭 **개체** 탭 합니다.
2. 복사한 코드 다음 hello를 붙여넣습니다.

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. Hello 실행된 단추를 클릭 합니다.

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. 뒤로 toohello 전환 **개체** 탭 합니다.
5. Hello 별칭 이름을 확장 한 다음 확장 **테이블**합니다.  Hello 새 테이블 아래에 나열 참조 해야 합니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 배웠습니다 어떻게 toouse HDInsight의 Apache 피닉스 합니다.  toolearn을 참조 합니다.

* [HDInsight HBase 개요][hdinsight-hbase-overview]: HBase는 대량의 비구조적/반구조적 데이터에 대해 임의 액세스 및 강력한 일관성을 제공하는 Hadoop 기반의 Apache 오픈 소스 NoSQL 데이터베이스입니다.
* [Azure 가상 네트워크에서 HBase 클러스터를 프로 비전][hdinsight-hbase-provision-vnet]: 가상 네트워크 통합 HBase 클러스터 동일한 가상 네트워크로 응용 프로그램 이므로 배포 된 toohello 수 있는 응용 프로그램이 통신할 수 HBase에 직접 해당 합니다.
* [HDInsight에서 HBase 복제 구성](hdinsight-hbase-replication.md): 자세한 방법 두 Azure 데이터 센터에서 tooconfigure HBase 복제 합니다.
* [HDInsight에서 HBase와 Twitter 감성 분석][hbase-twitter-sentiment]: 자세한 방법을 toodo 실시간 [감성 분석](http://en.wikipedia.org/wiki/Sentiment_analysis) HDInsight의 Hadoop 클러스터의 HBase를 사용 하 여 빅 데이터의 합니다.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
