# Piping and Redirection in Linux – Quick Reference

---

## 1. Streams

In Linux, every command operates using three standard streams:

- **stdin (0)** → Standard Input  
- **stdout (1)** → Standard Output  
- **stderr (2)** → Standard Error  

---

## 2. Redirection Operators

Redirection allows you to control where input and output go.

- **`>`** → Redirect stdout to a file (overwrite)  
  ```bash
  ls > file.txt
  ```

- **`>>`** → Redirect stdout to a file (append)  
  ```bash
  echo hello >> file.txt
  ```

- **`<`** → Redirect stdin from a file  
  ```bash
  wc -l < file.txt
  ```

- **`2>`** → Redirect stderr to a file  
  ```bash
  ls missing.txt 2> error.txt
  ```

- **`2>&1`** → Redirect stderr to the same place as stdout  
  ```bash
  ls missing.txt > out.txt 2>&1
  ```

- **`2>/dev/null`** → Hide error messages  
  ```bash
  ls missing.txt 2>/dev/null
  ```

---

## 3. Piping (`|`)

A pipe sends the output of one command directly as input to another.

```bash
sort data.txt | uniq -u
```

### Without piping:
You usually run one command at a time:

```bash
sort data.txt
```

### With piping:
You can chain multiple commands together:

```bash
sort data.txt | uniq -u | wc -l
```

### Step-by-step breakdown:

1. `sort data.txt` → Sorts the lines  
2. `uniq -u` → Keeps only unique lines  
3. `wc -l` → Counts the number of unique lines  

---

## 4. Important Tips

- `>` overwrites a file, `>>` appends to a file  
- `<` is for input, `>` and `>>` are for output  
- Pipes (`|`) avoid creating intermediate files  
- Combine stdout and stderr when needed using `2>&1`  
- Use `2>/dev/null` to suppress noisy error messages  

---

## 5. Additional Resource

For further reading and examples:  
https://ryanstutorials.net/linuxtutorial/piping.php
