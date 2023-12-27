# i-spec

## Что подтолкнуло к идее?

Общий смысл подхода заключается в том чтобы вытащить бизнес логику
приложения на уровень данных. И чтобы бизнес-операции превратились в операции
трансформации одних моделей в другие.

Видео, которое подтолкнуло к идее:

[![Watch the video](https://img.youtube.com/vi/ZhuHCtR3xq8/hqdefault.jpg)](https://www.youtube.com/embed/ZhuHCtR3xq8)

## Суть идеи

Первое - логика строиться на основе данных (моделей). Бизнес процесс опистывается
моделью - объектом.

Второе - к модели-объекту может быть привязан эффект - функция, выполняющая ввод-вывод.

Принципиально это всё, два правила которые позволяют описывать
бизнес процесс на уровне данных а не на уровне операций.

## Схема

![image](https://github.com/kosukhin/i-spec/assets/109918884/72487054-b934-4297-881d-5e11ce7d9882)


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

// В контроллере
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

// В контроллере
renderScene({
  floorTexture: '/floor.jpeg',
  floorSize: [200, 200],
  skyColor: 'blue'
})

// В сервисе
function resolveSkyColor(model: Scene) {
  return {
    ...model,
    skyColor: 'red',
  }
}
```

## Альтернативное решение использование классов

ТК в JS есть классы, то можно объединить модель и ее эффекты внутри одного класса.
В каком-то смысле это даже упростит код и не нарушит идею.
