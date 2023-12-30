# 사용법
## gcd.yaml
```
gitSecret:
  username: "jalju0804"
  password: ""
  email: "dlckswn334@naver.com"
docker:
  configJson: ""
  ImageReference: "dlckswn334/gcd-server"
application:
  name: "example"
  gitRepoUrl: "https://github.com/woozco/Woozco_BE.git"
  destinationNamespace: default
manifestGitRepo: 
  baseURL: "https://github.com/jalju0804/gcd-manifest.git"
  branch: "main"
  FilePath: "backend/deploy.yaml"
```


Github에 로그인하고, Settings/Developer settings/Personal access tokens/Tokens(classic)에서, Personal access tokens (classic)를 만들어주면 됨.


**주의: 해당 토큰의 이름과 Github username를 똑같이 설정해주삼**


해당 Git Token 값이  gcd.yaml의 gitSecret.password인거임

docker login을 로컬에서 진행 ㄱ
로그인을 하는 순간, 해당 계정의 권한 토큰 정보를 가지고 있는 config.json이 생성됨


```
docker login
cat ~/.docker/config.json | base64
```


출력되는 값이 gcd.yaml의 docker.configJson 필드에 들어갈 값임

## 명령어

```
gcd add
```
OR
```
ansible-playbook ./playbooks/tekton-resource.yml 
```
해당 명령어를 치면, playbooks 안의 gcd.yaml를 기반으로 repository.yaml이 만들어짐

```
gcd tekton
```


OR


```
ansible-playbook ./playbooks/tekton.yml
ansible-playbook ./playbooks/tekton-resource.yml  
```

위에 명령어에 task, pipeline, secret 등 tekton 돌아갈 때 필요한 crd를 전부 선언하는 
```
ansible-playbook ./playbooks/tekton.yml
```
가 추가된거임

아직 커스텀한 tekton-polling-operator 배포를 안해서 일단 주석처리해놈 이건 알아서 주석풀고 실행하던가 하셈