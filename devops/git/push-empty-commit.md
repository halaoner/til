# Push Empty Commit

Commit and push an empty commit (e.g., *trigger a pipeline*) to the GitHub without the actual changes of a particular file, run the following command:


```bash
$ git commit --allow-empty -m "trigger pipeline" --no-verify
```


You can skip `pre-commit` hooks by following flag:

`--no-verify`
