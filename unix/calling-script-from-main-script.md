# Calling Script from the Main Script

Calling a bash script inside the main bash script like following:

`/bin/bash .script.sh`

...is **wrong** because:
- to use `/bin/bash` is redundant as this is defined with the `shebang` on the called scripts.
- `./` before the script should be replaced with `${ownlocation}/`, as this variable is defined at the beginning and surely references to the proper location. 
- calling scripts with `./` could be wrong if the current directory has changed in between.
- instead, use the following:

```bash
ownLocation="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"
cd "${ownLocation}" || exit
```

> **INFO**
>
> `SHEBANG:`\
> The shebang line must be the very first line in a script and it is used to determine the programme, which should be used to  interpret/run the following script. So after all there could be only one shebang line at all.

Reference: 
- Stackoverflow: [How do I get the directory where a Bash script is located from within the script itself?](https://stackoverflow.com/questions/59895/how-do-i-get-the-directory-where-a-bash-script-is-located-from-within-the-script)