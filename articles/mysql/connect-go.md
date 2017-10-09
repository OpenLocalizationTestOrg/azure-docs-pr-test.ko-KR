---
title: "Go를 사용 하 여 MySQL 용 tooAzure 데이터베이스 연결 | Microsoft Docs"
description: "이 퀵 스타트의 tooconnect를 사용 하 고 MySQL에 대 한 Azure 데이터베이스에서 데이터를 쿼리할 수 여러 Go 코드 샘플을 제공 합니다."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: go
ms.topic: hero-article
ms.date: 07/18/2017
ms.openlocfilehash: e8067b807ee729e04850c5325f476806bcd54983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="0bddc-103">MySQL에 대 한 azure 데이터베이스: 언어 tooconnect 및 쿼리 데이터 사용 하 여 이동</span><span class="sxs-lookup"><span data-stu-id="0bddc-103">Azure Database for MySQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="0bddc-104">이 빠른 시작에서는 tooconnect tooan Azure 데이터베이스를 사용 하 여 MySQL에 대 한 코드에서 작성 된 hello [이동](https://golang.org/) 창, Ubuntu Linux 및 Apple macOS 플랫폼에서 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using code written in hello [Go](https://golang.org/) language from Windows, Ubuntu Linux, and Apple macOS platforms.</span></span> <span data-ttu-id="0bddc-105">Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="0bddc-106">이 문서에서는 하지만 새 tooworking MySQL에 대 한 Azure 데이터베이스는 Go를 사용 하 여 개발에 잘 알고 있다면 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bddc-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0bddc-107">Prerequisites</span></span>
<span data-ttu-id="0bddc-108">이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="0bddc-109">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="0bddc-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="0bddc-110">Azure CLI를 사용한 MySQL용 Azure 데이터베이스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="0bddc-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-go-and-mysql-connector"></a><span data-ttu-id="0bddc-111">Go 및 MySQL 커넥터 설치</span><span class="sxs-lookup"><span data-stu-id="0bddc-111">Install Go and MySQL connector</span></span>
<span data-ttu-id="0bddc-112">설치 [이동](https://golang.org/doc/install) 및 hello [MySQL에 대 한 드라이버-go-sql](https://github.com/go-sql-driver/mysql#installation) 사용자의 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-112">Install [Go](https://golang.org/doc/install) and hello [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation) on your own machine.</span></span> <span data-ttu-id="0bddc-113">플랫폼에 따라 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="0bddc-114">Windows</span><span class="sxs-lookup"><span data-stu-id="0bddc-114">Windows</span></span>
1. <span data-ttu-id="0bddc-115">[다운로드](https://golang.org/dl/) Go toohello에 따라 Microsoft Windows 용 설치 [설치 지침](https://golang.org/doc/install)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="0bddc-116">Hello 시작 메뉴에서 hello 명령 프롬프트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="0bddc-117">다음과 같이 프로젝트 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-117">Make a folder for your project such.</span></span> <span data-ttu-id="0bddc-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`</span><span class="sxs-lookup"><span data-stu-id="0bddc-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span></span>
4. <span data-ttu-id="0bddc-119">와 같은 hello 프로젝트 폴더로 디렉터리를 변경 `cd %USERPROFILE%\go\src\mysqlgo`합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\mysqlgo`.</span></span>
5. <span data-ttu-id="0bddc-120">GOPATH toopoint toohello 소스 코드 디렉터리에 대 한 hello 환경 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="0bddc-121">`set GOPATH=%USERPROFILE%\go`</span><span class="sxs-lookup"><span data-stu-id="0bddc-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="0bddc-122">Hello 설치 [mysql에 대 한 드라이버-go-sql](https://github.com/go-sql-driver/mysql#installation) hello를 실행 하 여 `go get github.com/go-sql-driver/mysql` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-122">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="0bddc-123">요약 하자면, Go 설치 후 hello 명령 프롬프트에서 다음이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="0bddc-124">Linux(Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="0bddc-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="0bddc-125">Hello Bash 셸의 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="0bddc-126">`sudo apt-get install golang-go`를 실행하여 Go를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="0bddc-127">홈 디렉터리에서 프로젝트 폴더를 만듭니다(예: `mkdir -p ~/go/src/mysqlgo/`).</span><span class="sxs-lookup"><span data-stu-id="0bddc-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="0bddc-128">와 같은 hello 폴더로 디렉터리를 변경 `cd ~/go/src/mysqlgo/`합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-128">Change directory into hello folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="0bddc-129">집합 hello GOPATH 환경 변수 toopoint tooa 유효한 소스와 같은 디렉터리에 현재 홈 디렉터리의 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="0bddc-130">Hello bash 셸의 실행 `export GOPATH=~/go` tooadd hello GOPATH hello 현재 셸 세션에 대 한 hello으로 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="0bddc-131">Hello 설치 [mysql에 대 한 드라이버-go-sql](https://github.com/go-sql-driver/mysql#installation) hello를 실행 하 여 `go get github.com/go-sql-driver/mysql` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-131">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="0bddc-132">요약하자면, 다음과 같은 Bash 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a><span data-ttu-id="0bddc-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="0bddc-133">Apple macOS</span></span>
1. <span data-ttu-id="0bddc-134">다운로드 및 설치 toohello를 따라 이동 [설치 지침](https://golang.org/doc/install) 플랫폼에 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="0bddc-135">Hello Bash 셸의 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="0bddc-136">홈 디렉터리에서 프로젝트 폴더를 만듭니다(예: `mkdir -p ~/go/src/mysqlgo/`).</span><span class="sxs-lookup"><span data-stu-id="0bddc-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="0bddc-137">와 같은 hello 폴더로 디렉터리를 변경 `cd ~/go/src/mysqlgo/`합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-137">Change directory into hello folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="0bddc-138">집합 hello GOPATH 환경 변수 toopoint tooa 유효한 소스와 같은 디렉터리에 현재 홈 디렉터리의 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="0bddc-139">Hello bash 셸의 실행 `export GOPATH=~/go` tooadd hello GOPATH hello 현재 셸 세션에 대 한 hello으로 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="0bddc-140">Hello 설치 [mysql에 대 한 드라이버-go-sql](https://github.com/go-sql-driver/mysql#installation) hello를 실행 하 여 `go get github.com/go-sql-driver/mysql` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-140">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="0bddc-141">요약하자면, Go 설치 후 다음 bash 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a><span data-ttu-id="0bddc-142">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="0bddc-142">Get connection information</span></span>
<span data-ttu-id="0bddc-143">MySQL 용 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-143">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="0bddc-144">정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="0bddc-145">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0bddc-146">Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 같은 creased 한 hello 서버에 대 한 검색 **myserver4demo**합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="0bddc-147">Hello 서버 이름을 클릭 **myserver4demo**합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-147">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="0bddc-148">선택 hello 서버 **속성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="0bddc-148">Select hello server's **Properties** page.</span></span> <span data-ttu-id="0bddc-149">Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="0bddc-150">![MySQL용 Azure Database - 서버 관리자 로그인](./media/connect-go/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="0bddc-150">![Azure Database for MySQL - Server Admin Login](./media/connect-go/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="0bddc-151">서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-151">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="build-and-run-go-code"></a><span data-ttu-id="0bddc-152">Go 코드 작성 및 실행</span><span class="sxs-lookup"><span data-stu-id="0bddc-152">Build and run Go code</span></span> 
1. <span data-ttu-id="0bddc-153">toowrite Golang 코드, Microsoft Windows의 메모장과 같은 간단한 텍스트 편집기를 사용할 수 있습니다 [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) 또는 [Nano](https://www.nano-editor.org/) Ubuntu, 또는 macOS에서 TextEdit 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-153">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="0bddc-154">보다 풍부한 IDE(대화형 개발 환경)를 선호하는 경우 Jetbrains의 [Gogland](https://www.jetbrains.com/go/), Microsoft의 [Visual Studio Code](https://code.visualstudio.com/) 또는 [Atom](https://atom.io/)을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="0bddc-154">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="0bddc-155">텍스트 파일에 hello 아래 hello 섹션에서 Go 코드를 붙여 넣고 파일 확장명으로 프로젝트 폴더에 저장할 \*Windows 경로 같은.go `%USERPROFILE%\go\src\mysqlgo\createtable.go` 또는 Linux 경로 `~/go/src/mysqlgo/createtable.go`합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-155">Paste hello Go code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\mysqlgo\createtable.go` or Linux path `~/go/src/mysqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="0bddc-156">Hello 찾습니다 `HOST`, `DATABASE`, `USER`, 및 `PASSWORD` hello 코드 및 고유한 값으로 바꾸기 hello 예제 값에는 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-156">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span> 
4. <span data-ttu-id="0bddc-157">Hello 명령 프롬프트를 시작 하거나 bash 셸은 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-157">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="0bddc-158">디렉터리를 프로젝트 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-158">Change directory into your project folder.</span></span> <span data-ttu-id="0bddc-159">예를 들어 Windows에서는 `cd %USERPROFILE%\go\src\mysqlgo\`이고,</span><span class="sxs-lookup"><span data-stu-id="0bddc-159">For example, on Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span></span> <span data-ttu-id="0bddc-160">Linux에서는 `cd ~/go/src/mysqlgo/`입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-160">On Linux `cd ~/go/src/mysqlgo/`.</span></span>  <span data-ttu-id="0bddc-161">언급 된 hello IDE 편집기의 일부 셸 명령이 필요 없이 디버그 및 런타임 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-161">Some of hello IDE editors mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="0bddc-162">Hello 명령을 입력 하 여 hello 코드 실행 `go run createtable.go` toocompile hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-162">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="0bddc-163">네이티브 응용 프로그램에 hello 코드 또는 toobuild `go build createtable.go`, 다음 실행 `createtable.exe` toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-163">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="0bddc-164">테이블 연결, 생성 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="0bddc-164">Connect, create table, and insert data</span></span>
<span data-ttu-id="0bddc-165">사용 하 여 hello 다음 tooconnect toohello 서버 코드, 테이블을 만들고 및 사용 하 여 hello 데이터 로드는 **삽입** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-165">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="0bddc-166">hello 코드는 세 가지 패키지를 가져옵니다: hello [sql 패키지](https://golang.org/pkg/database/sql/), hello [mysql에 대 한 이동 sql 드라이버](https://github.com/go-sql-driver/mysql#installation) hello MySQL에 대 한 Azure 데이터베이스와 hello 드라이버 toocommunicate로 [fmt 패키지](https://golang.org/pkg/fmt/)인쇄 된 입력 및 hello 명령줄에 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-166">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="0bddc-167">메서드를 호출 하는 hello 코드 [sql 합니다. Open ()](http://go-database-sql.org/accessing.html) tooconnect tooAzure MySQL 및 메서드를 사용 하 여 검사 hello 연결에 대 한 데이터베이스 [db입니다. Ping()](https://golang.org/pkg/database/sql/#DB.Ping)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-167">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="0bddc-168">A [데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB) hello 데이터베이스 서버에 대 한 hello 연결 풀을 보유, 전체에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-168">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="0bddc-169">hello 코드 호출 hello [exec ()](https://golang.org/pkg/database/sql/#DB.Exec) 메서드가 여러 번 toorun 여러 개의 DDL 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-169">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several DDL commands.</span></span> <span data-ttu-id="0bddc-170">또한 사용 하 여 hello hello 코드 [Prepare()](http://go-database-sql.org/prepared.html) 및 준비 된 문을 다른 매개 변수와 함께 tooinsert 세 행 toorun exec ().</span><span class="sxs-lookup"><span data-stu-id="0bddc-170">hello code also uses hello [Prepare()](http://go-database-sql.org/prepared.html) and Exec() toorun prepared statements with different parameters tooinsert three rows.</span></span> <span data-ttu-id="0bddc-171">될 때마다 사용자 지정 checkError() 메서드 이면 사용된 toocheck에서 오류가 발생 했으며 tooexit 상관 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-171">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="0bddc-172">Hello 대체 `host`, `database`, `user`, 및 `password` 를 원하는 값으로는 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-172">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed).")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table.")

    // Insert some data into table.
    sqlStatement, err := db.Prepare("INSERT INTO inventory (name, quantity) VALUES (?, ?);")
    res, err := sqlStatement.Exec("banana", 150)
    checkError(err)
    rowCount, err := res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("orange", 154)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("apple", 100)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}

```

## <a name="read-data"></a><span data-ttu-id="0bddc-173">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="0bddc-173">Read data</span></span>
<span data-ttu-id="0bddc-174">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="0bddc-175">hello 코드는 세 가지 패키지를 가져옵니다: hello [sql 패키지](https://golang.org/pkg/database/sql/), hello [mysql에 대 한 이동 sql 드라이버](https://github.com/go-sql-driver/mysql#installation) hello MySQL에 대 한 Azure 데이터베이스와 hello 드라이버 toocommunicate로 [fmt 패키지](https://golang.org/pkg/fmt/)인쇄 된 입력 및 hello 명령줄에 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="0bddc-176">메서드를 호출 하는 hello 코드 [sql 합니다. Open ()](http://go-database-sql.org/accessing.html) tooconnect tooAzure MySQL 및 메서드를 사용 하 여 검사 hello 연결에 대 한 데이터베이스 [db입니다. Ping()](https://golang.org/pkg/database/sql/#DB.Ping)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-176">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="0bddc-177">A [데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB) hello 데이터베이스 서버에 대 한 hello 연결 풀을 보유, 전체에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="0bddc-178">hello 코드 호출 hello [query ()](https://golang.org/pkg/database/sql/#DB.Query) 메서드 toorun hello select 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-178">hello code calls hello [Query()](https://golang.org/pkg/database/sql/#DB.Query) method toorun hello select command.</span></span> <span data-ttu-id="0bddc-179">실행 한 다음 [next ()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate hello 결과 집합 및 [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) tooparse hello 열 값을 hello 값을 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-179">Then it runs [Next()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate through hello result set and [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) tooparse hello column values, saving hello value into variables.</span></span> <span data-ttu-id="0bddc-180">될 때마다 사용자 지정 checkError() 메서드 이면 사용된 toocheck에서 오류가 발생 했으며 tooexit 상관 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-180">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="0bddc-181">Hello 대체 `host`, `database`, `user`, 및 `password` 를 원하는 값으로는 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-181">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from hello table.
    rows, err := db.Query("SELECT id, name, quantity from inventory;")
    checkError(err)
    defer rows.Close()
    fmt.Println("Reading data:")
    for rows.Next() {
        err := rows.Scan(&id, &name, &quantity)
        checkError(err)
        fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
    }
    err = rows.Err()
    checkError(err)
    fmt.Println("Done.")
}
```

## <a name="update-data"></a><span data-ttu-id="0bddc-182">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="0bddc-182">Update data</span></span>
<span data-ttu-id="0bddc-183">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 업데이트는 **업데이트** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="0bddc-184">hello 코드는 세 가지 패키지를 가져옵니다: hello [sql 패키지](https://golang.org/pkg/database/sql/), hello [mysql에 대 한 이동 sql 드라이버](https://github.com/go-sql-driver/mysql#installation) hello MySQL에 대 한 Azure 데이터베이스와 hello 드라이버 toocommunicate로 [fmt 패키지](https://golang.org/pkg/fmt/)인쇄 된 입력 및 hello 명령줄에 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="0bddc-185">메서드를 호출 하는 hello 코드 [sql 합니다. Open ()](http://go-database-sql.org/accessing.html) tooconnect tooAzure MySQL 및 메서드를 사용 하 여 검사 hello 연결에 대 한 데이터베이스 [db입니다. Ping()](https://golang.org/pkg/database/sql/#DB.Ping)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-185">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="0bddc-186">A [데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB) hello 데이터베이스 서버에 대 한 hello 연결 풀을 보유, 전체에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="0bddc-187">hello 코드 호출 hello [exec ()](https://golang.org/pkg/database/sql/#DB.Exec) 메서드 toorun hello update 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello update command.</span></span> <span data-ttu-id="0bddc-188">될 때마다 사용자 지정 checkError() 메서드 이면 사용된 toocheck에서 오류가 발생 했으며 tooexit 상관 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-188">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="0bddc-189">Hello 대체 `host`, `database`, `user`, 및 `password` 를 원하는 값으로는 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-189">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a><span data-ttu-id="0bddc-190">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="0bddc-190">Delete data</span></span>
<span data-ttu-id="0bddc-191">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 데이터를 제거는 **삭제** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-191">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="0bddc-192">hello 코드는 세 가지 패키지를 가져옵니다: hello [sql 패키지](https://golang.org/pkg/database/sql/), hello [mysql에 대 한 이동 sql 드라이버](https://github.com/go-sql-driver/mysql#installation) hello MySQL에 대 한 Azure 데이터베이스와 hello 드라이버 toocommunicate로 [fmt 패키지](https://golang.org/pkg/fmt/)인쇄 된 입력 및 hello 명령줄에 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="0bddc-193">메서드를 호출 하는 hello 코드 [sql 합니다. Open ()](http://go-database-sql.org/accessing.html) tooconnect tooAzure MySQL 및 메서드를 사용 하 여 검사 hello 연결에 대 한 데이터베이스 [db입니다. Ping()](https://golang.org/pkg/database/sql/#DB.Ping)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-193">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="0bddc-194">A [데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB) hello 데이터베이스 서버에 대 한 hello 연결 풀을 보유, 전체에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="0bddc-195">hello 코드 호출 hello [exec ()](https://golang.org/pkg/database/sql/#DB.Exec) 메서드 toorun hello 명령을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello delete command.</span></span> <span data-ttu-id="0bddc-196">될 때마다 사용자 지정 checkError() 메서드 이면 사용된 toocheck에서 오류가 발생 했으며 tooexit 상관 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-196">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="0bddc-197">Hello 대체 `host`, `database`, `user`, 및 `password` 를 원하는 값으로는 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="0bddc-197">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a><span data-ttu-id="0bddc-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0bddc-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0bddc-199">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="0bddc-199">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
