## Binary studio academy: third task

1. Запрос поиска всех студентов, у которых score > 87% и < 93% по любому из типов выполненных заданий:

```
db.BSACollection.find({
	"scores": {
		$elemMatch: {
			score: {
				$gt: 87,
				$lt: 93
			}
		}
	}
})
```

2. Запрос-агрегация для поиска всех студентов, у которых результат по экзамену (type: "exam") более 90%.

```
db.testCollection.aggregate([{
	$unwind: "$scores"
}, {
	$match: {
		"scores.type": "exam",
		"scores.score": {
			$gt: 90
		}
	}
}])
```

3. Запрос для поиска всех студентов с именем Dusti Lemmond и добавление к их документам поля "accepted" со значением "true".

```
db.testCollection.updateMany({
	name: "Dusti Lemmond"
}, {
	$set: {
		"accepted": true
	}
})
```