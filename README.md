# i-spec

## Что подтолкнуло к идее?

Общий смысл подхода заключается в том чтобы вытащить бизнес логику
приложения на уровень данных. И чтобы бизнес-операции превратились в операции
трансформации одних моделей в другие.

Видео, которое подтолкнуло к идее:

## Суть идеи

Первое - логика строиться на основе данных (моделей). Бизнес процесс опистывается
моделью - объектом.

Второе - к модели-объекту может быть привязан эффект - функция, выполняющая ввод-вывод.

Принципиально это всё, два правила которые позволяют описывать
бизнес процесс на уровне данных а не на уровне операций.

## Примеры

### Запрос Request

```ts
type Request = {
  method: string,
  url: string,
  params: Record<string, string>
  body: any
}

async function request(model: Request) {
  // do request
}

const result = await request({
  method: 'GET',
  url: '/hello/world',
  params: {
    test: 'me'
  }
})
```

### Сцена игры

```ts
type Scene = {
  floorTexture: string,
  floorSize: [number, number],
  skyColor: string,
}

function renderScene(model: Scene) {
  // do rendering
}

renderScene({
  floorTexture: '/floor.jpeg',
  floorSize: [200, 200],
  skyColor: 'blue'
})
```
