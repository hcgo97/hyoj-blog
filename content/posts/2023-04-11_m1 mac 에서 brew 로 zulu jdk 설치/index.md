---
title: m1 mac 에서 brew 로 zulu jdk 설치
slug: "/m1-mac-에서-brew-로-zulu-jdk-설치"
date: 2023-04-11
tags:
  - Java
  - Command
---

## zulu jdk 버전 검색

```bash
# 버전별로 검색할 수 있도록 cask-versions 설치
brew tap homebrew/cask-versions

# 검색
brew search zulu
```

### 특정 버전 다운

```bash
brew install --cask zulu17
```

## 환경변수 설정

```bash
vim ~/.zshrc # or ~/.bashrc

export JAVA_HOME="/Library/Java/JavaVirtualMachines/zulu-17.jdk/Contents/Home"
export PATH=${PATH}:$JAVA_HOME/bin
```

### 확인

```bash
echo $JAVA_HOME
```
