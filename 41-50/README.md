# 쿠버네티스 스터디 (41-50)

## Namespaces

- 개인이 만드는 pod, deployment, service 등으로 이루어진 namespace: default name space
- 네트워크 솔루션, dns 등이 포함된 내부목적을 위한 pod와 service가 모여있는 namespace: kube-system
- 모든 사용자들이 사용할 resource들이 모여있는 namespace: kube-public

![Untitled](%E1%84%8F%E1%85%AE%E1%84%87%E1%85%A5%E1%84%82%E1%85%A6%E1%84%90%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20(41-50)%20b987d1908f1749f39e02711c2606f890/Untitled.png)

- dev와 prod의 공간을 분리할 때 등 사용
- 컴퓨팅 리소스 할당량을 분리할 수 있음

![Untitled](%E1%84%8F%E1%85%AE%E1%84%87%E1%85%A5%E1%84%82%E1%85%A6%E1%84%90%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20(41-50)%20b987d1908f1749f39e02711c2606f890/Untitled%201.png)

- 같은 namespace 내부에서는 resource를 호출하기 위해 단순히 resource 이름만 명시해주면 됨

![Untitled](%E1%84%8F%E1%85%AE%E1%84%87%E1%85%A5%E1%84%82%E1%85%A6%E1%84%90%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20(41-50)%20b987d1908f1749f39e02711c2606f890/Untitled%202.png)

- 하지만 다른 namespace의 resource를 호출하기 위해서는 명시적으로 fullname을 적어주어야함

![Untitled](%E1%84%8F%E1%85%AE%E1%84%87%E1%85%A5%E1%84%82%E1%85%A6%E1%84%90%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20(41-50)%20b987d1908f1749f39e02711c2606f890/Untitled%203.png)

- resource를 만들거나 조회할 때도 마찬가지로 뒤에 namespace 설정을 해주어야함
- 약간 aws credential profile 설정이랑 비슷하다고 생각해도 될듯?

![Untitled](%E1%84%8F%E1%85%AE%E1%84%87%E1%85%A5%E1%84%82%E1%85%A6%E1%84%90%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20(41-50)%20b987d1908f1749f39e02711c2606f890/Untitled%204.png)

- 위와 같은 yml 파일을 통해서 namespace를 생성 가능

![Untitled](%E1%84%8F%E1%85%AE%E1%84%87%E1%85%A5%E1%84%82%E1%85%A6%E1%84%90%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20(41-50)%20b987d1908f1749f39e02711c2606f890/Untitled%205.png)

- spec 섹션을 통해서 각 namespace에 할당할 resource 총량도 제한할 수 있음

```
kubectl config set-context $(kubectl config current-context) --namespace=dev

```

- 위 코드를 통해서 기본적으로 작업할 namespace를 switch할 수 있음

## Imperative vs Declarative

- imperative
    - 명령적 접근법
    - 언제 어떤 것을 할지를 명시하는 접근법
    - vm을 설치하고....nginx를 깔고....서버호스팅하고....를 하나씩 수동으로 하는 방식
- declarative
    - 선언적 접근법
    - 최종적으로 무엇을 해야하는지 만을 명시하는 접근법
    - 최종 목표를 위한 어떤 것을 해야하는 지는 시스템이 찾음

![Untitled](%E1%84%8F%E1%85%AE%E1%84%87%E1%85%A5%E1%84%82%E1%85%A6%E1%84%90%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20(41-50)%20b987d1908f1749f39e02711c2606f890/Untitled%206.png)

- yaml 파일에 원하는 액션을 적어두면 내부적으로 코드가 실행됨
- 자격증시험에서는 쓸모없음 (오히려 느림)
- config file을 git에 넣어두고 버전 관리를 할 수 있는 장점
- 쿠버네티스 판 테라폼

![Untitled](%E1%84%8F%E1%85%AE%E1%84%87%E1%85%A5%E1%84%82%E1%85%A6%E1%84%90%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20(41-50)%20b987d1908f1749f39e02711c2606f890/Untitled%207.png)

이거는 test하다가 실수했던 건데 label에는 - 를 넣을 수 없나봅니다

## Kuberctl Apply Command

- 기존적으로 local file과 live kubernetes object를 동시에 고려

![Untitled](%E1%84%8F%E1%85%AE%E1%84%87%E1%85%A5%E1%84%82%E1%85%A6%E1%84%90%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20(41-50)%20b987d1908f1749f39e02711c2606f890/Untitled%208.png)

- local file을 쿠버네티스에 적용시키려고 하면, 내부적으로 local file을 한 번 last applied configuration으로 만들어 저장한 후 live object configuration을 만듦
- live object configuration은 kubernetes cluster object에 관한 additional information을 저장하는 추가 field가 존재 (status field)
- local file에서 변경사항 존재 -> live object configuration과 비교 -> live object configuration update -> last applied confiugration update
- last applied config 같은게 왜 필요하냐
    - 로컬 파일에서 어떤 필드가 막 제거됐는지 알아내기 위함
- 그럼 last applied config는 어디에 저장돼나
    - 사실 live object config 에 metadata.annotations 필드에 last-applied-configuratrion이라는 필드로 저장됨
    - command apply 시에만 사용
    - **imperative command로 변경된 구성은 저장되지 않음**
    - 따라서 imperative와 declarative command를 섞어서 쓰면 위험
    -