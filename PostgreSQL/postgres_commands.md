
# PostgreSQL Commands

### Database Commands
- **Connect to a Database:**
  ```
  \c database_name
  ```

- **List Databases:**
  ```
  \l
  ```

- **List Tables:**
  ```
  \dt
  ```

- **Exit psql:**
  ```
  \q
  ```

- **Execute SQL Commands from a File:**
  ```
  \i file_path
  ```

- **Describe a Table:**
  ```
  \d table_name
  ```

---

### SQL Query Commands
- **Select with Order By:**
  ```sql
  SELECT * FROM table_name ORDER BY column_name ASC|DESC;
  ```

- **Select with Limit:**
  ```sql
  SELECT * FROM table_name LIMIT number;
  ```

- **Select with Offset:**
  ```sql
  SELECT * FROM table_name OFFSET number;
  ```

- **Select with Limit and Offset:**
  ```sql
  SELECT * FROM table_name LIMIT number OFFSET number;
  ```

- **Select with IN:**
  ```sql
  SELECT * FROM table_name WHERE column_name IN (value1, value2, ...);
  ```

- **Select with Group By:**
  ```sql
  SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name;
  ```

- **Select with Group By and Having:**
  ```sql
  SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name HAVING COUNT(*) > number;
  ```

- **Select with Order By, Limit, Offset, and Group By:**
  ```sql
  SELECT column_name, COUNT(*) 
  FROM table_name 
  WHERE column_name IN (value1, value2, ...) 
  GROUP BY column_name 
  ORDER BY COUNT(*) DESC 
  LIMIT number OFFSET number;
  ```
