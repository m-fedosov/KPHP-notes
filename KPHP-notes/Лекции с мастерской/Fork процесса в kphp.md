круто использовать когда нужно выйти в сеть за данными. Пока ждём ответ из сети, можем дальше выполнять код пока нам не понадобиться результат из сити

## Как это работает в PHP? 
в PHP всё работает синхронно
```php
$res = rpsCall(...); // тут ждём пока получим данные из сети
$coeff = calcCoeff(...); // тут всё выполняется процессором
render($res, $coeff); // и тут тоже
```

## Как это можно ускорить в KPHP?
В KPHP можно сделать запуск ассинхронным
```php
$f_res = fork(rpsCall(...)); // оно не создаёт новый поток, вметсо этого
// мы остаёмся в одном потоке, а компилятор преобразует код так, чтобы 
// по ожиданию ответа от сети исполнение переключалось на след. сценарий
$coeff = calcCoeff(...); // тут всё выполняется процессором
$res = wait($f_res); // показывает, что нужно получить значение
render($res, $coeff); // продолжаем обычную работу
```
