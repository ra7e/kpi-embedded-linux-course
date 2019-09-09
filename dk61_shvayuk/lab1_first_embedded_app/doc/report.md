###  Результати виконання лабораторної роботи №1

У ході виконання лабораторної роботи №1 була написана програма на мові С, що інкрементує глобальну змінну із двох потоків. Багатопотоковість реалізована за допомогою бібліотеки pthread.
Вихідний код програми доступний за посиланням:
[сирцевий код](https://github.com/maximwowpro/kpi-embedded-linux-course/blob/pr/dk61_shvayuk/lab1_threaded_applications/src/example_mt.c)

Збірка програми виконується за допомогою системи збірки Make. Makefile має дві функції: видалення попеедніх версій бінарних файлів програми та, власне, збірка програми. Його вихідний доступний за посиланням:
[сирцевий код](https://github.com/maximwowpro/kpi-embedded-linux-course/blob/pr/dk61_shvayuk/lab1_threaded_applications/Makefile)

Результат виконання програми на платформах х86 та ARM виявився ідентичним: програма завжди показувала правильний результат.
Результат виконання на платформі х86:
```
[max@hpprobook build]$ ./example_mt_O0
Waiting for threads...
:Counter value: 10000
[max@hpprobook build]$ ./example_mt_O2
Waiting for threads...
:Counter value: 10000
```
Результат виконання на платформі ARM:
```
debian@beaglebone:~/lab1_threaded_applications/build$ ./example_mt_O0
Waiting for threads...
:Counter value: 100
debian@beaglebone:~/lab1_threaded_applications/build$ ./example_mt_O2
Waiting for threads...
:Counter value: 100
```

Я не можу зі 100-відсотковою впевненістю пояснити чому програма давала однаковий результат на всіх платформах та при різних рівнях оптимізації. Це йде всупереч із здоровим глуздом, адже через наявність у х86 окремої інструкції inc там програма має виконуватися без помилок, а на ARM, де такої інструкції немає мають бути помилки (особливо при великих числах), але у своєму експерименті я цього не побачив.
Можливо причина у занадто великій затримці (1 мс) в тілі циклу, що інкрементує глобальну змінну, або просто помилка є настільки рідкісною, що мені не пощастило її спостерігати (я провів близько 10 тестів для кожного рівня оптимізації на кожній платформі).