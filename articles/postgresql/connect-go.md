---
title: "aaaConnect tooAzure Go 언어를 사용 하 여 PostgreSQL 데이터베이스 | Microsoft Docs"
description: "이 퀵 스타트의 Go 프로그래밍 언어에서는 예제를 제공 tooconnect 사용 및 PostgreSQL에 대 한 Azure 데이터베이스에서 데이터를 쿼리할 수 있습니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: go
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: aa3c93da03116b8fcb54557494dccfad558e5f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="87a17-103">Azure 데이터베이스에 대 한 PostgreSQL: 언어 tooconnect 및 쿼리 데이터 사용 하 여 이동</span><span class="sxs-lookup"><span data-stu-id="87a17-103">Azure Database for PostgreSQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="87a17-104">이 빠른 시작에서는 PostgreSQL 사용에 대 한 tooconnect tooan Azure 데이터베이스에서 작성 된 hello 코드가 방식 [이동](https://golang.org/) 언어 (golang).</span><span class="sxs-lookup"><span data-stu-id="87a17-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using code written in hello [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="87a17-105">Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="87a17-106">이 문서에서는 하지만 새 tooworking PostgreSQL에 대 한 Azure 데이터베이스는 Go를 사용 하 여 개발에 잘 알고 있다면 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87a17-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="87a17-107">Prerequisites</span></span>
<span data-ttu-id="87a17-108">이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="87a17-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="87a17-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="87a17-110">DB 만들기 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="87a17-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="87a17-111">Go 및 pq 커넥터 설치</span><span class="sxs-lookup"><span data-stu-id="87a17-111">Install Go and pq connector</span></span>
<span data-ttu-id="87a17-112">설치 [이동](https://golang.org/doc/install) 및 hello [순수 이동 Postgres 드라이버 (pq)](https://github.com/lib/pq) 사용자의 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-112">Install [Go](https://golang.org/doc/install) and hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="87a17-113">플랫폼에 따라 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="87a17-114">Windows</span><span class="sxs-lookup"><span data-stu-id="87a17-114">Windows</span></span>
1. <span data-ttu-id="87a17-115">[다운로드](https://golang.org/dl/) Go toohello에 따라 Microsoft Windows 용 설치 [설치 지침](https://golang.org/doc/install)합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="87a17-116">Hello 시작 메뉴에서 hello 명령 프롬프트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="87a17-117">다음과 같이 프로젝트 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-117">Make a folder for your project such.</span></span> <span data-ttu-id="87a17-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`</span><span class="sxs-lookup"><span data-stu-id="87a17-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="87a17-119">와 같은 hello 프로젝트 폴더로 디렉터리를 변경 `cd %USERPROFILE%\go\src\postgresqlgo`합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="87a17-120">GOPATH toopoint toohello 소스 코드 디렉터리에 대 한 hello 환경 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="87a17-121">`set GOPATH=%USERPROFILE%\go`</span><span class="sxs-lookup"><span data-stu-id="87a17-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="87a17-122">Hello 설치 [순수 이동 Postgres 드라이버 (pq)](https://github.com/lib/pq) hello를 실행 하 여 `go get github.com/lib/pq` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-122">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="87a17-123">요약 하자면, Go 설치 후 hello 명령 프롬프트에서 다음이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="87a17-124">Linux(Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="87a17-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="87a17-125">Hello Bash 셸의 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="87a17-126">`sudo apt-get install golang-go`를 실행하여 Go를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="87a17-127">홈 디렉터리에서 프로젝트 폴더를 만듭니다(예: `mkdir -p ~/go/src/postgresqlgo/`).</span><span class="sxs-lookup"><span data-stu-id="87a17-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="87a17-128">와 같은 hello 폴더로 디렉터리를 변경 `cd ~/go/src/postgresqlgo/`합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-128">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="87a17-129">집합 hello GOPATH 환경 변수 toopoint tooa 유효한 소스와 같은 디렉터리에 현재 홈 디렉터리의 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="87a17-130">Hello bash 셸의 실행 `export GOPATH=~/go` tooadd hello GOPATH hello 현재 셸 세션에 대 한 hello으로 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="87a17-131">Hello 설치 [순수 이동 Postgres 드라이버 (pq)](https://github.com/lib/pq) hello를 실행 하 여 `go get github.com/lib/pq` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-131">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="87a17-132">요약하자면, 다음과 같은 Bash 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="87a17-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="87a17-133">Apple macOS</span></span>
1. <span data-ttu-id="87a17-134">다운로드 및 설치 toohello를 따라 이동 [설치 지침](https://golang.org/doc/install) 플랫폼에 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="87a17-135">Hello Bash 셸의 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="87a17-136">홈 디렉터리에서 프로젝트 폴더를 만듭니다(예: `mkdir -p ~/go/src/postgresqlgo/`).</span><span class="sxs-lookup"><span data-stu-id="87a17-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="87a17-137">와 같은 hello 폴더로 디렉터리를 변경 `cd ~/go/src/postgresqlgo/`합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-137">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="87a17-138">집합 hello GOPATH 환경 변수 toopoint tooa 유효한 소스와 같은 디렉터리에 현재 홈 디렉터리의 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="87a17-139">Hello bash 셸의 실행 `export GOPATH=~/go` tooadd hello GOPATH hello 현재 셸 세션에 대 한 hello으로 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="87a17-140">Hello 설치 [순수 이동 Postgres 드라이버 (pq)](https://github.com/lib/pq) hello를 실행 하 여 `go get github.com/lib/pq` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-140">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="87a17-141">요약하자면, Go 설치 후 다음 bash 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="87a17-142">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="87a17-142">Get connection information</span></span>
<span data-ttu-id="87a17-143">PostgreSQL를 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-143">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="87a17-144">정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="87a17-145">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="87a17-146">Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 등 생성 한 hello 서버에 대 한 검색 **mypgserver 20170401**합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="87a17-147">Hello 서버 이름을 클릭 **mypgserver 20170401**합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-147">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="87a17-148">선택 hello 서버 **개요** 페이지.</span><span class="sxs-lookup"><span data-stu-id="87a17-148">Select hello server's **Overview** page.</span></span> <span data-ttu-id="87a17-149">Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="87a17-150">![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="87a17-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="87a17-151">서버 로그인 정보를 잊은 경우 탐색 toohello **개요** 페이지 및 보기 hello 서버 관리자 로그인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-151">If you forget your server login information, navigate toohello **Overview** page, and view hello Server admin login name.</span></span> <span data-ttu-id="87a17-152">필요한 경우 hello 암호를 재설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-152">If necessary, reset hello password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="87a17-153">Go 코드 작성 및 실행</span><span class="sxs-lookup"><span data-stu-id="87a17-153">Build and run Go code</span></span> 
1. <span data-ttu-id="87a17-154">toowrite Golang 코드, Microsoft Windows의 메모장과 같은 간단한 텍스트 편집기를 사용할 수 있습니다 [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) 또는 [Nano](https://www.nano-editor.org/) Ubuntu, 또는 macOS에서 TextEdit 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-154">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="87a17-155">보다 풍부한 IDE(대화형 개발 환경)를 선호하는 경우 Jetbrains의 [Gogland](https://www.jetbrains.com/go/), Microsoft의 [Visual Studio Code](https://code.visualstudio.com/) 또는 [Atom](https://atom.io/)을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="87a17-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="87a17-156">텍스트 파일로 hello 섹션 아래에서 hello Golang 코드를 붙여 넣고 파일 확장명으로 프로젝트 폴더에 저장할 \*Windows 경로 같은.go `%USERPROFILE%\go\src\postgresqlgo\createtable.go` 또는 Linux 경로 `~/go/src/postgresqlgo/createtable.go`합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-156">Paste hello Golang code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="87a17-157">Hello 찾습니다 `HOST`, `DATABASE`, `USER`, 및 `PASSWORD` hello 코드 및 고유한 값으로 바꾸기 hello 예제 값에는 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-157">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span>  
4. <span data-ttu-id="87a17-158">Hello 명령 프롬프트를 시작 하거나 bash 셸은 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-158">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="87a17-159">디렉터리를 프로젝트 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-159">Change directory into your project folder.</span></span> <span data-ttu-id="87a17-160">예를 들어 Windows에서는 `cd %USERPROFILE%\go\src\postgresqlgo\`이고,</span><span class="sxs-lookup"><span data-stu-id="87a17-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="87a17-161">Linux에서는 `cd ~/go/src/postgresqlgo/`입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="87a17-162">일부 hello IDE 환경 셸 명령이 필요 없이 디버그 및 런타임 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-162">Some of hello IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="87a17-163">Hello 명령을 입력 하 여 hello 코드 실행 `go run createtable.go` toocompile hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-163">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="87a17-164">네이티브 응용 프로그램에 hello 코드 또는 toobuild `go build createtable.go`, 다음 실행 `createtable.exe` toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-164">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="87a17-165">테이블 연결 및 생성</span><span class="sxs-lookup"><span data-stu-id="87a17-165">Connect and create a table</span></span>
<span data-ttu-id="87a17-166">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 테이블을 만들 **CREATE TABLE** SQL 문 다음에 **INSERT INTO** hello 테이블에 SQL 문 tooadd 행입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-166">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="87a17-167">hello 코드는 세 가지 패키지를 가져옵니다: hello [sql 패키지](https://golang.org/pkg/database/sql/), hello [pq 패키지](http://godoc.org/github.com/lib/pq) hello Postgres 서버 hello와 드라이버 toocommunicate로 [fmt 패키지](https://golang.org/pkg/fmt/) 인쇄에 대 한 입력 및 hello 명령줄에 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-167">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="87a17-168">메서드를 호출 하는 hello 코드 [sql 합니다. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL, 및 메서드를 사용 하 여 검사 hello 연결에 대 한 데이터베이스 [db입니다. Ping()](https://golang.org/pkg/database/sql/#DB.Ping)합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-168">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="87a17-169">A [데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB) hello 데이터베이스 서버에 대 한 hello 연결 풀을 보유, 전체에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="87a17-170">hello 코드 호출 hello [exec ()](https://golang.org/pkg/database/sql/#DB.Exec) 메서드가 여러 번 toorun 몇 가지 SQL 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-170">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several SQL commands.</span></span> <span data-ttu-id="87a17-171">각 오류가 발생 한 경우 사용자 지정 checkError() 메서드 toocheck 시간 및 tooexit 오류가 발생 하면 당황 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-171">Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="87a17-172">Hello 대체 `HOST`, `DATABASE`, `USER`, 및 `PASSWORD` 를 원하는 값으로 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-172">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed)")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table")

    // Insert some data into table.
    sql_statement := "INSERT INTO inventory (name, quantity) VALUES ($1, $2);"
    _, err = db.Exec(sql_statement, "banana", 150)
    checkError(err)
    _, err = db.Exec(sql_statement, "orange", 154)
    checkError(err)
    _, err = db.Exec(sql_statement, "apple", 100)
    checkError(err)
    fmt.Println("Inserted 3 rows of data")
}
```

## <a name="read-data"></a><span data-ttu-id="87a17-173">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="87a17-173">Read data</span></span>
<span data-ttu-id="87a17-174">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="87a17-175">hello 코드는 세 가지 패키지를 가져옵니다: hello [sql 패키지](https://golang.org/pkg/database/sql/), hello [pq 패키지](http://godoc.org/github.com/lib/pq) hello Postgres 서버 hello와 드라이버 toocommunicate로 [fmt 패키지](https://golang.org/pkg/fmt/) 인쇄에 대 한 입력 및 hello 명령줄에 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="87a17-176">메서드를 호출 하는 hello 코드 [sql 합니다. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL, 및 메서드를 사용 하 여 검사 hello 연결에 대 한 데이터베이스 [db입니다. Ping()](https://golang.org/pkg/database/sql/#DB.Ping)합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-176">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="87a17-177">A [데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB) hello 데이터베이스 서버에 대 한 hello 연결 풀을 보유, 전체에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="87a17-178">메서드를 호출 하 여 hello select 쿼리를 실행할 [db입니다. Query ()](https://golang.org/pkg/database/sql/#DB.Query), 형식의 변수에 유지 되는 결과 행 hello 및 [행](https://golang.org/pkg/database/sql/#Rows)합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-178">hello select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and hello resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="87a17-179">hello 코드 메서드를 사용 하 여 hello 현재 행의 hello 열 데이터 값을 읽고 [행. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) 및 hello 반복기를 사용 하 여 hello 행에 대해 루프 [행. Next ()](https://golang.org/pkg/database/sql/#Rows.Next) 행이 더 이상 존재 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-179">hello code reads hello column data values in hello current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over hello rows using hello iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="87a17-180">각 행의 열 값은 아웃 인쇄 toohello 콘솔입니다. 각 오류가 발생 한 경우 사용자 지정 checkError() 메서드 toocheck 시간 및 tooexit 오류가 발생 하면 당황 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-180">Each row's column values are printed toohello console out. Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="87a17-181">Hello 대체 `HOST`, `DATABASE`, `USER`, 및 `PASSWORD` 를 원하는 값으로 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-181">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Read rows from table.
    var id int
    var name string
    var quantity int

    sql_statement := "SELECT * from inventory;"
    rows, err := db.Query(sql_statement)
    checkError(err)

    for rows.Next() {
        switch err := rows.Scan(&id, &name, &quantity); err {
        case sql.ErrNoRows:
            fmt.Println("No rows were returned")
        case nil:
            fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
        default:
            checkError(err)
        }
    }
}
```

## <a name="update-data"></a><span data-ttu-id="87a17-182">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="87a17-182">Update data</span></span>
<span data-ttu-id="87a17-183">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 업데이트는 **업데이트** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="87a17-184">hello 코드는 세 가지 패키지를 가져옵니다: hello [sql 패키지](https://golang.org/pkg/database/sql/), hello [pq 패키지](http://godoc.org/github.com/lib/pq) hello Postgres 서버 hello와 드라이버 toocommunicate로 [fmt 패키지](https://golang.org/pkg/fmt/) 인쇄에 대 한 입력 및 hello 명령줄에 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="87a17-185">메서드를 호출 하는 hello 코드 [sql 합니다. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL, 및 메서드를 사용 하 여 검사 hello 연결에 대 한 데이터베이스 [db입니다. Ping()](https://golang.org/pkg/database/sql/#DB.Ping)합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-185">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="87a17-186">A [데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB) hello 데이터베이스 서버에 대 한 hello 연결 풀을 보유, 전체에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="87a17-187">hello 코드 호출 hello [exec ()](https://golang.org/pkg/database/sql/#DB.Exec) 메서드 toorun hello hello 테이블을 업데이트 하는 SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="87a17-188">사용자 지정 checkError() 메서드 toocheck에서 오류가 발생 했으며 오류가 tooexit 당황 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-188">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="87a17-189">Hello 대체 `HOST`, `DATABASE`, `USER`, 및 `PASSWORD` 를 원하는 값으로 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-189">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a><span data-ttu-id="87a17-190">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="87a17-190">Delete data</span></span>
<span data-ttu-id="87a17-191">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **삭제** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-191">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="87a17-192">hello 코드는 세 가지 패키지를 가져옵니다: hello [sql 패키지](https://golang.org/pkg/database/sql/), hello [pq 패키지](http://godoc.org/github.com/lib/pq) hello Postgres 서버 hello와 드라이버 toocommunicate로 [fmt 패키지](https://golang.org/pkg/fmt/) 인쇄에 대 한 입력 및 hello 명령줄에 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="87a17-193">메서드를 호출 하는 hello 코드 [sql 합니다. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL, 및 메서드를 사용 하 여 검사 hello 연결에 대 한 데이터베이스 [db입니다. Ping()](https://golang.org/pkg/database/sql/#DB.Ping)합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-193">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="87a17-194">A [데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB) hello 데이터베이스 서버에 대 한 hello 연결 풀을 보유, 전체에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="87a17-195">hello 코드 호출 hello [exec ()](https://golang.org/pkg/database/sql/#DB.Exec) 메서드 toorun hello hello 테이블을 업데이트 하는 SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="87a17-196">사용자 지정 checkError() 메서드 toocheck에서 오류가 발생 했으며 오류가 tooexit 당황 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-196">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="87a17-197">Hello 대체 `HOST`, `DATABASE`, `USER`, 및 `PASSWORD` 를 원하는 값으로 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="87a17-197">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a><span data-ttu-id="87a17-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="87a17-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="87a17-199">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="87a17-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
