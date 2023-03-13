## VCS
> Version Control System
- 동일한 정보에 대한 여러 버전을 관리하는 것
- 소프트웨어 개발에서 팀 단위로 개발 중인 소스 코드나, 문서를 관리하는데 사용
- v1.0.0.zip, v1.0.1.zip과 같은 압축파일 형태로 공유하지 않기 위함


## Git
Linux 프로젝트 중 버전관리 소프트웨어의 내부 개발이 필요하다 판단되어 만들어졌습니다.
초기 개발자는 Linux의 개발자인 리누스 토발즈입니다. Git은 다음과 같은 목표로 개발되었습니다.
- 빠른 속도
- 단순한 구조
- 비선형적인 개발(수천 개의 동시 다발적인 브랜치)
- 완벽한 분산(DVCS)
- Linux 커널 같은 대형 프로젝트에도 유용할 것(속도나 데이터 크기 면에서)

비선형적인 개발을 위해 브랜치 시스템을 도입했고, 원격저장소와 로컬을 분리함으로써 여러 개발자가 분산작업을 원활하게 할 수 있게 고안되었습니다.

또한, 모든 커밋에 대해 Checksum(Hash)을 만들어 데이터 무결성을 보장합니다.(SHA-1)


### Inside of Git
1. Git은 기본적으로 파일 시스템의 스냅샷을 저장합니다.(커밋 당시의 Git 디렉토리의 모든 파일 정보를 저장)
2. 또한 파일 및 스냅샷을 해시하여 빠르게 바뀐 버전인지, 아닌지를 체크합니다.
3. 이후 스냅샷들의 크기가 커지면 주기적으로 git gc(garbage collection)를 통해 delta를 만듭니다.


### Git 명령어
#### 기초적인 명령어 사용
- git init : Git 디렉토리를 시작합시다.
- git add * : Git으로 관리할 파일을 골라봅시다.
- git commit -m "메세지" : 메세지와 함께 디렉토리의 상태를 저장합시다.
- git push : 원격 저장소에 커밋 내용을 보내봅시다.


#### 조금 더 잘 알고 있다면
- git checkout : 브랜치의 상태로 디렉토리를 변경합니다.
- git brach {name} : 새로운 브랜치를 만듭니다.
- git reset --hard HEAD : 마지막 커밋으로 모든 것을 되돌립니다.
- git merge {branch-name} : 현재 체크아웃된 브랜치를 기준으로 name을 머지합니다.


#### File Status Lifecycle
![lifecycle.png](img/lifecycle.png)
- git status : 파일들의 상태를 확인할 수 있습니다.
- git status -s : 간단하게 보기 옵션 사용
- git add {filename} : untracked 파일을 staged로 만들거나, modified 파일을 staged로 만들 수 있습니다.
- git add * : 많이 쓰이지만, 충분히 안전할 때 사용합니다.
- git diff : staged 상태와 unstaged(modified) 상태의 차이를 보여줍니다.
- git diff --staged(또는 git diff --cached) : staged와 commited 상태를 비교합니다.
- git diff --name-only HEAD~1 : 리비전끼리 HEAD로 변경된 파일만 확인할 수 있습니다.
- git commit -m "커밋메세지" : staged 상태의 파일을 기록합니다.
- git commit -a : modified(delete 포함)를 staged로 만든 후 커밋할 수도 있습니다.
- git rm {파일} : 실제 디렉토리에서 파일을 삭제하고, unstaged가 됩니다.
- git rm --cached : 실제 디렉토리에서 삭제하지 않고 git 내에서만 삭제할 수도 있습니다.


#### gitignore

Git이 몇몇 파일(자동 생성 파일 등)을 무시하게끔 하고 싶으면 .gitignore을 수동으로 만듭니다.

.gitignore는 쉘 등에서 사용하는 glob 패턴을 따릅니다.

git clean -df 등의 명령어도 ignore 안의 파일은 무시하게 됩니다.

- <strong>*.a</strong> : 확장자가 .a인 파일 무시
- <strong>!lib.a</strong> : 위에서 확장자가 .a인 파일은 무시하게 했지만 lib.a는 무시하지 않음
- <strong>/TODO</strong> : 현재 디렉토리에 있는 TODO 파일은 무시하고 subdir/TODO처럼 하위 디렉토리에 있는 파일은 무시하지 않음
- <strong>build/</strong> : build/ 디렉토리에 있는 모든 파일은 무시
- <strong>doc/*.txt</strong> : doc/notes.txt 파일은 무시하고 doc/server/arch.txt 파일은 무시하지 않음
- <strong>doc/**/*.pdf</strong> : doc 디렉토리 아래의 모든 .pdf 파일을 무시


#### log
git에서 커밋 히스토리를 조회하기 위해 사용하는 방법입니다.
- <strong>git log</strong> : 기본적인 조회
- <strong>git log --online</strong> : 깔금하게 보기
- <strong>git log -p</strong> : 각 커밋의 diff와 함께 보기
- <strong>git log --stat</strong> : 각 커밋의 통계 정보와 보기 (변경된 파일 수, insertion/deletion line 수)
- <strong>git log --graph</strong> : 브랜치와 머지 히스토리까지 그래프 모양으로 보여줍니다.
- <strong>git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"</strong>을 터미널에 입력하고 <strong>git lg</strong> 명령어로 git log --graph했을 때보다 직관적이고 하이라이팅된 형태로 확인

<strong>Author</strong> : 실제로 커밋을 한 사람
<strong>Commiter</strong> : 커밋을 Git repo에 저장한 사람(pull request merge의 경우 GitHub라고 보입니다.)
