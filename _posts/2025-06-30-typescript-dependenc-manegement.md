---
layout: post
title: TypeScript 의존성 관리
date: 2025-06-30
description: SeSAC 영등포캠퍼스 풀스택 과정 공부 기록
tags: sesac typescript
categories: study
giscus_comments: true
related_posts: false
toc:
  sidebar: left
---

타입스크립트 공부를 시작했는데 npm으로 패키지들을 설치한다.<br> 파이썬은 패키지 버전 충돌때문에 매번 고생하기때문에 가상환경을 만들어서 버전별로 라이브러리간 충돌되지 않게 관리했던게 생각이 났다.<br>
타입스크립트는 가상환경 세팅이 필요없는건지 궁금해졌다.
<br>
<br>
> claude 답변

### Node.js 프로젝트의 의존성 관리:
Node.js는 기본적으로 프로젝트 단위로 의존성을 관리<br> 각 프로젝트 폴더에 package.json 파일이 있고, npm install을 실행하면 해당 프로젝트의 node_modules 폴더에만 패키지가 설치됨 <br> 이는 Python의 가상환경과 비슷한 격리 효과를 제공함

### 추천하는 현대적인 접근법:

Node Version Manager 사용
- nvm (Mac/Linux) 또는 nvm-windows (Windows)
- 프로젝트별로 다른 Node.js 버전 사용 가능
- `nvm use 18.17.0` : 특정 버전 사용

#### 패키지 매니저 선택
- npm (기본)
- yarn (Facebook에서 개발)
- pnpm (요즘 인기, 디스크 공간 효율적)

### 버전 관리 모범 사례

```json
// package.json에서 정확한 버전 지정
{
  "dependencies": {
    "typescript": "^5.0.0",  // 5.x.x 호환 버전
    "express": "~4.18.2"     // 4.18.x 패치 버전만
  }
}
```

### lock 파일 활용
- `package-lock.json` (npm) 또는 `yarn.lock` (yarn)
- 정확한 버전을 기록해 팀원들과 동일한 환경 보장

### 실제 프로젝트 시작 방법:

```shell
mkdir my-typescript-project
cd my-typescript-project
npm init -y
npm install -D typescript @types/node
npx tsc --init
```


## 프로젝트별로 다른 node 버전을 사용해야할때
> node version manager (nvm) 사용!

### 프로젝트별 node 전환

```shell
# 프로젝트 A (Node 22)
cd project-a
nvm use 22.0.0
node --version  # v22.0.0

# 프로젝트 B (Node 24)  
cd project-b
nvm use 24.0.0
node --version  # v24.0.0
```

### 자동 버전 전환 설정

각 프로젝트 루트에 .nvmrc 파일을 만들어두면:

```shell
# project-a/.nvmrc
22.0.0

# project-b/.nvmrc  
24.0.0
```

그러면 프로젝트 폴더로 이동해서 nvm use만 실행하면 자동으로 해당 버전으로 전환!

```shell
cd project-a
nvm use  # .nvmrc 파일을 읽어서 22.0.0으로 전환
```


### shell script 활용 자동화
shell 설정에 추가하면 디렉터리 이동할 때마다 자동으로 Node 버전이 바뀜

```shell
# .zshrc 또는 .bashrc에 추가
autoload -U add-zsh-hook
load-nvmrc() {
  if [[ -f .nvmrc && -r .nvmrc ]]; then
    nvm use
  fi
}
add-zsh-hook chpwd load-nvmrc
```

### 실제 워크플로우:

```shell
# 새 프로젝트 A 시작 (Node 22 필요)
mkdir project-a && cd project-a
echo "22.0.0" > .nvmrc
nvm use
npm init -y

# 새 프로젝트 B 시작 (Node 24 필요)  
mkdir project-b && cd project-b
echo "24.0.0" > .nvmrc
nvm use
npm init -y
```

> pyenv + virtualenv 조합과 비슷한 방법!