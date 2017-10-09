API 앱에 대 한 hello Azure CLI tooget hello 원격 배포 URL을 사용 합니다. Hello에서 다음 명령을, 대체  *\<app_name >* 웹 앱의 이름으로 합니다.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

사용자 로컬 Git 배포 toobe 수 toopush toohello 원격를 구성 합니다.

```bash
git remote add azure <URI from previous step>
```

Azure 원격 toodeploy toohello 응용 프로그램을 푸시하십시오. Hello 배포 사용자를 만들 때 앞에서 만든 hello 암호를 묻는 메시지가 나타납니다. Hello 퀵 스타트 앞부분에서에서 만든 hello 암호 및 toolog toohello Azure 포털에서에서 사용 하 여 hello 암호가 하지 않은 경우을 입력 했는지 확인 합니다.

```bash
git push azure master
```
