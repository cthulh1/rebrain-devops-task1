# Вебморда для инвентаризации

Тестовый readme для прекрасной(нет) самописной вебморде для офисной инвентаризации и учета оборудования. 
Реализован на **apache**+**php**+**postgresql**

## Как оно выглядит

![site](https://bitbucket.org/cthulh1/rebrain-devops-task1/raw/6dddd60f91506fcf172f0a1544c7e59f3a23e38e/site.JPG)
_____
## Структура БД
|   | ID | Наименование | Дата инвент. | Номер инвент | Время записи | Последнее редактирование |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| тип поля | primary key | text | date | text | timestamp | text |
| пример | 370 | Монитор 27* Samsung F27T450FQI | 2021-03-12 | БК0000443 | 2022-07-11 14:50:38 | 2022-07-11 14:49:49 |


## Файлы

- index.php
- dbconn.php
- style.css
- export.php
- auth.php

## Описание файлов
### index.php
Основной файл со всем html кодом. Содержит в себе:
1. ввод данных в БД
2. редактирование и удаление данных :writing_hand: :x:
3. сортировку
4. пагинацию
5. поиск

### dbconn.php

Коннект к sql, собственно

### style.css

Содержит в себе все спертые и сгенерирование редакторами цсски

### export.php
Экспорт из БД в CSV-файл при нажатии на :floppy_disk:
```php
    <?php
    include_once "dbconn.php";
    date_default_timezone_set('Asia/Almaty');
    $t = date("_d-m-y_H_i_s");
    if(isset($_GET['dbtable'])) {
    $dbtable = $_GET['dbtable'];
    }
    else {
    $dbtable = 'begalina';
    }
    if (isset($_GET['download'])) {
	    header("Content-Type: text/csv; charset=utf-8");
	    header("Content-Disposition: attachment; filename=".$dbtable.$t.".csv");
	    $output = fopen("php://output", "w");
	    fputs($output, $bom =( chr(0xEF) . chr(0xBB) . chr(0xBF) ));
	    fputcsv($output, array('ID', 'Наименование', 'Дата инвент.', 'Инвент. номер', 'Время записи в БД'));
	    $sql = "SELECT * FROM $dbtable ORDER BY invid DESC";
	    $result = pg_query($dbconn, $sql);
 
    while ($row = pg_fetch_assoc($result)) {
       fputcsv($output, $row);
    } 
    	fclose($output);
	    exit;
	}
    ?>
```

### auth.php

Самописная суперсекретная авторизация, с хранящимися в открытом виде логином/паролем прямо в коде

## Ссылки
[Ссылка на проект :fingers_crossed:](127.0.0.1)

## Автор
Аронов Александр