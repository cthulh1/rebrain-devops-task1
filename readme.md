# �������� ��� ��������������

�������� readme ��� ����������(���) ���������� �������� ��� ������� �������������� � ����� ������������. 
���������� �� **apache**+**php**+**postgresql**

## ��� ��� ��������

![site](https://bitbucket.org/cthulh1/rebrain-devops-task1/raw/6dddd60f91506fcf172f0a1544c7e59f3a23e38e/site.JPG)
_____
## ��������� ��
|   | ID | ������������ | ���� ������. | ����� ������ | ����� ������ | ��������� �������������� |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| ��� ���� | primary key | text | date | text | timestamp | text |
| ������ | 370 | ������� 27* Samsung F27T450FQI | 2021-03-12 | ��0000443 | 2022-07-11 14:50:38 | 2022-07-11 14:49:49 |


## �����

- index.php
- dbconn.php
- style.css
- export.php
- auth.php

## �������� ������
### index.php
�������� ���� �� ���� html �����. �������� � ����:
1. ���� ������ � ��
2. �������������� � �������� ������ :writing_hand: :x:
3. ����������
4. ���������
5. �����

### dbconn.php

������� � sql, ����������

### style.css

�������� � ���� ��� ������� � �������������� ����������� �����

### export.php
������� �� �� � CSV-���� ��� ������� �� :floppy_disk:
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
	    fputcsv($output, array('ID', '������������', '���� ������.', '������. �����', '����� ������ � ��'));
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

���������� �������������� �����������, � ����������� � �������� ���� �������/������� ����� � ����

## ������
[������ �� ������ :fingers_crossed:](127.0.0.1)

## �����
������ ���������