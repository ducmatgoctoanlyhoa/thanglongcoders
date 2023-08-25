# Bài toán: Số mũ

### Link đề: https://open.kattis.com/problems/associativeexponents

## Đề bài: 

>Cho 3 số tự nhiên $a, b, c$ thỏa mãn $1 \leq a, b, c \leq 2*10^6$, hỏi $(a^b)^c$ và $a^{b^c}$ có bằng nhau không?

## Giải

### Cách 1: Giải trực tiếp


Để giải trực tiếp bài toán này thì không hề khó, chỉ cần tính trực tiếp hai giá trị như đề bài rồi so sánh chúng là xong. Như đã nói ở bài trước, ta có thể dùng [Lũy thừa nhanh](https://hackmd.io/@DeMen100ms/DeMenBlog3) để giảm thời gian tính các phép mũ.

```python
def pow(a: int, b: int) -> int:
	t = 1
	while (b > 0):
		if (b % 2 == 1):
			t *= a
		a = a * a
		b //= 2

print(pow(a, pow(b, c)) == pow(pow(a, b), c))
```
```cpp
long long pow(long long a, long long b){
	long long t = 1;
	while (b > 0){
		if (b % 2 == 1) t *= a;
		a = a * a;
		b /= 2;
	}
}

cout << (pow(a, pow(b, c)) == pow(pow(a, b)), c);
```
ĐPT: $O(log \ b^c + log \ b + log \ c)$ vì cần dùng công thức mũ nhanh để tính $a^{b^c}$, $a^b$ và $(a^b)^c$

Ngoài ra, vì $(a^b)^c = a^{bc}$ nên ta chỉ cần xét tính đúng sai của $b^c = bc$.

```python 
def pow(a: int, b: int) -> int:
	t = 1
	while (b > 0):
		if (b % 2 == 1):
			t *= a
		a = a * a
		b //= 2

print(pow(b, c) == b*c)
```
```cpp
long long pow(long long a, long long b){
	long long t = 1;
	while (b > 0){
		if (b % 2 == 1) t *= a;
		a = a * a;
		b /= 2;
	}
}

cout << (pow(b, c) == b*c);
```
ĐPT: $O(log \ c)$

Thế nhưng cách này cần xử lý những số rất lớn với các $a, b, c$ lớn hơn. Vì vậy, nó không thuận tiện. Chú ý rằng vì $a, b, c$ là các số tự nhiên và $1 \leq a, b, c \leq 2*10^{6}$ nên ta có thể sử dụng 1 phương pháp khác.

### Cách 2: Xét trường hợp.

Đầu tiên, ta để ý thấy với mọi số thực $x, y$ thì $1^x = 1^y = 1$ nên nếu $a = 1$ thì không cần xét tính đúng sai của $b^c = bc$.

```python
if (a == 1): 
	#điều kiện đúng
```
```cpp
if (a == 1){
	//điều kiện đúng
}
```

Với các trường hợp $a \neq 1$, vấn đề phức tạp hơn. Chúng ta quay lại ý tưởng trước, xét $b^c = bc$. Nhưng làm thế nào để kiểm chứng tính đúng đắn của phép tính này? Ta có thể giải phương trình đa thức $b^c - bc$ theo $b$ lấy $c$ làm tham số, nhưng cách này sẽ rất phức tạp (còn về làm thế nào để giải một đa thức mình sẽ viết sau). Thay vào đó, chúng ta sẽ suy luận theo một hướng khác. Đặt $c = b^k$, ta có

$$b^c = bc$$ 
$$b^{b^k} = b*{b^k}$$ 
$$log_{b}(b^{b^k}) = log_{b}{(b*b^k)}$$ 
$$b^k = 1 + k$$ 
$$b = \sqrt[k]{1 + k}$$

và $b$ là một số tự nhiên, nên chỉ có $k = 1$ thỏa mãn. Khi đó $b = \sqrt[1]{1 + 1} = 2$ và $c = b^k = 2$. Do đó, ta chỉ cần xét tính đúng đắn của $b = 2$ và $c = 2$

```python
if (b == c == 2):
	#điều kiện đúng
```
```cpp
if (b == 2 && c == 2){
	//đièu kiện đúng
}
```
ĐPT: $O(1)$

Tác giả: Hoàng Minh Đức / ducmatgoctoanlyhoa




