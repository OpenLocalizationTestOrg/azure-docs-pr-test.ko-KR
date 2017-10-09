## <a name="push-tooazure-from-git"></a><span data-ttu-id="a3677-101">Git에서 tooAzure 푸시</span><span class="sxs-lookup"><span data-stu-id="a3677-101">Push tooAzure from Git</span></span>

<span data-ttu-id="a3677-102">Azure 원격 tooyour 로컬 Git 리포지토리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3677-102">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="a3677-103">Azure 원격 toodeploy toohello 응용 프로그램을 푸시하십시오.</span><span class="sxs-lookup"><span data-stu-id="a3677-103">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="a3677-104">Hello 배포 사용자를 만들 때 앞에서 만든 hello 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a3677-104">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="a3677-105">만든 hello 암호를 입력 했는지 확인 [배포 사용자 계정 구성](#configure-a-deployment-user), toolog toohello Azure 포털에서에서 사용 하 여 hello 암호가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a3677-105">Make sure that you enter hello password you created in [Configure a deployment user](#configure-a-deployment-user), not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```

<span data-ttu-id="a3677-106">hello 위의 명령은 표시 정보 비슷한 toohello 다음 예제:</span><span class="sxs-lookup"><span data-stu-id="a3677-106">hello preceding command displays information similar toohello following example:</span></span>
