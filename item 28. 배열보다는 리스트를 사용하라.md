아이템28_배열보다는 리스트를 사용하라
mkkim90 edited this page on 9 Dec 2019 · 3 revisions
이펙티브 자바_아이템28_배열보다는 리스트를 사용하라
코드28-4
```
public class Chooser { 
private final Object[] choiceArray;

public Chooser(Collection choices) {
	choiceArray = choices.toArray();
}

public Object choose() {
	Random rnd = ThreadLocalRandom.current();
	return choiceArray[rnd.nextInt(choiceArray.length];
}
}
```
이 클래서를 사용하려면 choose 메서드를 호출할 때마다 반환된 Object를 원하는 타입으로 형변환해야 한다. 혹시나 타입이 다른 원소가 들어있었다면 런타임에 형변환 오류가 날 것이다.

코드28-5 제너릭 시도
```
public class Chooser { 

private final T[] choiceArray;

public Chooser(Collection<T> choices) {
	choiceArray = (T[])choices.toArray();
}

// choose 메서드는 그대로다.
}
```
-> 상기 클래스는 T가 무슨 타입인지 알 수 없으니 컴파일러는 이 형변환이 런타임에도 안전한지 보장할 수 없다는 경고 메시지가 뜬다. 제너릭에서는 원소의 타입 정보가 소거되어 런타임에는 무슨 타입인지 알수 없다. 그러므로 안전을 보장할 수 없다.

코드 28-6 리스트 기반 Chooser - 타입 안전성 확보 
```
public class Chooser {

  private final List choiceList;

  public  Chooser(Collection<T> choices) {
    choiceList = new ArrayList<>(choices);
  }

  public T choose() {
    Random rnd = ThreadLocalRandom.current();
    return choiceList.get(rnd.nextInt(choiceList.size()));
  }
}
```
-> 컴파일오류와 경고를 제거하려면 리스트를 쓰면된다. 물론 조금 더 느릴 수도 있겠지만, 코드28-5보다 타입 안전성과 상호운용성은 좋아진다.
