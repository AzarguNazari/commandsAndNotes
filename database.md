The most common used queries of SQL
```
SELECT c1, c2 FROM t;

SELECT * FROM t;

SELECT c1, c2 FROM t
WHERE condition;

SELECT DISTINCT c1 FROM t
WHERE condition;

SELECT c1, c2 FROM t
ORDER BY c1 ASC [DESC];


SELECT c1, c2 FROM t
ORDER BY c1 
LIMIT n OFFSET offset;

SELECT c1, aggregate(c2)
FROM t
GROUP BY c1;

SELECT c1, aggregate(c2)
FROM t
GROUP BY c1
HAVING condition;

SELECT c1, c2 
FROM t1
INNER JOIN t2 ON condition;

SELECT c1, c2 
FROM t1
LEFT JOIN t2 ON condition;


SELECT c1, c2 
FROM t1
RIGHT JOIN t2 ON condition;

SELECT c1, c2 
FROM t1
FULL OUTER JOIN t2 ON condition;

SELECT c1, c2 
FROM t1
CROSS JOIN t2;

SELECT c1, c2 
FROM t1, t2;

SELECT c1, c2
FROM t1 A
INNER JOIN t2 B ON condition;

SELECT c1, c2 FROM t1
UNION [ALL]
SELECT c1, c2 FROM t2;

SELECT c1, c2 FROM t1
INTERSECT
SELECT c1, c2 FROM t2;

SELECT c1, c2 FROM t1
MINUS
SELECT c1, c2 FROM t2;

SELECT c1, c2 FROM t1
WHERE c1 [NOT] LIKE pattern;

SELECT c1, c2 FROM t
WHERE c1 [NOT] IN value_list;

SELECT c1, c2 FROM t
WHERE  c1 BETWEEN low AND high;

SELECT c1, c2 FROM t
WHERE  c1 IS [NOT] NULL;

CREATE TABLE t (
     id INT PRIMARY KEY,
     name VARCHAR NOT NULL,
     price INT DEFAULT 0
);

DROP TABLE t ;

ALTER TABLE t ADD column;

ALTER TABLE t ADD column;

ALTER TABLE t DROP COLUMN c ;

ALTER TABLE t ADD constraint;

ALTER TABLE t DROP constraint;

ALTER TABLE t DROP constraint;

ALTER TABLE t1 RENAME TO t2;

ALTER TABLE t1 RENAME c1 TO c2 ;

TRUNCATE TABLE t;

CREATE TABLE t(
    c1 INT, c2 INT, c3 VARCHAR,
    PRIMARY KEY (c1,c2)
);

CREATE TABLE t1(
    c1 INT PRIMARY KEY,  
    c2 INT,
    FOREIGN KEY (c2) REFERENCES t2(c2)
);

CREATE TABLE t(
    c1 INT, c1 INT,
    UNIQUE(c2,c3)
);

CREATE TABLE t(
  c1 INT, c2 INT,
  CHECK(c1> 0 AND c1 >= c2)
);

CREATE TABLE t(
     c1 INT PRIMARY KEY,
     c2 VARCHAR NOT NULL
);

INSERT INTO t(column_list)
VALUES(value_list);

INSERT INTO t(column_list)
VALUES (value_list), 
       (value_list), …;
       
INSERT INTO t1(column_list)
SELECT column_list
FROM t2; 

UPDATE t
SET c1 = new_value;

UPDATE t
SET c1 = new_value, 
        c2 = new_value
WHERE condition;

DELETE FROM t;

DELETE FROM t
WHERE condition;

CREATE VIEW v(c1,c2) 
AS
SELECT c1, c2
FROM t;

CREATE VIEW v(c1,c2) 
AS
SELECT c1, c2
FROM t;
WITH [CASCADED | LOCAL] CHECK OPTION;

CREATE RECURSIVE VIEW v 
AS
select-statement -- anchor part
UNION [ALL]
select-statement; -- recursive part

CREATE TEMPORARY VIEW v 
AS
SELECT c1, c2
FROM t;

DROP VIEW view_name;

CREATE INDEX idx_name 
ON t(c1,c2);

DROP INDEX idx_name;

CREATE OR MODIFY TRIGGER trigger_name
WHEN EVENT
ON table_name TRIGGER_TYPE
EXECUTE stored_procedure;
```

WHEN

- `BEFORE` – invoke before the event occurs
- `AFTER` – invoke after the event occurs

EVENT
- `INSERT` – invoke for INSERT
- `UPDATE` – invoke for UPDATE
- `DELETE` – invoke for DELETE

TRIGGER_TYPE
- `FOR EACH ROW`
- `FOR EACH STATEMENT`


![](https://cdn.sqltutorial.org/wp-content/uploads/2016/04/SQL-Cheet-Sheet-1.png)
![](https://cdn.sqltutorial.org/wp-content/uploads/2016/04/SQL-Cheat-Sheet-2.png)
