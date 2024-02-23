# CPU

Это небольшой архитектурный принцип разделения кода на 3 группы.

# Composables

**Композаблы** - представляют из себя бизнес логику приложения, они описываются в стиле функций высшего порядка, что значит что
все зависимости которые нужны бизнес логике для работы поставляются в параметрах функции в виде функций возвращающих нужные значения.
Этот подход больше применим для процедурного стиля написания кода.

```ts
const useAddresses = (
  getAddressForm: () => AddressForm,
  getAddressList: () => Address[],
  doAddressRequest: (filter: AddressFilter) => void,
) => {
  // ... Логика ...
}
```
В случае функционального стиля кода в composables можно хранить функции-композиции в виде цепочки Монад или цепочки Промисов.
```js
pipe(
  some(game),
  chain(ensureNotGameOver),
  chain(ensureNotPaused),
  chain(ensureShapeInBoundsByYAxis(currentShoot)),
  map(moveShapeToDirection(currentShoot)),
  map(checkEnemyShooted(currentShoot)),
  tap(removeShootIfStopped(currentShoot, game)),
  repeat(50)
).do()
```

# Providers

**Провадйеры** - это частично примененные функции из набора функций utils. Название провайдеры связано с тем что
обычно в этих функциях будет логика работы с источниками данных.

```ts
const addressProvider = request.bind(null, 'api/addresses', 'get')
```

# Utils

**Утилиты** - это простые функции, выполняющие конкретные взаимодействия на низком системном уровне. Работа с сетью со строками, числами, датами.

```ts
const request = (url: string, method: string, params: Record<string, any>, body: any) => any;
```
