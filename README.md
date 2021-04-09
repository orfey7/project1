Мультиклассовая классификация - программа распознавания рукописных цифр


 ![00e2c8f57a0041b394e922789194494d](https://user-images.githubusercontent.com/55453859/114109722-836c3300-98de-11eb-87f9-18fea6c012a6.png)

Реализация:

    1)Для начала создадим класс нашей нейросети. На вход мы будем получать кол-во нейронов во входном, скрытом
    и выходном слоях. За количество нейронов входного слоя будем принимать количество пикселей картинки. 
    Соответственно количество нейронов выходного слоя
    будет равно 10(10 цирф). 
    Рандомно проинициализируем матрицу весов для соединения входного и скрытого слоя. 
    Рандомно проинициализируем матрицу весов для соединения скрытого и выходного слоя. 
    И зададим функцию активации(сигмоиду). 



    2) Создадим метод нашего класса для обучения нейронной сети. На вход получаем массив со значениями 
    пикселей картинки и массив с настоящим ответом.
    Затем транспонируем входные данные для корректного перемножения матриц. 
    Умножаем матрицу весов входного и скрытого слоев на вектор значений пикселей нашей картинки 
    (т.е. матрицу размера HxI умножаем на вектор размера Ix1, получаем вектор размера Hx1)
    Полученный вектор Hx1 вставим в функцию активации
    (эта функция вернет вектор Hx1 но уже со значениями от 0 до 1)
    
    Умножаем матрицу весов скрытого и выходного слоев на вектор полученный на предыдущем шаге
    (т.е. матрицу OxH умножаем на вектор Hx1 и получаем вектор Ox1. Полученный вектор Ox1 
    вставляем функцию активации - она вернет вектор Ox1, но уже с нужными нам 
    значениями(получим ответ, что за цифра на картинке)



    3) Здесь реализуем Back Propagation. Вычисляем насколько ответ нейросети отличается от 
    настоящего ответа(поэлементное вычитание векторов т.е вычисляем ошибки выходного слоя)
    
    Далее вычисляем ошибки допущенные нейросетью в скрытом слое на основе знаний о значениях
    ошибок на выходном слое (умножаем транспонированную матрицу (OxH)=> HxO на вектор ошибки
    Ox1 получаем вектор Hx1. Затем перейдем к самой корректировки весов.
    Исправляем веса в матрице весов скрытого и выходного слоев. 
    
    Эта строка выводится из формулы производной функции активации: 
    f'(x) == f(x) * (1 - f(x)) 
    
    После перемножения получаем матрицу того на сколько нужно изменить нашу матрицу весов. 
    Теперь поэлементно умножаем все это дело на learning rate и прибавляем к матрице весов.
    Проделаем это для обеих матриц весов.



    4) Далее реализуем метод для предсказаний нейронной сети. Даем на вход картинку -  
    получаем ответ от нейроки, как она думает,какая цифра на картинке.



    5) Считаем наш датасет рукописных цифр. Затем проверим, чтобы все нормально 
    считалось - возьмем первую строчку датасета и превратим ее обратно в картинку. 
    Вывод картинки цифры с помощью imshow.



    6) Следующим действием инициализируем нейронную сеть и создаем объект класса нашей нейронки  



    7) Далее проводим обучение нашей сетки. 
    Переводим значения цветов пикселей в размерность значений от 0 до 1, чтоб все работало нормально.
    Создаем корректный формат настоящего ответа (изначально это лишь одна цифра, нам же нужен массив)
    В дополнение решил попробовать интересную вещь называется аугментация. 
    Трюк в том, чтобы искусственно увеличить датасет с помощью того, что мы просто картинку 
    поворачиваем на 10 градусов влево и называем это новым примером. 
    Поворачиваем на 10 градусов вправо еще один новый пример. 
    
    Таким образом мы увеличиваем датасет в 3 раза и учим нейронку распознавать цифры написанные под углом.



    8) Открываем данные для теста, проверяем все то же самое



    9) В тестовом варианте смотрим на предсказание нашей сети для самого первого тестового примера. 
    Видим, что наша сеть на 98 процентов уверена, что это семерка тип индекс 7.
    Далее подсчитываем accuracy нашей сети, прогоняя все тестовые примеры и смотрим если наша 
    нейронная сеть угадала записываем 1, если нет, то 0.



    10) Теперь смотрим на отношение правильных ответов ко всем ответам. Дальше я уже решил 
    сам нарисовать цифру в Paint и проверить, действительно ли сеть работает правильно. 
    
    
    
    11) Затем я инвертирую цвета для корректной работы, и делаю проверку.
    Ну и нормализация значений пикселей.
    
    Тестируем
