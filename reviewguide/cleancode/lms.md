# LMS - 수강신청

---

## 리뷰어 가이드
## 1단계
1단계 미션이 레거시 코드 리팩토링하는 미션으로 서비스 레이어의 코드를 도메인 객체로 리팩토링하는 미션이다.
지금까지 학습한 내용을 실무에 적용해보는 상당히 중요한 미션인 만큼 도메인 객체로 로직 분리를 잘 하도록 리뷰한다.
가능하면 리뷰어가 판단하기에 만족하는 수준이 될 때까지 피드백을 남긴다.
QnaService의 결과 코드는 다음과 같은 구조가 되도록 피드백 하면 좋겠다.

```
@Transactional
public void deleteQuestion(User loginUser, long questionId) throws CannotDeleteException {
    Question question = findQuestionById(questionId);
    List<DeleteHistory> deleteHistories = question.delete(loginUser);
    deleteHistoryService.saveAll(deleteHistories);
}
```

## 2단계
2단계 요구사항에 대한 비지니스 로직을 도메인 모델 객체에 구현하는 경험이다.
기존에 비지니스 레이어(Service 또는 Manager라 불리는 클래스)에 로직을 구현하는 것이 일반적이다.
1단계 경험과 같이 비지니스 로직을 도메인 객체에 잘 구현하는지에 대해 집중해서 피드백한다.
2단계는 데이터베이스에 대한 CRUD는 없다.

## 3단계
3단계는 2단계에서 구현한 도메인 객체를 데이터베이스와 매핑하고, CRUD를 진행하는 단계이다.
3단계에서 집중적으로 피드백할 부분은 2단계에서 구현한 도메인 객체를 최대한 깨트리지 않으면서 데이터베이스와 매핑하는 부분을 집중 피드백한다.

## 4단계
현장에서 자주 발생하는 테이블 칼럼에 변경사항이 발생했을 때의 레거시 코드 리팩터링 경험을 하는 단계이다.
요구사항이 변경되면서 데이터베이스 테이블의 칼럼에 변화가 있는 경우이다.
코드 리팩터링과 같이 테이블에 변경이 발생하더라도 점진적인 리팩터링을 하는 것이 이 단계의 핵심 목표이다.
점진적이고, 안정적으로 레거시 코드를 리팩터링하려면 항상 AS-IS와 TO-BE 데이터가 공존하는 순간이 필요하다.

리뷰이와 소통할 때 점진적인 리팩터링을 어떻게 진행했는지에 대해 이야기 나눠보면 서로의 성장에 도움이 될 것이다.
