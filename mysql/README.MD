## copy example data for tests

> example schema from vendor: https://dev.mysql.com/doc/refman/8.3/en/mysql-shell-tutorial-python-download.html
> [official doc](https://dev.mysql.com/doc/refman/8.3/en/mysql-shell-tutorial-python-download.html)

```bash
wget https://dbconvert.com/downloads/dbs/sample-data/products.csv --output-document ./source/mysql/products.csv
```

## Populate source table with sample data.

```bash
docker exec -it \
    mysql \
    mysql -uroot -p123456 -D source
```

```bash
LOAD DATA INFILE '/var/lib/mysql-files/products.csv' INTO TABLE products FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n' IGNORE 1 ROWS;
```


## Table

## System properties

Системная переменная innodb_flush_log_at_trx_commit определяет частоту сброса транзакций в журнал повторов:

Когда значение равно 0, при фиксации ничего не выполняется; скорее, буфер журнала записывается и сбрасывается в журнал повтора InnoDB раз в секунду. Это повышает производительность, но сбой сервера может стереть последнюю секунду транзакций.

Когда значение равно 1, буфер журнала записывается в файл журнала повтора InnoDB и после каждой транзакции выполняется сброс на диск. Это необходимо для полного соответствия ACID.

Когда значение равно 2, буфер журнала записывается в журнал повтора InnoDB после каждой фиксации, но очистка выполняется раз в секунду. Производительность немного лучше, но сбой операционной системы или питания может привести к потере транзакций в последнюю секунду.

Когда значение равно 3, InnoDB эмулирует более старую реализацию групповой фиксации с 3 синхронизациями на диск для каждой групповой фиксации.


