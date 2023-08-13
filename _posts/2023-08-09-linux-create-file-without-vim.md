# linux create file without vim.

- single line file
    ```
    [root@cn01 test]# echo "192.168.1.1" >test.txt
    [root@cn01 test]# cat test.txt 
    192.168.1.1

    ```
- single line append
    ```
    [root@cn01 test]# echo "192.168.1.1" >>test.txt
    [root@cn01 test]# cat test.txt 
    192.168.1.1
    192.168.1.1
    ```

- multi line file
  ```
  cat > test.txt or cat >>test.txt
  ```