# Полиз
1) Оператор присваивания ( `:=` )
	- `I E :=` | `I = E`

`E` $\rightarrow$ `E1` `( ( + | - ) E1)*`
`E1` $\rightarrow$ `E2` `( ( * | / ) E2)*`
`E2` $\rightarrow$
- `(` `E` `)`
- `var`
```cpp
E2() {
	if (lex == '(') {
		E();
	} else if (lex.type == 'var') {
		queue.push(var);
	}
}

E1() {
	E2()
	while (lex == '*' || lex == '/') {
		E2();
		queue.push(znak);
	}
}
```

2) Оператор перехода (`P!)
3) Условный оператор
	- `if` `(` `!` `B` `)` `goto` `L`

| B   | L   | !F  |
| --- | --- | --- |
- **B** - условие
- **L** - инструкция
- **!F** - goto


`if` `(!B)` `goto` $L$
--------------------------
`if` `e` `then` $S_1$ `else` $S_2$
`if` `(!e)` `goto` $L_2$ `;` $S_1$ `;` `goto` $L_3$ `;` $L_2$ `;` $S_2$ `;` $L_3$


| e   | $\cdot$ | !F  | $S_1$ | $\cdot$ |
| --- | ------- | --- | ----- | ------- |

Тип проверяем на этапе семантического анализа

`if` `(a > b)` `c` `=` `a` `;` `else` `c` `=` `b`

| a    | b    | >    | 10   | !F   | c    | a    | :=   | 13   | p!      | c       | b       | =:      |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ------- | ------- | ------- | ------- |
| $_1$ | $_2$ | $_3$ | $_4$ | $_5$ | $_6$ | $_7$ | $_8$ | $_9$ | $_{10}$ | $_{11}$ | $_{12}$ | $_{13}$ |


`E` $\rightarrow$ `E1` `( ( + | - ) E1)*`
`E1` $\rightarrow$ `E2` `( ( * | / ) E2)*`
`E2` $\rightarrow$
- `(` `E` `)`
- `num`

```cpp
bool E() {
	if (E1) {
		while (true) {
			if (tokens[position] == '+' || tokens[position] == '+') {
				++position;
				
				if (!E1) {
					return false;
				}
			} else {
				return false;
			}
		}
	}
}
```

```cpp
void E() {
	E1();
	
	while (currToken.type == TokenType::PLUS || currToken.type == TokenType::MINUS) {
		if (currToken.type == TokenType::PLUS) {
			getLex();
			E1();
			result.push_back(convertForResult(TokenType::PLUS));
		} else {
			getLex();
			E1();
			result.push_back(convertForResult(TokenType::MINUS));
		}
	}
}

void E1() {...}

void E2() {
	if (currToken.type == /*TokenType::...*/ '(') {
		getLex();
		E();
		
		if (currToken.type == /*TokenType::...*/ ')') {
			throw std::runtime_error("Error");
		}
		getLex();
	} else if (currToken.type == TokenType::NUMBER) {
		result.push_back(convertForResult(TokenType::NUMBER));
		getLex();
	} else {
		throw std::runtime_error("Error");
	}
}
```

