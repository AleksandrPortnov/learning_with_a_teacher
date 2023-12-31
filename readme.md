Отток клиентов
Описание:
Из «Бета-Банка» стали уходить клиенты. Каждый месяц. Немного, но заметно. 
Банковские маркетологи посчитали: сохранять текущих клиентов дешевле, чем привлекать новых.

Нужно спрогнозировать, уйдёт клиент из банка в ближайшее время или нет. 
Нам предоставлены исторические данные о поведении клиентов и расторжении договоров с банком.

Необходимо построить модель с предельно большим значением F1-меры. Чтобы сдать проект успешно, нужно довести метрику до 0.59. 
Нужно проверить F1-меру на тестовой выборке самостоятельно.

Дополнительно нужно измерять AUC-ROC и сравнивать её значение с F1-мерой.


Мы проверили качество моделей логистическая регрессия, дерево решений и случайный лес.
В ходе проверки выяснили, что наилучший результат показала модель случайный лес:
F1-мера без учета дисбаланса :
у логистической регресси: 0.023529411764705882
у дерева решений: 0.5006045949214026
у случайного леса: 0.5769805680119582

AUC-ROC без учета дисбаланса :
у логистической регресси: 0.45469970178866315
у дерева решений: 0.6837644190927842
у случайного леса: 0.840733672475638

Для борьбы с дисбалансом увеличили количество положительных ответов в 4 раза. Количество отрицательных и положительных ответов почти сравнялось:
0: 0.501043
1: 0.498957

Обучили наши модели с учетом дисбаланса. Качество всех моделей стало заметно лучше: 

F1-мера с учетом дисбаланса:
у логистической регресси: 0.40257648953301123
у дерева решений: 0.6010471204188481
у случайного леса: 0.6195069667738478

AUC-ROC с учетом дисбаланса:
у логистической регресси: 0.5960506656827104
у дерева решений: 0.8367353419752117
у случайного леса: 0.8530038894500934

Лучшей моделью стал случайный лес с гиперпараметрами:
n_estimators: 31
criterion: gini
max_features: log2
bootstrap: True
max_depth: 10
min_samples_split: 16

Проверили лучшую модель (случайный лес) на тестовой выборке. Результат оказался хорошим:
F1-мера: 0.602711157455683
AUC-ROC: 0.8548775167860694
Цель достигнута, F1-мера на тестовой выборке больше 0.59.

Далее мы сравнили нашу модель с константной.
F1-мера константной модели: 0.3491539413949649
F1-мера нашей модели: 0.6004016064257028

F1-мера нашей модели почти в два раза выше, чем константной. 
Полнота (recall) нашей модели равна 0.706855791962175. 
Это значит, что 70% клиентов, собирающихся расторгнуть договор с банком, наша модель определит верно.