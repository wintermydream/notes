# Tools, coding, project management
All sorts of infrastructure stuff.

## Python

### Core Python
* Tips from Chip Huyen: https://github.com/chiphuyen/python-is-cool
* Nice [list of Python gotchas](https://www.toptal.com/python/top-10-mistakes-that-python-programmers-make) from Martin Chilikian
* f-strings: http://zetcode.com/python/fstring/ , and [this specification](https://docs.python.org/3/library/string.html#format-specification-mini-language) (mini-language!)

### Random Python tips:
* If in a module you start a method name with one underscore, like `_helper`, this method isn't imported on `from module import *`. Unfortunately is still acessible if you do `import module`and address it as `module._helper()`.
* Conventions: underscore for variables and functions; all-caps for constants, capitalized camelcase for objects, leading-underscore for local methods.
* Nested comprehensions: same syntax as in writing nested loops (even tho it looks unformulaic), e.g. `[j for i in range(5) for j in range(i)]
* To add += 1 to a dict when a key may not exist, use `get()` as it has a default value: `a[i] = a.get(i,0)+1`
* To get some (or rather, first) dict from a dict, do `next(iter(a.keys()))`
* Objects (including empty lists `[]`) should never be used as default arguments for functions, as they are evaluated only once per program (during object definition), not when methods are called! Insetad use `x=None`, then `if x is None: x=[]`. It sounds super-cumbersome, but that's just how it is. ([source](https://docs.python-guide.org/writing/gotchas/))

### Matplotlib
* Brief intro from Brad Solomon: https://realpython.com/python-matplotlib-guide/
* Cheatsheet: [https://github.com/rougier/matplotlib-cheatsheet](<https://github.com/rougier/matplotlib-cheatsheet>)

### Pandas
* `[[]]` simply means "a list inside a `[]` call"
* Select columns by label: `d['x']`. Alternative spelling: `d.x`. Returns a series. 
* Select rows by label: `d.loc[1]`. Works for both df (returns a row-series), and for column-series (returns a single value).
* **Chained Assignment**: a problem while writing to a frame, selecting by both column and row.
    * Good: reference both by label (index): `d.loc[1,'x']`
    * Also Good: reference both by position:`d.iloc[1,0]`. Row goes first. 
    * Read, but not write: `d.x[1]`, which is equivalent to `d['x'][1]`.
    * Read but not write: Both `d.x.iloc[1]` and `d.iloc[1].x`. Documentation states that whether any given slice would work orn ot is "officially unpredictable", so chaining shoud never be used.
* Out-of-range integers are forgiven (ignored) on reading, but cause an error if you try to write
* For **conditional data retrieval**, either logical indexing `d.loc[d.x>0]` (can be combined with list comprehensions, can be written to) or queries: `d.query('x>0')` (easier to read, slightly faster, but cannot be written to).
* Conditional indexing supports functions, as long as they take, and return, Pandas series (or something similar, like Numpy array)

## Scikit-learn
* A bunch of notebooks that implement all key ML methods, by Aurélien Geron, to accompany his book ("Hands-On Machine Learning with Scikit-Learn and TensorFlow"): https://github.com/ageron/handson-ml2

## Coding habits for data scientists
* Keep code clean (not smelly). Types of **smells** ([ref](https://www.thoughtworks.com/insights/blog/coding-habits-data-scientists)):
    * Dead code (commented, inconsequential)
    * Print statements everywhere
    * Bad variable names
    * Functions that do too many things instead of one thing
    * Code repetition
    * Magic values
* Smuggle code from Jupyter to classes as soon as possible (Jupyter only for protopying, reporting, and use case)
* Write unit tests ([link to a decent intro](https://www.freecodecamp.org/news/an-introduction-to-testing-in-python/))
* Make small and frequent commits

## Tensorflow and Keras
* Links to several tutorials: https://github.com/sayakpaul/TF-2.0-Hacks/blob/master/README.md

**Random Notes:**
* **Tensor object**:  type, shape, and a bunch of numbers. For example, when working with images, we have a 4D structure: image# × W × H × ColorChannels.
* TF relies on a function that iterates through (features, labels) as tuples. And instead of directly linking to data, it wants to receive a data-generating function (for lazy / parallel execution?)

## ML Project Organization
#management

Basic ideas:
1. Define scope, feasibility, targets (accuracy, speed, size?)
2. Define ground truth
3. Validate data, swim in it, write data tests upfront.
4. Version your data
5. Identify baselines (stupid / simplistic models). Fit and overfit with them
7. Is there a SoTA model?
8. Start very simple (aka "Don't be a hero")
9. Develop model by iterating through a cycle ([ref](http://josh-tobin.com/assets/pdf/troubleshooting-deep-neural-networks-01-19.pdf)): 
                        * add complexity; 
                        * debug; 
                        * tune hyperparameters, 
                        * benchmark
10. Test on test data
11. Write tests for model performance (to be alerted if it unexpectedly drops on new data)

How to fight bad fit:
* Underfitting: bigger model (model capacity); less regularization; advanced architecture; hyperparameters; more features
* Overfitting: more training data; regularization; data augmentation; reduce model size

Refs:
* How to tell whether an ML solution is ready for production? [[Breck2017testing]]
* Blog of [Jeremy Jordan](https://www.jeremyjordan.me/ml-projects-guide/)
* Blog of [Aseem Bansal](https://medium.com/infinity-aka-aseem/things-we-wish-we-had-known-before-we-started-our-first-machine-learning-project-336d1d6f2184)
* [Presentation by Josh Tobin](http://josh-tobin.com/assets/pdf/troubleshooting-deep-neural-networks-01-19.pdf)
* [Andrej Karpathy on training NNs](http://karpathy.github.io/2019/04/25/recipe/)
* [Advice from Chip Huyen](https://github.com/chiphuyen/machine-learning-systems-design/blob/master/build/build1/consolidated.pdf)

## ML lore

**Deep learning maxims**: ([ref](https://pcc.cs.byu.edu/2017/10/02/practical-advice-for-building-deep-neural-networks/)):
* Use ADAM with 3e-4. Don't decay learning rate: ADAM takes care of that.
* ReLU are best units (except for LSTMs that use tanhs ([ref](http://josh-tobin.com/assets/pdf/troubleshooting-deep-neural-networks-01-19.pdf)))
* Never use activation function in the last layer
* Use bias in every layer
* Use variance-scaled weight initialization: $\mathcal{N}(0,\sqrt{2/n})$, aka "He et al." (after 2015 paper)
* Normalize (-m, /s) input data. Particularly critical for L1/L2 regularization ([ref](https://medium.com/ai%C2%B3-theory-practice-business/top-6-errors-novice-machine-learning-engineers-make-e82273d394db)))
* Compress (transform) variables if necessary (say, apply  tanh(x/C) )
* 128 filters in a convlution layer is a lot; if you need more, something is wrong
* Pooling (maxpooling) helps with transform invariance (? why ?)
* For very different inputs (say, images + words) project to low-dim (dozens) space first, then concat ([ref](http://josh-tobin.com/assets/pdf/troubleshooting-deep-neural-networks-01-19.pdf))

**Checkpoints**:
* Normal training (minutes to hours, while playing and debugging): test every n_epochs, save k best models, based on validation metrics ([ref](https://blog.floydhub.com/checkpointing-tutorial-for-tensorflow-keras-and-pytorch/))
* Slow training (hours to days): possibly a nest strategy, with infrequent unconditional checkpoints, and more regular performance-based checkpoints

**Debugging tricks**:
* Fix random seed, to have reproducability
* Try a rock-bottom simple model, iteratively add stuff back
* Switch to a simplified training set (fewer labels, classes, [ref](http://josh-tobin.com/assets/pdf/troubleshooting-deep-neural-networks-01-19.pdf))
* Verify that your loss starts at a theoretically expected value ([ref](http://karpathy.github.io/2019/04/25/recipe/))
* Overfit one batch (shoudl always be doable)
* Play with learning rate (higher to get the gist of dynamics, lower to assess the minima)
* Play with batch size (1 to get the gist of what's happening, very high for most gentle and careful descent)
* Remove bach normalization, check if explosions or vanishings are happening (batch normalization is so good and useful that it obscures problems, such as NaNs)
* Find a bunch of incorrect predictions, look for commonalities
* Make sure you don't softmax outputs to a loss that expects logits or something like that
* Check for class imbalance in the testing set (compared to training)

**Unit tests for ML**:
* Unit tests for ML: write a test that takes one step, and compared before and after, or at least check that it changed ([ref](https://medium.com/@keeper6928/how-to-unit-test-machine-learning-code-57cf6fd81765))
* Assert that loss != 0 (ibid)
* Test that params that need to be frozen at a particular stage of training actually don't change (ibid)

**Other advice:**
* If labels are hard to get, use manual **active learning**: label small part of the dataset, use it to provide (bad) labels to the full dataset; make the model report uncertainty, use it to identify observations that need to be labeled first to most improve model performance ([ref](https://www.jeremyjordan.me/ml-projects-guide/))
* Separate data pre-processing from the learning pipeline: at rearch phase you want to pre-process data once, then play with it repeatedly ([ref](https://medium.com/infinity-aka-aseem/things-we-wish-we-had-known-before-we-started-our-first-machine-learning-project-336d1d6f2184))
* You can always gain a few more % by using ensembles ([ref](http://karpathy.github.io/2019/04/25/recipe/))

## GIT
* Funny short cheatsheet "Dangit": http://dangitgit.com/

## SQL
[This is a good reference](https://www.w3schools.com/sql/default.asp), and here's a **generic query**: 
```sql
SELECT col1, MAX(col2) AS colname2
FROM table1 AS t1
WHERE (col1=1 AND col2>2) OR NOT (col5 IN ("cat","dog")) OR (col8 BETWEEN 3 AND 7)
GROUP BY col3
HAVING COUNT(*)>1 or SUM(col7)>0
ORDER BY col4 DESC, col5 ASC
LIMIT 10
FROM table2 AS t2 JOIN *
ON t1.id=t2.id
WHERE t2.col2 IS NULL;
```

**More bells and whistles:**
* `DISTINCT` - return unique results only. Can go right after select: `SELECT DISTINCT`, or can be put inside count, like in `COUNT (DISTINCT col2)`.
* `LIKE` - search for a pattern in text; goes inside the condition: `WHERE col LIKE 'a%'`. Supports wildcards: `%` for any number of characters (including none), `_` for a single character; `[ab]` for either a or b (as in regular expressions), `[^ab]` for any character except a and b (not on all systems). In general, wildcards seem to differ a bit across systems.
* Depending on the version, SQL may use either `<>` or `!=` for 'not equal'. It seems that `!=` is actually preferred, but `<>` is older, and so is used as a legacy operator. At least in some versions, `!<` (not less than) and `!>` also exist. They seem to compare strings, in a case-sensitive maner, and if string would meet a number, it seems there will be an attempt to convert them for comparison. It is also possible to cast a string to a different type, or to transform it, including changing its encoding (see below).
* Precedence: arithmetics (including bitwise `~&|`) > comparisons > `NOT` > `AND` > `OR` and its friends (`LIKE`, `IN`, `BETWEEN`, `ALL`, `ANY`, `SOME`) > assignment.
* `IN` can use either a fixed list, or a subquery.
* `AVG`, `MIN`, `MAX` - other functions for grouped queries, similar to SUM. They can also go in the SELECT block (to be returned, instead of conditioned), and combined with aliasing.
* `COALESCE (col1, col2, "default value")` - returns the first non-null element from this list
* `CASE` - a whole case switch system for binning values on-the fly, and returning the bin name (uses WHEN, THEN, and ELSE as other keywords inside the CASE structure. Read the manual if needed.)
* `HAVING` is used for clauses on aggregate functions, as it is performed after WHERE (and after grouping).
* `ASC` is used with `ORDER BY` by default, and so can be omitted
* Some systems use `TOP 10` (SQL Server, MS Access) or `ROWNUM <= 10` (Oracle) instead of `LIMIT 10` (mySQL). Those that use TOP also support a codeword `TOP 10 PERCENT`.
* `OFFSET 1` - a rather rare thing that goes in the same part as LIMIT, and makes the query return not the rows that were found, but rows that are offset from this rows by this number.
* `UNION`, `INTERSECT`, `EXCEPT` - Logical operations on selects. Usage: `SELECT * FROM table1 UNION SELECT * FROM table 2;`. The tables should match in terms of their columns, otherwise it'll break (use JOINs if the tables don't match perfectly). The first table that was called defines column names for the entire output. By default UNION only returns dinstinct rows, but use `UNION ALL` if duplicates are needed.

Types of  **joins**:
* `INNER JOIN` - only those records that exist in both tables. A simple `JOIN` without anything else, is an INNER JOIN by default.
* `LEFT JOIN` - all rows from the first table, and if possible - matching rows from the 2nd table. If not possible, it pads the output with nulls. Some manuals claim that one should add the word OUTER before JOIN, but it doesn't seem to be necessary.
* `RIGHT JOIN`- same as left, but reverse
* `FULL JOIN` - combines both tables (and thus acts same as UNION describe above).
* To imitate subtraction, do: `SELECT * FROM t1 LEFT JOIN t2 ON t1.key=t2.key WHERE t2.key is NULL;`. This way it will first try to JOIN, but set t2.key to null for all missing elements, and then they'll immediately be filtered.
* Something like a self-join is also possible, using syntax with aliasing: `SELECT a.name AS name1, b.name AS name2 FROM table1 AS a, table1 AS b WHERE a.manager=b.id;`. In this case we'll have a list of all relations between people in an organization, all from one self-referencing table.

**Subquery:**: `SELECT * FROM table1 WHERE id IN (SELECT ...);`.
* `ALL`, `ANY` - used within where or having, as conditions on subqueries. So you can do `WHERE col1 = ANY (SELECT ...)`.
* `SOME` - exact synonim to `ANY` used in some versions.
* `EXISTS`- to check whether a subquery returned anything: `WHERE EXISTS (SELECT ...)`.

**Inserting to a table:** `INSERT INTO table1 (col1, col2) VALUES (1, "dog");`. If you know the order of columns, you can also skip the first brackeet, and just do `INSERT INTO table1 VALUES (...);`. If not all columns are specified, all remaining will be set to null.

Interesting way to copy some selected stuff from one table to another: `INSERT INTO table1 SELECT * FROM table2 WHERE condition;`. Interestingly, the condition may reference both tables, allowing for interesting data movements. If the table doesn't exist yet, use a different syntax: `SELECT * INTO table1 FROM table2 ...;`.

**Update rows in a table** Like a simple select query (without grouping and other fancy things obviously), just instead of SELECT you do: `UPDATE table1 SET col1=1, col2="dog" WHERE id=0;`. Be careful to always have a `WHERE` statement there, as without it the statement will still be valid; just it will update all records. Updates can directly reference table fields, so things like `col1 = col1+1` are normal. Updates can also reference other tables by running a subquery, or doing a JOINT, or (in some versions) even by having a FROM sequence directly following the UPDATE part.

**Virtual table:** `CREATE VIEW view_name AS SELECT * FROM table1 WHERE coll="whatever";`. Can also be updated by `CREATE OR REPLACE VIEW view_name`. After you are done with this virtual table, it should be dropped using `DROP VIEW view_name`.

**Create stuff:**
* Create database: `CREATE DATABASE dbname;`
* Create a table: `CREATE TABLE table1 (col1 type, col2 type ...);`. There are many types, but key ones are: INT (medium, 4 bytes), BIGINT, DOUBLE, BOOL, CHAR(size) - fixed length, TEXT - variable length, LONGTEXT, ENUM(val1,val2,...) - a limited list of options, DATE, TIME. These really depend on the system though, so need to be researched.
* Columns can have **constraints** that are specified during creation, like that: `col_name data_type constraint`, where constraints come from the following list: `NOT NULL` - cannot be nulll; `UNIQUE` - all records are unique; `PRIMARY KEY` - both not null and unique (often combined with `AUTO INCREMENT`, which is not technically a constraint, but a built-in resolution of it); `FOREIGN KEY REFERENCES table2(keycol) ` - a key for a diff table; `CHECK (col_name>0)` - requires a condition to be met; `DEFAULT value` - sets a default value; `INDEX` - makes retrieval faster. If a constraint like CHECK or UNIQUE isn't met, it triggers an error, and in a real system it shoudl be handled properly (see below for control structures). Also the syntax of constraints differs a bit between systems.
* Another way to build an index: `CREATE INDEX ind ON table1 (col1);`. More than one column may be indexed, which may make reading faster, but it will also make writing slower. Ideally, indices should match selects, but maybe almost anti-match insertions, deletions, and updates.

**Updating table structure:** `ALTER TABLE tb ADD col_name type;`, or `ALTER TABLE tb DROP COLUMN col_name`, or `ALTER TABLE tb MODIFY COLUMN col_name type` (some systems use ALTER COLUMN instead of MODIFY). Constraints may be removed from columns using `ALTER TABLE tb DROP CONSTRAINT constraint;` (slightly diff syntax in MySQL).

**Deleting stuff**
* Delete a row: `DELETE FROM table WHERE condition;`. As usual, without WHERE would delete everything.
* Delete (drop) a whole table: `DROP TABLE table1;`. Simple and brutal.
Apparently it's possible not to grant users permissions to delete rows and drop tables (something like `REVOKE DELETE ON table TO username;` for this particular user), and it is possible to create server-wide triggers and auto-rollback on dropping; and in some editions. There may also be a way to protect tables using a schema, but I'm not sure about that.
* `BACKUP DATABASE dbname` also exists.

**Operations on strings, numbers, and dates**: there are lots of built-in functions; too many to mention, including math, trigonometry, string manipulation (like `LEFT`, `LEN`, `LOWER`, and alike), and what not. Some interesting ones that are not obvious are `LEAST` and `GRATEST` that work across differenct columns within the same row, as opposed to MAX and MIN that work along all rows (entries) for a returned column. There are also lots of system-specific operaions on dates and times. Read the manual.

**Control structures:** apparently SQL (especially larger systems, like SQLServer, or Transact-SQL from Microsoft) also has its own system of control structures, with IF, ELSE, BEGIN TRY, BEGIN CATCH, WHILE, and what not.