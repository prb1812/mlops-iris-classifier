# DVC Workflow
## Remote
Local folder remote `myremote` at C:\Users\Asus\dvc-remote-storage (default).
## Cycle for every data change
1. `dvc add data/raw/iris_v1.csv`
2. `git add data/raw/iris_v1.csv.dvc`
3. `git commit -m "data: ..."`
4. `dvc push`
## Comparing and restoring versions
- `dvc diff <commit>` compares the workspace data against an earlier commit.
- `git checkout <commit> -- data/raw/iris_v1.csv.dvc` restores the old pointer.
- `dvc checkout data/raw/iris_v1.csv.dvc` restores the matching data from the cache.
## Versions
| Version | Commit  | Rows | MD5       |
|---------|---------|------|-----------|
| 1       | e8315e3 | 150  | 21d441a2... |
| 2       | 7032ad3 | 170  | 674c8c36... |
