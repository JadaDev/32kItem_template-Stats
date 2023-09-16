# Removing 32k Stat Cap for Items in TrinityCore

This tutorial explains how to remove the stat cap when making items with stats above 32767 in TrinityCore.

## Requirements

- Any MySQL Editor (e.g., HeidiSQL, SQLyog, Navicat)
- Any Text Editor (e.g., Notepad, Notepad++, Visual Studio Code)
- TrinityCore Source Code
- Database Access

## Steps

1. Locate the `ObjectMgr.cpp` file in your TrinityCore source code. You can find it under `\src\server\game\globals`.

2. Open the `ObjectMgr.cpp` file using any of the text editors mentioned and navigate to around line 2700+.

3. Search for `[GetInt16]` without square brackets. You should find something similar to this:

    ```cpp
    itemTemplate.ItemStat.ItemStatValue = int32(fields[29 + i * 4 + 1].GetInt16());
    ```

4. Change `[GetInt16]` to `[GetInt32]` without square brackets. It should now look like this:

    ```cpp
    itemTemplate.ItemStat.ItemStatValue = int32(fields[29 + i * 4 + 1].GetInt32());
    ```

5. Recompile your source code and replace the existing `worldserver.exe` with the new one you've compiled.

6. It's time to update the database `stat_valueX` details. Open any MySQL Editor from the requirements list.

7. Navigate to the World database and find the "item_template" table. Edit the table's structure and locate all columns named `stat_value1`, `stat_value2`, and so on.

8. Change their data type from SMALLINT or whatever it is to INT.

9. Save your changes and you're all set.

Remember to always create a backup before making any changes.

Happy modding!

## You Could also be using this SQL to update the Item_template : 
```SQL
ALTER TABLE item_template
MODIFY COLUMN stat_value1 INT,
MODIFY COLUMN stat_value2 INT,
MODIFY COLUMN stat_value3 INT,
MODIFY COLUMN stat_value4 INT,
MODIFY COLUMN stat_value5 INT,
MODIFY COLUMN stat_value6 INT,
MODIFY COLUMN stat_value7 INT,
MODIFY COLUMN stat_value8 INT,
MODIFY COLUMN stat_value9 INT,
MODIFY COLUMN stat_value10 INT;
```
