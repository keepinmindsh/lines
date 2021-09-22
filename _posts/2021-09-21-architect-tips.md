---
title: "Architect Tips"
excerpt: "IT Architect가 하지 말아야할 128가지 "

categories:
  - Basic
tags:
  - Basic
classes: wide
last_modified_at: 2021-09-20T17:31:00-21:55:00
---

> 모든 것은 양면성을 가진다. 긍정적인 면이 있는 반면에 부정적인 면도 있다. 여기에서 중요한 것은 부정적인 면이 본인에게 미치는 영향에 따라 주관적인 기준으로 좋고 나쁨이 가려지는 것은 아닐까?  

***

# 패키지를 도입할 때 부가 기능 개발을 선행해서는 안된다. ! 

# 고객사나 협력사의 실 데이터 파일을 주고 받지 말것 !! 

# WBS의 작업 항목에는 1명의 담당자 혹은 1개의 업체를 선정해야한다. 다수인원/업체에 대한 중복 선정은 역할에 대한 애매모호함과 다양한 이슈 발생이 가능하므로 하지 말아야 한다. 

# 상황과 프로젝트 성향에 맞는 프로세스와 패턴을 적용해야지, 특정 프로세스와 패턴을 고집해서는 안된다. 

# 소프트웨어 개발 모델 

### 개발 생명 주기 

 - 주먹구구식 개발 모델 ( Build And Fix Model )
 - 폭포수 모델 ( WaterFall Model )
 - 원형 모델 ( Prototyping Model )
 - 나선형 모델 ( Spiral Model )
 - RAD 모델 ( Rapid Application Development )
 - 반복적 개발 모델 ( Iterative Development Model )
 - V 모델 ( V 모델 )
 - 컴포넌트 기반 모델 ( Component Based Development )

### 개발 방법론 

- UP ( Unified Process )
  - 도입
    비즈니스 케이스를 구축하며 시스템이 당면 문제를 알아낸다. 
  - 상세 
    프로젝트를 계획하고, 시스템의 기능과 구조를 정의한다. 
  - 구축 
    아키텍처에서 발생한 가정은 필요에 따라 테스트 되고, 리팩토링 된다. 
  - 이행 
    테스트 후 사용자에게 인도된다. 


  - 많은 현장에서 사용하고 있는 UP의 작업 범위 
    - 유스 케이스 구동 
      유스케이스를 기본으로 개발을 진행한다. 
    - 반복 개발
      요구 -> 분석 -> 설계 -> 구축 -> 테스트의 사이클을 계속한다. 
    - UML 모델링 
      UML로 모델링 한다. 


- XP ( eXtreme Process )

# RFP ( Reqeust For Proposal ) 란 

발주자가 특정 과제의 수행에 필요한 요구사항을 체계적으로 정리하여 제시함으로써 제안자가 제안서를 작성하는데 도움을 주기 위한 문서이다. 제안요청서에는 해당 과제의 제목, 목적 및 목표, 내용, 기대성과, 수행기간, 금액(Budget), 참가자격, 제출서류 목록, 요구사항, 제안서 목차, 평가 기준 등의 내용이 포함된다.  

제안요청서는 시스템 설계에 사용자의 요구사항을 반영해 나중에 사용자의 제안이 잘 실행되고 있는지 판단하기 쉽게 만든다. 제안요청서를 만들면 현재 판매 회사의 상황을 잘 이해하고 있어야 한다.  

# Grand Design Phase 

- 현행 경영 과제의 추출 
- 새로운 경영 니즈의 추출
- 경영 과제, 경영 니지의 해결책 책정
- 해결책을 실현하기 위한 방법으로 적용 시스템(ERP, 개별 패키지, 내부 개발)을 비교 평가 
- 신 시스템의 요건 정리 
- RFP 작성
- 제안 비교, 선정 

# PT, CRP, UAT 

- PT

 모형을 만들어 최적화 모형을 개발/테스트 하는 것으로, 여기서 사용하는 모형은 프로젝트 대상인 ERP 시스템이다. ERP 시스템의 도입의 목적에 부합하는 최적의 기능과 프로세스를 도출하는 방법이라고 볼 수 있다. 

- CRP

실제 상황과 유사한 소규모의 시스템을 구축하여 테스트 하는 것이며, 프로세스 보다는 기능, 비 기능 중심의 테스트이며, 소프트웨어를 구입하기 위한 테스트와 시스템을 적용하는 도중에 테스트 하느느 것의 2가지 측면에서 사용된다. 

- UAT 

사용자가 완성된 시스템을 인수하기 위한 테스트로 실제 상황과 동일한 환경으로 테스트 한다. 프로세스, 기능, 비 기능 시험을 한다. 검토회으를 거쳐 사용자의 승인을 필요로 한다. 

# 고객이 말하는 패키지의 갭 판단을 그대로 받아들여서는 안된다.

 - 가장 귀찮은 것은 의사 결정의 근거나 전제 조건을 애매하게 진행하여 , 실제로 운용하기 어렵게 된 경우이다. 

 - 이유를 끝까지 따져 대책을 구상하여 표준 기능으로 해결책 제시 
   - 원하는 기능이 빠져있다. 
    그 기능이 왜 필요한지, 앞으로도 계속 필요한 기능인지에 대해서 정확히 알아야 한다. 
   - 수작업으로는 대응할 수 없다. 
    작업량이라는 수치로 표형하는 것이 가장 좋다. 대상 데이터의 발생 빈도를 조사한다. 
   - 사용자가 잘 다룰 수 없다. 
   - 수작업으로는 통제하기가 어렵다. 

위의 내용들에 대해서 정확한 고객의 니즈를 확인하는게 중요함. 단지 어렵다. 등의 고객 의견은 요구사항 정의에 도움이 되지 않는다. 그들의 요구사항을 수치화하고, 명확하게 "대응할 수 없다", "어렵다"에 대한 이유를 파악해야 한다. 


# 출처

> <https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=okkk00&logNo=110044849255>
> IT 아키텍트가 하지 말아야할 128가지 

 