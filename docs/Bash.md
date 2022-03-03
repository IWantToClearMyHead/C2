### Bash choose position

```
$ cat ~/go.sh
#!/usr/bin/env bash

HEIGHT=15
WIDTH=40
CHOICE_HEIGHT=4
BACKTITLE="Backtitle here"
TITLE="Where to go?"
MENU="Choose one of the following options:"

OPTIONS=(1 "Gem5"
         2 "FVP"
         3 "Qemu")

CHOICE=$(dialog --clear \
                --backtitle "$BACKTITLE" \
                --title "$TITLE" \
                --menu "$MENU" \
                $HEIGHT $WIDTH $CHOICE_HEIGHT \
                "${OPTIONS[@]}" \
                2>&1 >/dev/tty)

clear
case $CHOICE in
        1)
            echo "You chose Option 1"
            cd /home/zzx/85test/gem/gem5-resources/src/spec-2017/gem5
            ;;
        2)
            echo "You chose Option 2"
            cd /home/zzx/85test/fvp/rdn2-cfg1/model-scripts/rdinfra
            ;;
        3)
            echo "You chose Option 3"
            cd /home/zzx/85test/qemu/
            ;;
esac
pwd
exec bash

```

### add into pre
```
# sh script.sh c.c c.html
exec >"$2"
cat <<HERE
<html><body><h1>Log output for: $1</h1>
<pre>
HERE
grep "${3:-^}" "$1"
echo '</pre></body></html>'
```

### put code into lines

<a href="#top">Back to top</a>
