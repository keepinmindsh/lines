---
title: "트랜잭션"
excerpt: "트랜잭션의 기본과 이해, Spring 를 이용한 Transaction 처리"

categories:
  - Programming
tags:
  - Programming
classes: wide
last_modified_at: 2019-05-16T16:00:00-05:00
---

> "지금" 무엇을 하고 있는지 스스로 생각해야 한다는 것. 

***

# 트랜잭션의 특성

- 원자성
- 일관성
- 고립성
- 지속성

# 트랜잭션의 종류 

- 로컬 트랜잭션
- 분산 트랜잭션 

여러 사용자가 데이터 베이스에 접근할 때 여러 트랜잭션이 수행되는데 이 여러 트랜잭션들을 병행 수행 시키는 방식이다. 이는 마치 운영 체제가 멀티 프로세스를 지원하는 것과 비슷한 모양이다. 여러 트랜잭션을 수행하는 순서가 중요하므로 트랜잭션 스케쥴이라고 부르는 스케줄 순서에 따라서 트랜잭션을 실행한다.  

- 직렬스케쥴  
인터리빙 방식을 사용하지 않고 각 트랜잭션을 순차적으로 수행시키는 방식   
인터리빙 : 트랜잭션 연산 단위로 번걸아가며 수행하는 방식. 운영 체제의 시분할 방식과 비슷하다.  

- 비직렬 스케쥴  
인터리빙을 사용해 트랜잭션을 병행 수행시키는 방식. 병행 수행이 비직렬 스케줄에 포함된다.  

- 직렬 가능 스케쥴  
직렬 스케쥴 처럼 정확한 결과를 생성하는 비직렬 스케쥴

- 갱신분실  
하나의 트랜잭션이 수행한 데이터 변경 연산이 저장되기 전에 다른 트랜잭션이 데이터를 가지고 가서 데이터를 변경하고 다시 저장하는 경우 첫번째 트랜잭션이 수행한 연산은 무효가 된다.

- 모순성  
트랜잭션이 여러개의 데이터를 변경하는 연산을 할 때 동일하지 않은 시간에 각각의 데이터를 가지고 오면 연산의 일관성이 사라져 모순이 생긴다. 갱신 분실과 비슷해 보이지만 여러 데이터를 가져올 때 발생하는 문제라는 점에서 다르다.

- 연쇄복귀  
트랜잭션에 장애가 발생해서 rollback 연산을 하려면 해당 트랜잭션이 사용했던 데이터를 사용한 다른 트랜잭션들도 rollback을 수행해야 하는데 이미 그 트랜잭션이 완료되었더라도 rollback이 수행된다.

- 미완료 의존성  
한 트랜잭션이 수행 중 장애가 생겨 rollback 연산을 하기 전에 해당 트랜잭션이 갱신한 데이터를 다른 트랜잭션에서 이미 가져갔다면 데이터베이스에 있는 데이터와 트랜잭션이 가지고 있는 데이터가 다르게 되는 문제가 발생한다.

# 병행 제어 

여러 트랜잭션이 병행 수행되며 서로 다른 데이터에 접근하지 않고, 같은 데이터에 접근한다면 데이터에 무네작 생길 수 있다. 이를 방지하기 위해 같은 데이터에 접근하더라도 문제가 생기지 않도록 제어하는 것을 말한다. 운영체제가 멀티 프로세스 또는 멀티 스레드로 프로그램을 실행할 때 임계구역을 설정하는 것과 비슷하다.