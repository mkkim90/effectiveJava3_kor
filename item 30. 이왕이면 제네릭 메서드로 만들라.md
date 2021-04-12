클라이언트에서 입력 매개변수와 반환값을 명시적으로 형변환해야 하는 메서드보다 제네릭 메서드가 더 안전하며 사용하기도 쉽다. 타입과 마찬가지로
메서드도 형변환 없이 사용할 수 있는 편이 좋으며 많은 경우 그렇게 하려면 제네릭 메서드가 되어야한다.

역시 타입과 마찬가지로, 형변환을 해줘야 하는 기존 메서드는 제네릭하게 만들자.
기존클라이언트는 그대로 둔 채 새로운 사용자의 삶을 훨씬 편하게 만들어줄 것이다. 


코드 30-1
```
public static Set union(Set s1, Set s2) {
	Set result = new HashSet(s1);
	result.addAll(s2);
	return result;
} 
```
-> 경고 발생 -> 이 메서드 선언에서의 세집합의 원소타입을 타입 매개변수로 명시하고 메서드 안에서도 이 타입 매개변수만 사용하게 수정하면됨

코드 30-2 
```
public static <E> Set<E> union(Set<E> s1, Set<E> s2) {
	Set<E> result = new HashSet<>(s1);
	result.addAll(s2);
  return result;
}
```
코드 30-7
```
public static<E extends Comparable<E>> E max(Collection<E> c) {
	if(c.isEmpty)
		throw new IllegalArgumentException("컬렉션이 비어 있습니다");
		
	E result = null;
	for (E e : c)
		if (result == null || e.compareTo(result) > 0)
			result = Object.requireNonNull(e);
			
	return result;
}
```
