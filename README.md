# Домашнее задание "Синхронизация горутин"

### Нужно выполнить и отправить на проверку задания  

## Задание
Инструкция по выполнению.  
Создайте переменную counter (тип int) — общий счётчик для всех горутин.  
Объявите sync.Mutex и sync.WaitGroup.  
Запустите N горутин (например, 10) в цикле. Каждая горутина должна увеличить counter на 1000.  
Обеспечьте потокобезопасный доступ к counter с помощью Mutex.  
Используйте WaitGroup, чтобы main() дождалась завершения всех горутин.  
Выведите итоговое значение счётчика. Оно должно быть равно N * 1000.

## Код

```go
package main

import (
	"fmt"
	"sync"
)

func main() {
	var counter int
	var mu sync.Mutex
	var wg sync.WaitGroup

	const goroutines = 10
	const increments = 1000

	wg.Add(goroutines)

	for i := 0; i < goroutines; i++ {
		go func() {
			defer wg.Done()

			for j := 0; j < increments; j++ {
				mu.Lock()
				counter++
				mu.Unlock()
			}
		}()
	}

	wg.Wait()

	fmt.Println("Final counter value:", counter)
}
```

### Ссылка на песочницу  [Синхронизация горутин](https://go.dev/play/p/0fsq-I277UY) 


### Выполнение кода и основые тесты.

![image](https://github.com/Byzgaev-I/-Goroutine_synchronization-/blob/main/Парал-1.png) 


### Все работает: 

- Результат 10000 — правильно.  
- Программа завершилась без ошибок.    
- Код компилируется и работает.    




























