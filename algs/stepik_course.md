###Числа фибоначи

1. Нативная реализация с помощью рекурсии, имеет сложность O(e^n)
2. Использовать HashMap в кач-ве кеша
3. Вычисление от меньшего к большему с использованием кеша для предыдущих значений


int fibonaci(int n ) {
	int a = 0;
	int b = 1;
	int c;
	fori (i = 0; i < n; i++) {
		c = a + b;
		a = b;
		b = c;
	}
	return c;
}

###Наибольший общий делитель

алгоритм Евклида:

если a > b = > return gcd(a%b, b)
иначе return gcd(a, b%a)
