## <a name="push-tooazure-from-git"></a>Git에서 tooAzure 푸시

Azure 원격 tooyour 로컬 Git 리포지토리를 추가 합니다.

```bash
git remote add azure <URI from previous step>
```

Azure 원격 toodeploy toohello 응용 프로그램을 푸시하십시오. Hello 배포 사용자를 만들 때 앞에서 만든 hello 암호를 묻는 메시지가 나타납니다. 만든 hello 암호를 입력 했는지 확인 [배포 사용자 계정 구성](#configure-a-deployment-user), toolog toohello Azure 포털에서에서 사용 하 여 hello 암호가 아닙니다.

```bash
git push azure master
```

hello 위의 명령은 표시 정보 비슷한 toohello 다음 예제:
