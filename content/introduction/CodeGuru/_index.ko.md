---
title: "CodeGuru"
weight: 13
pre: "<b>1-3 </b>"
tag:
  - CodeGuru
  - CodeReview
---

## AWS CodeGuru

AWS의 CodeGuru는 기계학습을 이용한 코드리뷰 및 어플리케이션 성능권장 사항을 제공하는 서비스 입니다. 이 서비스를 사용하여 어플리케이션의 숨겨진 문제와 문제를 일으킬 여지가 있는 코드를 찾을 수 있습니다. 구체적인 권장사항도 제공하기 때문에 코드를 수정하거나 개선할 수 있습니다. CodeGuru는 수백만 건의 코드리뷰와 오픈소스 프로젝트, Amazon 내부에서 프로파일링된 수천개의 어플리케이션을 기반으로 구축되었습니다. CodeGuru는 **JAVA Code**를 지원하고 있습니다. 
Repository는 **GitHub**또는 **CodeCommit**을 사용할 수 있습니다. 또한 손쉽게 통합이 가능합니다. 


![codeguru](/images/codequeility.png)

CodeGuru의 서비스는 크개 두가지로 구성되어 있습니다. 그래서 각각의 코드 라이프사이클에 관여할 수 있습니다. 


### 1. CodeReview 기능을 제공하는 CodeGuru Reviewer
  CodeGuru Reviewer는 GitHub 또는 CodeCommit에서 Pull-Request 발생시 자동을 코드를 분석하여 적절한 멘트를 달아줍니다. 
  CodeGuru Reviewer는 코드 결함을 찾아 표기하고 권장사항을 제안합니다. 

  ![codegurureviewer](/images/git-pr-codereviewer.png) 

  CodeGuru Reviewer가 탐지하는 내용은 크게 아래와 같은 카테고리로 나눌 수 있습니다. 

  1. AWS Best Practices : AWS APIs를 올바르게 사용
  1. Concurrency : 동시성을 고려하지 않아 생기는 잘못된 결과 발견 (Thread-safe)
  1. Resource Leaks : 잘못된 리소스 핸들링의 사용
  1. Sensitive Information Leak : 민감한 개인정보 유출 문제.


### 2. Profiling기능을 제공하는 CodeGuru Profiler

  CodeGuru Profiler는 라이브 애플리케이션에서 런타임 성능 데이터를 수집하고 애플리케이션 성능을 미세 조정할 수있는 권장 사항을 제공합니다. 
  CodeGuru Profiler는 기계 학습 알고리즘을 사용하여 가장 비싼 코드를 찾고 효율성을 개선하고 CPU 병목 현상을 제거 할 수있는 방법을 제안 할 수 있습니다.

- [ 이제 실습을 위한 준비를 해봅시다.](/ko/setup/)
