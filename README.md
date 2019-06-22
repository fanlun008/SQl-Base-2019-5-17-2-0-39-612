请在本地创建一个学生考试系统的数据库(student_examination_sys)，里面有三张表：

1. 学生表(student):

   |  id  | name | age  | sex  |
   | :--: | :--: | :--: | :--: |
   | 001  | 张三 |  18  |  男  |
   | 002  | 李四 |  20  |  女  |

2. 考试科目表(subject)：

   |  id  | subject | teacher |   description    |
   | :--: | :-----: | :-----: | :--------------: |
   | 1001 |  语文   | 王老师  | 本次考试比较简单 |
   | 1002 |  数学   | 刘老师  |  本次考试比较难  |

3. 成绩表(score)：

   |  id  | student_id | subject_id | score |
   | :--: | :--------: | :--------: | :---: |
   |  1   |    001     |    1001    |  80   |
   |  2   |    002     |    1002    |  60   |
   |  3   |    001     |    1001    |  70   |
   |  4   |    002     |    1002    | 60.5  |

请用SQL实现上面的需求并将实现的效果截图说明。


```mysql
CREATE DATABASE IF NOT EXISTS `student_examination_sys` DEFAULT CHARSET utf8mb4;
USE student_examination_sys;

# 创建 student 表
CREATE TABLE student (
	id VARCHAR ( 32 ) NOT NULL PRIMARY KEY,
	NAME VARCHAR ( 32 ) NOT NULL,
	age INT ( 3 ) NOT NULL,
	sex CHAR ( 1 ) NOT NULL 
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

#student 数据
INSERT INTO student
VALUES
	( '001', '张三', 18, '男' ),
	( '002', '李四', 20, '女' );
	
#创建 subject 表
CREATE TABLE SUBJECT (
	id VARCHAR ( 32 ) NOT NULL PRIMARY KEY,
	SUBJECT VARCHAR ( 12 ) NOT NULL,
	teacher VARCHAR ( 12 ) NOT NULL,
	description VARCHAR ( 255 ) 
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

#subject 数据
INSERT INTO SUBJECT
VALUES
	( '1001', '语文', '王老师', '本次考试比较简单' ),
	( '1002', '数学', '刘老师', '本次考试比较难' );

# 创建 score 表
CREATE TABLE score (
	id INT ( 32 ) NOT NULL PRIMARY KEY auto_increment,
	student_id VARCHAR ( 32 ) NOT NULL,
	subject_id VARCHAR ( 32 ) NOT NULL,
	score DECIMAL ( 4, 1 ) NOT NULL DEFAULT 0,
	CONSTRAINT `fk_student_id` FOREIGN KEY ( `student_id` ) REFERENCES `student` ( `id` ) ON DELETE CASCADE,
	CONSTRAINT `fk_subject_id` FOREIGN KEY ( `subject_id` ) REFERENCES `subject` ( `id` ) ON DELETE CASCADE 
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

#score 数据
INSERT INTO score
VALUES
	( 1, '001', '1001', 80 ),
	( 2, '002', '1002', 60 ),
	( 3, '001', '1001', 70 ),
	( 4, '002', '1002', 60.5 );
```


